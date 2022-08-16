---
title : "[CentOS 7] Tomcat 8.5 Install"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Tomcat

toc: true
toc_sticky: true
---


## [CentOS7] Tomcat 8.5 Install

## 테스트 환경
<div style="font-size:16px;">
<li> OS Version : CentOS 7 64bit </li>
<li> Open JDK Version : 1.8.0 </li>
<br>
open JDK 1.8 설치가 안되신 분들은 아래 URL 을 통해 진행 해주시면 됩니다.<br>
<li> URL : <a href="https://hyundo0630.github.io/centos/CentOS-7-Open-JDK-1.8-Install/"> Open JDK 1.8 Install</a></li>
</div>

## Open JDK 설치 확인
```
# javac -version
javac 1.8.0_222

# java -version
openjdk version "1.8.0_222"
OpenJDK Runtime Environment (build 1.8.0_222-b10)
OpenJDK 64-Bit Server VM (build 25.222-b10, mixed mode)
```

## Tomcat 8.5 설치
```
# mkdir -p /home/tomcat8
# cd /home/tomcat8
# wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz

// 압축 해제
# tar zxvf apache-tomcat-8.5.27.tar.gz

// 폴더 이동
# mv apache-tomcat-8.5.27.tar.gz /usr/local/tomcat8
```

## 환경 변수 등록
```
# vi /etc/profile
```

```
// 맨 하단에 입력
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64
CATALINA_HOME=/usr/local/tomcat8
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib-jsp-api.jar:$CATAL
INA_HOME/lib/servlet-api.jar
PATH=$PATH:$JAVA_HOME/bin:/bin:/sbin
export JAVA_HOME PATH CLASSPATH CATALINA_HOME
```

```
# source /etc/profile
```