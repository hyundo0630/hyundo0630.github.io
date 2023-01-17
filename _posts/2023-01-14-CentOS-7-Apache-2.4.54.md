---
title : "[CentOS 7] Apache 2.4.54 Install"
categories : 
    - Install 
tags :
    - CentOS 7
    - Apache

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.54</li>
<li>Apache 설치 전, 서버 내부 Port 상태를 확인 해줍니다.</li><br>

```bash
$ netstat -tlnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd           
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      4158/sshd           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      4772/master         
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd           
tcp6       0      0 :::22                   :::*                    LISTEN      4158/sshd           
tcp6       0      0 ::1:25                  :::*                    LISTEN      4772/master  
```

## 패키지 Yum 설치
```bash
$ yum install -y gcc gcc-++ pcre-devel expat-devel
```

## Apache 필요 설치 파일
```bash
$ mkdir -p /home/Apache
$ cd /home/Apache
$ wget https://dlcdn.apache.org/apr/apr-1.7.0.tar.gz --no-check-certificate
$ wget https://dlcdn.apache.org/apr/apr-util-1.6.1.tar.gz --no-check-certificate
$ wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz --no-check-certificate
$ wget https://dlcdn.apache.org/httpd/httpd-2.4.54.tar.gz --no-check-certificate
$ ll
total 13180
-rw-r--r-- 1 root root 1093896 Apr  5  2019 apr-1.7.0.tar.gz
-rw-r--r-- 1 root root  554301 Oct 23  2017 apr-util-1.6.1.tar.gz
-rw-r--r-- 1 root root 9743277 Jun  8  2022 httpd-2.4.54.tar.gz
-rw-r--r-- 1 root root 2096552 Jun 22  2021 pcre-8.45.tar.gz
```

### 압축 해제
```bash
$ tar zxvf apr-1.7.0.tar.gz
$ tar zxvf apr-util-1.6.1.tar.gz
$ tar zxvf httpd-2.4.54.tar.gz
$ tar zxvf pcre-8.45.tar.gz
$ ll
total 13204
drwxr-xr-x 27 1001  1001    4096 Apr  2  2019 apr-1.7.0
-rw-r--r--  1 root root  1093896 Apr  5  2019 apr-1.7.0.tar.gz
drwxr-xr-x 20 1001  1001    4096 Oct 18  2017 apr-util-1.6.1
-rw-r--r--  1 root root   554301 Oct 23  2017 apr-util-1.6.1.tar.gz
drwxr-xr-x 12  504 games    4096 Jun  6  2022 httpd-2.4.54
-rw-r--r--  1 root root  9743277 Jun  8  2022 httpd-2.4.54.tar.gz
drwxr-xr-x  7 1169  1169    8192 Jun 16  2021 pcre-8.45
-rw-r--r--  1 root root  2096552 Jun 22  2021 pcre-8.45.tar.gz
```

### 경로 이동
```bash
$ mv apr-1.7.0 apr-util-1.6.1 httpd-2.4.54 pcre-8.45 /usr/local
```

### PCRE 컴파일 설치
```bash
$ cd /usr/local/pcre-8.45
$ ./configure --prefix=/usr/local/pcre
$ make && make install
```

### apr,apr-util 디렉토리 httpd 디렉토리로 이동 후 컴파일 설치 진행
```bash
$ mv /usr/local/apr-1.7.0 /usr/local/httpd-2.4.54/srclib/apr
$ mv /usr/local/apr-util-1.6.1 /usr/local/httpd-2.4.54/srclib/apr-util
$ cd /usr/local/httpd-2.4.54
$ ./configure --prefix=/usr/local/httpd \
--enable-modules=all \
--enable-so \
--with-included-apr \
--with-mpm-shared=all
$ make && make install
```

## systemctl 등록
```bash
$ vim /etc/systemd/system/httpd.service
$ vim /etc/systemd/system/httpd.service
[Unit]
Description=The Apache HTTP Server

[Service]
Type=forking
#EnvironmentFile=/usr/local/httpd/bin/envvars
PIDFile=/usr/local/httpd/logs/httpd.pid
ExecStart=/usr/local/httpd/bin/apachectl start
ExecReload=/usr/local/httpd/bin/apachectl graceful
ExecStop=/usr/local/httpd/bin/apachectl stop
KillSignal=SIGCONT
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

### 재기동
```bash
$ systemctl daemon-reload
```

## 아파치 실행
```bash
$ systemctl enable httpd
$ systemctl start httpd
```
```bash
$ netstat -tnlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd           
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      4158/sshd           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      4772/master         
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd           
tcp6       0      0 :::80                   :::*                    LISTEN      31269/httpd         
tcp6       0      0 :::22                   :::*                    LISTEN      4158/sshd           
tcp6       0      0 ::1:25                  :::*                    LISTEN      4772/master  
```
<li>80 Port 올라오면 성공</li><br>

## 웹 페이지 접근 확인
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/20230114_143525.png?raw=true">

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>