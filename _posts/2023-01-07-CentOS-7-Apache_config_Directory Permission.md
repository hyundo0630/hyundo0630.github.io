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
<li>Require IP denied : 해당 IP 접근 불허</li>
<li>Require IP granted : 해당 IP 접근 허용</li>
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
    Require IP 183.99.76.4
</Directory>
```

### 홈페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/183.99.76.4%20Requird%20IP.png?raw=true">
▶ 183.99.76.4 IP 허용을 해두었기에 해당 IP로는 정상적으로 접근이 가능하다.

### Option
<li>FollowSymLinks : 심볼릭 링크를 허용한다.</li>
<li>Includes : SSI 을 허용한다</li>
<li>MultiViews : 클라이언트 요청에 따라 적절하게 페이지를 보여준다. 쉽게 생각하면 HTTP 헤드 정보가<br>Accept-Language:ko 라면 Korea 언어에 맞게 데이터를 클라이언트에 전송한다.</li>
<li>Indexes : 웹 서버의 디렉토리에 접근했을 때 DirectoryIndex 지시자로 설정한 파일이 없을 경우<br>디렉토리 안의 파일 목록을 보여준다.</li>
<li>None : 모든 설정을 부정한다.</li><br>

### [ 확인 ]

```bash
<Directory "/var/www">
    AllowOverride None
    # Allow open access:
    Require all granted
</Directory>
```
<li>Require all granted 상태에서 웹 페이지 접근</li>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/granted%20%EC%98%B5%EC%85%98%20%EC%8B%9C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">
<li> 정상 접근 가능</li>
<br>

```bash
<Directory "/var/www">
    AllowOverride None
    # Allow open access:
    Require all denied
</Directory>
```

<li>Require all denied 상태에서 웹 페이지 접근</li>

<img src="
<li> 정상 접근 가능</li>

▶ /var/www 경로의 권한은 /var/www/html 상위에 존재하나, 연관성은 없다.

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

<li>/var/www/html _ Require all granted 상태에서 웹페이지 접근 </li>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/granted%20%EC%98%B5%EC%85%98%20%EC%8B%9C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">
<li> 정상 접근 가능</li>
<br>
[ /var/www/html _ Require all denied 상태에서 웹페이지 접근 ]
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Directory%20Permission%20%EA%B4%80%EB%A0%A8/denied%20%EC%98%B5%EC%85%98%20%EC%8B%9C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">
<li>접근 불가능</li>
<br>
▶ 명시된 디렉토리의 절대경로의 단위로 퍼미션 권한이 주어진다는 것을 알 수 있다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>