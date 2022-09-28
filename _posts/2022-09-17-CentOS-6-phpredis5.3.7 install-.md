---
title : "[CentOS 6] PHP-Redis 설치"
categories : 
    - Redis
tags :
    - CentOS 6

toc: true
toc_sticky: true
---


테스트 환경<br>
<li>OS : CentOS 6</li>
<li>PHP-Redis Version : 5.3.7</li>
<br>

## Wget 을 이용한 PHP - phpredis 다운로드
```bash
$ wget https://pecl.php.net/get/redis-5.3.7.tgz
```

## PHP - phpredis 압축 해제 및 디렉토리 이동
```bash
$ tar xvf redis-5.3.7.tgz
$ cd redis-5.3.7
```

## phpize 진행
<li> phpize 경로를 모르실 경우 find / -name phpize 를 통해 확인 가능 하십니다. </li><br>

```bash
$ find / -name phpize
/usr/bin/phpize 

// phpize 실행
$ /usr/bin/phpize
```

## 컴파일 진행
<li> redis-5.3.7 압축 풀었던 경로로 가서 컴파일을 진행 해줍니다.</li><br>

```bash
$ ./configure --with-php-config=/usr/bin/php-config

// 컴파일 완료 시 아래와 같이 출력 될 것입니다.
Installing shared extensions: /usr/lib64/php/modules/

해당 경로를 기억해 둡시다.
```

```
-rwxr-xr-x 1 root root   21960 Sep 29  2020 bz2.so
-rwxr-xr-x 1 root root   31032 Sep 29  2020 calendar.so
-rwxr-xr-x 1 root root   13416 Sep 29  2020 ctype.so
-rwxr-xr-x 1 root root   73928 Sep 29  2020 curl.so
-rwxr-xr-x 1 root root   62280 Sep 29  2020 exif.so
-rwxr-xr-x 1 root root 3160232 Sep 29  2020 fileinfo.so
-rwxr-xr-x 1 root root   53160 Sep 29  2020 ftp.so
-rwxr-xr-x 1 root root   12560 Sep 29  2020 gettext.so
-rwxr-xr-x 1 root root   41840 Sep 29  2020 iconv.so
-rwxr-xr-x 1 root root   37928 Sep 29  2020 json.so
-rwxr-xr-x 1 root root  274544 Sep 29  2020 phar.so
-rwxr-xr-x 1 root root 2451529 Sep 17 22:37 redis.so // redis.so 파일이 생성 됨을 확인
-rwxr-xr-x 1 root root   83216 Sep 29  2020 sockets.so
-rwxr-xr-x 1 root root   17072 Sep 29  2020 tokenizer.so
```

### php 모듈 확인
<br>

```bash
php -m | grep redis
redis
```

<li> 에러 발생 시 </li><br>

```bash
PHP Warning:  PHP Startup: Unable to load dynamic library '/usr/lib64/php/modules/redis.so' - /usr/lib64/php/modules/redis.so: cannot open shared object file: No such file or directory in Unknown on line 0

상위와 같은 에러가 발생 된다면 아래와 같이 진행하여 조치가 가능하다.

$ php -i | grep ".ini files"
Scan this dir for additional .ini files => /etc/php.d
Additional .ini files parsed => /etc/php.d/20-bz2.ini,

// /etc/php.d 경로 확인
echo "extension=redis.so" > /etc/php.d/redis.ini

이후 다시 php -m | grep redis 진행
```

## php.ini 파일 내 redis 적용 시키기
<br>

```bash
$ vi /etc/php.ini

// php.ini 파일 제일 아래 입력
extenstion=/usr/lib64/php/modules/redis.so
session.save_handler = redis
session.save_path = "tcp://127.0.0.1:6379"
```
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/Redis%20%EA%B4%80%EB%A0%A8/phpinfo.png?raw=true"><br>
<li> 위와 같이 별도의 redis 섹션이 존재하면 완료 입니다.</li><br>

### php redis 연동 테스트

```bash
` ㅌㅋㅍㅊ뉴무`

// 위와 같이 적용 시켰을 때 웹 페이지에서 test_val 값이 나오면 성공입니다,
```
<br><br>
<div style="text-align:center;">
<img src="https://github.com/hyundo0630/hyundo0630.github.io/blob/main/images/%EA%B0%90%EC%82%AC%ED%95%A9%EB%8B%88%EB%8B%A4.gif?raw=true" width="200" height="200">
</div>