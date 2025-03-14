---
title : "[Azure] Virtual Machine 생성"
categories : 
    - Azure
tags :
    - Rocky Linux
    - Azure
toc: true
toc_sticky: true
---

# Azure Virtual Machine 생성
### Azure Portal Access
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Image.png?raw=true">
▲ Azure Potal 에 기본적으로 접근하면 위와 같은 화면을 보실 수 있습니다.<br><br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine.png?raw=true">
▲ Azure Virtual Machine 을 만들기 위해 빨간 네모박스를 클릭해 줍니다.
<br><br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create.png?raw=true">
▲ 만들기를 클릭하여 줍니다.
<br><br><br>

### :computer: 기본 사양

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-1.png?raw=true">
<li>리소스 그룹 : 신규로 만들거나, 기존 생성한 리소스 선택</li>
<li>지역 : 원하는 Resion 선택</li>
<li>가용성 영역 : AWS 의 Multi-AZ 와 같이 가용성 영역을 선택</li>
<br><br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-2.png?raw=true">
<li>크기 : Image 별 기본 크기가 있는 것으로 생각 된다. 사양을 올리고 싶은 경우 모든 크기 보기를 선택하여 원하는 사양으로 지정해주면 적용 된다.</li>
<li>SSH 공개키 원본 : 3가지 형태가 존재한다.</li>
　　- 새 키 쌍 생성<br>
　　- Azure에 저장된 기존 키 사용<br>
　　- 기존 퍼블릭 키 사용<br>
<li>SSH 키 유형 : 원하는 Key 암호화 방식을 선택</li>
<li>키 쌍 이름 : SSH Private Key 이름</li>
<li>인바운드 포트 규칙 : VM 생성 시 사전 추가 없이 허용할 포트 선택</li>

### :dvd: Disk
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-3.png?raw=true">
<li>OS 디스크 크기 : GiB 단위로 표기되며, 원하는 Disk 용량 선택</li>
<li>OS 디스크 유형
<ol><b>로컬 중복 스토리지</b>
<ul>- 프리미엄 SSD : 프로덕션 및 성능에 중요한 워크로드에 적합</ul>
<ul>- 표준 SSD : 웹 서버, 사용량이 적은 엔터프라이즈 어플리케이션 및 개발/테스트에 적합</ul>
<ul>- 표준 SSD : 중요하지 않고 드문 백업 엑세스에 적합</ul>
</ol>
<ol><b>영역 중복 스토리지</b>
<ul>- 프리미엄 SSD : 영역 실패에 대한 스토리지 복원이 필요한 프로덕션 워크로드에 적합</ul>
<ul>- 표준 SSD : 영역 실패에 대한 스토리지 복원력이 필요한 웹 서버, 사용량이 적은 엔터프라이즈 어플리케이션 및 개발/테스트에 적합</ul>
</ol>
</li>
<li>키 관리 </li>
<ol>
<b>플랫폼 관리형 키(PMK)</b>
<ul>- Azure 에서 완전히 생성, 저장 및 관리하는 암호화 키</ul>
</ol>
<ol>
<b>고객 관리형 키(CMK)</b>
<ul>- Azure Key Vault 사용자가 생성, 저장 및 관리하는 암호화 키</ul>
</ol>
<ol>
<b>플랫폼 관리형 키 및 고객 관리형 키</b>
<ul>플랫폼 관리형 키가 있는 인프라 암호화 계층과 디스크 암호화 집합에서 정의하는 고객 관리형 키가 있는 디스크 암호화 계층, 2개의 암호화 계층</ul>
</ol>

### :satellite: Networks
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-4.png?raw=true">
<li>가상 네트워크</li>
<ol>
<ul>- 가상 네트워크는 Azure에서 서로 논리적으로 격리</ul>
<ul>- 데이터 센터의 기존 네트워크와 상당히 비슷하게 IP 주소 범위, 서브넷, 경로 테이블, 게이트웨이 및 보안 설정 구성</ul>
<ul>- 동일한 가상 네트워크 내 VM들은 기본적으로 서로 통신이 가능</ul>
</ol>
<li>인바운드 포트 선택 (4가지 기본 제공)</li>
<ol>
<ul>- HTTP</ul>
<ul>- HTTPS</ul>
<ul>- SSH</ul>
<ul>- RDP</ul>
<br>

위의 과정을 모두 진행 하였다면, `검토+만들기` 를 통해 VM 을 생성합니다.<br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-5.png?raw=true">

▲ 마지막으로 본인이 설정한 값이 맞는지 재 검토 후, `만들기` 버튼을 클릭하여 VM 을 생성해 줍니다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">