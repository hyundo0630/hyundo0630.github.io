---
title : "[RockyLinux 8] Kernel 업데이트"
categories :
    - Rocky Linux
tags :
    - Kernel
    - Version
    - Update

toc : true
toc_sticky : true
---

# :star: Rocky Linux Kernel Update

## :star2: 테스트 서버 정보
<li> OS : Rocky Linux release 8.10 (Green Obsidian) </li>
<li> Kernel : 4.18.0-553.el8_10.x86_64 </li>

# 1. 버전 확인
## 1-1. OS 버전 확인
```bash
$ cat /etc/redhat-release
혹은
$ cat /etc/os-release
```
```bash
[master@k8s-master ~]$ cat /etc/redhat-release 
Rocky Linux release 8.10 (Green Obsidian)

[master@k8s-master ~]$ cat /etc/os-release 
NAME="Rocky Linux"
VERSION="8.10 (Green Obsidian)"
ID="rocky"
ID_LIKE="rhel centos fedora"
VERSION_ID="8.10"
PLATFORM_ID="platform:el8"
PRETTY_NAME="Rocky Linux 8.10 (Green Obsidian)"
ANSI_COLOR="0;32"
LOGO="fedora-logo-icon"
CPE_NAME="cpe:/o:rocky:rocky:8:GA"
HOME_URL="https://rockylinux.org/"
BUG_REPORT_URL="https://bugs.rockylinux.org/"
SUPPORT_END="2029-05-31"
ROCKY_SUPPORT_PRODUCT="Rocky-Linux-8"
ROCKY_SUPPORT_PRODUCT_VERSION="8.10"
REDHAT_SUPPORT_PRODUCT="Rocky Linux"
REDHAT_SUPPORT_PRODUCT_VERSION="8.10"
```

## 1-2. Kernel 버전 확인
```bash
$ uname -r
```
```bash
[master@k8s-master ~]$ uname -r
4.18.0-553.el8_10.x86_64
```

## 1-3. DNF Update
```bash
$ sudo dnf update -y
```
```bash
[master@k8s-master ~]$ sudo dnf update -y
```

## 1.4 ELRepo 저장소를 통한 최신 커널 설치
**ELREPO 저장소 추가**
```bash
sudo dnf install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
```
```bash
$ [master@k8s-master ~]$ sudo dnf install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
[sudo] master의 암호: 
마지막 메타자료 만료확인(0:36:54 이전): 2025년 05월 19일 (월) 오전 01시 24분 09초.
elrepo-release-8.el8.elrepo.noarch.rpm                                                                                                                                                  8.4 kB/s |  19 kB     00:02    
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

<br>

**최신 커널 설치**
```bash
sudo dnf --enablerepo=elrepo-kernel install kernel-ml -y
```
```bash
[master@k8s-master ~]$ sudo dnf --enablerepo=elrepo-kernel install kernel-ml -y
ELRepo.org Community Enterprise Linux Repository - el8                                                                                                                                   60 kB/s | 253 kB     00:04    
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                                           755 kB/s | 2.8 MB     00:03    
종속성이 해결되었습니다.
========================================================================================================================================================================================================================
 꾸러미                                                 구조                                        버전                                                       저장소                                              크기
========================================================================================================================================================================================================================
설치 중:
 kernel-ml                                              x86_64                                      6.14.7-1.el8.elrepo                                        elrepo-kernel                                      150 k
종속 꾸러미 설치 중:
 kernel-ml-core                                         x86_64                                      6.14.7-1.el8.elrepo                                        elrepo-kernel                                       66 M
 kernel-ml-modules                                      x86_64                                      6.14.7-1.el8.elrepo                                        elrepo-kernel                                       62 M

연결 요약
========================================================================================================================================================================================================================
설치  3 꾸러미

전체 내려받기 크기: 128 M
설치된 크기 : 174 M
꾸러미 내려받기 중:
(1/3): kernel-ml-6.14.7-1.el8.elrepo.x86_64.rpm                                                                                                                                          90 kB/s | 150 kB     00:01    
(2/3): kernel-ml-core-6.14.7-1.el8.elrepo.x86_64.rpm                                                                                                                                    4.1 MB/s |  66 MB     00:15    
(3/3): kernel-ml-modules-6.14.7-1.el8.elrepo.x86_64.rpm                                                                                                                                 3.8 MB/s |  62 MB     00:16    
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
합계                                                                                                                                                                                    7.6 MB/s | 128 MB     00:16     
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                                           1.6 MB/s | 1.7 kB     00:00    
GPG키 0xBAADAE52 가져오는 중:
사용자 ID : "elrepo.org (RPM Signing Key for elrepo.org) <secure@elrepo.org>"
지문: 96C0 104F 6315 4731 1E0B B1AE 309B C305 BAAD AE52
출처 : /etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
키 가져오기에 성공했습니다
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                                           3.0 MB/s | 3.1 kB     00:00    
GPG키 0xEAA31D4A 가져오는 중:
사용자 ID : "elrepo.org (RPM Signing Key v2 for elrepo.org) <secure@elrepo.org>"
지문: B8A7 5587 4DA2 40C9 DAC4 E715 5160 0989 EAA3 1D4A
출처 : /etc/pki/rpm-gpg/RPM-GPG-KEY-v2-elrepo.org
키 가져오기에 성공했습니다
연결 확인 실행 중
연결 확인에 성공했습니다.
연결 시험 실행 중
연결 시험에 성공했습니다.
연결 실행 중
  준비 중     :                                                                                                                                                                                                     1/1 
  설치 중     : kernel-ml-core-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                           1/3 
  구현 중     : kernel-ml-core-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                           1/3 
  설치 중     : kernel-ml-modules-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                        2/3 
  구현 중     : kernel-ml-modules-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                        2/3 
  설치 중     : kernel-ml-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                                3/3 
  구현 중     : kernel-ml-core-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                           3/3 
  구현 중     : kernel-ml-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                                3/3 
  확인 중     : kernel-ml-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                                1/3 
  확인 중     : kernel-ml-core-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                           2/3 
  확인 중     : kernel-ml-modules-6.14.7-1.el8.elrepo.x86_64                                                                                                                                                        3/3 

설치되었습니다:
  kernel-ml-6.14.7-1.el8.elrepo.x86_64                               kernel-ml-core-6.14.7-1.el8.elrepo.x86_64                               kernel-ml-modules-6.14.7-1.el8.elrepo.x86_64                              

완료되었습니다!
```
## 1.5Cgoups v2 활성화
```bash
$ sudo vi /etc/default/grub

# GRUB_CMDLINE_LINUX_DEFAULT 위에 아래 옵션 추가
systemd.unified_cgroup_hierarchy=1
```
```bash
[master@k8s-master ~]$ sudo vi /etc/default/grub 

GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto resume=/dev/mapper/rl-swap rd.lvm.lv=rl/root rd.lvm.lv=rl/swap systemd.unified_cgroup_hierarchy=1"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

## 1.6 부팅 메뉴 설정
```bash
#  GRUB 설정 파일 수정
$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg

# 기본 부팅 커널 설정
sudo grub2-set-default 0
```
```bash
[master@k8s-master ~]$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
done

[master@k8s-master ~]$ sudo grub2-set-default 0
```

# :cyclone: 2. 재부팅
```bash
$ sudo reboot
```

## 2.1 재부팅 후 커널 버전 확인
```bash
$ uname -r
```
```bash
[root@k8s-master master]# uname -r
6.14.7-1.el8.elrepo.x86_64
```

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>