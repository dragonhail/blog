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
```shell
init 0 # 종료
init 1 # 복구 모드로 한 명의 사용자만 접속 가능
init 6 # 재부팅
```
### 명령어 사용법
* SHELL: 명령어 해석기. 터미널이나 원격접속툴에서 명령을 내리면 SHELL이 번역을 해서 kernel에 전달하고 실제 명령이 수행됨
* 기능: 
  * 명령어해석기
  * 프로그래밍
  * 사용자환경설정: shell은 사용자 환경을 설정할 수 있도록 초기화 파일 제공<br>
  전체 설정 파일을 읽은 후 사용자 환경 설정 파일을 읽어서 사용자 별로 환경을 구성
* shell에 보여지는 문자열-프롬프트
  ```shell
  사용자이름@호스트이름(컴퓨터):~$
  슈퍼사용자일 경우 사용자이름@호스트이름(컴퓨터):~#
  ```
  * 로그인 할 때 하나의 shell이 보여지게 됨. 이 shell을 로그인 shell이라함
  * 현재 사용중인 shell 확인하는 명령
  ```shell
  echo $SHELL
  ```
  * ~: 홈디렉토리
* 명령어 입력 시 에러가 발생한 경우
  * 키보드 입력이 안될 시 CTRL + s를 눌러 잠금을 한 경우: CTRL + q를 눌러 잠금해제
  * 명령이 종료되지 않은 경우: CTRL + c 눌러 현재 실행중 프로세스 강제 종료
  * 실수로 텍스트파일이 아닌 파일을 열어 한글이 깨지는 경우: CTRL + l(clear)을 눌러 화면 클리어

* 명령어의 구조는 기본적으로 명령 [옵션] [인자]
* 명령은 실행 프로그램 또는 내장 명령어
* 옵션은 - 또는 --
  * - 다음에는 한글자
  * -- 다음에는 단어
* 옵션은 대부분의 경우 순서에 상관없이 여러개 입력 가능
* 한글자인 경우 결합가능

```shell
ls -a 또는 ls --all
ls -a -l -> ls -al # 결합 가능
docker -dit -> docker -d -i -t # d=background, i=interactive, t=terminal
```

### 명령어 자동완성
* 입력 중 입력 한 단어로 시작하는 명령이 하나만 존재한다면 tab을 누르면 명령어는 자동완성이 됨. <br>
입력 중 입력한 단어로 시작하는 명령이 여러 개 존재한다면 tab을 한 번 더 누르면 모든 명령 출력

### 명령어 입력방식
* 텍스트파일에 만들어두고 이 파일의 내용을 읽어서 수행: 스크립트 방식이라고 하고 파일의 확장자는 sh

### 히스토리 기능
* 이전에 수행했던 명령어를 저장
* 키보드화살표 사용 또는 CTRL + p, CTRL + n명령 이용
* CTRL + r을 이용하면 증분 모드로 검색 가능
* history라고 입력 시 수행한 모든 명령어 출력
```shell
history
```
* more로 파일내용
```shell
more 파일명
```