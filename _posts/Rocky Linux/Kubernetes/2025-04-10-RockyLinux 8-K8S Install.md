---
title : "[Kubernetes] 컨테이너 런 타임 설치"
categories :
    - K8s
tags :
    - Rocky Linux
    - OS

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
<!---->

# 컨테이너 런타임이란?
컨테이너 실행을 담당하는 소프트웨어

## 필수 요소 설치 및 구성

### :fire: 1. IPv4를 포워딩하여 iptables가 브리지된 트래픽 보게 하기

<span class="tooltip"><u>lsmod</u>
  <span class="tooltiptext">리눅스 커널에 있는 모듈(module)들의 정보를 보여주는 명령어.</span>
</span>
| grep br_netfilter 를 실행하여 
<span class="tooltip">`br_netfilter`
  <span class="tooltiptext">리눅스 커널의 네트워크 필터링 모듈로, 브리지된 네트워크 트래픽을 처리하는 데 사용됩니다</span>
</span>
모듈이 로드 되어있는 지 확인한다.
<br>
```bash
$ [root@master master]# lsmod | grep br_netfilter
$ [root@master master]# 
```
:arrow_up_small: br_netfilter 모듈이 로드되어 있지 않을 때

br_netfilter 를 로드하기 위해 `sudo modprobe br_netfilter` 를 실행하여 줍니다.

```bash
$ [root@master master]# modprobe br_netfilter
$ [root@master master]# lsmod | grep br_netfilter
br_netfilter           28672  0
bridge                294912  1 br_netfilter
```
:arrow_up_small: br_netfilter 모듈이 로드된 것을 확인하실 수 있습니다.


리눅스 노드의 iptables 가 브리지된 트래픽을 올바르게 보기 위한 요구사항으로, `sysctl` 구성에서 `net.bridge.bridge-nf-call-iptables`가 1로 설정되어있는지 확인 하여 줍니다.
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