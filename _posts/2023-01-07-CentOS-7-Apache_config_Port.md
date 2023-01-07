---
title : "[CentOS7] Apache httpd.conf_Port"
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
(예시)

```bash
Listen 80
Listen 8080
```