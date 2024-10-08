---
title: 프로세스
linkTitle: 프로세스
weight: 1
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---

## Process
### 개요
- 실행 중인 프로그램
- 리눅스는 다중 프로세스 시스템
- 프로세스는 부모-자식 관계를 가지고 생성
- 프로세스 구분 방법 중 하나로 시스템 프로세스(운영체제가 생성)와 사용자 프로세스로 나누기도 함
- 리눅스가 부팅이 될 때 systemd 프로세스와 kthreadd 프로세스 생성, 이 프로세스 제외한 모든 프로세스는 부모 프로세스 존재
- 자식 프로세스는 부모 프로세스에 의해 만들어지고 자식 프로세스는 자신의 작업이 종료되면 부모 프로세스에게 결과를 돌려주고 종료됨
- 결과는 정상 수행이나 에러로 인한 종료를 구분하기 위한 값
- 로그인을 해서 bash shell을 실행하고 그 안에서 vi편집기를 실행하면 이 경우는 vi 프로세스가 자식 프로세스가 되고 bash shell이 부모 프로세스가 됨
- vi편집기 종료하면 결과를 bash shell에게 전달하고 종료됨

### 프로세스 번호
- 프로세스는 만들어질 때 관리의 편리성을 위해 고유번호 부여 PID(Process Identification Number)
- 이름 사용하지 않고 번호 사용하는 이유는 하나의 프로그램을 동시에 여러번 실행할 수 있기 때문에 일반적으로 네이밍 방법으로는 구분하기 어려움
- PID는 1번부터 일련번호 형태로 부여됨
- 부팅될 때 실행되는 systemd가 1번이고 kthreadd가 2번으로 생성, 나머지 프로세스는 이들의 자식
- 유닉스에서는 init 프로세스가 1번이었지만 우분투는 init의 이름을 systemd로 변경

### 프로세스 종류
- 리눅스의 프로세스 중 사용자가 실행한 경우에는 잠깐 실행되었다가 종료
- Daemon Process
  - 특정 서비스를 계속 제공하기 위해 존재
  - 커널에 의해서 실행
  - 평소에는 대기 상태로 있다가 요청이 오면 서비스를 제공
  - 서버에서 구동되는 프로세스들이 여기에 해당되는 경우가 많음

- Orphan Process
  - 자식 프로세스는 부모 프로세스가 종료되면 같이 종료가 되어야 하는데 부모 프로세스는 종료되었는데 종료되지 않고 남아있는 프로세스
  - 1번 프로세스가 새로운 프로세스가 됨
  
- Zombie Process
  - 자식 프로세스가 종료될 때 자신이 종료되었다는 사실을 부모 프로세스에게 알려주고 종료되는데 프로세스는 종료가 되었는데 부모 프로세스의 자식 프로세스 테이블에는 남아있는 형태
  - 자식 프로세스의 종료를 부모 프로세스가 제대로 처리를 하지 못해서 발생하게 되는데 프로세스 목록에서는 defunct라고 표시
  - 부모 프로세스는 자식 프로세스를 테이블 형태로 관리하는데 테이블의 용량이 유한
    테이블의 용량이 다 차면 더 이상 프로세스 생성 불가
  - 좀비는 실체가 없어서 kill 명령으로 종료 안됨, 부모 프로세스를 종료하거나 SIGCHLD 시그널을 부모 프로세스에게 보내서 좀비 프로세스를 찾아서 정리하도록 해야함
  - SIGCHLD 시그널을 보내면 이 프로세스를 고아 프로세스로 만들고 1번 프로세스가 부모 프로세스가 되고 일정 시간 단위로 1번 프로세스가 조회를 해서 제거

### 프로세스 목록 확인
- ps
  - ps [옵션]
    e: 모든 프로세스 정보 출력
    f: 프로세스에 대한 자세한 정보 출력
    u uid: 유저가 실행한 프로세스
    p pid: 프로세스 id에 해당하는 프로세스의 정보를 출력
    a: 터미널에서 실행한 모든 프로세스 정보를 출력
    u: 자세히 출력
    x: 시스템에서 실행한 모든 프로세스 출력
- 프로세스 검색 ```ps -ef | grep bash```

## 프로세스 관리
### 특정 프로세스 검색
- 기본형식: ```pgrep [옵션] [패턴]```
- 옵션
  x: 패턴과 일치하는 프로세스의 정보를 출력
  n: 패턴을 포함하고 있는 가장 최근 프로세스의 정보를 출력
  u: 사용자이름: 특정 사용자가 수행 중인 모든 프로세스를 출력
  l: PID와 프로세스 이름 출력
  t: 터미널 특정 단말기와 관련된 프로세스의 정보를 출력
- 특정 프로세스를 조회할 때 ps와 grep를 조합해서 수행, pgrep는 이 두개를 합쳐논 명령어

### 프로세스 종료
- 시그널
  - 프로세스에 무언가 발생했음을 알려주는 간단한 메시지
  - 현재 버전의 리눅스에서 사용가능한 시그널을 확인 ```kill -l```
  - SIGHUP(1): 터미널과 연결이 끊겼을 때 발생하는 시그널로 종료를 시켜줌
  - SIGINIT(2): 인터럽트(CTRL + c) 발생 
    - (Interrupt - 정상 수행 중에 강제로 중지), 현재 수행 중인 작업보다 우선순위가 높은 경우에만 중지
  - SIGQUIT(3): 종료 신호인데 사용자가 CTRL + \ 를 입력하면 발생
  - **SIGKILL(9): 프로세스를 강제로 종료시키는 시그널로 이 시그널을 받은 프로세스는 이 시그널을 무시할 수 없음**
  - SIGALRM(14): 알람에 의해서 발생
  - SIGTERM(15): kill 명령이 보내는 기본 시그널

- kill
  - 프로세스 종료 명령
  - 형식: ```kill [시그널] PID```

- pkill
  - 프로세스 이름으로 종료

- killall
  - 프로세스 이름을 종료

- top
  - 프로세스 정보를 주기적으로 출력

### 작업제어
- 포그라운드 작업
  - 터미널에서 작업할 때 일반적으로 사용자가 명령을 입력하면 쉘이 그 명령을 해석해서 커널에 전달해 실행을 하고 커널이 실행한 결과를 쉘이 받아서 화면에 출력하고 사용자는 화면에 출력된 결과를 보면서 대화식으로 작업을 수행
  - 사용자가 입력한 명령이 실행되서 출력될 때 기다리는 방식으로 처리되는 프로세스를 포그라운드 프로세스라고 함
  - 포그라운드 작업은 명령이 수행되는 동안에는 프롬프트가 출력되지 않기 때문에 다른 명령을 입력할 수가 없음
- 백그라운드 작업
  - 다른 프로세스를 실행되는 동안 뒤에서 실행되도록 하는 작업
  - 프롬프트에서 백그라운드로 프로세스를 실행시키면 작업은 뒤에서 실행되고 프롬프트는 바로 출력
  - 우분투에서 백그라운드로 작업을 시키는 방법은 작업 뒤에 &를 추가
  - 백그라운드로 수행시켜야 하는 작업은 웹 서버나 데이터베이스 서버 처럼 계속해서 구동되어 있어야 하는 프로그램이나 오랜 시간이 걸리는 작업
  - 백그라운드로 작업을 수행시킬 때는 바로 결과가 나오지 않기 때문에 작업이 수행 중인지 확인하는 것이 좋음
  100초 동안 현재 스레드를 중지시키는  프로세스를 백그라운드로 실행하고 확인, ps pgrep 사용

### jobs
  - 모든 백그라운드 작업을 조회하는 명령
  - 형식: ```jobs [%작업번호]```
```shell
  dh@dh:~$ jobs
  [1]+  Running                 sleep 100 &
```
  맨 앞의 1은 작업 번호로 작업이 늘어날 때마다 1씩 증가
  \+ 기호는 가장 최근에 수행된 백그라운드 작업
  Running은 작업 상태
  sleep 100은 작업 내용

- 작업 전환
  - ctrl + z: 포그라운드 작업을 중지
  - bg %작업번호: 작업 번호가 지시하는 작업을 백그라운드로 전환
  - fg %작업번호: 백그라운드 작업을 포그라운드로 전환

- 계속 실행
  - 일반적인 작업은 로그아웃을 하면 종료
  - 로그아웃 후에도 백그라운드에서 계속 작업이 수행되도록 하고자 할 때는 nohup 명령 & 로 실행시키면 됨

### cronjob(작업예약)
- 운영체제 제공 기능 이용
  - 프로그래밍 언어로 프로그램을 만들어서 이용
  - 응용 프로그램이 제공하는 기능 이용
    쿠버네티스 크론잡, 에어플로우
  - 정해진 시간에 한번만 실행
    at 명령으로 실행
- 형식
```shell
at [옵션] [시각] 
작업내용
```
```
- 옵션:
  l: 현재 실행 대기 중인 명령 목록을 출력
  r 작업번호: 작업번호에 해당하는 작업을 삭제
  m: 출력 결과가 없더라도 작업이 완료되면 사용자에게 메일로 알려줌
  f 파일경로: 작업을 직접 입력하지 않고 파일의 내용을 수행하고자 하는 경우
  - 시간 설정 방법: at 시간: 시간에 동작
```
```shell
  at 04:00 pm: 오후4시
  at 1 am tomorrow: 내일 오전 1시
  at 1 am jul 31: 7/31 1시
  at 4 pm + 3days: 3일 후 오후 4시
```
- 작업 확인 명령 ```ls -l /var/spool/cron/atjobs```
- 실습:
  - 오전 10시 50분에 ls -l 명령의 결과를 a.out에 출력
```bash
at 10:50 am
at>/usr/bin/ls -l > a.out
```
- 작업확인 
```sudo ls -l /var/spool/cron/atjobs```

### crontab - 주기를 가지고 작업을 계속 수행
- 형식: ```crontab [-u 사용자계정] [옵션] [파일 경로]```
```
- 옵션
    e: 사용자의 크론탭 파일 편집
    l: 크론탭 파일의 목록을 출력
    r: 크롭탭 파일 삭제
```
- crontab 명령으로 관리하는 파일은 사용자 별로 생성되는데 이 파일에 반복 실행할 작업을 저장
- 작성할 때 여러 개의 명령을 하나의 파일에 기록할 수 있는데 이 경우 각 명령은 별도의 행에 작성해야 함
- 작성 방법 ```분(00-59) 시간(00-23) 일(1-31) 월(1-12) 요일(0-6) 작업내용```
  - 요일은 0이 일요일
  - 앞에 5개 항목에서 *이 있으면 해당 항목의 모든 값을 의미
```
30 23 1 * * 작업 -> 매월 1일 23:30 분에 작업을 수행
30 * 1 * * 작업 -> 매월 1일 매시간 30분에 작업을 수행
```
  - 하이픈 연산자 사용하면 범위 설정 가능
  - 요일 설정할 때 1-5로 설정하면 월요일부터 금요일까지
  - ,를 이용해 여러개의 값 지정가능 ```1,3,5```
  - /를 이용해서 단계값을 설정가능 
  - ```1-10/2 -> 1,3,5,7,9```
  - ```*/20```
```bash
crontab -e # crontab 파일 생성
sudo -l /var/spool/cron/crontabs # crontab 목록확인
crontab -l # crontab 파일 내용 확인
crontab -r # crontab 삭제
```
### systemd service
- 리눅스 시스템과 서비스 관리로 유닉스의 init을 대체
- 다양한 서비스 데몬을 시작하고 프로세스들의 상태를 유지하고 시스템 상태를 관리하는 역할을 수행
- init에 비해 개선된점:
  - 쉘과 독립적으로 부팅 가능
  - 시스템 상태에 대한 스냅샷을 유지
  - 셧다운전에 사용자 세션의 안전한 종료가 가능

#### unit
- 서비스의 종류를 구분하기 위해 사용하는 개념
- systemd는 관리 대상의 이름을 서비스명:유닛종류 형태로 관리
```
- 종류:
  - service: 시스템 서비스 유닛으로 데몬을 시작, 재시작, 종료 및 로드
  - target: 유닛을 그룹화
  - automount: 디렉터리 계층 구조에서 자동 마운트 포인트를 관리
  - device: 리눅스 장치 트리에 있는 장치를 관리
  - path: 파일 시스템의 파일이나 디렉터리 경로를 관리
  - scope: 외부에서 생성된 프로세스를 관리
  - slice: 시스템의 프로세스를 계층적으로 관리
  - socket: 소켓을 관리하는 유닛
  - swap: 스왑 관리
  - timer: 타이머
```
#### 명령
- systemd를 위한 명령은 systemctl
- systemctl 명령을 이용해 서비스를 시작하거나 중지
```bash
systemctl [옵션] [명령] [유닛이름]
```
- 유닛 이름은 이름.service 이지만 .service는 생략 가능
```
- 옵션
  -a: 유닛 전체를 출력
  -t 유닛종류: 유닛 종류만 출력
- 명령
  start: 서비스시작
  stop: 서비스중지
  reload: 설정파일다시읽기
  restart: 재시작
  status: 유닛 상태를 출력
  enable: 부팅할 때 자동 시작하도록
  disable: 부팅할 때 자동 시작 않도록
  is-active: 동작 중인지 확인
  is-enabled: 부팅할 때 자동 시작 여부
  isolate: 지정한 유닛 및 이와 관련된 유닛만 시작하고 나머지는 중지
  kill: 유닛에 시그널
```
### cgroup
- 자원 사용을 프로세스 그룹 단위로 제어할 수 있는 리눅스 커널 기능
- CPU, Memory, Network, IO 등을 포함
- 컨테이너의 핵심 기술
- 사용방법
  - cgroup이라는 가상 파일 시스템을 수동으로 마운트해서 사용
  - libcgroup과 같은 툴을 사용해서 생성하고 관리
  - cgroup을 사용하는 소프트웨어(docker, LXC가상화 등) 활용
  
## 소프트웨어 관리
### 우분투에서의 패키지
* 리눅스에서 소프트웨어는 소스 코드 형식 및 바로 설치가 가능한 패키지 또는 압축된 형태로 배포
* 소스 코드는 직접 컴파일을 해서 사용
* 패키지는 자동 설치
* 압축된 형태는 압축을 풀어서 사용
* 패키지 형태로 배포가 될 때 압축을 해서 배포를 하는데 리눅스에서 주로 사용하는건 RPM과 deb 두가지 형식, 우분투가 deb 사용, redhat 계열이 RPM 사용
* 이 부분에서 CentOS(Rocky)와 Ubuntu가 명령어가 달라지게 됨
* 우분투에서는 snap이라는 형식이 추가
  * deb와 호환
  * 의존성 문제를 해결

#### 특징
- 파이너리 파일로 구성되서 컴파일을 할 필요 없음
- 패키지 파일이 관련 디렉터리에 자동으로 설치
- 패키지를 삭제하면 관련된 파일을 일괄적으로 삭제
- 기존 패키지를 삭제하지 않고 업그레이드 가능
- 패키지 설치 상태 검증
- 의존성 관련 패키지를 자동으로 설치: 의존성을 알 필요가 없음

#### 패키지의 카테고리
- main: 우분투에서 공식적으로 지원되는 버전으로 자유롭게 배포 가능
- restricted: 우분투에서 지원은 하지만 완전한 자유 라이선스 소프트웨어는 아님
- universe: 일반적으로 사용하는 것인데 자유 라이선스 여부를 알 수 없음, 기술 지원 여부도 보장하지 않음
- multiverse: 자유 라이선스 소프트웨어 이 외의 것을 포함

#### 패키지 이름
- 패키지이름_버전_데비안리비전우분투리비전넘버_아키텍쳐.deb

#### 패키지 저장소
- 패키지와 패키지에 대한 정보를 저장하고 있는 서버
- 페키지 저장소에는 패키지의 기능 추가나 보안 패치 등 지속적인 업그레이드를 수행하고 사용자는 이 저장소에 접속해서 최신 버전을 다운로드 받아서 사용
- 패키지 저장소에 대한 정보는 /etc/apt/sources.list 에 작성되있음
- 이 파일 수정하면 저장소를 추가하거나 삭제 가능
- 특별한 경우에는 이 파일에 private 저장소를 추가해서 사용하기도 함

### 패키지 관련 명령
#### APT 명령
- apt-cache 명령
  - APT 캐시(데이터베이스)에서 정보를 검색해서 출력
  - apt-cache [옵션] 서브명령
  - 옵션은 f(검색 결과로 패키지에 대한 전체 기록을 출력)와 h(간단한 도움말 출력)
```
서브명령
stats: 캐시에 대한 통계정보
dump: 현재 설치된 패키지를 업데이트
search 검색어: 검색어를 검색
showpkg 패키지명: 패키지에 대한 의존성과 역의존성을 출력
show 패키지이름: 패키지에 대한 정보를 출력
pkgnames: 사용가능한 모든 패키지를 출력
```
- apt-get 명령
  - 패키지 저장소를 업데이트하고 패키지를 설치하거나 제거
  - 형식
  - apt-get [옵션] 서브명령 [패키지이름]
```
옵션
d: 패키지를 다운로드 받음
i: 의존성이 깨진 패키지를 수정하려고 시도
h: 도움말

서브명령
update: 패키지 저장소에서 새로운 패키지 정보를 가져옴
upgrade: 현재 설치된 패키지를 업그레이드
install: 패키지를 설치
remove: 패키지삭제
download: 패키지를 현재 디렉터리에 다운로드
autoclean: 불안전하게 받은 패키지나 오래된 패키지를 삭제
clean: 캐시되어 있는 모든 패키지 삭제해 디스크 공간 확보
check: 의존성이 깨진 패키지 확인
```
- **apt-get update** 명령은 처음 리눅스를 설치했을 때 그리고 새로운 버전의 패키지를 설치하고자 할 때 수행
- **apt-get upgrade** 명령은 현재 컴퓨터에 설치된 패키지를 업그레이드. 리눅스를 오래전 설치해서 사용하면 새로운 버전의 패키지 배포된 경우 업그레이드할 때 사용
- **apt-get install** 명령은 다운로드 받아서 설치까지 진행하는 명령
  - 설치를 할 때 설치 여부를 묻는 대화상자가 나오게 됨
  - y 옵션 추가하면 설치 여부 묻는 대화상자 나오지 않음
  - 여러개의 패키지 한꺼번에 설치하는 것이 가능 ```sudo apt-get install -y a b c d```
  - 설치만 하고 업그레이드를 하지 않고자 할 때는 맨 뒤에 --no-upgrade 추가
  - 새로 설치는 하지 않고 업그레이드만 하고자 할 때는 --only-upgrade
- apt-get remove 명령은 패키지 제거
  - 패키지 삭제는 하지만 설정 파일은 남겨둠
  - 설정파일까지 지울 때는 --purge 옵션을 이용
- apt-get autoremove 명령은 불필요한 패키지를 정리
  - 시스템이 설치될 때 자동으로 설치했으나 불필요한 패키지들이 있을 수 있음
- **apt-get clean** 명령은 검색했거나 내려받은 패키지 파일을 삭제
- apt-get download 패키지이름 : 패키지 다운로드만 받는 것도 가능
- apt-get source 패키지이름 : 소스코드를 다운로드

#### dpkg 명령
- Fedora(CentOS, Rockey) 버전에는 yum이나 dnf, rpm(rpm->yum->dnf)이라는 명령어로 패키지 관리
- apt-get명령은 yum, dnf에 해당하는 패키지 관리 명령어
- dpkg는 rpm에 해당하는 명령
- 설치만 하는 경우 apt-get명령으로 충분한데 시스템의 특정 파일이 어느 패키지에 속했는지를 확인하는 것처럼 세부적인 기능을 사용하고자 할 때 활용
- 형식: ```dpkg [옵션] 패키지이름 또는 파일이름```
  ```
  옵션
  l: 설치된 패키지 목록 출력
  l 패키지이름: 패키지의 설치 상태
  s 패키지이름: 패키지의 상세 정보 출력
  S 경로명: 경로명이 포함된 패키지를 조회
  L 패키지명: 패키지가 설치한 파일 목록 출력
  c deb파일: deb 파일의 내용을 출력
  i deb파일: 설치
  r 패키지이름: 삭제
  P 패키지이름: 해당 패키지와 설정 정보를 같이 삭제
  X deb파일 디렉터리: 디렉터리에 압축 해제
  ```
#### aptitude 명령
- apt-get 과 유사한 명령어로 패키지를 관리해주는 명령어

#### 스냅 패키지
- 우분투가 새로 도입한 패키지 형식
- 샌드박스 형태의 패키지
- 패키지를 만들 때 프로그램이 사용하는 모든 라이브러리를 패키지 안에 포함시키는 방식
- 스마트폰 애플리케이션이 이 방식 이용
- 장점: 개발자가 다른 패키지나 라이브러리 외의 의존성 신경 안써도됨, 기존 시스템과 완전히 격리되 보안 강화
- 단점: 패키지 용량이 커짐
- 명령: ```snap [옵션] 명령 [패키지이름]```
- 옵션은 h로 도움말 출력
 ```
명령
  disable
  download
  enable
  find
  info
  install
  list
  remove
```

#### wget 명령
- 리눅스에서 패키지 형태가 아닌 압축 파일 형태로 제공되는 애플리케이션도 존재
- 이런 경우 wget 명령으로 다운로드 받아서 사용
  ```
  wget 다운로드경로
  wget https://www.ebi.ac.jk/~zerbino/velvet_1.2.10.tgz
  ```

### 파일 압축 및 해제
- 아카이브는 파일을 묶어서 하나로 만드는 작업

#### 파일 아카이브
- tar(tape archive): 여러 파일이나 디렉터리를 묶어서 하나로 만드는 명령 또는 작업
- 명령 형식 ```tar 기능 [옵션] [아카이브파일] [파일명]```
- 기능: 옵션과 사용 방법은 동일하나 -를 붙이지 않음
  ```
  c: 새로 생성
  t: 내용 출력
  x: 원본 파일을 추출
  r: 새로운 파일을 추가
  u: 수정된 파일을 업데이트
  ```
- 옵션
  ```
  f: 아카이브파일이나 장치를 지정
  v: 처리하고 있는 파일의 정보를 출력
  h: 심볼릭 링크의 경우 원본 파일을 포함
  p: 파일을 복원할 때 원래의 접근 권한을 유지
  j: bzip2로 압축하거나 해제
  z: gzip으로 압축하거나 해제
  ```
- 압축을 할 때 cvf를 이용하고 압축 해제를 할 때는 xvf를 주로 이용
```bash
tar cvf file.tar file1 file2 # 압축
tar xvf file.tar # 압축해제

tar rvf file.tar file3 # file.tar에 file3추가
```

## Shell Programming
- 리눅스의 셸 스크립트는 C언어와 유사한 방법으로 프로그래밍 할 수 있음
- 셸 스크립트 파일의 확장자는 sh
- 최상단에는 #!/bin/sh 를 추가 -> 셔뱅: bash 셸을사용하겠다는 의미
- #으로 시작하면 주석이지만 #!는 주석이 아님

### 스크립트 파일 실행 방법
- sh 스크립트 파일경로 - 읽기 권한만 있으면 실행
- 스크립트 파일의 경로 - 현재 디렉터리에 있는 경우 ./ 를 추가해서 경로를 작성, 실행 권한 필요
```bash
./test.sh
sh test.sh
```

### 변수
- 기본적으로 변수에 넣는 값은 전부 문자열로 취급
- 변수 이름은 대소문자 구분
- 데이터 대입시 = 좌우에 공백 없어야
- 값에 공백이 있는 경우는 ""로 묶어 줘야
- $가 들어간 내용 출력시 "로 묶어주거나 \ 붙여줘야

### 계산식 사용
- 백틱 안의 expr로 시작해서 작성
- 수식에 괄호를 사용하거나 곱하기인 *를 사용힐 때는 \ 를 붙여야
  ```bash
  n=`expr 100 + 200`
  n=`expr 100 \* 300`
  echo $n
  ```

### 파라미터 설정
- 실행할 때 같이 넘겨주는 데이터
- 파라미터를 사용할 때는 $파라미터위치
- $0은 파일명
```bash
  vi param.sh
  1 #! /bin/sh$
  2 echo "$0 $1 $2"$
  3 echo "$2"$

  chmod 775 param.sh
```

### 제어문
#### if
```bash
if [ 표현식 ]
then
    참일 때 수행할 내용
else
    거짓일 때 수행할 내용
fi
```
```bash
파일 경로 조건
  -d 파일경로: 디렉터리이면 참
  -e 파일경로: 존재하면 참
  -f 파일경로: 일반 파일이면 참
  -g 파일경로: setGID가 설정되면 참
  -r 파일경로: 읽기 가능이면참
  -s 파일경로: 크기가 0이 아니면 참
  -u 파일경로: setUID가 설정되면 참
  -w 파일경로: 쓰기 가능이면 참
  -x 파일경로: 실행 가능이면 참d
```

- /lib/systemd/system/cron.service 라는 파일의 존재 여부를 확인해서 존재하면 존재한다고 않다고 메시지 출력

```bash
  1 #! /bin/sh
  2 if [ -f /lib/systemd/system/cron.service ]
  3 then
  4   echo Hello World
  5 else
  6   "No FILE"
  7 fi
```

#### case - esac
- 값으로 분기
- 형식
  ```bash
  case 데이터 in
        값)
            값일 때 수행할 내용
        값)
            값일 때 수행할 내용
        *)  
            나머지 경우 수행할 내용
  esac
  ```
  - case 구문에 각 값 안에서 여러 개의 실행문을 작성할 수 있기 때문에 내용을 작성할 때 마지막에 ;; 를 추가해줘야함
  - 여러 개의 값에 동일한 내용을 수행하고자 하는 경우는 ```값 | 값``` 형태로 작성
```bash
#! /bin/sh

case "$1" in
s | S | start)
  echo "HI";;
e)
  echo "E";;
*)
  echo "NO OHTER";;
esac
```

#### and, or
- and - &&, -a
- or - ||, -o
- `if [조건] && [조건]` 의 형태로 입력
- lib/systemd/system/cron.service 가 있고 홈 디렉터리에 if.sh파일이 있다면 성공 그렇지 않다면 실패라고 출력
  ```bash
  #! /bin/sh
  if [ -f /lib/systemd/system/cron.service ] && [ -f ~/if.sh ]
  then
      echo "success"
  else
      echo "fail"
  fi
  ```
#### for ~ in
- 형식
  ```bash
  for 임시변수 in 데이터나열
  do
      데이터를 임시변수에 하나씩 대입하고 수행할 문장
  done
  ```
  ```bash
  for i in 1 2 3 4 5
  do
      hap=`expr $hap + $i`
  done
  echo $hap
  ```
- 현대 디렉터리의 모든 txt 파일을 읽어서 내용을 출력
  ```bash
  for fname in $(ls *.txt)
  do
      cat $fname
  done

#### while
- 표현식이 거짓이 될 때까지 반복
- 형식
  ```bash
  while [표현식]
  do
      표현식이 거짓이 아니면 수행할 내용
  done
  ```
- 1부터 5까지의 합
  ```bash
  hap=0
  i=1
  while [ $i -le 5 ]
  do
      hap=`expr $hap + $i`
      i=`expr $i + 1`
  done
  echo "Total: $hap"
  ```
#### 기타 제어문
- break, for 나 while을 강제로 중단하고자 할 때 사용
- until: 반복문
- continue: for나 while의 시작 부분으로 이동
- exit: 프로그램 완전히 종료, 상위 프로세스에게 넘겨줄 정수를 같이 사용 `exit 0`
- return: 함수를 호출한 곳으로 돌아가는 제어 명령

### Function
- 자주 사용하는 구문을 묶어서 하나의 이름으로 사용하는 것
- 메모리를 별도로 할당 받아서 사용

#### 생성
```bash
이름(매개변수 나열){
    함수 내용
    return
}
```

#### 호출
- `함수이름(매개변수)`
- 매개변수가 없는 경우 이름만으로 호출 가능
  
```bash
myfunc () {
  echo "My Function"
  return
}
myfunc
exit 0
```

#### eval
- 문자열을 명령으로 수행
- 파이썬이나 자바스크립트에서 이 함수가 문자열을 데이터로 치환
  ```bash
  ls -l
  eval "ls -l"
  ```