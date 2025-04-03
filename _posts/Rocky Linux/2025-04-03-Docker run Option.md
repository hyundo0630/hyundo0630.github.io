---
title : "Docker run Option"
categories :
    - Docker
tags :
    - Rocky Linux
    - Docker
    - Install
    - Docker image
    - Docker container

toc : true
toc_sticky : true
---

# Docker run options
```bash
- docker run : docker image로 부터 컨테이너를 실행시키는 명령어
```
```bash
- i : 컨테이너에 접속(attach)하지 않은 상태여도 표준 입력(stdin)을 활성화하고 유지한다.
```
```bash
- t : TTY 모드(pseudo-TTY)를 사용하는 것으로, 쉘에 명령어를 작성할 수 있다.
```
```bash
- it : 두 옵션을 모두 적용하여 docker는 pseudo-TTY를 할당하고, container의 stdin에 연결한다.
```
```bash
- d : 컨테이너를 백그라운드에서 실행하도록 하는 옵션. 실행한 container id를 출력한다
```
```bash
- e : 컨테이너에 환경 변수를 추가하는 옵션.
```
```bash
- p : 호스트에 연결된 컨테이너의 특정 포트를 외부에 노출하기 위해 사용한다.
```
```bash
- w : 컨테이너의 working directory 를 변경하는 옵션이다.
```
```bash
- v : 현재 working directory를 컨테이너에 마운트 하는 옵션
```
```bash
- u : 특정 user 또는 uid 로 컨테이너에 사용하기 위해 사용하는 옵션
```
```bash
- h : 컨테이너의 호스트 네임을 설정하는 옵션
```
```bash
- --name : 컨테이너의 이름을 설정할 때 사용하는 옵션
```
```bash
- --rm : 명령어 수행 후 container 가 삭제 되도록 하는 옵션. 컨테이너를 일회성으로 사용할때 사용한다.
```


<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>