---
title : "[RockyLinux 8] DNF 란?"
categories :
    - Rocky_Linux
tags :
    - OS
    - Command

toc : true
toc_sticky : true
---

# DNF (Dandified YUM)
「DNF」 는 리눅스에서 패키지 관리와 소프트웨어 설치, 업데이트, 제거 등을 수행하는 명령어이다.<br>
「DNF」 는 RPM 기반의 리눅스 배포판에서 주로 사용되며, Fedora, CentOS, RHEL (RED Hat Enterprise Linux) 등에서 사용되기 때문에 리눅스 시스템 관리자나 사용자에게 패키지 관리와 시스템 업데이트에 매우 유용한 도구이다.

## DNF 와 YUM 공통점

||YUM|DNF|
|:--:|:--:|:--:|
|패키지설치|yum install [패키지명]|dnf install [패키지명]|
|패키지 재설치|yum reinstall [패키지명]|dnf reinstall [패키지명]|
|업데이트 체크|yum check-update [패키지명]|dnf check-update [패키지명]|
|업데이트|yum update [패키지명]|dnf update [패키지명]|
|설치된 패키지 삭제|yum remove [패키지명]|dnf remove [패키지명]|
|설치된 패키지 목록|yum list installed [패키지명]|dnf list installed [패키지명]|
|Repository에서 패키지 검색|yum search [패키지명]|dnf search [패키지명]|

## DNF 와 YUM 차이점

||YUM|DNF|
|:--:|:--:|:--:|
|RPM 의존성 문제 해결|패키지 설치 간 의존성이 있는 다른 패키지가 선 설치가 되어야하는 종속성 문제가 발생 될 수 있으며, 이러한 문제를 해결하려면 수동 개입이 필요할 수 있다.|패키지 설치 시 의존성이 있는 다른 패키지를 먼저 설치한다. rpm은 설치하려는 rpm 파일이 dvd에 있거나 인터넷을 통해 미리 다운로드 하여 설치해야 하지만, dnf는 인터넷을 통해 알아서 설치해준다.|
|성능|복잡한 트랜잭션 및 패키지 관리 작업 처리 간 속도가 느려질 수 있다.|특히 대규모 패키지 세트로 작업할 때 리소스 사용량 측면에서 더 효율적이고 더 나은 성능을 바루히하도록 설계되어있다. 명령에 대한 보다 빠른 응답을 제공하는 것을 목표로 한다.|
|트랜잭션 기록|내장된 트랜잭션 기록을 제공하지 않으므로 패키지 설치, 업데이트 및 제거 기록을 추적하기 어렵다.|트랜잭션 기록을 유지하여 과거 패키지 관리 작업을 검토할 수 있다. 이는 문제 해결 및 감사 목적으로 유용할 수 있다.|
|플러그인|플러그인 수가 제한되어있어 확장성과 추가 기능이 제한 될 수 있다.|더 많은 유연성과 확장성을 허용하는 모듈식 플러그인 시스템이 함께 제공 된다.|
|소프트웨어 호환성|여전히 작동 가능하고 이전 시스템에서 사용할 수 있지만 일부 최신 소프트웨어 저장소 및 패키지와 완전히 호환되지 않을 수 있다.|Red Hat 및 Fedora에서 적극적으로 개발 및 유지 관리하는 패키지 관리자로, 최신 리포지토리 및 패키지와 더욱 호환됩니다.|

## 결론
DNF 는 일반적으로 의존성 해결 성능, 이력 추적 및 사용자 친화성 면에서 yum 보다 우수하다고 여겨지며, 현대의 Red Hat 기반 Linux 배포판에서는 dnf를 사용하는 것이 좋다.<br>
yum은 여전히 사용 가능하고 이전 시스템에서 사용할 수 있지만 더 나은 패키지 관리를 위해 dnf로 전환하는 것이 좋다.



<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>