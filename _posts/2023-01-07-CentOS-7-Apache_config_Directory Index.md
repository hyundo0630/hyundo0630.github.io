---
title : "[CentOS7] Apache httpd.conf_Directory_Index"
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

## [ Directory Index ]

```bash
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```
<li>DirectoryIndex [지정 파일] : DocumentRoot 경로 내 지정 파일을 자동으로 불러온다. </li><br>
<li>인덱스(Index) 란?</li>
색인과 같은 의미로 목차 역할을 한다.
<br><br>

## [ 확인 ]
<br>
현재 Document Root 경로 내 파일 확인

```bash
$ cd /var/www/html
$ ll
total 4
-rw-r--r-- 1 root root 16 Jan  7 17:02 index.html
```
<li> index.html 파일이 있는 것을 확인 할 수 있다.</li><br>

### DirectoryIndex 제외
```bash
$ vi /etc/httpd/conf/httpd.conf
```
```bash
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex
</IfModule>
```
```bash
$ systemctl restart httpd
```

[ 웹 사이트 접근 ]
```bash
$ 서버 IP or 도메인 접근
```
<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/d6072ec5251d52d34eefb92af4ce7c2eb8f9f047/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Index%20%EA%B4%80%EB%A0%A8/DirectoryIndex%20%EC%A0%9C%EA%B1%B0.png">
<br>
<li>테스트 페이지가 출력되는 부분을 확인할 수 있다.</li><br>

### DirectoryIndex 추가
```bash
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```
```bash
$ systemctl restart httpd
```
```bash
vi /var/www/html/index.html
```
```bash
$ i (Insert) // 편집기 삽입
$ DirectoryIndex Success !!
$ :wq
```

[ 웹 사이트 접근 ]
<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/d6072ec5251d52d34eefb92af4ce7c2eb8f9f047/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Index%20%EA%B4%80%EB%A0%A8/DirectoryIndex%20%EC%B6%94%EA%B0%80.png">

### DirectoryIndex 여러 개 추가
```bash
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex index.html test.html
</IfModule>
```
```bash
$ systemctl restart httpd
```
```bash
vi /var/www/html/test.html
```
```bash
$ i (Insert) // 편집기 삽입
$ DirectoryIndex two Success !!
$ :wq
```

[ 웹사이트 접근 ]
