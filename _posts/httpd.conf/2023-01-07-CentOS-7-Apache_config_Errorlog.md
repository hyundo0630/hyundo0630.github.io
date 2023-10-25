---
title : "[CentOS7] Apache httpd.conf_Errorlog"
categories :
    - Apache_config
tages :
    - CentOS 7
    - Apache

toc : true
toc_sticky : true
---

## 테스트 환경
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.6</li>
<br>

## Apache Install
<li> <a href="https://hyundo0630.github.io/install/CentOS-7-Apache-Install/"> Apache 2.4.6 Version Install URL </a></li>
<br>

## httpd.conf 설정
```bash
$ vim {apache 설치 경로}/conf/httpd.conf
```
<br>

## httpd.conf 설명

## [ ErrorLog ]
```bash
#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "logs/error_log"

#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel warn
```
<li>ErrorLog "경로/파일명"</li>
<ul>경로 앞단에 "/" 붙이지 않을 경우 ServerRoot/경로/파일명 으로 생성된다.</ul>

### [ 확인 ]

<li> ErrorLog 경로 확인</li>

```bash
$ 상위와 같은 설정일 경우
$ cd /etc/httpd/logs
$ ls -l
total 16
-rw-r--r-- 1 root root 4368 Jan  7 18:04 access_log
-rw-r--r-- 1 root root  992 Jan  7 16:45 error_log
-rw-r--r-- 1 root root    0 Jan  7 16:45 ssl_access_log
-rw-r--r-- 1 root root  348 Jan  7 16:45 ssl_error_log
-rw-r--r-- 1 root root    0 Jan  7 16:45 ssl_request_log
```
▲ error_log 가 보이는 것을 확인 할 수 있다.

<li>errorlog 명칭 변경</li>

```bash
$ vi /etc/httpd/conf/httpd.conf

#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "logs/test_error_log"

$ wq
```
▲ error_log → test_error_log 명칭 변경

```bash
$ systemctl restart httpd
$ cd /etc/httpd/logs
$ ll
total 20
-rw-r--r-- 1 root root 6743 Jan  9 23:02 access_log
-rw-r--r-- 1 root root 1110 Jan 10 10:48 error_log
-rw-r--r-- 1 root root    0 Jan  7 16:45 ssl_access_log
-rw-r--r-- 1 root root  694 Jan 10 10:48 ssl_error_log
-rw-r--r-- 1 root root    0 Jan  7 16:45 ssl_request_log
-rw-r--r-- 1 root root  731 Jan 10 10:48 test_error_log
```
▲ test_error_log 가 생긴것을 확인할 수 있다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>