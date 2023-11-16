---
title : "[CentOS 7] Swap Memory 설정"
categories : 
    - Linux
tags :
    - CentOS 7
    - Memory

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 7.8</li>
<li>Platfrom : Naver Cloud</li>
<li>Swap Memory 설정 용량 : 32GB</li><br>

## swap Memory 확인

```bash
$ free -m
              total        used        free      shared  buff/cache   available
Mem:          31995         474       31365           9         155       31213
Swap:             0           0           0
```
▲ Swap memory 가 아직 설정되지 않은 상태

```bash
$ swapon -s
```
▲ Swap Memory 를 설정하지 않았다면 아무런 값이 출력 되지 않을 것입니다.
<br>

## Swap File 생성

<li>저의 경우 Swap File 용량이 다소 크므로 여유있는 Disk 경로에 Swap File을 생성하겠습니다.</li><br>

### Disk 파티션 정보 확인
```bash
$ df -h
Filesystem                 Size  Used Avail Use% Mounted on
devtmpfs                    16G     0   16G   0% /dev
tmpfs                       16G     0   16G   0% /dev/shm
tmpfs                       16G  9.1M   16G   1% /run
tmpfs                       16G     0   16G   0% /sys/fs/cgroup
/dev/xvda2                  49G  2.2G   47G   5% /
/dev/xvda1                1014M  195M  820M  20% /boot
tmpfs                      3.2G     0  3.2G   0% /run/user/11000
/dev/mapper/DataVG-hiware  985G   77M  935G   1% /hiware6
```
▲ 1TB 할당 되어있는 디렉토리에 Swap File 을 생성하여 진행 할 예정입니다.

```bash
$ fallocate -l 32G /hiware6/swapfile
$ ll
total 33554452
drwx------ 2 root root       16384 Apr 18 11:16 lost+found
-rw-r--r-- 1 root root 34359738368 Apr 18 11:20 swapfile
```

## SwapFile 적용
```bash
$ dd if=/dev/zero of=/hiware6/swapfile count=32 bs=1G
```
▲ 위 명령어는 Count 와 bs의 값으로 크기를 계산하여 swapfile을 생성해줍니다.<br>
　저의 경우, bs 단위를 1G로 설정하여 Count를 32로 하여 32GB 진행을 하였지만,<br>
　1M 로 하신다면 Count를 1024*32=32,768 로 기재하여 진행하시면 됩니다.<br>
　(※ 용량이 클수록 시간이 다소 소요가 됩니다.)

```bash
dd if=/dev/zero of=/hiware6/swapfile count=32 bs=1G
32+0 records in
32+0 records out
34359738368 bytes (34 GB) copied, 320.808 s, 107 MB/s
```
▲ 완료 되었습니다.

### SwapFile 권한 변경
<li>상위 작업이 마무리 되셨다면 swapfile 권한을 600으로 변경하여 줍니다.</li>

```bash
$ chmod 600 /hiware6/swapfile
$ ll
total 33554452
drwx------ 2 root root       16384 Apr 18 11:16 lost+found
-rw------- 1 root root 34359738368 Apr 18 11:49 swapfile
```
### SwapFile 사용
<li>SwapFile 을 사용하기 위해서는 포맷을 맞춰줘야 합니다.</li>

```bash
$ mkswap /hiware6/swapfile
Setting up swapspace version 1, size = 33554428 KiB
no label, UUID=d9c22dfc-d6da-496d-acce-dc964e55f567
```

<li>실제로 적용하기 위해 시스템에 등록하여줍니다.</li>

```bash
swapon /hiware6/swapfile
```
<li>여기 까지 진행하셨으면 시스템등록까지 완료가 된 것입니다.</li>

### swapfile 영구 적용
<li>/etc/fstab 에 등록하여 영구적으로 적용하여 줍니다.</li>

```bash
# vim /etc/fstab
/hiware6/swap   swap    swap    deafults    0 0
```

## Swap Memory 확인
```bash
$ free -m
              total        used        free      shared  buff/cache   available
Mem:          31995         511        1222           9       30261       31084
Swap:         32767           0       32767
```

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>