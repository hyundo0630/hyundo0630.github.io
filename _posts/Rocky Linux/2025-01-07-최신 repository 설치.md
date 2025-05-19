---
title : "[RockyLinux 8] 최신 repository (codeit) 설치"
categories :
    - Rocky Linux
tags :
    - Repository

toc : true
toc_sticky : true
---

# Rocky Linux 최신 Repository (codeit) 설치
### [ 서버 정보]
- 서버명 : bhd-test-01
- OS : Rocky Linux
- Version : 8.10 Version

## codeit Repository 를 알게 된 경로

▶ HTTPD 패키지 최신 버전 업그레이드를 위해 검색을 하다 보니, 우연하게 codeit repository 를 알게 되었다. <br>
▶ codeit repository 를 설치하기 전 epel-release 설치가 선행이 되어야 한다. <br>
▶ KTCloud 의 Rocky Linux 8.10 Version 이미지의 경우 /etc/yum.repos.d/tmp 경로 내 Rocky Repo 파일들이 존재한다.

