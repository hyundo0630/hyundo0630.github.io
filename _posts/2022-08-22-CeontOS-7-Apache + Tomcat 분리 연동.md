---
title : "[CentOS 7] Apache + Tomcat 분리 연동"
categories : 
    - Connect
tags :
    - CentOS 7
    - Tomcat
    - Apache

toc: true
toc_sticky: true
---

## 테스트 환경
<div style="font-size:16px;">
<li> Apache Server </li>
<li> OS : CentOS 7 </li>
<li> IP : 172.27.0.98 </li>
<li> Apache Version : 2.4.52 </li>
<li> Tomcat-connector Version : 1.2.46 </li>
<br>
<li> Tomcat Server </li>
<li> OS : CentOS 7 </li>
<li> IP : 172.27.0.215 </li>
<li> Tomcat Version : 8.5 </li>
<li> Java Version : 1.8.0 </li>
</div>
<br>

## Apache Server setting
<li> Apache 설치가 안되신 분들은 아래 URL 접근하여 설치 진행해주시면 됩니다.</li>
<li> URL : <a href="https://hyundo0630.github.io/apache/CentOS-7-Apache-Install/"> Apache Install </a></li>
<br>

### Tomcat-Connector(mod_jk) 설치

<li> 설치가 되어 있는 항목은 제외 하고 진행 해 주시면 됩니다. </li>

```bash
$ yum install gcc gcc-++ httpd-devel
```

```bash
Dependencies Resolved

====================================================================================================================================================
 Package                                Arch                        Version                                      Repository                    Size
====================================================================================================================================================
Installing:
 httpd-devel                            x86_64                      2.4.6-89.el7.centos.1                        updates                      197 k
Updating:
 gcc                                    x86_64                      4.8.5-36.el7_6.2                             updates                       16 M
Installing for dependencies:
 apr-devel                              x86_64                      1.4.8-3.el7_4.1                              base                         188 k
 apr-util-devel                         x86_64                      1.5.2-6.el7                                  base                          76 k
 cyrus-sasl                             x86_64                      2.1.26-23.el7                                base                          88 k
 cyrus-sasl-devel                       x86_64                      2.1.26-23.el7                                base                         310 k
 expat-devel                            x86_64                      2.1.0-10.el7_3                               base                          57 k
 httpd                                  x86_64                      2.4.6-89.el7.centos.1                        updates                      2.7 M
 libdb-devel                            x86_64                      5.3.21-24.el7                                base                          38 k
 openldap-devel                         x86_64                      2.4.44-21.el7_6                              updates                      804 k
Updating for dependencies:
 cpp                                    x86_64                      4.8.5-36.el7_6.2                             updates                      5.9 M
 gcc-c++                                x86_64                      4.8.5-36.el7_6.2                             updates                      7.2 M
 gcc-gfortran                           x86_64                      4.8.5-36.el7_6.2                             updates                      6.7 M
 httpd-tools                            x86_64                      2.4.6-89.el7.centos.1                        updates                       91 k
 libgcc                                 x86_64                      4.8.5-36.el7_6.2                             updates                      102 k
 libgfortran                            x86_64                      4.8.5-36.el7_6.2                             updates                      300 k
 libgomp                                x86_64                      4.8.5-36.el7_6.2                             updates                      158 k
 libquadmath                            x86_64                      4.8.5-36.el7_6.2                             updates                      189 k
 libquadmath-devel                      x86_64                      4.8.5-36.el7_6.2                             updates                       53 k
 libstdc++                              x86_64                      4.8.5-36.el7_6.2                             updates                      305 k
 libstdc++-devel                        x86_64                      4.8.5-36.el7_6.2                             updates                      1.5 M
 openldap                               x86_64                      2.4.44-21.el7_6                              updates                      356 k

Transaction Summary
====================================================================================================================================================
Install  1 Package (+ 8 Dependent packages)
Upgrade  1 Package (+12 Dependent packages)

Total download size: 43 M
Is this ok [y/d/N]: y
```

```bash
$ wget http://mirror.navercorp.com/apache/tomcat/tomcat-connectors/jk/tomcat-connectors-1.2.48-src.tar.gz

--2022-09-05 16:13:22--  http://mirror.navercorp.com/apache/tomcat/tomcat-connectors/jk/tomcat-connectors-1.2.48-src.tar.gz
Resolving mirror.navercorp.com (mirror.navercorp.com)... 125.209.216.167
Connecting to mirror.navercorp.com (mirror.navercorp.com)|125.209.216.167|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3665280 (3.5M) [application/octet-stream]
Saving to: ‘tomcat-connectors-1.2.48-src.tar.gz’

100%[==========================================================================================================>] 3,665,280   --.-K/s   in 0.1s    

2022-09-05 16:13:22 (28.4 MB/s) - ‘tomcat-connectors-1.2.48-src.tar.gz’ saved [3665280/3665280]
```

### 압축 해제
```bash
$ tar xvf tomcat-connectors-1.2.48-src.tar.gz
$ cd /home/connector/tomcat-connectors-1.2.48-src/native/
```

### 컴파일 진행
```bash
$ find / -name apxs
$ /usr/local/httpd/bin/apxs
$ ./configure --with-apxs=/usr/local/httpd/bin/apxs
$ make && make install
```

### mod_jk 설치 확인
```bash
$ ll /usr/local/httpd/modules/ | grep mod_jk
-rwxr-xr-x 1 root root 1565864 Dec 22 03:29 mod_jk.so
```

### Apache 설정
<li> httpd.conf 내 LoadModule 추가 </li>

```bash
$ vim /usr/local/httpd/conf/httpd.conf // 본인 apache conf 경로 입력
```

```bash
// 아래 구문 추가
$ LoadModule jk_module modules/mod_jk.so
$ Include conf/extra/mod_jk.conf
```

### Mod_jk.conf 파일 생성
```bash
$ vim /usr/local/httpd/conf/extra/mod_jk.conf
```
```bash
// 아래 구문 추가
<IfModule jk_module>
 JkWorkersFile conf/extra/workers.properties
 JkShmFile /usr/local/httpd/logs/mod_jk.shm
 JkLogFile /usr/local/httpd/logs/mod_jk.log
 JkLogLevel info
 JkLogStampFormat "[%a %b %d %H:%M:%S %Y]"
</IfModule>
```
### httpd-vhost.conf 파일 생성
```bash
$ vim /usr/local/httpd/conf/httpd.conf
$ :set nu
$ 491 번라인 Include conf/extra/httpd-vhosts.conf 주석 해제
$ :wq
$ vim /usr/local/httpd/conf/extra/httpd-vhosts.conf
```
```bash
<VirtualHost *:80>
    ServerName localhost
    DocumentRoot /var/www/test

    CustomLog "logs/test.access_log" combined
    ErrorLog  "logs/test.error_log"

    JkMount /* test
</VirtualHost>
```

### worker.properties 파일 생성

```bash
$ vim /usr/local/httpd/conf/extra/workers.properties
```
```bash
// 아래 구문 추가
worker.list=test
worker.test.port=8009
worker.test.host={WAS 서버 IP}
worker.test.type=ajp13
worker.test.lbfactor=1

복사/붙여넣기를 하실 경우 // 뒤에있는 항목은 꼭 삭제 부탁 드립니다.
```
### syntax 확인
```bash
/usr/local/httpd/bin/apachectl -t
```

### 아파치 재기동
```bash
systemctl restart httpd
```

## Tomcat Server Setting
<li> Tomcat 설치가 안되신 분들은 아래 URL 접근하여 설치 진행해주시면 됩니다.</li>
<li> URL : <a href="https://hyundo0630.github.io/install/CentOS-7-Tomcat-9.0.70-Install/"> Tomcat Install </a></li>
<br>

### Tomcat Server.xml 설정 변경
<li> 상위 URL 내 8009 Port 설정 진행 해주시면 됩니다. </li>
<br>

## Apache & Tomcat 재기동
```bash
$ systemctl restart httpd
$ systemctl restart tomcat8
```

## Apache + Tomcat 연동 확인
<li> Apache Server </li>

```bash
// curl localhost IP 주소/index.jsp
$ curl 172.27.0.98/index.jsp

// curl 로 정상적으로 호출이 된다면 웹 사이트에서 확인
$ http://공인 IP/index.jsp
```

<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20+%20Tomcat%20%EA%B4%80%EB%A0%A8/20230114_160730.png?raw=true">
</div>

<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>