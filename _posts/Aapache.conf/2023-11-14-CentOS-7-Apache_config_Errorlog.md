---
title : "[CentOS 7] Apache httpd.conf_Log level"
categories :
    - Apache_config
tages :
    - CentOS 7
    - Apache

toc : true
toc_sticky : true
---

## 테스트 환경
- OS : CentOS Linux release 7.9.2009 (Core)
- Apache : Apache/2.4.6 (CentOS)

## Log Level

- Log level 의 경우 어느 레벨까지 에러를 기록할지 설정할 수 있으며, 8단계가 존재한다.
- 맨아래로 갈수록 상세한 에러를 기록할 수 있다.
- 보통 데이터를 전환하거나 개발할 경우 제일 아랫단계인 debug 로 해두면 트러블 슈팅하기 수월하다.

|**Log Level**|**단계**|
|:---:|:---:|
|emerg|서버가 가동할 수 없을 정도의 심각한 오류|
|alert|Crit 보다 심각한 오류|
|crit|치명적인 오류|
|error|오류|
|warn|경고|
|notice|알림메세지|
|info|서버정보|
|debug|디버깅을 위한 정보|

# Log Level 수정
```bash
# vim ${Apache 설치 경로}/conf/httpd.conf
```

# Log Level (debug)
```bash
#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel debug
```
▶ 기본 Default 는 warn 으로 되어 있습니다. <br>
▶ 제일 상세하게 에러로그를 출력할 수 있도록 "debug" 로 변경해 줍니다.

**[ Apache 재기동 ]**
```bash
# systemctl restart httpd
```

## Error_log 확인
- 각 Log Level 별로 출력되는 로그 확인을 위해 매 단계별 error_log 는 초기화 진행합니다.

## Error_Log 초기화
```bash
# [root@BHD-Study-DMZ ~]# cd /etc/httpd/logs/
# [root@BHD-Study-DMZ logs]# cat /dev/null > test_error_log
# [root@BHD-Study-DMZ logs]# vim test_error_log
```

## HTTP 접근
### test_error_log 확인
```bash
[Tue Nov 14 18:17:46.038464 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of Requi
re all granted: granted
[Tue Nov 14 18:17:46.038551 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of <Requ
ireAll>: granted
[Tue Nov 14 18:17:46.038557 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of <Requ
ireAny>: granted
[Tue Nov 14 18:17:46.038618 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of Requi
re all granted: granted
[Tue Nov 14 18:17:46.038625 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of <Requ
ireAll>: granted
[Tue Nov 14 18:17:46.038629 2023] [authz_core:debug] [pid 32037] mod_authz_core.c(809): [client 183.99.76.4:60868] AH01626: authorization result of <Requ
ireAny>: granted
```
▶ Debug 상태로 출력이 되는 것을 확인할 수 있다.

# Log Level (info)
```bash
#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel info
```

**[ Apache 재기동 ]**
```bash
# systemctl restart httpd
```