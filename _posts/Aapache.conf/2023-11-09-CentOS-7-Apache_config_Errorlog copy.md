---
title : "[CentOS 7] Apache httpd.conf_Errorlog"
categories :
    - Apache_config
tags :
    - CentOS 7
    - Apache

toc : true
toc_sticky : true
---

## 테스트 환경
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.6</li>
<br>

## Apache Error Log 의 이해
▶ 아파치 내에서 에러가 발생한 경우에 관련된 에러 로그를 지정한 파일에 출력한다.<br>
▶ 로그의 레벨을 설정하여, 필요에 따라 디버깅, trace 등 상세한 로그를 출력하여 이슈를 해결하는데 활용할 수 있다.<br>
▶ Error Log & Log Level 을 정리해보자.
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
▶ ErrorLog "경로/Error Log명"<br>
▶ Loglevel warn

- 현재 설정은 기본으로 셋팅 되어있는 설정 값이다.
- ErrorLog 를 선언한 뒤, 에러를 출력할 로그의 위치를 절대 경로나 상대 경로로 지정해주면 된다.
- 상대 경로로 기재할 경우, Apache 에 설정된 ServerRoot 를 기준으로 경로를 작성해주면 된다.

## Error Log 파일 설정

```bash
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "logs/error_log"
```
▶ 현재 ServerRoot 의 경로는 "/etc/httpd" 이다. <br>
▶ 상대 경로로 기재가 되어있으니, /etc/httpd/logs/ 내 error_log 파일이 존재할 것이다.

```bash
[root@BHD-Study-DMZ logs]# pwd
/etc/httpd/logs
[root@BHD-Study-DMZ logs]# ll
total 4
-rw-r--r-- 1 root root   0 Oct 22 03:28 access_log
-rw-r--r-- 1 root root 370 Nov 12 03:06 error_log
-rw-r--r-- 1 root root   0 Sep 21 17:29 ssl_access_log
-rw-r--r-- 1 root root   0 Oct 15 03:16 ssl_error_log
-rw-r--r-- 1 root root   0 Sep 21 17:29 ssl_request_log
```
▶ 해당 경로 내 error_log 가 있는 것을 확인할 수 있다.

## error_log 변경

```bash
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "logs/test_error_log"
```
▶ 기존 error_log -->  test_error_log 로 변경하였다.

## Apache 재기동
```bash
[root@BHD-Study-DMZ logs]# systemctl restart httpd
```

## error_log 확인

```bash
[root@BHD-Study-DMZ logs]# ll
total 8
-rw-r--r-- 1 root root   0 Oct 22 03:28 access_log
-rw-r--r-- 1 root root 488 Nov 14 17:34 error_log
-rw-r--r-- 1 root root   0 Sep 21 17:29 ssl_access_log
-rw-r--r-- 1 root root   0 Oct 15 03:16 ssl_error_log
-rw-r--r-- 1 root root   0 Sep 21 17:29 ssl_request_log
-rw-r--r-- 1 root root 494 Nov 14 17:34 test_error_log
```

▶ test_error_log 가 생긴 것을 확인할 수 있다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>