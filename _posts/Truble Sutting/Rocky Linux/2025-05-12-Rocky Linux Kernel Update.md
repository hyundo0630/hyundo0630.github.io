---
title : "[Rocky Linux 8.10] kernel Update"
categories : 
    - Truble_Shooting
    - Rocky Linux
    - Kernel
tags :
    - CentOS 8.10
    - dnf
    - Truble

toc: true
toc_sticky: true
---

# 개요
<li> K8S v1.32 Version 설치를 진행하며 Rocky Linux Kernel version 이슈로 인해 설치가 불가한 이슈가 발생했다. </li>
<li> Kernel 4.18.0-553.51.1.el8_10.x86_64 > 6.18 버전으로 업그레이드를 진행하고 나니, SystemCgroup 에서 CPU SET 를 하고있지 않는 이슈 발생</li>
<li> System Cgroup 에서 CPUSET 를 하지 못하면 K8s 설치가 불가 // 원복 진행 </li>
<br><br>

# 상황 재연을 위해 K8s 동일하게 설치 진행
## 기본 시스템 업데이트
```bash
$ sudo dnf update -y
```

## Docker 설치
```bash
$ sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
$ sudo systemctl enable docker
$ sudo systemctl start docker
$ sudo dnf install docker-ce docker-ce-cli containerd.io -y
```

## 필수 시스템 설정
```bash
# IPv4 포워딩 활성화
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

# 커널 모듈 로드
sudo modprobe overlay
sudo modprobe br_netfilter

# 시스템 설정
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

# 설정 적용
sudo sysctl --system
```

## 쿠버네티스 설치
###  kubeadm, kubelet, kubectl 설치
```bash
# 쿠버네티스 저장소 추가
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.32/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.32/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF

# 패키지 설치
sudo dnf install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# kubelet 활성화 및 시작
sudo systemctl enable kubelet
sudo systemctl start kubelet
```

### 클러스터 초기화
```bash
sudo kubeadm init --pod-network-cidr=100.100.0.0/16
```

★ 여기서 문제가 발생
```bash
[preflight] The system verification failed. Printing the output from the verification:
KERNEL_VERSION: 4.18.0-553.51.1.el8_10.x86_64
CONFIG_NAMESPACES: enabled
CONFIG_NET_NS: enabled
CONFIG_PID_NS: enabled
CONFIG_IPC_NS: enabled
CONFIG_UTS_NS: enabled
CONFIG_CGROUPS: enabled
CONFIG_CGROUP_BPF: enabled
CONFIG_CGROUP_CPUACCT: enabled
CONFIG_CGROUP_DEVICE: enabled
CONFIG_CGROUP_FREEZER: enabled
CONFIG_CGROUP_PIDS: enabled
CONFIG_CGROUP_SCHED: enabled
CONFIG_CPUSETS: enabled
CONFIG_MEMCG: enabled
CONFIG_INET: enabled
CONFIG_EXT4_FS: enabled (as module)
CONFIG_PROC_FS: enabled
CONFIG_NETFILTER_XT_TARGET_REDIRECT: enabled (as module)
CONFIG_NETFILTER_XT_MATCH_COMMENT: enabled (as module)
CONFIG_FAIR_GROUP_SCHED: enabled
CONFIG_OVERLAY_FS: enabled (as module)
CONFIG_AUFS_FS: not set - Required for aufs.
CONFIG_BLK_DEV_DM: enabled (as module)
CONFIG_CFS_BANDWIDTH: enabled
CONFIG_CGROUP_HUGETLB: enabled
CONFIG_SECCOMP: enabled
CONFIG_SECCOMP_FILTER: enabled
OS: Linux
CGROUPS_CPU: enabled
CGROUPS_CPUACCT: enabled
CGROUPS_CPUSET: enabled
CGROUPS_DEVICES: enabled
CGROUPS_FREEZER: enabled
CGROUPS_MEMORY: enabled
CGROUPS_PIDS: enabled
CGROUPS_HUGETLB: enabled
CGROUPS_BLKIO: enabled
        [WARNING SystemVerification]: cgroups v1 support is in maintenance mode, please migrate to cgroups v2
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR SystemVerification]: kernel release 4.18.0-553.51.1.el8_10.x86_64 is unsupported. Recommended LTS version from the 4.x series is 4.19. Any 5.x or 6.x versions are also supported. For cgroups v2 support, the minimal version is 4.15 and the recommended version is 5.8+
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
```
```bash
kernel release 4.18.0-553.51.1.el8_10.x86_64 is unsupported.
```

▲ kernel release 4.18 버전은 지원하지 않는다고 한다.

그래서 업데이트를 진행하고자 했다.

##  현재 커널 버전 확인
```bash
uname -r

[root@localhost yum.repos.d]# uname -r
4.18.0-553.51.1.el8_10.x86_64
```

## ELRepo 저장소를 통한 최신 커널 설치 (선택사항)
```bash
# ELRepo 저장소 추가
$ sudo dnf install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm

[bhd@localhost ~]$ sudo dnf install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
[sudo] bhd의 암호: 
Rocky Linux 8 - AppStream                                                                                                                                                               6.4 kB/s | 4.8 kB     00:00    
Rocky Linux 8 - AppStream                                                                                                                                                               4.3 MB/s |  18 MB     00:04    
Rocky Linux 8 - BaseOS                                                                                                                                                                  5.9 kB/s | 4.3 kB     00:00    
Rocky Linux 8 - BaseOS                                                                                                                                                                  5.0 MB/s |  23 MB     00:04    
Rocky Linux 8 - Extras                                                                                                                                                                  4.7 kB/s | 3.1 kB     00:00    
Rocky Linux 8 - Extras                                                                                                                                                                   20 kB/s |  15 kB     00:00    
Docker CE Stable - x86_64                                                                                                                                                                75 kB/s | 3.5 kB     00:00    
Kubernetes                                                                                                                                                                              6.0 kB/s | 1.7 kB     00:00    
elrepo-release-8.el8.elrepo.noarch.rpm                                                                                                                                                   14 kB/s |  19 kB     00:01    
종속성이 해결되었습니다.
========================================================================================================================================================================================================================
 꾸러미                                                구조                                          버전                                                     저장소                                               크기
========================================================================================================================================================================================================================
설치 중:
 elrepo-release                                        noarch                                        8.4-2.el8.elrepo                                         @commandline                                         19 k

연결 요약
========================================================================================================================================================================================================================
설치  1 꾸러미

전체 크기: 19 k
설치된 크기 : 8.3 k
진행할까요? [y/N]: y
꾸러미 내려받기 중:
연결 확인 실행 중
연결 확인에 성공했습니다.
연결 시험 실행 중
연결 시험에 성공했습니다.
연결 실행 중
  준비 중     :                                                                                                                                                                                                     1/1 
  설치 중     : elrepo-release-8.4-2.el8.elrepo.noarch                                                                                                                                                              1/1 
  확인 중     : elrepo-release-8.4-2.el8.elrepo.noarch                                                                                                                                                              1/1 

설치되었습니다:
  elrepo-release-8.4-2.el8.elrepo.noarch                                                                                                                                                                                

완료되었습니다!

```

## 최신 커널 설치
```bash
$ sudo dnf --enablerepo=elrepo-kernel install kernel-ml -y

[bhd@localhost ~]$ sudo dnf --enablerepo=elrepo-kernel install kernel-ml -y
ELRepo.org Community Enterprise Linux Repository - el8                                                                                                                                  104 kB/s | 276 kB     00:02    
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                                           719 kB/s | 2.2 MB     00:03    
종속성이 해결되었습니다.
========================================================================================================================================================================================================================
 꾸러미                                                 구조                                        버전                                                       저장소                                              크기
========================================================================================================================================================================================================================
설치 중:
 kernel-ml                                              x86_64                                      6.14.6-1.el8.elrepo                                        elrepo-kernel                                      150 k
종속 꾸러미 설치 중:
 kernel-ml-core                                         x86_64                                      6.14.6-1.el8.elrepo                                        elrepo-kernel                                       66 M
 kernel-ml-modules                                      x86_64                                      6.14.6-1.el8.elrepo                                        elrepo-kernel                                       62 M

연결 요약
========================================================================================================================================================================================================================
설치  3 꾸러미

전체 내려받기 크기: 128 M
설치된 크기 : 174 M
꾸러미 내려받기 중:
(1/3): kernel-ml-6.14.6-1.el8.elrepo.x86_64.rpm                                                                                                                                         105 kB/s | 150 kB     00:01    
(2-3/3): kernel-ml-core-6.14.6-1.el8.elrepo.x86_64.rpm                                   34% [==============================-                                                         ] 5.7 MB/s |  45 MB     00:14 ETA
```

## 부팅 메뉴 설정
```bash
# GRUB 설정 파일 수정
$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg

[root@localhost bhd]# sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
done

# 기본 부팅 커널 설정
sudo grub2-set-default 0
```

## 재부팅
```bash
$ reboot
```

## Kernel 버전 재 확인
```bash
$ uname -r

[root@localhost ~]$ uname -r
6.14.6-1.el8.elrepo.x86_64
```

정상적으로 업데이트가 완료 되었다.

K8s 를 재설치를 해보자.

## K8s 클러스터 초기화
```bash
$ sudo kubeadm init --pod-network-cidr=100.100.0.0/16

KERNEL_VERSION: 6.14.6-1.el8.elrepo.x86_64
CONFIG_NAMESPACES: enabled
CONFIG_NET_NS: enabled
CONFIG_PID_NS: enabled
CONFIG_IPC_NS: enabled
CONFIG_UTS_NS: enabled
CONFIG_CGROUPS: enabled
CONFIG_CGROUP_BPF: enabled
CONFIG_CGROUP_CPUACCT: enabled
CONFIG_CGROUP_DEVICE: enabled
CONFIG_CGROUP_FREEZER: enabled
CONFIG_CGROUP_PIDS: enabled
CONFIG_CGROUP_SCHED: enabled
CONFIG_CPUSETS: enabled
CONFIG_MEMCG: enabled
CONFIG_INET: enabled
CONFIG_EXT4_FS: enabled (as module)
CONFIG_PROC_FS: enabled
CONFIG_NETFILTER_XT_TARGET_REDIRECT: enabled (as module)
CONFIG_NETFILTER_XT_MATCH_COMMENT: enabled (as module)
CONFIG_FAIR_GROUP_SCHED: enabled
CONFIG_OVERLAY_FS: enabled (as module)
CONFIG_AUFS_FS: not set - Required for aufs.
CONFIG_BLK_DEV_DM: enabled (as module)
CONFIG_CFS_BANDWIDTH: enabled
CONFIG_CGROUP_HUGETLB: enabled
CONFIG_SECCOMP: enabled
CONFIG_SECCOMP_FILTER: enabled
OS: Linux
CGROUPS_CPU: enabled
CGROUPS_CPUACCT: enabled
CGROUPS_CPUSET: missing **<< Kernel 버전 업데이트 후 갑자기 Missing 이 발생**
CGROUPS_DEVICES: enabled
CGROUPS_FREEZER: enabled
CGROUPS_MEMORY: enabled
CGROUPS_PIDS: enabled
CGROUPS_HUGETLB: enabled
CGROUPS_BLKIO: enabled
```
```bash
```

### Cgroups v2 활성화
```bash
$ vi /etc/default/grup

# GRUB_CMDLINE_LINUX_DEFAULT 위에 아래 옵션 추가
systemd.unified_cgroup_hierarchy=1

sudo grub2-mkconfig -o /boot/grub2/grub.cfg
sudo reboot
```

### /etc/default/grub

|변경 전|변경 후|변경사항|
|:--:|:--:|:--:|
|GRUB_TIMEOUT=5|GRUB_TIMEOUT=5|없음|
|GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"|GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"|없음|
|GRUB_DEFAULT=saved|GRUB_DEFAULT=saved|없음|
|GRUB_DISABLE_SUBMENU=true|GRUB_DISABLE_SUBMENU=true|없음|
|GRUB_TERMINAL_OUTPUT="console"|GRUB_TERMINAL_OUTPUT="console"|없음|
||GRUB_CMDLINE_LINUX="crashkernel=auto resume=/dev/mapper/rl-swap rd.lvm.lv=rl/root rd.lvm.lv=rl/swap" systemd.unified_cgroup_hierarchy=1|systemd.unified_cgroup_hierarchy=1 옵션 추가|
|GRUB_DISABLE_RECOVERY="true"|GRUB_DISABLE_RECOVERY="true"|없음|
|GRUB_ENABLE_BLSCFG=true|GRUB_ENABLE_BLSCFG=true|없음|

## 재부팅 후 K8s 클러스터 초기화
```bash

# 결과

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.184.131:6443 --token godd3z.wa8fwyi5ktaqst9y \
        --discovery-token-ca-cert-hash sha256:4bf7ed9e549cb9897498c8bee313f56f8ded095c14ce6a56ade4efe620e11307 
```

제대로 설치가 되는 부분이 확인 되었다.