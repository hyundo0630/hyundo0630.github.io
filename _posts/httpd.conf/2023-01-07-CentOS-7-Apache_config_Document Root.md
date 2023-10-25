---
title : "[CentOS7] Apache httpd.conf_Document_Root"
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
<br>

### Document ROOT 확인

<li> httpd.conf 에 지정된 Document Root 경로 </li><br>

```bash
$ cd /var/www/html
$ pwd
/var/www/html
$ ls -l
total 0
```

<li> /var/www/html 경로에 파일이 없을 때 웹페이지 접근 </li>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Document%20Root%20%EA%B4%80%EB%A0%A8/Document%20Root%20%EB%82%B4%20%EC%95%84%EB%AC%B4%EA%B2%83%EB%8F%84%20%EC%97%86%EC%9D%84%20%EB%95%8C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">
<li> 테스트 페이지가 출력 되는 것을 확인할 수 있다. </li>
<br>

### html 파일 추가
```bash
$ vi /var/www/html/index.html (편집기 접근)
$ 안녕하세요
$ :wq
```

### html 파일 추가 후 웹페이지 접근
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/httpd.conf%20%EA%B4%80%EB%A0%A8/Document%20Root%20%EA%B4%80%EB%A0%A8/Document%20Root%20%EB%82%B4%20%ED%8C%8C%EC%9D%BC%EC%9D%B4%20%EC%9E%88%EC%9D%84%20%EB%95%8C%20%EC%9B%B9%ED%8E%98%EC%9D%B4%EC%A7%80.png?raw=true">
<li> 편집기에서 작성한 index.html 내 안녕하세요 문구가 출력 되는 것을 확인할 수 있다 </li>

<li> 즉, Document ROOT 는 /var/www/html 임을 알 수 있다. </li>
<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>