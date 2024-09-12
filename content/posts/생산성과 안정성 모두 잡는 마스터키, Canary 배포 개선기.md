---
title: 생산성과 안정성 모두 잡는 마스터키, Canary 배포 개선기
date: 2024-09-12
tags:
  - seed
  - 강의
---

> [[TOSS SLASH 24]]
> 이민우 토스뱅크 DevOps Engineer, 한태웅 토스뱅크 SRE
> https://static.toss.im/slash24/QR/slash24-21.pdf

**배포 전략 개요:**
[[Rolling Update]]: [[k8s]]에서 자주 사용되지만, 배포 중단 불가, 느린 롤백, 트래픽 조절 불가 등의 단점이 있다.
[[Canary]]: 빠른 롤백이 가능하고 트래픽을 세밀하게 조절할 수 있어 안정성이 높다.

**Canary 배포의 문제점:**
프론트엔드 서비스에서 새 버전 진입점과 예전 버전 페이지 간 불일치로 404 에러가 발생할 수 있다.
이를 해결하기 위해 "진입점"과 "페이지"를 분리 배포하는 방법이 있지만, 생산성 저하와 인적 오류 가능성이 있다.

**Sticky Canary 도입:**
```
UserUniqueKey → SSR API Gateway에서 버전을 고정 → VirtualService → app
```

- 사용자별로 특정 버전을 고정하여 일관된 경험을 제공한다.
- Istio의 VirtualService를 활용하여 구현한다.
- UserUniqueKey를 기반으로 SSR API Gateway에서 버전을 결정하고, 이를 헤더에 추가하여 VirtualService가 적절한 버전으로 라우팅한다.

장애가 발생된 버전을 빠르게 롤백하는 것이 Canary의 핵심이다.
하지만 모니터링이 되지 않으면 의미가 퇴색된다.

**Auto Canary 및 Auto Rollback:**
시스템 자체적으로 모니터링하여 문제가 있는 트래픽을 감지하고 차단했다.
자체 개발한 어플리케이션으로 성능 및 오류를 스코어링했다.
문제 발생 시 자동으로 롤백하여 장애 시간을 최소화했다.

---

**나의 한줄평:**
Canary 배포 전략에 대해 더 깊이 이해하고, 백엔드 팀과 협력하여 문제(예: 404 에러)를 해결할 방안을 같이 모색해 보면 좋겠다.