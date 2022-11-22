---
title : "[CentOS 7] MySQL 5.5 설치"
categories : 
    - Install
tags :
    - CentOS 7
    - MySQL

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 7</li>
<li>MySQL Version : 5.5</li>
<br>

## MySQL 5.5 설치 전 확인
```bash
$ rpm -qa | grep mysql*
$ rpm -qa | grep mariadb
```

## 확인 시 설치되어 있으면 삭제 진행
```bash
$ rpm -e {rpm 명}
$ rpm -e --nodeps {rpm 명}
```
## rpm 패키지 다운로드

```bash
$ yum install wget // wget 없을 경우
$ wget https://cdn.mysql.com//Downloads/MySQL-5.5/MySQL-5.5.61-2.el7.x86_64.rpm-bundle.tar
$ tar -vxf MySQL-5.5.61-2.el7.x86_64.rpm-bundle.tar
```

## 압축 해제
```bash
$ tar xvf MySQL-5.5.61-2.el7.x86_64.rpm-bundle.tar
```

## Perl 설치
```bash
$ yum install perl
$ yum install perl-DBI
```
### Perl 이란?
```bash
Perl ( Practical Extranction and Report Language )
- Perl은 C, awk, sed, sh 같은 언어들의 장점을 가지고 있다.
- Perl 은 쉘 스크립트 (shell scripts) 언어로 컴파일러 ( Compiler ) 가 필요 없다.
- Perl 은 문자열 처리가 어떤 언어보다도 뛰어나다.
- Perl 은 시스템 프로그래밍에 유용하다.
- Perl 은 여러 운영 체제를 지원한다.
```

## rpm 설치 진행
```
$ rpm -ivh rpm -ivh mysql-community-common-5.5.61-2.el7.x86_64.rpm
$ rpm -ivh rpm -ivh mysql-community-libs-5.5.61-2.el7.x86_64.rpm
$ rpm -ivh mysql-community-client-5.5.61-2.el7.x86_64.rpm
$ rpm -ivh mysql-community-server-5.5.61-2.el7.x86_64.rpm
```
## Mysqld 기동
```bash
$ systemctl enable mysqld
$ systemctl start mysqld
```

## MySQL Console 접근 ( 현재 패스워드 없는 상태 )
```bash
$ mysql -u root -p
```

## MySQL 초기 패스워드 설정
```bash
$ mysql_serucre_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MySQL
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!


In order to log into MySQL to secure it, we'll need the current
password for the root user.  If you've just installed MySQL, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): ( Enter )
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MySQL
root user without the proper authorisation.

Set root password? [Y/n] ( Y )

New password: ( 패스워드 입력 )
Re-enter new password: ( 동일 패스워드 입력 )
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] ( Y )
By default, a MySQL installation has an anonymous user, allowing anyone
to log into MySQL without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] ( Y )
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] ( Y )
 ... Success!

By default, MySQL comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] ( Y )
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] ( Y )
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MySQL
installation should now be secure.

Thanks for using MySQL!

```
<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>