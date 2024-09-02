---
title: Redis
linkTitle: Redis
weight: 3
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---

### 1. DB종류 분류
* RDBMS와 NoSQL
* DISK 기반의 DB와 In Memory DB

### 2. In Memory DB
* 디스크에 데이터 저장않고 메모리 저장했다가 요청있으면 메모리 데이터를 빠르게 돌려주는 방식
* 디스크보다는 메모리가 빨라 고속으로 컨텐츠 제공 장점

### 3. REDIS (REmote Dictionary Server)
* 오픈소스 인 메모리 key-value Data Store
* key는 중복불가->UPSERT 개념, key는 해싱을 이용
* 사용사례: 캐싱, 세션관리(네트워크에서 정보 저장하는 공간), pub/sub, 순위표
* BSD 라이선스 (오픈소스), C언어로 구현됨, 다양한 프로그래밍 언어 지원
* 퍼블릭 클라우드에서도 유사한 서비스 제공
* 클러스터 기능 제공 - 확장 가능
* 백업 기능 제공 - 디스크에 저장 가능
* 싱글스레드 기반->이벤트 큐를 이용해 싱글스레드 구현
* 백업 방법
 * RDB 방식: 스냅샷(데이터 전체의 복사본) 이용
  * 간단-복원할 때 스냅샷만 복사해서 붙여넣으면 됨
  * 단점-스냅샷 이후의 변경 데이터는 복원 불가
 * AOF(Append Only File)
  * 변경된 작업을 저장해서 복원
  * 장점-복원 시 데이터 유실량 거의 없음
  * 단점-용량이 커지고 시간 오래 걸림
* 실제 구현을 할 때는 Master와 Replica 서버를 만들어서 Master에 작업을 수행하고 Master에 변경이 생기면 Replica서버에 복제하는 방식으로 구현
* Master에 장애가 발생하면 Replica 서버가 Master가 되도록 해서 장애에 대비
* 센티넬이 마스터-클라이언트 중계

## 참고
### TCP/IP
클라이언트 -----요청------> 서버
          <-----키발급----
          -----키/요청---->

### 멀티스레드
* 동시수행 생각
* mutual exclusion
* Synchronized
* Dead Lock