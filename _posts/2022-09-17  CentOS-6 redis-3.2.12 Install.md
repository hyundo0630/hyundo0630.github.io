---
title : "[CentOS 6] Redis 설치"
categories : 
    - Redis
tags :
    - CentOS 6

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 6</li>
<li>Redis Version : 3.2.12</li>
<br>

## wget 을 이용한 Redis 3.2.12 다운로드
```bash
$ wget https://download.redis.io/releases/redis-3.2.12.tar.gz
```

### 압축 해제
```bash
$ tar xvf redis-3.2.12.tar.gz
```
## Redis 빌드

### Dependencies 빌드
```bash
// 압축 해제 한 Redis 디렉토리로 이동
$ cd redis-3.2.12

// Dependencies 디렉토리 이동
$ cd deps

// Dependencies 빌드
$ make hiredis jemalloc linenoise lua

// 만일 진행하시면서 make[1] gcc: Command not found 에러가 발생하시면 gcc를 설치해주시면 됩니다.
$ yum install gcc

// 이후 다시 make hiredis jemalloc linenoise lua 진행
```

## Redis 설치
```bash
// 상위에서 진행하셨던 디렉토리의 상위 디렉토리로 이동하시어 make 를 통해 Redis 컴파일을 진행해봅시다.
$ cd ..
$ make

// 컴파일이 모두 완료되었다면 아래와 같은 메세지가 생성됨을 확인 하실 수 있습니다.
Hint: It's a good idea to run 'make test' ;)

make[1]: Leaving directory `/home/ncloud/redis-3.2.12/src'
```

### Redis 설치 2
<li> 컴파일 된 파일을 원하는 디렉토리로 이동해줍시다. </li>
<li> 저는 /etc/redis 설치 하도록 하겠습니다. </li>
<br>

```bash
$ cp -aurp ./src/ /etc/redis/
```

<li> 복사가 되었다면 ./utils/install_server.sh 를 한번 실행해 설치를 진행 해주도록 합니다.</li>


<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>