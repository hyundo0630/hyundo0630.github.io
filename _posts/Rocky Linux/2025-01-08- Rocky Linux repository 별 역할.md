---
title : "[RockyLinux 8] repository 별 역할"
categories :
    - Rocky_Linux
tags :
    - Repository

toc : true
toc_sticky : true
---

# Rocky Linux Repository 별 역할

### 1. Rocky BaseOS Repository
● **역할** : `시스템의 기본적인 운영 체제 기능을 제공하는 패키지`를 포함하고 있다.<br>
　　　　이 `Rpository` 는 Rocky 시스템이 부팅하고 실행되는 데 필수적인 모든 패키지를 제공한다.<br>
● **예시 패키지** : 커널, 시스템 라이브러리, 필수적인 유틸리티들 <br>
● **주요 용도** : 시스템을 설치하고 기본적인 기능을 수행하기 위해 필수적인 소프트웨어를 제공

### 2. Rocky Appstream Repository
● **역할** : `애플리케이션과 관련된 패키지`들을 제공한다. Rocky 시스템에서 사용자가 설치할 수 있는 다양한 소프트웨어<br>(예 : 웹서버, 데이터베이스 , 개발 도구 등)가 포함된다. `Appstream`은 다양한 버전의 소포트웨어를 제공하고, 선택적으로 여러 버전을 사용할 수 있도록 한다. <br>
● **예시 패키지** : Apache HTTP Server, PostgreSQL, Nodejs, Python 등.<br>
● **주요 용도** : 추가적은 애플리케이션과 개발 도구들을 설치하고 관리하기 위해 사용 됩니다.

### 3. Rocky CodeReady Builder Repository
● **역할** : `개발자들이 시스템에서 필요한 빌드 도구와 라이브러리를 제공`하는 Repository 이다.<br>
　　　  소스코드에서 소프트웨어를 컴파일하거나 개발하는 데 필요한 도구와 패키지들이 포함된다.<br>
● **예시 패키지** : GCC 컴파일러, Make, CMake, Java 개발 키트 (JDK) 등. <br>
● **주요 용도** : 개발 환경 구축 및 소프트웨어 개발에 필요한 패키지를 제공합니다.

### 4. Rocky Extras Repository (Optional)
● **역할** : `기본 Rocky Repository 에 포함되지 않는 추가적인 패키지`들을 제공한다. 이 `Repository`는 특정 하드웨어나 소프트 웨어에 맞춰 제공되는 선택적인 <br>
　　　  패키지를 제공한다. <br>
● **예시 패키지** : 드라이버, 특정 하드웨어에 필요한 소프트웨어 등 <br>
● **주요 용도** : 특정 기능이나 하드웨어에 필요한 추가적인 소프트웨어를 설치할 때 사용된다.

### 5. Rocky Supplemental Repository
● **역할** : Rocky 의 `다른 Repository에서 제공하지 않는 특정 기능이나 하드웨어를 지원하는 패키지`를 제공한다.<br>
　　　  이 `Repository`는 대개 서브스크립션을 통해 제공되며, 특정 서비스나 응용 프로그램을 지원한다.<br>
● **예시 패키지** : 고급 네트워크 도구, 특정 하드웨어의 드라이버, 특수한 라이브러리 등.<br>
● **주요 용도** : 특정 서비스나 하드웨어를 지원하기 위해 필요하다.

### 6. Rocky Optional Repository
● **역할** : `선택적으로 설치할 수 있는 다양한 패키지`를 제공하는 `Repository`. 사용자가 원하는 패키지를 선택하여 설치할 수 있다.<br>
● **예시 패키지** : 다양한 오픈소스 라이브러리, 개발 도구 등.<br>
● **주요 용도** : 추가적인 기능을 지공하며, 선택적으로 사용할 수 있는 패키지.

### 7. Rocky High Availability Repository
● **역할** : `고가용성 환경`에서 사용할 수 있는 패키지를 제공한다. 클러스터링, 리던던시 및 장애조치(Failover) 등을 지원하는 소프트웨어가 포함된다. <br>
● **예시 패키지** : Pacemaker, Corosync 등.<br>
● **주요 용도** : 고가용성 시스템을 구축하교 운영할 때 필요한 소프트웨어와 도구를 제공한다.

### 8. Rocky High Resilient Storage Repository
● **역할** : `데이터 저장소의 안정성을 보장`하는데 필요한 도구들을 제공한다. 특히, RAID, 클러스터링 및 복제 시스템 등을 지원하는 패키지가 포함된다. <br>
● **예시 패키지** : Red Hat Ceph Storage, GluterFS 등.<br>
● **주요 용도** : 안정적인 스토리지 환경을 제공하고 관리할 때 사용된다.

### 9. Rocky Debuginfo Repository
● **역할** : 시스템에서 실행되는 소프트웨어 패키지에 대한 `Debug sysbols`를 제공한다. 이 정보는 프로그램이 충돌하거나 오류가 발생했을 때, 원인을 분석하는데 필요하다.<br>
● **예시 패키지** : glibc-debuginfo, kernel-debuginfo, httpd-debuginfo 등.<br>
● **주요 용도** : 시스템에서 발생하는 소프트웨어 오류나 충돌을 추적하고 분석할 수 있다. 예를 들어, gdb 와 같은 디버깅 툴을 사용할 때, 심볼 정보가 없으면 오류가 발생한 위치와 원인을 정확하게 파알 할 수 있다.

### 10. Rocky Devel Repository
● **역할** : 애플리케이션을 개발하고 빌드할 때 필요한 `헤더 파일, 라이브러리, 빌드도구`를 제공한다. 이러한 도구는 소스 코드에서 프로그램을 컴파일하고 빌드하는 데 필수적이다.<br>
● **예시 패키지** : gcc, glibc-devel, make, pyton3-devel 등.<br>
● **주요 용도** : 애플리케이션 개발, 소스코드 컴파일, C/C++ 개발 라이브러리 개발 및 확장, 패키지 빌드 및 배포 시 많이 쓰인다.

### 11. Rocky Media Repository
● **역할** : Rocky 의 설치 미디어에서 제공되는 패키지들을 포함한다. 이 Repository 는 설치 또는 업그레이드 중에 필요한 패키지들을 제공한다.<br>
　　　  인터넷에 연결되지 않은 환경에서 Rocky를 설치하거나 업데이트 할 때 사용자가 미디어를 통해 로컬로 설치할 수 있도록 지원해준다.<br>
　　　  Rocky 시스템을 처음 설치할 때 또는 복구 작업 중 필요한 기본적인 시스템 패키지를 제공한다.<br>
● **예시 패키지** : redhat-release, anaconda, kexec-tools, dracut, grub2, rpm 등.<br>
● **주요 용도** : Rocky 시스템 설치, 시스템 복구, 오프라인 설치 및 업데이트, Rocky 업그레이드 시 많이 쓰인다.

### 12. Rocky NFV Repository
● **역할** : NFV Repository 는 NFV 관련 소프트웨어와 도구들을 제공한다. `NFV는 네트워크 서비스를 물리적 장비 대신 가상화 된 인프라에서 제공하는 기술`로, 이를 구현하기 위한 다양한 페키지들이 이 Repository 에서 관리된다.<br>
● **예시 패키지** : OpenStack, VNF, OVS, DPDK 등. <br>
● **주요 용도** : NFV 기반 네트워크 환경 구축, 클라우드 기반 네트워크 서비스 제공, 네트워크 성능 최적화, 오픈소스 기반 NFV 솔루션 구현 등.<br>

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>