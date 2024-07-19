---
title : "Broadcast"
categories :
    - Networks
tags :
    - Networks

toc : true
toc_sticky : true
---

# BroadCast

- 로컬 LAN 상 붙어있는 (브로드캐스트 도메인 안에 있는) 모든 네트워크 장비들에게 보내는 통신
```bash
- 1 vs ALL
- Bradcast 의 주소는 FFFF.FFFFF.FFFF ( MAC Address 일 경우 ) 이다.
- 이 주소로 패킷을 CPU 가 받으면 무조건 읽어들인다. 
  ( 본래 자신의 MAC Address 와 목적지 Address 가 다르면 버린다. )
- Broadcast 는 네트워크 상의 전체 노드로 전송되기 때문에 전체 트래픽이 증가한다.
- 이 패킷을 받은 CPU 는 이 패킷을 처리하게 되고 PC의 성능도 떨어진다.
- 즉, 과도한 Broadcast 는 전체 네트워크 성능 뿐 아니라 PC 의 성능도 떨어지게 한다.
```

## 사용 예시
- 처음 두 PC가 통신하는 경우, 상대 IP는 알 수 있더라도 MAC Address 는 알 수 없다.
- 이 때 상대편의 MAC Address 를 알기 위해 하는 동작이 ARP ( Address Resolution Protocol ) 이다.
- ARP 는 Broadcast 방식이다.
- 네트워크 내의 컴퓨터에게 목적지 IP의 컴퓨터를 Broadcast 를 보내면 대상 IP를 보유한 컴퓨터가  
응답과 함께 본인의 Mac Address 를 같이 보내는 과정을 ARP 라고 한다.
- 이 외에도 라우터끼리 정보를 교환하거나, 다른 라우터를 찾을 경우에 사용한다.
- 서버들이 자신의 어떤 서비스를 제공한다는 것을 모든 클라이언트들에게 알릴 때 브로드 캐스트를 사용한다.
- 브로드 캐스트는 한 번 발생하고 끝나는 것이 아닌 30초나 1분에 한 번씩 주기적으로 발생한다.

<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>