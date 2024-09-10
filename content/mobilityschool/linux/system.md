---
title: 시스템 관리
linkTitle: 시스템 관리
weight: 3
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---
# 디스크 사용량 설정
- 리눅스는 기본적으로 여러 사용자가 한꺼번에 사용하는 시스템
- 디스크 사용량을 제한하는 기능을 제공: 디스크 쿼터
- 설정 방식
  - 사용자가 사용할 수 있는 파일의 전체 용량을 설정
  - 파일의 개수를 제한
- 쿼터 설정 시 한계치 설정
  - hard limit: 절대로 넘어설 수 없는 용량을 설정
  - soft limit: 일정 시간 동안은 용량을 넘어설 수 있는 방식

### 사용하는 패키지: quota
- 스크립트로 자동화시 `-y`옵션 필수, 대화상자 뜨면 안됨
```bash
sudo apt upgrade
sudo apt install -y quota
```

### 준비
- 파일 시스템의 마운트 옵션에 쿼터 속성을 설정
  - usrquota: 개별 사용자의 쿼터를 제한할 수 있는 속성
  - grpquota: 개별 그룹의 쿼터를 제한할 수 있는 속성
- 쿼터 속성 설정은 /etc/fstab 파일에 설정
```
df -TH # 현재 파일 시스템 확인
ls /dev # 디바이스 확인
```

### 실습
- 루트에 실습 위한 디렉터리와 계정 생성
  ```
  sudo mkdir /home2
  
  sudo mount /dev/sda2 /home2 # 마운트: 디렉터리를 어떤 디스크에 생성할 것인지 설정

  sudo useradd -m -d /home2/qtest1 qtest1
  sudo useradd -m -d /home2/qtest2 qtest2

  ls /home2
  tail -2 /etc/passwd
  ```

### 쿼터 속성 설정 - /etc/fstab 
```
파일시스템이름 디렉터리경로 파일시스템종류 defaults,usrquota 1
/dev/sda2 /home2 ext4 default,usrquota 1 1
```
- remount `sudo mount -o remount`
- mount 정보 확인 `mount` 

### 쿼터 데이터베이스 파일을 생성
- 명령 - `quotacheck`
- 쿼터 파일을 생성 및 확인 그리고 수정하기 위해서 파일 시스템을 스캔하는 명령
- 형식: `quotacheck [옵션] [파일시스템]`
- 옵션:
  ```
  a: 전체 파일 시스템을 체크
  u: 사용자 쿼터를 확인
  g: 그룹 쿼터를 확인
  m: 파일 시스템을 리마운트하지 않음
  v: 명령 진행 상황을 상세하게 출력
  ```
- 명령 실행 `quotacheck -ugvm /home`
  - 2개의 데이터베이스 파일이 생성
    - aquota.usr: 사용자 쿼터 데이터베이스 파일
    - aquota.group: 그룹 쿼터 데이터베이스 파일
- 쿼터 사용 활성화: `quotaon`
  - `quotaon [옵션] [파일시스템]`
  - 옵션
  ```
  a: 전체 파일 시스템에 적용
  u: 사용자 쿼터 활성화
  g: 그룹 쿼터 활성화
  v: 명령 진행 상황을 상세히 출력
  ```
- 명령 수행 `sudo quotaon -uv /home2`
- 쿼터 설정 및 확인
  - 명령: edquota
  - 형식: `edquota [옵션] [사용자계정이나 그룹]`
  - 옵션
  ```
  u: 사용자쿼터 설정
  g: 그룹 쿼터 설정
  p: 쿼터 설정 복사
  ```
- `-u`옵션을 이용하면 쿼터 편집 창이 나오게 되는데 원하는 크기를 soft와 hard에 설정하고 저장한 후 빠져나오면 됨
- 주의할 점은 단위가 KB, 설정할 때 값을 0으로 설정하면 무한대
- 쿼터 확인 `quota [옵션] [사용자계정 및 그룹]`
  - 옵션은 u 와 g

# 네트워크 서비스 관리
### 네트워크 설정
- 리눅스에서 네트워크를 사용하기 위한 준비:
  - IP: 현재 컴퓨터를 인터넷 또는 LAN에서 구분하기 위한 주소
  - Netmask: 동일한 네트워크를 구분하기 위한 주소
  - Broadcast 주소: 동일한 네트워크에 있는 모든 컴퓨터에 데이터를 전송하기 위한 주소
  - 게이트웨이 주소: 내부 네트워크에서 외부 네트워크로 나가가 위한 주소
  - DNS 주소: 도메인 네임 서비스로 설정이 안되어 있으면 도메인을 사용할 수 없음

### 네트워크 관리자
- 네트워크 제어와 설정을 관리하는 데몬(백그라운드 작업으로 대기하고 있다가 사용자 요청이 오면 처리하는 프로세스)
- 네트워크 관리자를 이용해서 IP주소설정, 고정 라우터 설정, DNS 설정이 가능
- 예전에는 네트워크 설정을 관리자를 이용하지 않고 ifcfg 라는 설정 파일을 이용
- 현재는 이러한 설정 파일도 지원
- 지원하는 도구
  - 네트워크 관리자: 기본 네트워킹 데몬
  - nmcli 명령: 네트워크 관리자를 사용하는 명령 기반 도구
  - [설정] - [네트워크]: GUI 도구
  - nm-connection-editor: 네트워크 관리자를 사용하는 GUI 기반 도구
- 설치가 안된 경우 network-manager를 설치
  - `sudo apt install network-manager`
- 서비스 실행 여부 확인
  - `systemctl status NetworkManager`
  - active 상태가 아니라면 start 명령으로 시작해주어야 함
  - `sudo systemctl start NetworkManager`
  - `sudo systemctl enable NetworkManager`
- GUI로 설정
  - [설정] - [네트워크]
  - 터미널에서 `nm-connection-editor` 명령 수행

### nmcli 명령으로 네트워크 설정
- `nmcli`: 명령 기반으로 네트워크 관리자를 설정
- 기본 형식 `nmcli [옵션] 명령 [서브 명령]`
- 옵션
  ```
  t: 실행 결과를 간단히
  p: 사용자가 읽기 좋게
  v: 버젼
  h: 도움말
  ```
- 서브명령 
- `general [status | hostname]` - 네트워크 관리자의 전체적인 상태를 출력
- `networking {on | off | connectivity}` - 네트워크를 시작하고 연결 상태를 출력
- `connection {show | up | down | modify | add | delete | reload | load}` - 네트워크 설정
- `device {status | show}` - 네트워크 장치의 상태를 조회

- 전체 상태 확인: `nmcli general`
- 네트워크 실행 및 중지: `nmcli networking on 또는 off`
- 네트워크 설정: connection(con)
  - 서브명령
  ```
  show: 기본 옵션으로 네트워크 연결 프로파일을 출력
  up: 네트워크 연결 시작
  down: 네트워크 연결 중지
  modify: 연결 프로파일에서 속성을 추가 및 수정 그리고 삭제
  add: 새로운 연결 생성
  delete: 연결 삭제
  reload: 연결과 관련된 파일 다시 읽기
  load: 연결 파일 읽기
  ```
- 연결 확인 `nmcli con show`
  - UUID(Universally Unique IDentifier) - 네트워크 상에서 고유성을 보장하기 위한 구별하기 위한 문자열, 128비트의 숫자인데 32자리의 16진수로 표현하는 것이 일반적
  - DEVICE: 외부와 통신할 때 사용하는 네트워크 인터페이스의 명칭
- 연결 중지 `nmcli con down 이름`
- 사용 `nmcli con up 이름`
- 연결 추구 
  `nmcli connection add type ethernet con-name 이름 ifname 인터페이스이름 ip4 주소/넷마스크비트수 gw 게이트웨이주소`
- 연결 수정
  `nmcli connection modify 커넥션이름 속성 값`
  - 수정은 게이트웨이나 IP를 수정
- IP 주소 변경
  - `nmcli con mod 연결이름 ipv4.address IP주소`