---
title: OS
toc: true
breadcrumbs: false
weight: 5
---
## 시스템 콜
## 인터럽트

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
* short-term scheduler
* swapper