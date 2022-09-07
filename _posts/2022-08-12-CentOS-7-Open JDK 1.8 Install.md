---
title : "[CentOS 7] Open JDK 1.8 Install"
categories : 
    - Tomcat
tags :
    - CentOS 7
    - Open JDK
    - Tomcat

toc: true
toc_sticky: true
---



### 테스트 환경
<div style="font-size:16px;">
<li> OS : CentOS 7 </li>
</div>


## 현재 설치가 가능한 JDK Version 확인
```bash
$ yum list java*jdk-devel
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/OpenJDK1.8%20%EA%B4%80%EB%A0%A8/openJDK%20%EC%84%A4%EC%B9%98%20%EA%B0%80%EB%8A%A5%20list.png?raw=true">
<div style="font-size:16px;">
　- 상위와 같이 설치 가능 버전이 확인할 수 있으며, 1.8.0 을 설치 진행 할 예정입니다.
</div>

## Open JDK 1.8.0 설치 진행
```bash
$ yum install java-1.8.0-openjdk-devel.x86_64
```

### 설치 확인
```bash
$ java -version
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/OpenJDK1.8%20%EA%B4%80%EB%A0%A8/Java%20Version.png?raw=true">

### 환경 변수 설정

<li> 경로 확인 </li>

```bash
// Javac 설치 경로
$ which javac
/usr/bin/javac

// /usr/bin/javac 의 실제 경로 확인
$ readlink -f /usr/bin/javac
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64/bin/javac

// JAVA_HOME 이 될 경로
$ /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64
　--> 경로 맨 뒤에 /bin/javac 를 제외해 줍니다.
```
### /etc/profile 적용

<div style="font-size:16px;">
Javac 설치 경로를 확인 하셨다면, 해당 경로를 <code> /etc/profile </code> 맨 하단에 기입해줍니다.<br>
</div>

```bash
$ vi /etc/profile
$ export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64
$ :wq

// 변경 내용 적용
$ source /etc/profile
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/OpenJDK1.8%20%EA%B4%80%EB%A0%A8/etc_profile.png?raw=true">

## 결과 확인
```bash
$ echo $JAVA_HOME
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-0.el7_6.x86_64
```

<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>