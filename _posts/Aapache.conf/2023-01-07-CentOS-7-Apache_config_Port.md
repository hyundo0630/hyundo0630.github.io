---
title : "[CentOS 7] Apache httpd.conf_Port"
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

## [ Port ]

```bash
#
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to 
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen 80
```
<li> Listen 80</li>
▶ Apache 접근 할 포트를 지정한다. ( Default Port : 80 )<br>
▶기본 포트 변경도 가능하며, 여러 포트를 동시에 설정하여 다중 포트로도 접근이 가능하다.<br>

[서버 내 Port 상태 확인]
```bash
[root@Apache conf]# netstat -tnlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd           
tcp        0      0 172.27.0.170:53         0.0.0.0:*               LISTEN      752/named           
tcp        0      0 127.0.0.1:53            0.0.0.0:*               LISTEN      752/named           
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      4124/sshd           
tcp        0      0 127.0.0.1:953           0.0.0.0:*               LISTEN      752/named           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      4507/master         
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd           
tcp6       0      0 :::80                   :::*                    LISTEN      11961/httpd         
tcp6       0      0 :::22                   :::*                    LISTEN      4124/sshd           
tcp6       0      0 ::1:953                 :::*                    LISTEN      752/named           
tcp6       0      0 ::1:25                  :::*                    LISTEN      4507/master  
```
▶ httpd process 가 80Port 로 기동되어있는 부분을 확인할 수 있다. <br><br>
(예시)
 
```bash
#
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to 
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen 80
Listen 8080
```
```bash
$ systemctl restart httpd
```
```bash
[root@BHD-Study-DMZ conf]# netstat -tnlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      555/rpcbind         
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      891/sshd            
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1138/master         
tcp6       0      0 :::111                  :::*                    LISTEN      555/rpcbind         
tcp6       0      0 :::8080                 :::*                    LISTEN      26036/httpd         
tcp6       0      0 :::80                   :::*                    LISTEN      26036/httpd         
tcp6       0      0 :::22                   :::*                    LISTEN      891/sshd            
tcp6       0      0 ::1:25                  :::*                    LISTEN      1138/master         
tcp6       0      0 :::443                  :::*                    LISTEN      26036/httpd  
```
▶ httpd process 가 80 Port 와 8080 Port Listen 되어있는 것을 확인할 수 있다.
<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>