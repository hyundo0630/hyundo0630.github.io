---
title : "[CentOS 7] Apache + PHP 연동"
categories : 
    - CentOS
tags :
    - CentOS 7
    - Apache
    - PHP
toc: true
toc_sticky: true
---

<div style="font-size:16px;">
Apache 설치의 경우 아래 URL 을 통하여 진행 하실 수 있습니다.<br>
　- URL : <a href="https://hyundo0630.github.io/centos/CentOS-7-Apache-Install/"> Apache Install </a>
</div>

## 테스트 환경
- OS : CentOS 7
- Apache Version : 2.4.6
- PHP Version : 7.2

## EPEL 저장소 추가

### EPEL 이란?
- EPEL = (Extra Packages for Enterprise Linux)<br>
　- 기업용 리눅스를 위한 추가 패키지<br>
　- RHEL 이나 CentOS에 기본적으로 탑재되어있지 않는 패키지를 제공하기 위해 이런 패키지 저장소가 필요합니다.

### 설치 방법
```
yum install -y epel-release
```