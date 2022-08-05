---
title : "[CentOS 7] Apache Install"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Apache

toc: true
toc_sticky: true
---

## [CentOS7] Apache Install

테스트 환경<br>
    - OS : CentOS 7<br>
    - Apache Version : 2.4.6<br>

<li>Apache 설치 전, 서버 내부 Port 상태를 확인 해줍니다.</li>
```
# netstat -tlnp
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/CentOS7%20netstat.png?raw=true">

# 1. Apache Install
```
yum install httpd httpd-devel
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/CentOS7%20Install%20%EB%B2%84%EC%A0%84%20%EC%B2%B4%ED%81%AC.png?raw=true">
<br>
<li>버전 확인 후 'Y' 를 진행해 줍니다</li>
<br>
# 2. Apache 기동
```
# systemctl enable httpd ## 서버 재기동 시 자동 기동 되도록 설정
# systemctl start httpd ## Apache 실행
```

```
# netstat -tnlp
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/CentOS7%2080%20Port.png?raw=true">
<li>Apache 기동 후 정상적으로 80 Port 가 올라와 있는지 체크</li>
<br>
# 3. 웹 사이트 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/apache%20test%20page.png?raw=true">
<li> 위와 같이 Testing Page 가 접근이 되면 성공입니다.</li>
