---
title: OSPF
weight: 6
---
### OSPF
- Open Shortest Path First는 링크 상태 라우팅 프로토콜
- 클래스리스 라우팅 프로토콜
- RIP은 전체 토폴리지에 대하여 알 수 없고 홉의 개수를 가지고 선택하므로 반드시 속도가 빠르다는 보장을 못함
- 링크 상태 프로토콜은 속도, CPU, 메모리 등의 성능을 기반으로 라우팅
- 영역을 나누어서 설정하는 것도 가능
- 설정을 할 때 서브넷 마스크가 아니라 와일드 카드 마스크를 이용
- 와일드 카드 마스크는 서브넷 마스크 반대
- 설정 방법
```
(config)#router ospf 프로세스아이디
(config-router)#network 네트워크주소 와일드카드마스크 area-id
```
```
R1#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#router ospf 1
R1(config-router)#network 192.168.0.0 0.0.0.255 area 0
R1(config-router)#network 192.168.10.0 0.0.0.255 area 0
```
```
R2#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R2(config)#router ospf 1
R2(config-router)#network 192.168.0.0 0.0.0.255 area 0
R2(config-router)#network 192.168.20.0 0.0.0.255 area 0
```
```
R3#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R3(config)#router ospf 1
R3(config-router)#network 192.168.10.0 0.0.0.255 area 0
R3(config-router)#network 192.168.30.0 0.0.0.255 area 0
```
```
R4#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R4(config)#router ospf 1
R4(config-router)#network 192.168.20.0 0.0.0.255 area 0
R4(config-router)#network 192.168.30.0 0.0.0.255 area 0
```