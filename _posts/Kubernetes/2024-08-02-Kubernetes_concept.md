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

▣ Traditional Deployment<br>
초기에는 물리장비에 운영체제를 설치하고 운영체제에 애플리케이션을 설치하여 실행 했었다.<br>
여러 애플리케이션을 한 물리장비에서 실행하였을 때, 각 애플리케이션마다 할당되는 리소스를 정의할 방법이 없었기에 리소스 할당 문제가 발생했다.<br>
- ex ) 리소스를 전부 차지하는 애플리케이션이 존재할 수 있고, 이로 인해 다른 애플리케이션 성능이 저하될 수 있었다.

이에 대한 해결책으로 서로 다른 여러 물리장비에서 각 애플리케이션을 실행하는 방안이 있었으나, 이는 리소스가 충분이 활용되지 않는다는 점에서 확장 가능하지 않았고 여러 대의 물리 장비를 유지하는 데에 많은 비용이 발생 되었다.
