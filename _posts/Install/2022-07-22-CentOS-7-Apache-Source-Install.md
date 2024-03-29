---
title : "[CentOS 7] Apache Source Install"
categories : 
    - Install
tags :
    - CentOS 7
    - Apache

toc: true
toc_sticky: true
---


## 테스트 환경
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.6</li>
<li>Apache 설치 전, 서버 내부 Port 상태를 확인 해줍니다.</li>


```java
# netstat -tlnp
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/CentOS7%20netstat.png?raw=true"><br>

## 필요한 패키지 다운로드 및 설치

```java
 yum install -y wget expat-devel gcc gcc-c++
```

## 패키지 설명

### wget
<div style="font-size:16px;">
<li>CLI(Command Line Interface) 환경에서 URL 을 이용한 파일 다운로드 Util</li>
</div>

### expat-devel
<div style="font-size:16px;">
<li>
Apache 설치 시 htpasswd error 발생 원인
expat을 가지고 XML 응용 프로그램을 개발하는데 필요한 Libary들과 File들
</li>
</div>

### gcc
<div style="font-size:16px;">
<li>Linux C Compiler - apr 설치 시 필요</li>
</div>

### gcc-c++
<div style="font-size:16px;">
<li>Linux C Compiler - pcre 설치 시 필요</li><br>
</div>

## Source 파일 다운로드
<div style="font-size:16px;">
apr-util, apache2 의 경우 **apache.org** 에서 다운로드가 가능하며,<br> 아래 URL 을 통하여 다운로드를 진행해주셔도 됩니다.<br><br>
Source 설치 파일을 저장할 디렉토리 생성 및 이동<br><br>
</div>

```java
# mkdir -p /home/source
# cd /home/source
```

<div style="font-size:16px;">
<li>apr Download URL</li>
</div>

```java
# wget https://downloads.apache.org/apr/apr-1.7.0.tar.gz
```

<div style="font-size:16px;">
<li>apr-util Download URL</li>
</div>

```java
# wget https://downloads.apache.org/apr/apr-util-1.6.1.tar.gz
```

<div style="font-size:16px;">
<li> apache2 Download URL</li>
</div>

```java
# wget https://downloads.apache.org/httpd/httpd-2.4.54.tar.gz
```

<div style="font-size:16px;">
&nbsp;pcre 는 **pcer.org** 에서 다운로드가 가능하며, 아래 URL 을 통하여 다운로드를<p> 진행 해주셔도 됩니다.</p>
</div>

```java
# wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz --no-check-certificate
```

## Source 파일 압축 해제

```java
# tar xvfz apr-1.7.0.tar.gz
# tar xvfz apr-util-1.6.1.tar.gz
# tar xvfz httpd-2.4.54.tar.gz
# tar xvfz pcre-8.45.tar.gz
```

## 컴파일

```java
# cd /home/source/apr-1.7.0
# ./configure --prefix=/home/source/apr
# make && make install
```

```java
# cd /home/source/apr-util-1.6.1
# ./configure --prefix=/home/source/apr-util --with-apr=/home/source/apr
# make && make install
```

```java
# cd /home/source/pcre-8.45
# ./configure --prefix=/home/source/pcre
# make && make install
```

```java
# cd /home/httpd-2.4.54
# ./configure --prefix=/usr/local/apache2 --with-apr=/home/source/apr --with-apr-util=/home/source/apr-util --with-pcre=/home/source/pcre/bin/pcre-config
# make && make install
```

### 방화벽 설정

```java
# firewall-cmd --permanent --zone=public --add-port=80/tcp
```

### Port 확인

```java
netstat -tnlp
```

<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/59b404f42b98ab7b42acb7d7fdfe151b86d9fa6d/images/apache%20Port.png">

## Apache 실행

```java
/usr/local/apache2/bin/apachectl start
```

## 웹 페이지 접근

<div style="font-size:16px;">
<li> Local PC 의 환경에서 apache 를 실행했을 경우 = localhost:80</li>
<li> 특정 서버에 환경에서 apache 를 실행했을 경우 = [공인IP:80]</li>
</div>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/apache%20web%20page.png?raw=true">

<div style="font-size:16px;">
<li> 상위와 같이 It works! 가 출력되면 성공입니다. </li>
<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>
