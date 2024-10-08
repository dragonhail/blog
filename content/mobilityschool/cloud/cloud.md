---
title: Cloud
weight: 1
---
## Cloud
### On-Premise
- 자체 데이터 및 솔루션 등을 저장하기 위해서 데이터 센터를 구축해서 IT서비스를 수행하는 방식 - Private Cloud
- 하드웨어를 포함한 모든 자원에 대한 초기 투자 비용과 탄력적이지 않은 제한된 용량으로 인해서 지속적 관리 비용이 증가하는 단점이 있지만 기업에 내재화된 서비스를 통해 품질 및 보안에 대한 신뢰도가 높고 아주 장기적으로 사용하면 비용이 감소될 수도 있음
- 최근에 많은 기업이 On-Premise 대신에 퍼블릭 클라우드를 선호하는 경향이 있는데 이는 높은 초기 투자 비용과 운용에 따른 추가 비용 때문
- 초기 투자 비용이 많이 드는 이유 중 하나로 들었던 것은 처음 설계를 할 때 확장성을 고려하지 않고 최대 사용량을 근거로 했기 때문 - 최근에는 엔지니어들이 늘어서 이런 부분은 어느 정도 해소가 됨
- Public Cloud Computing을 사용하는 경우 서비스에 대한 정확한 관리 및 조정 능력이 필요하고 적절한 비용 산정이 어려움

### Cloud Computing
- 자원을 물리적으로 현재 위치에 두는 것이 아니라 위치에 상관없이 자원을 사용할 수 있고 확장과 축소를 자유자재로 할 수 있는 환경
- 네트워크와 인터넷에 대한 개념이 없어도 연결하기만 하면 서비스를 이용할 수 있는 환경
- Cloud 이용자는 IT 자산을 소유하는 것이 아니라 서비스로 이용하는 모델

### 정보처리의 역사
- MainFrame을 이용
- 클라이언트 서버 모델
- 그리드 컴퓨팅과 같은 분산 처리 시스템
- 클라우드 컴퓨팅

### 클라우드 컴퓨팅이 등장한 배경
- 다양한 기술의 발전
  - CPU, GPU, TPU 등의 처리 속도 고속화
  - 가상화 기술과 분산 처리 기술 등의 발전
  - 모바일의 음성
  - 빨라지고 저렴해진 네트워크
  - 거대해진 데이터 센터에 의한 규모의 경제(스케일 메리트)

### Cloud의 정의
- NIST(미국 국립 표준 기술 연구소): 공유 구성이 가능한 컴퓨팅 리소스(네트워크, 서버, 스토리지, 애플리케이션 서비스 등)의 통합을 통해서 어디서나 간편하게 요청에 따라 네트워크를 통해 접근하는 것을 가능하게 하는 모델이며 이는 최소한의 이용 절차 또는 서비스 공급자의 상호 작용을 통해서 신속히 할당되어 제공되는 것

### Cloud의 특징
- On-Demand Self-Service: 사용자가 별도의 기술 습득없이 필요할 때 온라인으로 즉시 사용
- Broad Network Access: 네트워크를 통한 컴퓨팅 자원 접근 - Any Time, Any Place, Any Device
- Resource Pooling: 다중 임대 모델을 통한 자원 할당, Multi-Tenancy(하나의 자원을 여러 사용자에게 공유)
- Rapid Elasticity: 탄력적 사용, Flexibility(유연성), Scalability(확장성)
- Measured Service: 서비스를 사용한 만큼 비용 지불: Pay-Per_use, Pay as you go

### Public Cloud의 장점
- 경제성: 자원의 낭비를 줄일 수 있음
- 자동화: 업데이트나 보안 패치, 백업을 대부분 CSP업체가 대신 수행
- 이동성: 웹을 지원하는 모든 장치에서 사용이 가능
- 자원 공유
- 가용성: 데이터 센터 안의 일부 하드웨어에 장애가 발생하더라도 서비스를 계속해서 이용할 수 있도록 구성, 대부분의 CSP들은 가용성 계약서로써 SLA(Service Level Agreement)를 공개하고 있음
- 빠른 구축 속도
- 확장성 - 인디스쿨이 대표적인 사례
  - 인디스쿨: 초등학교 선생님들이 회원인 사이트
  - 회원수가 14만명 정도 되는 서비스인데 방학 중에는 트래픽이 거의 발생하지 않음
  - Private Cloud로 구축하게 되면 필연적으로 자원의 낭비가 발생
  - Public Cloud로 이전해서 트래픽에 따라 유연하게 운용해서 비용 절감 효과를 봄
- 중복성 및 탄력성: 글로벌 인프라를 이용할 수 있음

### Public Cloud의 한계
- Internet Access: No Internet <-> Cloud
- Security
- Privacy
- Vendor Lock-In(벤더 종속적 문제: 하나의 CSP에 구축한 시스템을 다른 CSP로 옮기는 것이 어려움)

### Public Cloud 서비스의 종류
- 자원: 네트워크, 스토리지, 서버, 가상화, OS, 미들웨어, 데이터, 애플리케이션으로 구분
- Infrastructure as a Service - IaaS
  - 네트워크, 스토리지, 서버와 같은 인프라 하드웨어 자원을 가상화해서 사용자 요구에 따라 인프라 자원을 사용할 수 있게 해주는 서비스 방식으로 AWS의 EC2가 대표적인 서비스
- IT인프라를 사용하고 비용은 사용량에 따라 지불
- All CSPs are providing IaaS to the public
- Platform as a Service - PaaS
  - IaaS에 OS나 미들웨어, 런타임을 추가로 임대해서 사용하는 서비스
  - 애플리케이션 개발 환경이나 데이터베이스 등을 미리 설치해준 플랫폼을 임대해서 단기간에 애플리케이션 개발해서 서비스를 제공할 목적으로 사용
  - 대표적인 서비스가 세일즈 포스가 제공하는 force.com이나 사이보우즈의 kintone, Cloud Foundary, Google Cloud Platform, DBMS on Cloud(OCI) 등
- Software as a Service - SaaS
  - 업무에서 사용하는 소프트웨어의 기능을 인터넷 등의 네트워크를 통해 필요한 만큼 서비스로 이용할 수 있도록 제공하는 형태
  - Google Apps, MS Office365, Naver Office
- Desktop as a Service - DaaS
  - 인터넷만 연결되면 언제 어디서나 어떤 기기로도 기업 내부 망에 접속할 수 있는 Cloud Service
  - 모든 정보가 중앙 서버에 저장되기 때문에 직원의 개별 PC가 바이러스에 노출되거나 파손, 분실되어도 유출의 위험이 적고 기업의 업무 망에 접근하는 가장 안전한 기술

### 이용 모델에 따른 분류
- Public Cloud
  - Cloud Service Provider(Amazon, Google, MS, Oracle, Naver 등)가 시스템을 구축하고 인터넷 망 등의 네트워크를 통해서 불특정 다수의 기업과 개인에게 서비스를 제공하는 형태
  - 대다수 Cloud이야기 하면 이 모델
  - 사용량에 따라 비용을 지불
  - 사용자 및 그룹 단위로 권한 관리를 수행
  - 서비스 이용자를 제한하지 않음
- Private Cloud
  - 폐쇄적인 구조
  - Cloud 서비스의 사용자 또는 사업자의 데이터 센터에 Cloud 관련 기술이 활용된 전용 환경을 구축해서 컴퓨터 리소스를 사용하는 형태
  - 특정 기업의 특정 사용자만을 대상으로 하는 서비스
  - 물리적인 보안 측면이 Public Cloud보다 우수
  - 구현 방식: 
    - 자원을 자사가 보유하고 운용: On-Premise Private Cloud
    - 자원을 Cloud 사업자가 보유하고 운용: Hosted Private Cloud
- Community Cloud
  - 공통의 목적을 지닌 특정 기업들이 Cloud 시스템을 구축
- Hybrid Cloud
  - Public Cloud와 Private Cloud를 네트워크를 통해서 결합해서 두 가지 서비스의 장점을 활용할 수 있도록 만든 서비스 방식
  - 서로 다른 cloud 간에 데이터와 애플리케이션 공유 및 이동이 유연하게 처리될 수 있고 용도에 맞는 서비스 구현에 유리
  - 기업 내부의 민감하고 중요한 데이터 처리 작업은 통제력 강화를 위해서 Private Cloud를 사용하고 일반 업무 처리 같은 보안 요구 사항이 낮은 작업이나 워크로드가 지속적으로 증가하는 작업에는 리소스 자동 조정이 가능한 Public Cloud를 사용
  - Client Application은 어디서나 다운로드 받아 사용가능하도록 Public Cloud에, Server Application은 보안 문제 때문에 Private Cloud에 배치하는 형태도 있음
  - 고객이 여러 나라에 퍼져 있는 경우 외국은 퍼블릭으로 구현하고 국내는 데이터센터 구축을 통해 프라이빗으로 구현
- Multi Cloud
  - 2개 이상의 Public Cloud를 사용하는 것
  - 여러 공급업체를 활용하는 전략을 자유롭게 수정해서 특정 비즈니스 요구에 가장 적합한 기능을 선택
  - 많은 조직들이 멀티 클라우드 전략과 멀티 클라우드 솔루션을 채택해서 복잡성 없이 필요한 곳에서 애플리케이션을 실행할 수 있도록 하고 있음
  - Docker나 Kubernetes와 같은 오픈 소스 기술을 기반으로 구축된 멀티 클라우드 솔루션은 다양한 클라우드 및 컴퓨팅 환경에서 애플리케이션을 마이그레이션, 빌드, 최적화하는 유연성과 이동을 제공

### Cloud를 지탱하는 2개 기술
- 가상화
  - 컴퓨터의 물리적인 자원을 소프트웨어로 대체하는 것
  - 가상 서버는 물리적인 서버 1대 위에 게스트가 되는 서버 여러 대를 가상으로 생성하는데 본래 서버에 필요한 물리적인 부품을 가상으로 생성해서 서버로 만드는 것
  - 네트워크의 경우도 하나의 회선을 분할해서 다른 네트워크와 통합하거나 연결을 바꿀 수 있는 기술
  - 가상 서버에 할당된 메모리와 스토리지는 자유롭게 늘리거나 줄일 수 있기 때문에 나중에 필요한 용량을 늘리거나 줄여서 사용하는 것이 가능한데 서버의 성능을 높이는 것은 한계가 있음
  - 성능을 한계까지 끌어올려도 부하가 발생하는 경우에는 서버 대수를 늘려야 함
  - 가상화는 소프트웨어처럼 구축하기 때문에 서버 복제가 쉽고 대수를 줄이거나 늘리는 것이 쉬움
- 로드 밸런서
  - 분산 처리
  - 하나의 요청을 여러 대에 분산해서 처리하는 기술
  - 같은 기능 또는 정보를 가진 여러 대의 컴퓨터를 이용해서 나누어 처리하면 서버 1대의 부담을 줄이고 서버가 응답할 수 없거나 다운되는 사태를 막을 수 있음
  - 서버 여러 대에 분배하는 장치를 Load Balancer라고 하는데 로드 밸런서는 각 서버를 확인해서 부하를 분산하고 경우에 따라서는 부하가 높아진 서버를 분리하기도 함
  - AWS에서는 ELB라고 서비스에서 제공
- 이중화
  - 시스템이나 서버에 문제가 생겨도 계속 가동할 수 있도록 하기 위해서 수행
  - 백업을 해놓거나 여러 대를 운영해서 구현

## 이중화
- SPoF(Single Point of Failure)
  - 시스템 구성 요소 중 동작하지 않으면 전체 시스템이 중단되는 요소
  - 단일 장애점이라고도 함
  - 고가용성을 추구하는 네트워크, 소프트웨어 애플리케이션, 상용 시스템에 단일 장애점이 있는 것은 바람직하지 않음
- 서비스를 제공하기 위한 인프라의 주요 목표 중 하나는 적시에 서비스를 출시하기 위해 인프라를 신속히 제공하는 것으로 이를 Time To Market을 위한 인프라의 민첩성이라고 하는데 인프라의 더 본질적인 목표는 더 가용성 높은 서비스에 필요한 인프라를 안정적으로 제공하는 것
- 인프라를 설계할 때 단일 점점의 장애가 전체 서비스에 영향을 미치지 않도록 SPoF를 만들지 않아야 함
- 이중화의 목적
  - 인프라를 구성하는 각 요소가 복수 개 이상으로 인프라를 구성해서 특정 인프라에 문제가 발생하더라도 이중화된 다른 인프라를 통해 서비스가 지속되도록 하는 것
- 서비스에 필요한 출발 지점부터 끝 지점에 속하는 모든 인프라에 이중화 구성을 고려
  - 심지어 데이터 센터 자체도 이중화를 하도록 함
  - DR CEnter나 Active-Active를 구축하도록 함
- 이중화를 구성할 때는 각 구성 요소가 동시에 동작할 것인지 아니면 하나의 구성 요소는 운영 상태이고 다른 하나는 대기 상태로 있다가 운영 상태인 인프라에 장애가 발생하면 대기 상태인 인프라가 운영 상태로 전환 될 것인지 여부에 따라 Active-Active 또는 Active-Stanby 형태로 구분
  - 스위치를 이중화 했을 때 Spanning Tree Algorithm으로 장애를 해결한다고 했는데 이 구조가 Active Standby
- 인프라가 이중화되어 있다면 특정 지점에 문제가 발생하더라도 이중화된 인프라를 이용해서 서비스를 할 수 있음
  - 특정 인프라에 장애가 발생하더라도 서비스의 연속성이 보장되는 형태를 Fault Tolerance가 보장된다고 함
- 액티브 스탠바이가 아닌 액티브 액티브 형태로 구성을 할 때는 이중화된 인프라에서 서비스 요청을 동시에 처리할 수 있으므로 처리 가능한 전체 용량이 증가함
  - 이중화된 인프라는 장비간 네트워크 연결이나 회선의 대역폭이 증가함
  - 이렇게 증가된 인프라 용량을 기준으로 서비스를 수용하면 특정 지점에 장애가 발생했을 때 인프라 용량이 떨어지므로 정상적인 서비스가 불가능할 수 있음
  - 하나의 인프라가 6G를 처리하고 이 인프라가 이중화가 되어 있고 active-active로 만들어지면 평상 시에는 12G를 처리할 수 있지만 한 쪽에 장애가 발생하면 성능은 6G가 됨

### 서버의 네트워크 이중화 설정
- 윈도에서는 team이나 teaming
- 리눅스에서는 bond나 bonding
- team이나 bond는 논리적인 인터페이스
- 네트워크 장비를 네트워크 이중화를 위해서 두 개 이상의 물리 인터페이스를 하나의 논리 인터페이스로 구성하면 각 인터페이스가 모두 활성화되는 Active-Active 상태가 됨
  - 서버는 하나의 논리 인터페이스를 만들 때 Active-Active가 아님
  - LACP를 이용해서 Active-Active 구조를 만들 수 있음

### 게이트웨이 이중화
- 특정 호스트가 동일한 서브넷에 있는 내부 네트워크와 통신을 할 때는 ARP(Address Resolution Protocol)을 직접 브로드캐스트해서 출발지와 목적지가 직접 통신하는데 이 경우 3계층 장비인 라우터의 도움 없이 직접 통신하기 때문에 이를 L2 통신이라고도 함
  - 서브넷이 다른 경우는 L3통신이라고 함
  - 게이트웨이 설정이 안되어 있거나 잘못되면 외부 네트워크와 통신을 할 수 없음
  - 게이트웨이에 문제가 생기면 외부 통신을 할 수 없음
- 2개의 네트워크 장비가 동일한 IP주소를 가질 수 있도록 설정해야만 게이트웨이 이중화를 구현할 수 있음
  - 이 때 사용되는 프로토콜이 FHRP(First Hop Redundancy Protocol)
  - 이 프로토콜을 이용하면 가상의 IP와 MAC Address가 할당됨
  - 이 가상의 IP를 Gateway로 사용하면 Active-Standby 형태로 동작
- Anycast Gateway
  - Overlay 기반의 SDN(Software Defined Network)을 구성하면 네트워크가 여러 위치에 존재
  - 이 경우에는 가까운 라우터에서 요청을 처리하도록 해서 자원의 낭비를 최소화하는 방식
  - 이 방식을 이용하게 되면 장애가 발생하지 않은 경우에는 트래픽을 분산해서 처리하고 장애가 발생하면 장애가 없는 곳에서 처리

## Load Balancer
### 부하 분산
- 서비스가 커지면 물리 또는 가상 서버 한대로는 모든 서비스를 수용할 수 없음
- 서버 한대가 처리할 수 있더라도 단일 장애점이 됨
- 서비스의 가용성을 높이기 위해서 하나의 서비스는 보통 두 대 이상의 서버로 구성하는데 각 서버의 IP를 다르게 구성해야 하는데 이렇게 하면 특정 서버에 장애가 발생하면 전체 사용자에게는 영향을 미치지 않는 부분적인 장애가 발생
- 위와 같은 문제를 해결하기 위해서 L4나 L7 스위치라는 Load Balancer를 사용
- 로드밸런서에는 동일한 서비스를 하는 다수의 서버가 등록되고 사용자로부터 서비스 요청이 오션 로드 밸런서가 받아서 사용자 별로 다수의 서버에 서비스 요청을 분산시켜서 부하를 분산하는데 대규모 서비스 제공을 위해서는 로드 밸런서가 필수
- 로드밸런서에서는 서비스를 위한 가상IP를 하나 제공하고 사용자는 각 서버의 개별IP가 아닌 동일한 가상IP를 통해서 서버로 접근

### FWLB
- 서버에 대한 부하 분산 뿐 아니라 방화벽을 액티브-액티브로 구성하기 위해서 로드 밸런서를 사용하기도 함
- 서버 부하 분산을 SLB(Server Load Balancer), 방화벽 부하 분산을 FWLB(FIreWall Load Balancer)라고 함

### 부하 분산 방법
- 가상 IP주소를 이용하게 되는데 가상 IP주소와 포트 번호를 가지고 각 애플리케이션을 서비스하는 컴퓨터에 매핑을 함
- 각 포트에 매핑하는 컴퓨터 그룹을 만들고 이를 활용해서 원하는 컴퓨터에 접속하는 구조
- 서버 1, 2, 3이 있고 서버1는 http 서비스만 서버2는 https 서비스만 서버3은 http와 https를 전부 지원하는 경우이고 가상의 IP가 10.10.10.1이라면 
```
서비스ID    서비스포트  서버
10.10.10.1  http(80)    서버 #1, #2
10.10.10.1  https(443)  서버 #2, #3

위의 테이블을 이용해서 어떤 서버에게 요청할 것인지 결정
서버는 IP와 Port번호를 같이 기재
```
- 포트 번호까지 기재를 해두고 매핑하기 때문에 서버의 포트와 실제 서비스되는 포트가 달라도 됨
장고 애플리케이션을 만들 때 실행은 5000번 포트를 이용하더라도 외부에서 접속할 때는 80번으로 접속하는 것이 가능

### 헬스 체크
- 로드 밸런서에는 부하 분산을 하는 각 서버의 서비스를 주기적으로 Health Check해 정상적인 서비스쪽으로만 부하를 분산하고 비정상적인 서버에는 서비스 그룹에서 제외해 트래픽을 보내지 않음
- 헬스 체크 방식
  - ICMP
    - 실제 서버에 대해서 ICMP(ping)로 헬스 체크를 수행하는 방법
    - 단순히 서버가 살아 있는지 여부만 체크: 잘 사용하지 않음
  - TCP 서비스 포트
    - 로드 밸런서에 설정된 서버의 서비스 포트를 확인
    - 로드 밸런서에서 서버에게 SYN 요청을 보내고 서버로부터 SYN과 ACK를 받으면 서버에 다시 ACK로 응답을 하고 FIN을 보내서 헬스 체크를 종료
  ```
  로드밸런서            서버
            -> SYN
            <- SYN ACK
            -> ACK
            -> FIN
  ```
  - 빠른 헬스 체크를 위해서 ACK와 FIN을 별도로 보내지 않고 RST 하나만 전송하는 방식도 존재
  - HTTP 상태 코드
    - 웹 서비스를 할 때는 서비스 포트까지는 정상적으로 열리지만 웹 서비스에 대한 응답을 정상적으로 해주지 못하는 경우가 있으므로 신호만 주고 받는 것이 아니고 정상적인 응답코드(200)을 응답하는 것 까지 체크하는 방법
  - 콘텐츠를 확인

### 헬스 체크 주기와 타이머
- 주기: 로드 밸런서에서 서버로 헬스 체크 패킷을 보내는 주기
- 응답 시간(Response): 응답을 기다리는 시간으로 이 시간내에 응답이 오지 않으면 실패로 간주
- 시도 횟수(Retries): 실패 시 최대 시도 횟수
- Timeout: 헬스 체크 실패 시 최대 대기 시간
- 서비스 다운 시의 주기(Dead Interval): 서비스가 다운 되었을 때의 헬스 체크 주기

### 부하 분산 알고리즘
- Round Robin: 현재 구성된 장비에 부하를 순차적으로 분산하는 방식으로 총 누적 세션 수는 동일하지만 활성화 된 세션 수는 달라질 수 있음
- Least Connection: 현재 구성된 장비 중 활성화 된 세션 수가 가장 적은 장비로 부하를 분산시킴
- Weighted Round Robin: 각 서버에 부여된 가중치가 높은 장비가 더 많은 처리를 수행, 처리 용량이 다른 서버에 부하를 분산시키 위해서
- Weighted Least Connection: 각 서버에 부여된 가중치와 세션의 수를 같이 확인, 처리 용량이 다른 서버에 부하를 분산시키 위해서
- Hash: 해시 방식은 서버의 부하를 고려하지 않고 클라이언트가 같은 서버에 지속적으로 접속하도록 하기 위해서 사용하는 부하 분산 방식
  - 서버 상태를 고려하는 것이 아니라 해시 알고리즘을 이용해 얻은 결과값으로 어떤 장비로 부하를 분산할 지를 결정
  - 알고리즘에 의한 계산값을 이용하기 때문에 동일한 알고리즘을 사용하면 항상 동일한 결과값을 가지고 서비스를 분산함
  - 이 때 출발지 IP주소, 목적지 IP주소, 출발지와 목적지 서비스 포트 등을 사용
  - 테스트를 할 때 많이 사용, UI개선을 위해 같은 특정 시기의 사용자 별로 다른 UI보여주는 방식 등

## Cloud Native
- Cloud Native 기술은 조직이 Public, Private, Hybrid Cloud와 같이 현대적이고 동적인 환경에서 확장 가능한 애플리케이션을 개발하고 실행할 수 있게 해주는 기술로 Container, Service Mesh, Micro Service, Immutable Infra, Declarative API가 이러한 접근 방식의 예시이며 이런 기술은 회복성, 관리 편의성, 가시성을 갖춘 **느슨하게 결합된 시스템**을 가능하게 해주며 견고한 자동화 기능을 함께 사용하면 엔지니어는 영향이 큰 변경을 최소한의 노력으로 자주 예측하게 수행할 수 있음
- Cloud Native Computing Foundation은 벤더 중립적인 오픈 소스 프로젝트 생태계를 육성하고 유지함으로써 위와 같은 패러다임 채택을 촉진
- 최신 기술 수준의 패턴을 대중화하여 이런 혁신이 누구나 접근 가능하도록 함

### Pillars of Cloud Native
- DevOps
- Microservices
- Containers
- Continuous Delivery

### DevOps
- Agile
  - 2001년부터 시작
  - 소프트웨어 프로젝트를 일련의 선형적 순서로 구성하는 Waterfall 방식의 프로젝트 관리에 대응하기 위해서 등장
  - Waterfall 모델은 과정 중간에 feedback이 없어서 중간에 고객의 needs가 변경되면 처음부터 다시 개발
  - Agile은 고객의 needs 변화에 대응하기 위해서 작은 기능 단위로 개발을 수행하는 방법론
  - 반복적인 개발 주기와 자기 조직화 팀을 강조하는 일련의 관행
  - 애자일 선언문
    - 개인과 개인 간의 상호 작용이 프로세스 및 툴보다 우선
    - 작동하는 소프트웨어가 포괄적인 문서보다 우선
    - 고객과의 협업이 계약 협상보다 우선
    - 변화에 대응하는 것이 계획을 따르는 것보다 우선
- ITIL
  - 1980년대 영국 정부의 CCTA(Central Computer and Telecommunications Agency)에서 IT 인프라 운영의 최고 사례를 모아서 발간
  - 2000년대 ITIL v2부터 IT 인프라 운영 관리 de facto로 전세계 IT 서비스 기업의 운영 방법론으로 자리잡음(ITSM)
  - 2019년 ITIL v4부터 Agile, Lean, DevOps 등의 방법론과의 연계성을 강화한 Service Value System 개념으로 전체 체계 변화
- DevOps 개요
  - IT 서비스 설계, SW 개발, 릴리즈 및 운영에 이르기까지 전체 서비스 수명 주기와 함께 참여하는 IT 서비스 운영 및 개발 엔지니어의 업무 방식
  - 팀이 애플리케이션 개발에서 프로덕션 운영에 이르는 전체 프로세스를 소유하는 방법론
  - 기술 구현을 넘어 문화와 프로세스의 완전한 변화를 요구
  - 전체 기능이 아닌 작은 구성 요소에서 작업하는 엔지니어 그룹을 요구하여 일반적인 오류 소스인 핸드 오프를 줄임
  - DevOps는 개발(Development)과 운영(Operations)의 합성어로서 소프트웨어 개발자와 정보 기술 전문가와의 소통, 협업 및 통합을 강조하는 개발문화나 환경
  - 개발 조직과 운영 조직간의 상호 의존적 대응이며 조직이 소프트웨어 제품과 서비스를 빠른 시간에 개발 및 배포하는 것이 목적
  - 기술이 아닌 철학이며 변경이 아닌 변화
- Tool Chain
  - Plan(계획): 목적을 수행하기 앞서 방법이나 절차 등을 미리 생각하여 계획
  - Code: 코드 개발 및 검토, 버전 관리 도구, 코드 병합
  - Build: 지속적 통합(CI) 도구, 빌드 상태
  - Test: 테스트
  - Packaging: 배포하기 직전 단계
  - Release & Deploy: 변경 사항 관리, 릴리즈 승인, 릴리즈 자동화
  - Operate: 인프라스트럭션 구성 및 관리, IaC(Infrastructure as Code) 도구
  - Monitoring: ELK Stack, 사용자 경험
- DevOps 변화
  - SOA, Agile Teams, Cloud Infra Automation => Microservices, DevOps Agile Mindset, CI/CD => Enterprise DevOps(Functional Microservices, DevOps Automation)
- 장점
  - 속도: 개발 기간이 적게 소요
  - 신속한 제공(Delivery): 배포 기간이 적게 소요
  - 안정성(Reliability): 모니터링과 로깅
  - 확장성(Scale): IaC(코드형 인프라)
  - 협업 강화(Collaboration) - CLAMS
  - 보안(Security): Policy as Code

### CI/CD
- 지속적인 통합(Continuous Integration), 지속적인 서비스 제공(Continuous  Delivery), 지속적인 배포(Continuous Deploy)
- 애플리케이션 개발과 배포를 자동화해서 애플리케이션을 보다 짧은 주기로 고객에게 전달하는 방법

### MicroService
- 애플리케이션을 상호 독립적인 최소 구성 요소로 분할
- 모든 하나의 애플리케이션에 구축하는 전통적인 모놀리식 접근 방식 대신 모든 요소가 독립적으로 연동되어 태스크를 수행

### Containers
- 실행에 필요한 모든 파일을 포함시켜 전체 실행 환경에서 애플리케이션을 패키지화하고 분리하는 기술

## DevOps
### 애자일 개발에 의한 계속적인 개발로의 변화
- 전통적 개발과 애자일 개발의 차이
  - 전통적 개발은 개발을 하고 인도를 해서 운영을 하는 과정이 1번
  - 애자일 개발은 개발을 하고 인도를 해서 운영을 하는 과정이 N번
- 서비스를 정책적으로 실시하면서 피드백을 받아 개발을 여러 번 반복하는 Prototype Model과 소규모 개발을 전제로 필요한 최소한의 요건을 적용한 성과물을 만들어 Release를 하고 고객의 피드백을 받아서 계속적인 개선을 반복하는 것이 애자일

### 계속적 개발로 인해 나타나기 시작한 운용 과제
- 개발자의 시점에서 기능 요건 외의 모니터링 그리고 이중화 및 백업이나 OS 등의 비기능 요건을 소홀하게 취급하는 것이 문제
- 운용 문제에 대해서는 데일리 스크럼(Daily Scrum)으로 불리는 일일 회의를 통해 진행 방향에 대한 해결책을 도출하고 팀 멤버의 관심 여부에 따라 우선순위를 매기거나 태스크 페어로 대응하고 정보 공유를 형성
- 개발 문제에 대한 해결책은 인프라팀을 포함시킨 애자일 개발을 이용하고 인프라 요건을 기존보다 이른 단계에서 가시화하고 과제에 대해서는 과제의 주인을 명확히 하는 것을 제안
- Infrastructure is code 라는 주제로 해결책을 제시

### 인프라 구성 관리 도구
- 운용 과제 해결을 위한 수단인 DevOps의 인프라 코드화는 서버와 스토리지 그리고 네트워크 등 인프라에 대한 설정을 수행하는 것을 Provisioning이라고 부르고 3개의 영역을 분류
- 프로미져닝 영역
  - Bootstrapping: 가상 서버 생성이나 OS 설치를 담당
  - Configuration: OS나 Middleware의 설정을 담당
  - Orchestration: Deploy나 노드 간 연계 등 복수의 서버에 대한 설정이나 관리를 담당
- 최근에는 Puppet이나 Chef, Ansible 등의 구성 관리 도구로 인해 Configuration과 Orchestration의 영역의 구분이 사라지고 있음

### IaC와 DevOps
- IaC는 인프라를 코드로 표현하는데 코드화를 위해서 고도의 프로그래밍 지식은 필요없는데 프로그래밍 언어보다는 학습 비용이 낮은 DSL로 인프라 구성과 컨피그를 기술할 수 있도록 되어 있기 때문에 적은 학습 비용으로 기술하는 것이 가능
- yaml을 주로 이용
- 개발과 운용이 긴밀하게 연계되어 비즈니스 가치를 높이고자 하는 DevOps에서는 애플리케이션 개발 담당자가 인프라 운용에 대해서 소프트웨어의 지식을 이용해서 이해하고 직접 설정을 변경할 수 있는 IaC는 중요한 사고 방식

### Ansible
- 장점
  - 자동화
  - 선언적
  - 추상화
  - 수렴화
  - 멱등성: 몇 번을 실행해도 동일한 결과를 얻을 수 있음

### DevOps 탄생과 역사
- 야후의 플리커 서비스 엔지니어 두명이 하루에 10회를 초과하는 배포에 대해서 프레젠테이션을 했는데 개발자는 고객의 니즈를 반영하기 위해서 변경을 하고자 하고 운용자 입장에서 안정적 가동이기 때문에 손을 대는 것을 싫어함
- 변화의 위험을 도구와 문화로 낮추자
  - 변화에 대응하기 위한 도구
    - Automated Infrastructure: 인프라 자동화
    - Shared Version Control: 버전 관리 공유
    - One step build and deploy: 빌드와 배포를 한 번의 과정으로 수행
    - Feature Flags: 애플리케이션 기능의 무효/무효를 설정 파일로 관리
    - Shared Metrics: 지표 공유
    - IRC and IM robots: 채팅과 인스턴스 메시지를 자동으로 전파
  - 문화
    - Respect(존중)
    - Trust(신뢰)
    - Healthy attitude about failure(실패에 대한 긍정적인 자세)
    - Avoiding Blame(비난을 하지 말 것)
- DevOps의 목적은 신속하게 비즈니스 요구에 응하는 것

### PDCA Cycle
- PDCA Cycle은 Plan(계획) -> Do(실행) -> Check(평가) -> Act(개선)를 계속적으로 실시
- 한 주기를 일주일이나 이주 정도 설정하는데 우리나라 플랫폼 기업들은 대부분 2주

### 지탱하는 기술
- 추상화(가상화)
  - 운영체제, 서버, 스토리지, 네트워크 가상화
  - 물리적인 자원을 소프트웨어로 구현
- 자동화
  - 빌드나 테스트 및 배포 등을 자동으로 수행하는 것

## CI/CD
- CI(Continuous Integration): 지속적인 통합
- CD(Continuous Delivery, Continuous Deployment): 지속적인 서비스 제공과 배포
- 애플리케이션 개발 단계를 자동화해서 애플리케이션을 보다 짧은 주기로 고객에게 제공하는 방법
- 개발 및 운용 팀 간의 협업 단계에서 발생하는 문제를 해결하기 위한 방법
- 지속적인 통합이 제대로 구현되면 애플리케이션 코드의 새로운 변경 사항이 정기적으로 빌드 및 테스트를 거쳐 공유 레포지토리에 병합이 되므로 여러 명의 개발자가 동시에 애플리케이션 개발과 관련된 코드 작업을 할 경우 서로 충돌하는 문제를 해결할 수 있음

### CI
- 개발 팀이 작은 변경 사항을 구현하고 코드를 버전 제어 레포지토리에 자주 체크인하도록 하는 코딩 철학이자 일련의 관행
- 목표는 애플리케이션을 빌드 하고 패키징하고 테스트하는 일관되고 자동화된 방법을 설정하는 것
- 일관성을 유지하면 팀이 코드 변경을 더 자주 커밋할 가능성이 높아져서 공동 작업과 소프트웨어 품질이 향상됨

### 지속적인 제공
- 개발자들이 애플리케이션에 적용한 변경 사항이 버그 테스트를 거쳐 레포지토리에 자동으로 업로드 되는 것
- 운영 팀은 이 레포지토리에서 애플리케이션을 실시간 프로덕션 환경으로 배포
- 개발 팀과 비즈니스 팀 간의 가시성과 커뮤니케이션 부족 문제를 해결
- 지속적인 제공은 최소한의 노력으로 새로운 코드를 배포하는 것

### 지속적인 배포
- 개발자의 변경 사항을 레포지토리에서 고객이 사용 가능한 프로덕션 환경까지 자동으로 릴리스 하는 것
- CI(Build -> Test -> Merge) -> Continuous Delivery(Automatically Release to Repository) -> Continuous Deployment(Automatically Release to Production)
