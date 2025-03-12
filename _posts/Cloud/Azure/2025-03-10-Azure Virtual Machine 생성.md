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

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-1.png?raw=true">
▲ 리소스 그룹&nbsp;:　신규로 만들거나, 기존 생성한 리소스 선택<br>
　지역&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;: 　원하는 Resion 선택<br>
　가용성 영역&nbsp;&nbsp;:　AWS 의 Multi-AZ 와 같이 가용성 영역을 선택
<br><br><br>

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Azure%20%EA%B4%80%EB%A0%A8/Azure%20Portal%20Virtual%20Machine%20Create_1-2.png?raw=true">
▲ 크기　　　　　　　:　Image 별 기본 크기가 있는 것으로 생각 된다. 사양을 올리고 싶은 경우 모든 크기 보기를 선택하여 원하는 사양으로 지정해주면 적용 된다.<br>
　SSH 공개키 원본　　:　3가지 형태가 존재한다.<br>
　　● 새 키 쌍 생성<br>
　　● Azure에 저장된 기존 키 사용<br>
　　● 기존 퍼블릭 키 사용<br>
　SSH 키 유형 　　　 :　원하는 Key 암호화 방식을 선택<br>
　키 쌍 이름　　　 　:　SSH Private Key 이름<br>
　인바운드 포트 규칙 :　VM 생성 시 사전 추가 없이 허용할 포트 선택
