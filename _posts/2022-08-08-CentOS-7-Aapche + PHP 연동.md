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
<img src="https://raw.githubusercontent.com/hyundo0630/hyundo0630.github.io/a3327a8b7c242e97809f950516d172b55788b595/images/epel-release.png">

- 설치 된 EPEL 은 <code>/etc/yum.repos.d/epel.repo</code> 에서 확인이 가능 하고, 사용하지 않을 경우<br>
아래와 같이 enabled 옵션을 0 으로 주면 됩니다.
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/epel.repo.png?raw=true">