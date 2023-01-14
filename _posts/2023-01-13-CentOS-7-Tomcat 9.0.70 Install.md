---
title : "[CentOS 7] Tomcat 9.0.70 Install"
categories : 
    - Install
tags :
    - CentOS 7
    - Tomcat

toc: true
toc_sticky: true
---




## 테스트 환경
<div style="font-size:16px;">
<li> OS Version : CentOS 7 64bit </li>
<li> Open JDK Version : 1.8.0 </li>
<br>
open JDK 1.8 설치가 안되신 분들은 아래 URL 을 통해 진행 해주시면 됩니다.<br>
<li> URL : <a href="https://hyundo0630.github.io/install/CentOS-7-Open-JDK-1.8-Install/"> Open JDK 1.8 Install</a></li>
</div>

## Open JDK 설치 확인
```bash
$ javac -version
javac 1.8.0_222

$ java -version
openjdk version "1.8.0_222"
OpenJDK Runtime Environment (build 1.8.0_222-b10)
OpenJDK 64-Bit Server VM (build 25.222-b10, mixed mode)
```

## Tomcat 9.0.70 설치
```bash
$ mkdir -p /home/tomcat9.0.70
$ cd /home/tomcat9.0.70
$ wget http://archive.apache.org/dist/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.tar.gz
$ ll
-rw-r--r-- 1 root root 11613418 Dec  1 23:20 apache-tomcat-9.0.70.tar.gz

// 압축 해제
$ tar zxvf apache-tomcat-9.0.71.tar.gz

$ ll
drwxr-xr-x 9 root root      220 Jan 13 16:09 apache-tomcat-9.0.70
-rw-r--r-- 1 root root 11613418 Dec  1 23:20 apache-tomcat-9.0.70.tar.gz

// 폴더 이동
$ mv apache-tomcat-9.0.71 /usr/local/Tomcat9
```
### Server.xml 설정
```bash
$ cd /usr/local/Tomcat9/conf
$ vim server.xml

// 아래 구문 주석 해제 및 secretRequired 추가
    <Connector protocol="AJP/1.3"
               address="0.0.0.0"
               port="8009"
               redirectPort="8443" 
               secretRequired="false" />
$ :wq
```


## 환경 변수 등록
```bash
$ vi /etc/profile
```

```bash
// 맨 하단에 입력
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.352.b08-2.el7_9.x86_64
CATALINA_HOME=/usr/local/Tomcat9
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib-jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar
PATH=$PATH:$JAVA_HOME/bin:/bin:/sbin
export JAVA_HOME PATH CLASSPATH CATALINA_HOME

$ :wq
```

```bash
$ source /etc/profile
```

## Tomcat 9.0.70 실행
```bash
$ cd /usr/local/Tomcat9/bin
$ ./startup.sh
```


### 포트 확인
```bash
$ netstat -tnlp

Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd           
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      4158/sshd           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      4687/master         
tcp6       0      0 :::8009                 :::*                    LISTEN      22986/java          
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd           
tcp6       0      0 :::8080                 :::*                    LISTEN      22986/java          
tcp6       0      0 :::22                   :::*                    LISTEN      4158/sshd           
tcp6       0      0 ::1:25                  :::*                    LISTEN      4687/master         
tcp6       0      0 127.0.0.1:8005          :::*                    LISTEN      22986/java 
```

<li> 8009, 8080, 8005 Port 올라왔는지 확인 </li><br>

### 페이지 출력 확인
```bash
localhost:8080
서버IP:8080
```


<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/3e3268a7b15ef66165f47fd669cd07f5f49d3bec/images/Tomcat%20%EA%B4%80%EB%A0%A8/Tomcat%209.0.70%20%EB%A9%94%EC%9D%B8%20%ED%8E%98%EC%9D%B4%EC%A7%80.png">
<br><br>

## systemctl 등록
```bash
$ vim /etc/systemd/system/httpd.service
[UNIT]
Description=tomcat
After=syslog.target network.target

[Service]
Type=forking

Environment=/usr/local/Tomcat9
ExecStart=/usr/local/Tomcat9/bin/startup.sh
ExecStop=/usr/local/Tomcat9/bin/shutdown.sh

User=root
Group=root

[Install]
WantedBy=multi-user.target
```
### 재기동
```bash
$ systemctl daemon-reload
```

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>