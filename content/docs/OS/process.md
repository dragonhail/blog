---
title: 프로세스
toc: true
breadcrumbs: false
weight: 1
---
## 동기식 입출력
* 입출력이 끝나고 난 후 프로세스 instruction 실행
### 구현방법 1
* IO 끝날 때 까지 CPU 대기
### 구현방법 2
* 다른 프로세스한테 CPU 줌

## 비동기식 입출력

## 프로세스 문맥
* 백업 용도: 어느 시점 까지 시행했는지
* 문맥 교환: 프로세스 A->프로세스 B, 오버헤드 큼

### 하드웨어 문맥
* CPU 수행상태 나타냄
  * program counter
  * register

### 프로세스 주소공간
* code: 기계어
* data: 변수
* stack: 함수

### 커널 상의 문맥
* data: PCB 생성해 프로세스 별 관리
* stack: 프로세스 마다 스택 따로 생성해 관리

## 프로세스 상태
* running ready blocked

## 스케줄러
### short-term scheduler
* 프로세스에 CPU 할당

### mid-term scheduler (swapper)
* 프로세스에서 메모리 박탈, 여유공간 위애 디스크로 메모리 쫓아냄 (프로세스 상태: suspended)

# 프로세스 생성
## 시스템 콜
* fork 시스템 콜로 OS에 부모 복제 요청
* exec 프로세스 덮어쓰기
* exit 
  * 자발적: 자식이 부모에게 output data 보낸 후 자식 종료-> 부모 종료
  * 비자발적: 부모 또는 외부에서 강제 종료 (kill, break)
* abort 부모가 강제로 자식 종료
* wait 자식 프로세스 종료될 때 까지 부모 block

## Copy-on Write (CoW)
* 부모 code, data, stack 내용이 바뀔 때 새로운 메모리 생성

## IPC (프로세스 간 통신)
### message passing
* 커널을 통해 메시지를 전달
* direct, indirect communication

### shared memory
* 주소 공간 공유

# CPU Scheduling
## IO bound job
* 사람이 사용
## CPU bound job
* CPU가 사용
