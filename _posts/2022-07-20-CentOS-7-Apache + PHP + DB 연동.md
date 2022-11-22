---
title : "[CentOS 7] PHP 7.2 Version InstallApache + PHP + DB 연동"
categories : 
    - PHP
tags :
    - CentOS 7

toc: true
toc_sticky: true
---


테스트 환경<br>
<li> OS : CentOS 7</li>
<li> Apache Version : 2.4.6
<li> PHP Version : 7.2</li>
<li> MariaDB Version : 10.5 </li>
<br>

## Apache, PHP 설치
<li><a href="https://hyundo0630.github.io/apache/CentOS-7-Apache-Install/"> Apache 2.4.6 설치</a></li>
<li><a href="https://hyundo0630.github.io/php/CentOS-7-PHP-7.2/"> PHP 7.2 설치 </a></li>
<li><a href="https://hyundo0630.github.io/mariadb/CentOS7-MariaDB-10.5-Version-Install/"> MariaDB 10.5 설치 </a></li>
// Apache, PHP, MariaDB 는 상위 URL 을 통해 설치 진행 해주시면 됩니다.

<br>

## Apache + PHP 연동
<li><a href="https://hyundo0630.github.io/apache/CentOS-7-Aapche-+-PHP-%EC%97%B0%EB%8F%99/"> Apache + PHP 연동</a></li>
// Apache + PHP 연동 방법은 상위 URL 로 접근하셔서 확인이 가능합니다.
<br>
<br>

## php-mysql 설치
<li>PHP와 MariaDB 연동을 위해 추가 Module 을 설치해야 합니다.</li>

```bash
$ yum install php-mysql
```

## Apache Document Root 경로 내 DB 와 connect 할 PHP 문 만들기
```bash
$ cd {Document Root 경로}
$ vim dbcon.php

<?php
    $host = "DB IP 주소";
    $user = "DB 연결 계정";
    $pw   = "Password";
    $dbName = "DB명";
    
    $conn = new mysqli($host, $user, $pw, $dbName);
    
    if($conn){echo "Connection Success"."<br>";}
    else{ die("Could not connect: " . mysqli_error($conn) );}
    
    mysql_close($conn);
?>
```