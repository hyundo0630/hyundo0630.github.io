---
title : "[CentOS 7] Apache httpd.conf_User_Group"
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

## Apache Install
<li> <a href="https://hyundo0630.github.io/install/CentOS-7-Apache-Install/"> Apache 2.4.6 Version Install URL </a></li>
<br>

## httpd.conf 설정
```bash
$ vim {apache 설치 경로}/conf/httpd.conf
```
<br>

## httpd.conf 설명

## User/Group 권한
```bash
#
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.  
#
# User/Group: The name (or #number) of the user/group to run httpd as.
# It is usually good practice to create a dedicated user and group for
# running httpd, as with most system services.
#
User apache
Group apache
```
<li>User apache</li>
<li>Group apache</li><br>
▶ apache Service 를 실행 할 때 소유권을 갖게되는 사용자와 그룹명을 지정한다.<br>
<br>
[ 사용자 & 그룹자 apache 인 상태로 apache 기동 시 ]<br>

```bash
[root@Apache conf]# ps -ef | grep httpd
root      1808     1  0 Sep05 ?        00:00:31 /usr/sbin/httpd -DFOREGROUND
root     16221 16095  0 17:38 pts/0    00:00:00 grep --color=auto httpd
apache   25586  1808  0 Sep10 ?        00:00:05 /usr/sbin/httpd -DFOREGROUND
apache   25587  1808  0 Sep10 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   25588  1808  0 Sep10 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   25589  1808  0 Sep10 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   25590  1808  0 Sep10 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
apache   25591  1808  0 Sep10 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
```
▶ 프로세스 UID가 Apache 로 표기가 된다.
<br>

[ 사용자 & 그룹자 BHD 로 변경하여 Apache 재기동 ]
```bash
#
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.  
#
# User/Group: The name (or #number) of the user/group to run httpd as.
# It is usually good practice to create a dedicated user and group for
# running httpd, as with most system services.
#
User BHD
Group BHD
```
<li>User BHD</li>
<li>Group BHD</li>
<li>systemctl restart httpd</li>

```bash
[root@Apache conf]# ps -ef | grep httpd
root     11961     1  1 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11962 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11963 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11964 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11965 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11966 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
BHD      11967 11961  0 11:33 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
root     11972 11757  0 11:33 pts/0    00:00:00 grep --color=auto httpd
```
▶ 프로세스 UID 가 BHD 변경 된 것을 확인할 수 있다.
<br><br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>