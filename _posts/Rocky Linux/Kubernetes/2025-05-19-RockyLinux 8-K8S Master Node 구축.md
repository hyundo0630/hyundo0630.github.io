---
title : "[Kubernetes] Master Node (컨트롤 플레인) 구축"
categories :
    - K8s
tags :
    - Rocky Linux
    - Master Node

toc : true
toc_sticky : true
---
<!-- 툴팁박스 공통 -->
<style>
.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 170px;
  background-color: black;
  color: white;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}
</style>
<!--
사용 예시

<span class="tooltip"><u>lsmod</u>
  <span class="tooltiptext">리눅스 커널에 있는 모듈(module)들의 정보를 보여주는 명령어.</span>
</span>
| grep br_netfilter 를 실행하여 
<span class="tooltip">`br_netfilter`
  <span class="tooltiptext">리눅스 커널의 네트워크 필터링 모듈로, 브리지된 네트워크 트래픽을 처리하는 데 사용됩니다</span>
</span>
모듈이 로드 되어있는 지 확인한다.


-->

# 컨테이너 런타임이란?
컨테이너 실행을 담당하는 소프트웨어

# 1. 사전 준비
## :star2: 1.1 OS 업데이트 및 필수 설정
※ Cloud 환경에서는 Kernel Update 를 권장하지 않으므로 Cloud 환경에서는 해당 항목 무시
<li>목적 : 최신 보안 패치 적용, 네트워크/리소스 문제 예방</li>
<br>

```bash
$ sudo dnf update -y
$ sudo hostnamectl set-hostname k8s-master
```

# 1.1 hosts 등록
```bash
# hosts 내 등록 상태 확인
$ cat /etc/hosts

[master@k8s-master ~]$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```
```bash
# hosts 내 k8s-master 추가
$ sudo sed -i '2a\{본인 Master Node 구축 서버 IP} k8s-master' /etc/hosts

# 확인
$ cat /etc/hosts
[master@k8s-master ~]$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
xxx.xxx.xxx.xxx k8s-master
```



## 1.2 SELinuxm, Firewalld, Swap 비활성화
<li>목적 : 쿠버네티스는 SELinux, Firewalld, Swap 이 활성화 되어있으면 정상 동작 하지 않을 수 있습니다.</li>
<br>

```bash
$ sudo setenforce 0
$ sudo sed -i 's/^SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config

$ sudo swapoff -a
$ sudo sed -i '/swap/d' /etc/fstab

$ sudo systemctl stop firewalld && sudo systemctl disable firewalld && sudo systemctl status firewalld

## 결과
Removed /etc/systemd/system/multi-user.target.wants/firewalld.service.
Removed /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
   Active: inactive (dead)
     Docs: man:firewalld(1)

 5월 19 02:15:27 k8s-master systemd[1]: Starting firewalld - dynamic firewall daemon...
 5월 19 02:15:28 k8s-master systemd[1]: Started firewalld - dynamic firewall daemon.
 5월 19 02:15:28 k8s-master firewalld[721]: WARNING: AllowZoneDrifting is enabled. This is considered an insecure configuration option. It will be removed in a future release. Please consider disabling it now.
 5월 19 03:38:50 k8s-master systemd[1]: Stopping firewalld - dynamic firewall daemon...
 5월 19 03:38:51 k8s-master systemd[1]: firewalld.service: Succeeded.
 5월 19 03:38:51 k8s-master systemd[1]: Stopped firewalld - dynamic firewall daemon.
```

# 1.3 IP 포워딩 등 커널 파라미터 설정
**IPv4 포워딩 활성화**
```bash
$ cat << EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

# 커널 모듈 로드
sudo modprobe overlay
sudo modprobe br_netfilter
```

**시스템 설정**
```bash
$ cat << EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
EOF

# 적용
sudo sysctl --system

# 결과
* Applying /etc/sysctl.d/k8s.conf ...
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1

이렇게 출력되면 정상 !
```



## :dizzy: 1.3 :fire: IP 포워딩 및 브릿지 설정
<li>목적 : Pod 네트워크 통신을 위해 커널 파라미터 조정</li>
<br>

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF

sudo modprobe br_netfilter
sudo sysctl --system
```

# 2. 컨테이너 런타임 (containerd) 설치
## 2.1 
```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```
```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```
```bash
# 필요한 sysctl 파라미터를 설정하면, 재부팅 후에도 값이 유지된다.
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
```
```bash
# 재부팅하지 않고 sysctl 파라미터 적용하기
sudo sysctl --system
```
```bash
$ [root@worker1 worker1]# sysctl --system
* Applying /etc/sysctl.d/k8s.conf ...
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
```
:arrow_up_small: 위와 같이 출력 되면 정상입니다.