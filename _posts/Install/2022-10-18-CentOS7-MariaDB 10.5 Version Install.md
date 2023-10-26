---
title : "[CentOS 7] MariaDB 10.5 Version Install"
categories : 
    - Install
tags :
    - CentOS 7
    - MariaDB

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 7</li>
<li>MariaDB Version : 10.5</li>
<br>

## MariaDB repository 설정
```bash
curl -LsS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.5"
```

## MariaDB Install
```bash
$ yum install mariadb-server
```

## 자동 기동 되도록 설정
```bash
$ systemctl enable mariadb
$ systemctl start mariadb
```

## MariaDB Console 접근

```bash
$ mysql -u root -p 혹은 mysql
```

## 패스워드 변경
```bash
$ MariaDB [none] > use mysql;
$ MariaDB [mysql] > set password for 'root'@'localhost' = password('패스워드');
$ MariaDB [mysql] > flush privileges;
```

## MariaDB Console 재 접근하여 패스워드 적용 여부 확인
```bash
$ mysql -u root -p
$ Enter password: ( Enter )
$ ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
// 패스워드 변경 후 접근이 불가한 점 확인
$ mysql -u root -p
Enter password: ( 패스워드 입력 )
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 47
Server version: 10.5.17-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 

접근 확인
```

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>