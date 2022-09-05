---
title : "[CentOS 7] Apache Install"
categories : 
    - Apache
tags :
    - CentOS 7
    - Apache

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 7</li>
<li>Apache Version : 2.4.6</li>
<li>Apache 설치 전, 서버 내부 Port 상태를 확인 해줍니다.</li><br>
```java
# netstat -tlnp
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/CentOS7%20netstat.png?raw=true">

## Apache Install
```java
yum install httpd httpd-devel
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/CentOS7%20Install%20%EB%B2%84%EC%A0%84%20%EC%B2%B4%ED%81%AC.png?raw=true">
<br>
<li>버전 확인 후 'Y' 를 진행해 줍니다</li>
<br>

## Apache 기동

```java
# systemctl enable httpd ## 서버 재기동 시 자동 기동 되도록 설정
# systemctl start httpd ## Apache 실행
```

```java
# netstat -tnlp
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/CentOS7%2080%20Port.png?raw=true">
<li>Apache 기동 후 정상적으로 80 Port 가 올라와 있는지 체크</li>
<br>

## 웹 사이트 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Apache%20Install/apache%20test%20page.png?raw=true">
<li> 위와 같이 Testing Page 가 접근이 되면 성공입니다.</li>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>