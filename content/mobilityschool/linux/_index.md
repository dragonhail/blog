---
title: Linux
linkTitle: Linux
weight: 4
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---

### 종료
```bash
poweroff
shutdown -P now #지금 종료
shutdown -P +10 #10분후 종료
shutdown -r 22:00 #22시 재부팅
shutdown -c #예약된 종료 취소
shutdown -k +15 #현재 접속한 사용자에게 15분후 종료한다는 메시지 전송, 실제로는 종료되지 않음
halt -p
init 0
```

### 재부팅
```bash
shutdown -r
reboot
init 6
```

### 로그아웃
* 관리자가 시스템 종료를 하면 접속된 모든 유저의 연결 해제
* 관리자가 접속을 해제하고자 하는 경우 logout이나 exit명령을 이용해서 로그아웃

### init
* run레벨을 의미
```bash
init 0 # 종료
init 1 # 복구 모드로 한 명의 사용자만 접속 가능
init 6 # 재부팅
```