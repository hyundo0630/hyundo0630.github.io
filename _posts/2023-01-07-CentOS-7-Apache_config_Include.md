---
title : "[CentOS7] Apache httpd.conf_Include"
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

## [ Include ]
```bash
#
# Dynamic Shared Object (DSO) Support
#
# To be able to use the functionality of a module which was built as a DSO you
# have to place corresponding `LoadModule' lines at this location so the
# directives contained in it are actually available _before_ they are used.
# Statically compiled modules (those listed by `httpd -l') do not need
# to be loaded here.
#
# Example:
# LoadModule foo_module modules/mod_foo.so
#
Include conf.modules.d/*.conf
```

<li>Include 파일 이름</li>
▶ Include 는 다른 설정파일을 포함 시킬 때 사용한다.<br>
▶ 파일 이름은 절대 경로로 지정하거나, "ServerRoot" 에 대한 상대 경로로 지정한다.<br>