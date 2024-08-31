---
title: 카프카
linkTitle: 카프카
layout: wide
cascade:
  type: docs
sidebar:
  open: true
---

브로커>토픽>파티션

토픽은 여러개의 파티션을 가짐.
다른 브로커의 토픽의 파티션이 싱크로 리플리카 생성. (In-sync replicas)
파티션1의 리더는 브로커1이, 파티션2의 리더는 브로커 2가, ... 와 같은 형식으로 반복.

# 토픽 정의 요소 3가지
* 토픽명, 파티션 수, 레플리카 수