---
title : "[CentOS7] Apache httpd.conf_Directory_Permission"
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

## [ Directory ]
```bash
#
# Deny access to the entirety of your server's filesystem. You must
# explicitly permit access to web content directories in other 
# <Directory> blocks below.
#
<Directory />
    AllowOverride none
    Require all denied
</Directory>
```
<li>Directory {path}</li>
<br>

### AllowOverride
<li>AllowOverride는 클라이언트의 디렉토리 접근 제어에 관한 설정이다.</li>
<li>AllowOverride는 AccessFileName 지시자와 밀접한 관계를 가지고 있다.</li><br>
( 아래 각 설정 값들은 AccessFileName 지시자에서 설정한 파일에 적용한다. )<br>
　　ㅇ None : AllowOverride 를 off<br>
　　ㅇ All : AccessFileName 지시자로 설정한 파일에 대해 민감하게 반응한다.<br>
　　ㅇ On : AllowOverride 를 On<br>

```bash
# Relax access to content within /var/www.
#
<Directory "/var/www">
    AllowOverride None
    # Allow open access:
    Require all denied
</Directory>
```

<li>Require all denied : 모든 접근을 불허한다.</li>
<li>Require all granted : 모든 접근을 허용한다.</li>
<li>Require ip xxx.xxx.xxx.xxx : 해당 IP 접근 불허</li>
<li>Require not ip xxx.xxx.xxx.xxx : 해당 IP 접근 허용</li>
<li>Require Host denied : 해당 호스트 접근 불허</li>
<li>Require Host granted : 해당 호스트 접근 허용</li>

<br>

# Require Option 확인

## Require all granted

```bash
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    Require all granted
</Directory>
```
### 홈페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/granted%20%EC%98%B5%EC%85%98%20%EC%8B%9C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true"><br>
▶ 정상적으로 접근이 가능하다.

## Require all denied ( 모든 접근 불허 )
```bash
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    Require all denied
</Directory>
```


### 홈페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/denied%20%EC%98%B5%EC%85%98%20%EC%8B%9C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">

▶ /var/www/html 디렉토리 접근이 차단되어 기본 페이지가 출력되는 것을 확인할 수 있다.

## Require IP granted ( 특정 IP 만 허용)
```bash
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    Require ip 183.99.76.4
</Directory>
```

### 홈페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/Require%20IP_%ED%97%88%EC%9A%A9_183.99.76.4.png?raw=true">
▶ 183.99.76.4 IP 허용을 해두었기에 해당 IP로는 정상적으로 접근이 가능하다.<br><br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/Require%20IP_%ED%97%88%EC%9A%A9_VPN%20IP.png?raw=true">
▶ 183.99.76.4 IP 를 제외한 다른 IP 에서는 /var/www/html 경로 접근이 불가하다. <br><br><br>

## Require IP granted ( 특정 IP 만 불허)

```bash
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    <RequireAll>
    Require all granted
    Require not ip 183.99.76.4
    </RequireAll>
</Directory>
```
▶ not ip 옵션을 주어 183.99.76.4 IP 접근 차단.

### 홈페이지 접근 확인
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/Require%20IP_%EC%B0%A8%EB%8B%A8_VPN%20IP.png?raw=true"><br>
▶ 139.28.219.138 IP 에서 접근 시 /var/www/html 정상 접근이 가능하다.<br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/Require%20IP_%EC%B0%A8%EB%8B%A8_183.99.76.4.png?raw=true"><br>
▶ 183.99.76.4 IP 에서 접근 시 /var/www/html 접근이 차단 된다.<br><br>


# Option
<li>FollowSymLinks : 심볼릭 링크를 허용한다.</li>
<li>Includes : SSI 을 허용한다</li>
<li>MultiViews : 클라이언트 요청에 따라 적절하게 페이지를 보여준다. 쉽게 생각하면 HTTP 헤드 정보가<br>Accept-Language:ko 라면 Korea 언어에 맞게 데이터를 클라이언트에 전송한다.</li>
<li>Indexes : 웹 서버의 디렉토리에 접근했을 때 DirectoryIndex 지시자로 설정한 파일이 없을 경우<br>디렉토리 안의 파일 목록을 보여준다.</li>
<li>None : 모든 설정을 부정한다.</li><br>

## FllowSymLinks
- 해당 옵션 존재 시 디렉토리 심볼릭 링크 접근이 허용되도록 한다.

```bash
[root@BHD-Study-DMZ html]# pwd
/var/www/html
[root@BHD-Study-DMZ html]# ll
total 8
drwxr-xr-x 2 root root 4096 Oct 13 16:44 1
-rw-r--r-- 1 root root   16 Oct 12 18:21 index.html
[root@BHD-Study-DMZ html]# ll 1
total 0
-rw-r--r-- 1 root root  0 Oct 13 16:42 test1
-rw-r--r-- 1 root root  0 Oct 13 16:42 test2
-rw-r--r-- 1 root root  0 Oct 13 16:42 test3
lrwxrwxrwx 1 root root 15 Oct 13 16:44 test4 -> /usr/local/test
```
▶ /var/www/html 경로 내 1 이라는 디렉토리 & test1~3 파일과 test4 디렉토리를 생성해뒀다.

### 웹 페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/FllowSymLinks.png?raw=true"><br>
▶ 해당 디렉토리 내 파일 및 심볼릭 링크 디렉토리도 노출된다

```bash
[root@BHD-Study-DMZ 1]# ll
total 0
-rw-r--r-- 1 root root  0 Oct 13 16:42 test1
-rw-r--r-- 1 root root  0 Oct 13 16:42 test2
-rw-r--r-- 1 root root  0 Oct 13 16:42 test3
lrwxrwxrwx 1 root root 15 Oct 13 16:44 test4 -> /usr/local/test
```
▶ test4 Directory 의 경우 /usr/local/test 로 심볼릭 링크를 걸어 뒀다.

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/FllowSymLinks_test4.png?raw=true">
▶ test4 Directory 클릭 시 심볼릭 링크도 접근 되는 부분을 확인할 수 있다.



## FllowSymLinks 제외
```bash
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    #Options Indexes FollowSymLinks
    Options Indexes 
```
▶ FollowSymLinks 제외

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/FllowSymLinks_%EC%A0%9C%EC%99%B8.png?raw=true">
▶ 심볼릭 링크 걸려있던 디렉토리는 노출되지 않는다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>