---
title : "[CentOS 7] Apache + PHP 연동"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Apache
    - PHP
toc: true
toc_sticky: true
---

<div style="font-size:16px;">
Apache 설치의 경우 아래 URL 을 통하여 진행 하실 수 있습니다.<br>
　- URL : <a href="https://hyundo0630.github.io/centos/CentOS-7-Apache-Install/"> Apache Install </a>
</div>

## 테스트 환경
<div style="font-size:16px">
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.6</li>
<li>PHP Version : 7.2</li>
</div>

## EPEL 저장소 추가

### EPEL 이란?
<div style="font-size:16px">
<li> EPEL = (Extra Packages for Enterprise Linux)</li><br>
　- 기업용 리눅스를 위한 추가 패키지<br><br>
　- RHEL 이나 CentOS에 기본적으로 탑재되어있지 않는 패키지를 제공하기 위해<br>
　　이런 패키지 저장소가 필요합니다.
</div>

### 설치 방법
```
yum install -y epel-release
```
<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/a3327a8b7c242e97809f950516d172b55788b595/images/epel-release.png">
<br>
<div style="font-size:16px">

- 설치 된 EPEL 은 <code>/etc/yum.repos.d/epel.repo</code> 에서 확인이 가능 하고, 사용하지 않을 경우<br>
아래와 같이 enabled 옵션을 0 으로 주면 됩니다.
</div>
<br>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/epel.repo.png?raw=true" width="850" heigth="850">

## webtatic 저장소 추가
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

## PHP7.2 와 일부 라이브러리 설치
```
yum install mod_php72w php72w-cli
yum install php72w-bcmath php72w-gd php72w-mbstring php72w-mysqlnd php72w-peer php72w-xml php72w-xmlrpc php72w-process
```

<div style="font-size:16px">
<li> mod_php72w : Apache HTTP 서버와 연동을 위한 모듈 </li>
<li> php-bcmath : bcmath 라이브러리 </li>
<li> php-mbstring : multi-byte 문자열 처리 (한글과 같은 2byte 문자열 처리) </li>
<li> php-mysql : MySQL DataBase 지원 </li>
<li> php-pear : php 확장 라이브러리 </li>


설치가 끝났다면 <code> vi /etc/php.ini </code> 를 통해 내부 설정을 변경을 해주어야 합니다.

★ vi 편집기 모드에서 /set mu 를 입력하시면 줄 번호를 표시해 줍니다.

<li> 202번 줄 short_open_tag = Off -> On </li>
　　- 짧은 태그 허용 (php 시작 태그를 <?php 가 아닌 <? 로도 사용 허용)<br>

<li> 462번 줄 display_errors = Off -> On </li>
　　- PHP 관련 오류 발생 시 홈페이지 화면에 오류 내용 노출 설정<br>

<li> 359번 줄 expose_php = On -> Off
　　- PHP Version 숨기기

<li> 810번 줄 allow_url_fopen = On </li>
　　- 외부 파일을 URL 방식으로 읽을 수 있도록 하는 설정<br>

</div>

## PHP 확장자 Apache 적용 시키기
```
# vi /etc/httpd/conf/httpd.conf
(※ 사용자의 apache 설정 파일 경로를 입력해주시면 됩니다.)
```
<br>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/apache%20index.php.png?raw=true">
<div style="font-size:16px;">
<li> 164번 줄 index.php 추가 </li><br>
</div>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/apache%20application-httpd.png?raw=true">
<div style="font-size:16px;">
<li> 285번 줄 AddType application/x-httpd-php .html .php .php3 .php4 .inc 추가 </li><br>
</div>

## Apache 재기동
```
# systemctl restart httpd
```

### PHP 연동 확인
```
# touch /var/www/html/index.php
# vi /var/www/html/index.php
```

```
<?php
phpinfo();
?>
```

```
# localhost/index.php
# 서버 IP/index.php
```
