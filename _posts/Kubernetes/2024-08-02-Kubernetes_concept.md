---
title : "Kubernetes 개념"
categories :
    - Kubernetes
tags :
    - Rocky Linux

toc : true
toc_sticky : true
---

### <img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Kubernetes/kubernetes_icon.png?raw=true" width="55" height="30" > Kubernetes 란 무엇인가? <img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Kubernetes/kubernetes_icon.png?raw=true" width="55" height="30" >
- 컨테이너화된 워크로드와 서비스를 관리하기 위한 이식성이 있고, 확장 가능한 오픈 소스 플랫폼
- 선언적 구성과 자동화를 모두 용이하게 해준다.
- 「쿠버네티스」 란 명칭은 키잡이(helmsman)나 파일럿을 뜻하는 그리스어 에서 유래 됐다.
### <img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Kubernetes/kubernetes_icon.png?raw=true" width="55" height="30" > K8s 의 의미 <img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Kubernetes/kubernetes_icon.png?raw=true" width="55" height="30" >
- K8s 라는 표기는 「K」 와 「s」 사이에 있는 8글자를 나타내는 약식 표기이다.

###  쿠버네티스가 나타나기 전까지 여정
<br>
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Kubernetes/iaas.png?raw=true" width="100%">

**▣ Traditional Deployment<br><br>**
초기에는 물리장비에 운영체제를 설치하고 운영체제에 애플리케이션을 설치하여 실행 했었다.<br>
여러 애플리케이션을 한 물리장비에서 실행하였을 때, 각 애플리케이션마다 할당되는 리소스를 정의할 방법이 없었기에 리소스 할당 문제가 발생했다.<br>
- ex ) 리소스를 전부 차지하는 애플리케이션이 존재할 수 있고, 이로 인해 다른 애플리케이션 성능이 저하될 수 있었다.

이에 대한 해결책으로 서로 다른 여러 물리장비에서 각 애플리케이션을 실행하는 방안이 있었으나, 이는 리소스가 충분이 활용되지 않는다는 점에서 확장 가능하지 않았고 여러 대의 물리 장비를 유지하는 데에 많은 비용이 발생 되었다.

**▣ Virtualized Deployment<br><br>**
Traditional Deployment 의 해결책으로 가상화가 도입 되었다.<br>
단일 물리서버의 CPU 에서 여러 가상시스템(VM, Virtual Machines) 을 실행할 수 있게 된다. 가상화 기술을 이용하여 VM 내 애플리케이션을 실행하고 애플리케이션의 정보를 다른 애플리케이션에서 자유롭게 액세스 할 수 없으므로 일정 수준의 보안성도 갖추게 되었다.<br><br>

가상화를 이용하여 물리 서버에서 리소스를 보다 효율적으로 활용할 수 있으며, 쉽게 애플리케이션을 추가하거나 업데이트 할 수 있고 하드웨어 비용을 절감할 수 있어 더 나은 확장성을 제공할 수 있게 되었다. 가상화를 통해 일련의 물리 리소스를 폐기 가능한(disposable) 가상 머신으로 구성된 클러스터로 만들 수 있다.

**▣ Container Deployment<br><br>**
Container 는 VM 과 유사하지만 격리 속성을 완화하여 애플리케이션 간 운영체제(OS)를 공유한다. 따라서 Container 는 가벼워진다. VM 과 마찬가지로 컨테이너에는 자체 파일시스템, CPU, Memory, Process 공간 등이 있다. 기본 인프라와의 종속성을 끊었기 때문에, 클라우드나 OS 배포본에 모두 이전할 수 있다.


### 컨테이너의 이점
Ⅰ. 기민한 애플리케이션 생성과 배포가 가능하다.<br>
　▶ VM 이미지보다 컨테이너 이미지 생성이 쉽고 보다 효율적이다. <br>
Ⅱ. CI/CD 가 가능하다.<br>
　▶ 안정적이고 주기적으로 컨테이너 이미지를 빌드해서 배포할 수 있고, 이미지 불변성 덕에 빠르고 효율적으로 롤백 할 수 있다.<br>
Ⅲ. 개발 / 운영 분리<br>
　▶ 배포 시점이 아닌 빌드/릴리스 시점에 애프리케이션 컨테이너 이미지를 만들기 때문에, 애플리케이션이 인프라스트럭처에서 분리된다.<br>
Ⅳ. 모니터링<br>
　▶ OS 수준의 정보와 메트릭을 표면화할 뿐만 아니라 애플리케이션 상태 및 기타 신호도 표시합니다.<br>
Ⅴ. 환경의 일관성<br>
　▶ 클라우드 환경 뿐만 아니라 랩탑에서도 동일하게 실행할 수 있다.<br>
Ⅵ. 클라우드 및 OS 배포 유연성<br>
　▶ Ubuntu, RHEL, CoreOS, 사내, 주요 퍼블릭 클라우드 및 기타 모든 곳에서 실행 됩니다.<br>
Ⅶ. 애플리케이션 중심 관리<br>
　▶ 가상 하드웨어 상에서 OS를 실행하는 수준에서 논리적인 리소스를 사용하는 OS 상에서 애플리케이션을 실행하는 수준으로 추상화 수준이 높아진다.<br>
Ⅷ. 애플리케이션은 더 작고 독립적인 형태로 나뉘며 동적으로 배포 및 관리할 수 있다.<br>
　▶ 리소스 격리: 애플리케이션 성능을 예측할 수 있다.
　▶ 리소스 사용량: 고효율 고집적

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>