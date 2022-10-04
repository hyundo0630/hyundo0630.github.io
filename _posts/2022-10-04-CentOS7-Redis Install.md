---
title : "[CentOS 7] Redis-Server 설치"
categories : 
    - Redis
tags :
    - CentOS 7

toc: true
toc_sticky: true
---

## 테스트 환경
<li> OS : CentOS 7 </li>
<li> Redis Version : 3.2.12 </li><br>

## EPEL Repo Install
```bash
$ yum install epel-release
```

## Redis Install
```bash
$ yum install redis
```
```bash
Dependencies Resolved

====================================================================================================================================================
 Package                            Arch                             Version                                   Repository                      Size
====================================================================================================================================================
Installing:
 redis                              x86_64                           3.2.12-2.el7                              epel                           544 k
Installing for dependencies:
 jemalloc                           x86_64                           3.6.0-1.el7                               epel                           105 k

Transaction Summary
====================================================================================================================================================
Install  1 Package (+1 Dependent package)
```

## Redis 자동 재기동 설정
```bash
$ systemctl enable redis
```

## Redis 기동
```bash
$ systemctl start redis
```

## 정상 기동 확인
```bash
$ netstat -tnlp

Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.1:6379          0.0.0.0:*               LISTEN      2646/redis-server 1 
```
<br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>