---
title : "[CentOS 7] Apache Source Install"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Apache

toc: true
toc_sticky: true
---

## [CentOS7] Apache Source Install

테스트 환경<br>
  - OS : CentOS 7<br>
  - Apache Version : 2.4.6<br>

<li>Apache 설치 전, 서버 내부 Port 상태를 확인 해줍니다.</li><br>

```
# netstat -tlnp
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/CentOS7%20netstat.png?raw=true"><br>

# 1. 필요한 패키지 다운로드 및 설치<br>
```
 yum install -y wget expat-devel gcc gcc-c++
```
<li>wget = CLI(Command Line Interface) 환경에서 URL 을 이용한 파일 다운로드 Util</li>
<li>expat-devel = 1. Apache 설치 시 htpasswd error 발생 원인</li>
        2. expat을 가지고 XML 응용 프로그램을 개발하는데 필요한 Libary들과 File들
<li>gcc = Linux C Compiler - apr 설치 시 필요</li>
<li>gcc-c++ = Linux C Compiler - pcre 설치 시 필요</li>
<br>

# 2. Source 파일 다운로드
&nbsp;apr-util, apache2 의 경우 **apache.org** 에서 다운로드가 가능하며, 아래 URL 을 통하여 다운로드를 진행해주셔도 됩니다.

<li>apr Download URL</li>
```
# wget https://downloads.apache.org/apr/apr-1.7.0.tar.gz
```
<li>apr-util Download URL</li>
```
# wget https://downloads.apache.org/apr/apr-util-1.6.1.tar.gz
```
<li> apache2 Download URL</li>
```
# wget https://downloads.apache.org/httpd/httpd-2.4.5.1.tar.gz
```

&nbsp;pcre 는 **pcer.org** 에서 다운로드가 가능하며, 아래 URL 을 통하여 다운로드를 진행 해주셔도 됩니다.
```
# wget = https://sourceforge.net/projects/pcre/files/pcre/8.4.5/pcre-8.45.tar.gz --no-check-certificate
```