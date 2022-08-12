---
title : "[CentOS 7] Open JDK 1.8 Install"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Open JDK
    - Tomcat

toc: true
toc_sticky: true
---


## [CentOS7] Open JDK Install

<div style="font-size:16px;">
테스트 환경<br>
- OS : CentOS 7<br>

## 현재 설치가 가능한 JDK Version 확인
```
# yum list java*jdk-devel
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/openJDK%20%EC%84%A4%EC%B9%98%20%EA%B0%80%EB%8A%A5%20list.png?raw=true">
<div style="font-size:16px;">
　- 상위와 같이 설치 가능 버전이 확인할 수 있으며, 1.8.0 을 설치 진행 할 예정입니다.
</div>

## Open JDK 1.8.0 설치 진행
```
# yum install java-1.8.0-openjdk-devel.x86_64
```

### 설치 확인
```
# java -version
```
