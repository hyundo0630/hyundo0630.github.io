---
title : "[CentOS 7] dbimport"
categories :
    - Apache_config
tags :
    - CentOS 7
    - Apache

toc : true
toc_sticky : true
---

#### tbsql 상
drop user JEJU_PARK           cascade;
drop user JEJU_PARKING_LOT    cascade;
drop user JEJU_PARK_ADMIN     cascade;
drop user PARKINGFEEREDUCTION cascade;
drop user PARK_FEE            cascade;
drop user TEST_JEJU_PARK      cascade;

create user JEJU_PARK identified by JEJU_PARK
default tablespace usr
temporary tablespace temp;

create user JEJU_PARKING_LOT identified by JEJU_PARKING_LOT
default tablespace usr
temporary tablespace temp;

create user JEJU_PARK_ADMIN identified by JEJU_PARK_ADMIN
default tablespace usr
temporary tablespace temp;

create user PARKINGFEEREDUCTION identified by PARKINGFEEREDUCTION
default tablespace usr
temporary tablespace temp;

create user PARK_FEE identified by PARK_FEE
default tablespace usr
temporary tablespace temp;

create user TEST_JEJU_PARK identified by TEST_JEJU_PARK
default tablespace usr
temporary tablespace temp;

grant connect, resource to JEJU_PARK;
grant connect, resource to JEJU_PARKING_LOT;
grant connect, resource to JEJU_PARK_ADMIN;
grant connect, resource to PARKINGFEEREDUCTION;
grant connect, resource to PARK_FEE;
grant connect, resource to TEST_JEJU_PARK;

#### 서버 CLI 상
tbimport username=sys password=tibero port=8629 sid=jejupark file=export_tibero_jejupark.dat log=export_tibero_jejupark.log user=JEJU_PARK ,JEJU_PARKING_LOT ,JEJU_PARK_ADMIN ,PARKINGFEEREDUCTION,PARK_FEE ,TEST_JEJU_PARK  