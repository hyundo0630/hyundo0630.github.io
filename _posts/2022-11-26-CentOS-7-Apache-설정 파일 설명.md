---
title : "[CentOS7] Apache httpd.conf 설정 파일 설명"
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

## [ 서버 위치 디렉토리 ]
```bash
#
# This is the main Apache HTTP server configuration file.  It contains the
# configuration directives that give the server its instructions.
# See <URL:http://httpd.apache.org/docs/2.4/> for detailed information.
# In particular, see 
# <URL:http://httpd.apache.org/docs/2.4/mod/directives.html>
# for a discussion of each configuration directive.
#
# Do NOT simply read the instructions in here without understanding
# what they do.  They're here only as hints or reminders.  If you are unsure
# consult the online docs. You have been warned.  
#
# Configuration and logfile names: If the filenames you specify for many
# of the server's control files begin with "/" (or "drive:/" for Win32), the
# server will use that explicit path.  If the filenames do *not* begin
# with "/", the value of ServerRoot is prepended -- so 'log/access_log'
# with ServerRoot set to '/www' will be interpreted by the
# server as '/www/log/access_log', where as '/log/access_log' will be
# interpreted as '/log/access_log'.

#
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
#
# Do not add a slash at the end of the directory path.  If you point
# ServerRoot at a non-local disk, be sure to specify a local disk on the
# Mutex directive, if file-based mutexes are used.  If you wish to share the
# same ServerRoot for multiple httpd daemons, you will need to change at
# least PidFile.
#
ServerRoot "/etc/httpd"

```
<li> ServerRoot "/etc/httpd"</li>
▶ Apache 각종 설정에서 절대 경로가 아닌, 상대 경로로 작성되면 ServerRoot 에 지정된 디렉토리로부터의 상대 경로이다.
<br><br>


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

## User/Group 권한
```bash
#
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.  
#
# User/Group: The name (or #number) of the user/group to run httpd as.
# It is usually good practice to create a dedicated user and group for
# running httpd, as with most system services.
#
User apache
Group apach
```
<li>User apache</li>
<li>Group apache</li>
▶apache Service 를 실행하는 유저를 설정한다.<br>

## [ Server Name ]
```bash
#
# ServerName gives the name and port that the server uses to identify itself.
# This can often be determined automatically, but we recommend you specify
# it explicitly to prevent problems during startup.
#
# If your host doesn't have a registered DNS name, enter its IP address here.
#
#ServerName www.example.com:80
```
<li>ServerName {도메인명}:{포트}</li>
▶현재는 로컬이여서 주석 처리 되어있으나, 실 서비스중인 경우 도메인명과 서비스 포트를 등록해주면 된다.<br>

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
<li> Directory /var/www/html 보다 상위의 /var/www/ 접근 권한을 denied 로 주었지만,<br>
/var/www/html 경로를 지정하여 granted ( 접근허용 ) 권한을 주게 되면 /var/www/html 경로 접근이 가능하다.</li>

### Option
<li>FollowSymLinks : 심볼릭 링크를 허용한다.</li>
<li>Includes : SSI 을 허용한다</li>
<li>MultiViews : 클라이언트 요청에 따라 적절하게 페이지를 보여준다. 쉽게 생각하면 HTTP 헤드 정보가<br>Accept-Language:ko 라면 Korea 언어에 맞게 데이터를 클라이언트에 전송한다.</li>
<li>Indexes : 웹 서버의 디렉토리에 접근했을 때 DirectoryIndex 지시자로 설정한 파일이 없을 경우<br>디렉토리 안의 파일 목록을 보여준다.</li>
<li>None : 모든 설정을 부정한다.</li><br>


## Document Root

```bash
#
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "/var/www/html"
```
<li>DocumetRoot</li>
▶Apache 는 WWW 서버이기에 클라이언트에서 콘텐츠 요청에 대응하는 콘텐츠를 반환한다.<br>
▶그 콘텐츠들을 배치해두는 위치를 DocumentRoot 로 지정한다.<br>

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
<li>DirecryIndex [지정 파일] : DocumentRoot 경로 내 지정 파일을 자동으로 불러온다. </li><br>

## [ ErrorLog ]
```bash
#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "logs/error_log"

#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel warn
```
<li>ErrorLog "경로/파일명"</li>
<ul>경로 앞단에 "/" 붙이지 않을 경우 ServerRoot/경로/파일명 으로 생성된다.</ul>
