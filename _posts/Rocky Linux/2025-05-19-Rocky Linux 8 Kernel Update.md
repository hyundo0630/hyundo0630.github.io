---
title : "[RockyLinux 8] Date 날짜 및 시간 변경"
categories :
    - Date
tags :
    - Rocky Linux
    - Time

toc : true
toc_sticky : true
---

# ⏰ Rocky Linux Date 날짜 및 시간 변경

### :computer: Desktop 시간 확인
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Rocky%20Linux%20%EA%B4%80%EB%A0%A8/Date%20%EB%B3%80%EA%B2%BD/Windows%20%EC%8B%9C%EA%B0%84.png?raw=true">
<li>2025년 03월 22일 오후 01시 35분을 나타내고 있다.</li>
<li>Desktop Time 시간은 time.windows.com NTP Server 와 동기화 하고 있다.</li>

### 🎆Rocky Linux 시간 확인
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Rocky%20Linux%20%EA%B4%80%EB%A0%A8/Date%20%EB%B3%80%EA%B2%BD/Rocky%20Linux%20%EC%8B%9C%EA%B0%84.png?raw=true">
<li>EDT 시간으로 표기되고 있으며, EDT 의 경우 미 동부시간을 의미한다.</li>

### 🕜 한국 시간으로 변경

```bash
$ timedatectl set-time zone Asia/Seoul
```

### 🕑 한국 시간 변경 확인

```bash
$ timedatectl
```

<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Rocky%20Linux%20%EA%B4%80%EB%A0%A8/Date%20%EB%B3%80%EA%B2%BD/Rocky%20Linux%20%ED%95%9C%EA%B5%AD%20%EC%8B%9C%EA%B0%84%20%EB%B3%80%EA%B2%BD.png?raw=true">


<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>