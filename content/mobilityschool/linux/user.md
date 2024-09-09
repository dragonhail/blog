---
title: Ubuntu 사용자 관리
linkTitle: 사용자 관리
weight: 2
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---

## 사용자 계정 관련 파일
### /etc/passwd
- 사용자 계정 정보가 저장된 기본 파일
- 초창기에는 암호도 저장되었지만 지금은 암호는 /etc/shadow 파일에 저장
- 구조
  - 7개의 항목으로 구성, 콜론으로 구분
  - 로그인ID:x:UID:GID:설명:홈디렉터리:로그인쉘
  - x는 예전에 비밀번호 저장하던 영역인데 호환성 문제 때문에 남아있음
  - UID는 사용자를 구분하기 위한 번호로 일반적으로 0~9999 번과 65534는 시스템 사용자를 위한 UID로 예약되어 있고 일반 사용자는 1000번 부터 할당
  - root가 0번, 시스템 데몬이 1, 명령어를 위한 관리 계정이 2
  - GID는 사용자가 속한 그룹의 ID로 사용자를 등록할 때 정해지고 특별히 소속 그룹을 지정하지 않는 경우 로그인 ID가 그룹으로 등록
  - 그룹에 대한 정보는 /etc/group 에 저장
  - 설명은 사용자의 실제 이름이나 부서명 같은 것을 적을 수 있는 부분
  - 홈디렉터리: 로그인을 했을 때 자동으로 로그인 되는 디렉터리의 절대 경로
  - 로그인 쉘은 로그인했을 때 처음 보여지는 쉘
  - 로그인 쉘

### /etc/shadow
- 사용자 암호에 대한 정보를 저장하는 파일
- 9개 영역으로 구성 -> ID:비밀번호:비밀번호 변경날짜:비밀번호 변경하고 사용해야 하는 최소 날짜:비밀번호 변경하고 사용해야 하는 최대 날짜:경고 발생할 날짜:비밀번호가 유효한 마지막 날짜:미래를 위해서 만든 항목
- 비밀번호 영역은 단방향 암호화를 이용해서 저장, 시스템계정은 *
- 단방향 암호화: 암호화한 내용과 평문 비교해서 일치 여부는 알 수 있지만 복원은 안됨
- 양방향 암호화: 암호화한 내용을 기반으로 원래 내용을 만들 수 있는 방식
- 비밀번호 변경 날짜: 1970/1/1 을 기준으로 지나온 날짜
```bash
dh@dh:~$ sudo cat /etc/shadow  | grep user3
[sudo] password for dh: 
user3:$y$j9T$TDKiiNpxhl096xX71cg0W1$k1dnZsYuMuXn4mchUNSqZtRl6f7OCi1NztcQExFQqIC:19975:0:99999:7::20088:
```

### /etc/login.defs
- 로그인과 기본 설정 파일
- 주요 설정 값
  - MAIL_DIR -> /var/mail : 기본 메일 디렉터리
  - PASS_MAX_DAYS -> 99999
  - PASS_MIN_DAYS -> 0
  - PASS_WARN_AGE -> 7
  - UID_MIN, UID_MAX -> 1000~60000: 사용자 계정의 UID 범위
  - SYS_UID_MIN, SYS_UID_MAX -> 100~699: 사용자 계정의 UID 범위
  - GID_MIN, GID_MAX -> 1000~60000: 사용자 계정의 GID 범위
  - SYS_GID_MIN, SYS_GID_MAX -> 100~699: 사용자 계정의 GID 범위
  - DEFAULT_HOME -> yes: 사용자 홈 디렉터리 생성 여부
  - UMASK -> 0002: umask 값 설정
  - USERGROUP_ENAB: yes: 계정 삭제 시 그룹 삭제 여부
  - ENCRYPT_METHOD -> SHA512: 암호화 기법

### /etc/group
- 그룹의 정보가 저장된 파일
- 리눅스에서 사용자는 하나 이상의 그룹에 속해야 함
- 기본 그룹은 /etc/passwd에 작성되어 있고 2차 그룹에 대한 내용을 /etc/group에 작성
- 그룹이름:x:GID:그룹멤버

### /etc/gshadow
- 그룹 암호가 저장된 파일
- 유닉스에는 없는 파일

## 계정 관리 명령
### 사용자 계정 생성
- 형식
  - `useradd [옵션] [로그인ID]`
  - 옵션
  ```
  u: UID 지정
  o: UID 중복 허용
  g: GID 지정
  G: 2차 그룹 지정
  d: 홈 디렉터리 지정
  s: 기본 쉘
  c: 부가적인 설명
  D: 기본값을 설정하거나 출력
  e: EXPIRE 항목을 설정
  f: 비활성 설정
  k: 계정 생성할 때 사용할 초기화 파일을 저장한 디렉터리 설정
  ```
- 사용자 계정 시 설정된 옵션은 vi를 이용해서 /etc/default/user 파일을 수정해서 변경할 수 있지만 되도록이면 -b, -e, -f -g, -s 와 같은 옵션을 이용해서 수정하는 것을 권장
- 옵션을 이용한 사용자 계정 설정
```bash
dh@dh:~$ sudo useradd -s /bin/bash -m -d /home/user2 -u 2000 -g 1000 -G 3 user2
[sudo] password for dh: 
dh@dh:~$ grep user2 /etc/passwd
user2:x:2000:1000::/home/user2:/bin/bash
```
- 사용자 계정을 생성할 때는 `sudo passwd 새유저` 명령을 이용해서 비밀번호를 설정을 해야함
- 사용자 계정이 만들어질 때의 옵션 확인: `useradd -D`
- EXPIRE 변경: `sudo useradd -D -e 2024-12-31`
```bash
dh@dh:~$ useradd -D
GROUP=100               # 그룹 ID
HOME=/home              # 홈 디렉터리 생성 위치
INACTIVE=-1             # 0으로 설정하면 암호가 만료되자 마자 바로 계정이 잠김, -1: 1의 2의 보수 (1111, 음수가 없을 때 가장 큰 수 의미)
EXPIRE=                 # 계정 종료일
SHELL=/bin/bash         # 기본 로그인 쉘을 설정
SKEL=/etc/skel          # 홈 디렉터리에 복사할 기본 환경 파일의 경로
CREATE_MAIL_SPOOL=no    # 메일 디렉터리 생성 여부 
LOG_INIT=yes            # 로그
```

```bash
/etc/skel 디렉터리

dh@dh:~$ ls -al /etc/skel
total 28
drwxr-xr-x   2 root root  4096 Aug 28 00:37 .
drwxr-xr-x 139 root root 12288 Sep  9 12:33 ..
-rw-r--r--   1 root root   220 Mar 31 17:41 .bash_logout
-rw-r--r--   1 root root  3771 Mar 31 17:41 .bashrc
-rw-r--r--   1 root root   807 Mar 31 17:41 .profile
```
- adduser 명령
- 사용자계정을 생성하는 명령
- 형식
  ```
  adduser [옵션] 로그인ID
  옵션
    --uid
    --gid
    --home
    --shell: 
    --gecos: 설명을 붙여주는 옵션
  ```
- 생성할 때 옵션 적용 내용이 출력됨
```bash
dh@dh:~$ sudo adduser user3
info: Adding user `user3' ...
info: Selecting UID/GID from range 1000 to 59999 ...
info: Adding new group `user3' (1002) ...
info: Adding new user `user3' (1002) with group `user3 (1002)' ...
info: Creating home directory `/home/user3' ...
info: Copying files from `/etc/skel' ...
New password: 
BAD PASSWORD: The password is a palindrome
Retype new password:
passwd: password updated successfully
Changing the user information for user3
Enter the new value, or press ENTER for the default
        Full Name []: userdh
        Room Number []: none
        Work Phone []: none
        Home Phone []: none
        Other []: none
Is the information correct? [Y/n] y
info: Adding new user `user3' to supplemental / extra groups `users' ...
info: Adding user `user3' to group `users' ...
```
- 생성한 유저 확인
```bash
dh@dh:~$ tail -3 /etc/passwd
newdh:x:1001:1001::/home/newdh:/bin/sh
user2:x:2000:1000::/home/user2:/bin/bash
user3:x:1002:1002:userdh,none,none,none,none:/home/user3:/bin/bash
dh@dh:~$ cat /etc/passwd | grep user3
user3:x:1002:1002:userdh,none,none,none,none:/home/user3:/bin/bash
```
- adduser로 유저를 생성할 때는 /etc/adduser.conf 파일을 기반으로 함, useradd와 달리 bash shell 사용

### 계정 수정
- 명령 형식 `usermod [옵션] [로그인ID]`
- 옵션
  ```
  u: UID 수정
  o: UID 중복 허용
  g: 기본 그룹 수정
  G: 2차 그룹 수정
  d: 홈 디렉터리 수정
  s: 기본 쉘 수정
  c: 보충 설명 수정
  f: 계정 비활성화 날짜를 수정
  e: 계정 만료날짜 수정
  i: 계정 이름 변경
  ```
- UID를 수정해서 중복을 허용하게 되면 사용자ID가 달라도 동일한 계정으로 로그인 한 것으로 간주

### 패스워드 에이징
- aging - 시간이 지남에 따라 기다린 시간 만큼 우선순위가 높아지는 것 ( 작업시간 + 대기시간 / 대기시간)
- 패스워드 에이징: 비밀번호의 유효 기간을 설정하는 것
- 관련 명령
```
            useradd, usermod, passwd 명령 수정          change 명령으로 수정
  - MIN         passwd -n 날짜                              change -m
  - MAX         passwd -x 날짜                              change -M
  - WARNING     passwd -w 날짜                              change -W
  - INACTIVE    useradd -f 날수, usermod -f 날수            change -I
  - EXPIRE      useradd -e 날짜, usermod -e 날짜            change -E
```
```bash
dh@dh:~$ sudo usermod -u 3003 user2
[sudo] password for dh:
dh@dh:~$ cat /etc/passwd | grep user2
user2:x:3003:1000::/home/user2:/bin/bash
```
###
- 기존의 값을 확인 `sudo cat /etc/shadow | grep user3`
- 변경: `sudo usermod -f 10 -e 2024-12-31 user3`
```bash
dh@dh:~$ sudo cat /etc/shadow | grep user3
user3:$y$j9T$TDKiiNpxhl096xX71cg0W1$k1dnZsYuMuXn4mchUNSqZtRl6f7OCi1NztcQExFQqIC:19975:0:99999:7:10:20088:
```