---
title : "[CentOS 7] Tomcat 8.5 Install"
categories : 
    - Tomcat
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
<li> URL : <a href="https://hyundo0630.github.io/tomcat/CentOS-7-Open-JDK-1.8-Install/"> Open JDK 1.8 Install</a></li>
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

## Tomcat 8.5 설치
```bash
$ mkdir -p /home/tomcat8
$ cd /home/tomcat8
$ wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz

// 압축 해제
$ tar zxvf apache-tomcat-8.5.27.tar.gz

// 폴더 이동
$ mv apache-tomcat-8.5.27.tar.gz /usr/local/tomcat8
```
### Server.xml 설정
```bash
$ vim /usr/local/tomcat8/conf/server.xml

// 아래 구문 추가
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" URIEncoding="UTF-8" />
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Tomcat%20%EA%B4%80%EB%A0%A8/Server.xml.png?raw=true">

## 환경 변수 등록
```bash
$ vi /etc/profile
```

```bash
// 맨 하단에 입력
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64
CATALINA_HOME=/usr/local/tomcat8
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib-jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar
PATH=$PATH:$JAVA_HOME/bin:/bin:/sbin
export JAVA_HOME PATH CLASSPATH CATALINA_HOME
```

```bash
$ source /etc/profile
```

## Tomcat 8.5 실행
```bash
$ /usr/local/tomcat8/bin/startup.sh
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Tomcat%20%EA%B4%80%EB%A0%A8/Tomcat%20%EC%8B%A4%ED%96%89.png?raw=true">

### 포트 확인
```bash
$ netstat -tnlp
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Tomcat%20%EA%B4%80%EB%A0%A8/Port%20%ED%99%95%EC%9D%B8.png?raw=true">
<li> 8009, 8080, 8005 Port 올라왔는지 확인 </li>

### 페이지 출력 확인
```bash
localhost:8080
서버IP:8080
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Tomcat%20%EA%B4%80%EB%A0%A8/Tomcat%20%EB%A9%94%EC%9D%B8%20%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">

<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>

