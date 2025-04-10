---
title : "[Kubernetes] 컨테이너 런 타임 설치"
categories :
    - K8s
tags :
    - Rocky Linux
    - OS

toc : true
toc_sticky : true
---
<!--> 툴팁박스 공통 -->
<style>
.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 170px;
  background-color: black;
  color: white;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}
</style>
<!--> -->

# 컨테이너 런타임이란?
컨테이너 실행을 담당하는 소프트웨어

## 필수 요소 설치 및 구성

### IPv4를 포워딩하여 iptables가 브리지된 트래픽 보게 하기

<span class="tooltip"><u>lsmod</u>
  <span class="tooltiptext">리눅스 커널에 있는 모듈(module)들의 정보를 보여주는 명령어.</span>
</span>
| grep br_netfilter 를 실행하여




