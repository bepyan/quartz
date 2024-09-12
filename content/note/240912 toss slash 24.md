---
title: 240912 toss slash 24
date: 2024-09-12
tags:
  - seed
---

세션 노트

## Yarn Plugin으로 우아하게 자동 로깅하기
전성 토스 Frontend Platform Engineer

hoc로 클릭 이벤트를 주입.
hoc tds 패키지를 별도로 관리하기엔 코드 변경을 대응하기 어려움.

TDS와 logger의 버전을 독립적으로 운영?

yarn plugin으로 tds 컴포넌트를 가로채기
resolution → fetch → link
TDS을 resolution step에서 로깅 TDS 패키지를
코드 단에서는 TDS 패키지를 그대로 사용할 수 있게 된다.

## N개의 탭, 단 하난의 웹소켓: SharedWorker
박건영 토스증권 Frontend Developer

모바일에서는 웹소켓으로 서버와 연결.
하지만 PC에서는 여러 탭, 여러 브라우저를 띄울 수 있기에 웹소켓이 과도하게 생성되어 서버에 부하가 부담스럽다.

visibility change 기준으로 WebSocket을 줄이는 것에는 한계가 있음

web worker api를 통해서 브라우저 별도의 쓰레드를 생성할 수 있다.

dedicated worker
`postMessage`로 메인 스레드와 워커 스레드간의 통신을 다룰 수 있다.

shared worker
1. 같은 origin
2. 같은 JS 파일

브라우저 호환버전에 대한 고민.
dedicated worker를 fallback으로 두면 탭별로 WebSocket를 적용할 수 있다.

고민1. 번들러
webpack에서는 `new URL`의 링크를 자동으로 파싱한다.

고민2. 메모리 누수
탭이 무수히 생기고 닫힐 때의 메모리
BeforeUnload Event는 신뢰성이 부족하다.
WeakRef + MessagePort를 활용


## 클릭 한 번으로 테스트 45만 개 완료! 테스트 자동화 플랫폼 구축기
박정웅 토스페이먼츠 Node.js Developer

playwright + nodejs
vscode에서 테스트를 쉽게 실행할 수 있음.
결과 리포트.

컴퓨팅 리소스
테스트에 따라 필요한 리소스의 크기가 동적으로 변함.

Playwright.config에 리포트 청크 적용.


## 웹뷰로 시작되는 Nest.js 프레임워크로 똑똑하게 서류 스크립핑하기
박진수 토스뱅크 Node.js Platform Team Leader

Message 방식 vs API 방식

Nest.js
컴포넌트 기반 개발 방식을 채택
Custom HTTP Adapter를 통해 express, fastify 등의 기반 프레임워크를 쉽게 교체 가능

NestCA Request/Response로 응답을 잘 래핑했다.
```
{
	code: ""
	clientMessage: "불편을 드려 죄송합니다.",
	systemMessage: "[Error] ...",
	data: {
		"발급번호": ""
		// ...
	}
}
```

동시성 제어
Critical Section, Lock 등 방법이 있다
데코레이터를 사용했음

WebView Server
표준화된 도구를 통해 로깅 및 성능 측정이 가능하다.
대출에 필요한 서류를 자동으로 제출하는 [[스크래핑 시스템]]에 활용되었다.
브라우저 런타임에 대한 제약점이 적진 않다.


## 생산성과 안정성 모두 잡는 마스터키, Canary 배포 개선기
이민우 토스뱅크 DevOps Engineer, 한태웅 토스뱅크 SRE

**Rolling Update**
[[k8s]]을 쓴다면 많이 쓰이는 기능이다.
배포 중 중단할 수 없다는 단점이 있다. 롤백이 느리고 트래픽 조절이 불가하기에 장애에 취약하다.

Blue / Green은 사용하지 않는다.

**Canary**
이슈 발생시 바로 롤백이 가능하는 장점이 있다.

프론트엔드 서비스에서 Canary를 배포했을 때의 이슈.

새로운 버전의 진입점에서 예정 버전 페이지로 이동하면서 404 에러가 발생될 수 있다.
→ "진입점"과 "페이지"를 분리하여 배포해 문제를 해결할 수 있다.

생산성 하락, 휴먼 에러

**Sticky Canary**
네트워크 Load Balanser에서 버전을 고정한다.
istio 기능을 이용
weight 변경 이후 첫 요청이 달라 질 수 있는 문제가 있다.

**VirtualService**

UserUniqueKey → SSR API Gateway에서 버전을 고정 → VirtualService → app

Canary가 종료되면 Gateway에서 Header를 추가하지 않게 된다.
여기서 VirtualService가 이제 새로운 버전의 앱으로 라우팅한다.

장애가 발생된 버전을 빠르게 롤백하는 것이 Canary의 핵심이다.
모니터링이 되지 않으면 의미가 퇴색된다.

**Auto Canary**
시스템도 모니터링하게 해서 문제가 있는 트래픽을 차단시킨다.
오픈소스 Scoring을 많이 쓰지만,, 자체 어플리케이션을 만들었다.

**Auto Rollback**

복잡한 문제를 단순하게 해결..?



## 클러스터 운영부터 서비스 라이프사이클 관리까지, 데브옵스 업무 효율화
양석준 토스 DevOps Engineer

[[Kubespray]]
클러스터

k8s 버전이 빠르게 올라가고 있기 때문에 정기적으로 버전업을 따라 가야 한다.
메이저 버전이 올라가고 규모가 큰 클러스터는 

Kubespray는 버전을 하나 하나 순차적으로 업그레이드를 해야 한다.
노드 조인 → 운영체제/커널 업그레이드 → k8s 업그레이드

짧게는 30분, 길게는 12시간 소요되는 버전 업그레이드 시간을 어떻게 해결할 수 있을까?

...

컨슈머 트래픽 



https://static.toss.im/slash24/QR/slash24-08.pdf


사용자가 요청하신대로 "slash24-08" 부분의 08을 1부터 24까지 나열하겠습니다:

https://static.toss.im/slash24/QR/slash24-01.pdf
https://static.toss.im/slash24/QR/slash24-02.pdf
https://static.toss.im/slash24/QR/slash24-03.pdf
https://static.toss.im/slash24/QR/slash24-04.pdf
https://static.toss.im/slash24/QR/slash24-05.pdf
https://static.toss.im/slash24/QR/slash24-06.pdf
https://static.toss.im/slash24/QR/slash24-07.pdf
https://static.toss.im/slash24/QR/slash24-08.pdf
https://static.toss.im/slash24/QR/slash24-09.pdf
https://static.toss.im/slash24/QR/slash24-10.pdf
https://static.toss.im/slash24/QR/slash24-11.pdf
https://static.toss.im/slash24/QR/slash24-12.pdf
https://static.toss.im/slash24/QR/slash24-13.pdf
https://static.toss.im/slash24/QR/slash24-14.pdf
https://static.toss.im/slash24/QR/slash24-15.pdf
https://static.toss.im/slash24/QR/slash24-16.pdf
https://static.toss.im/slash24/QR/slash24-17.pdf
https://static.toss.im/slash24/QR/slash24-18.pdf
https://static.toss.im/slash24/QR/slash24-19.pdf
https://static.toss.im/slash24/QR/slash24-20.pdf
https://static.toss.im/slash24/QR/slash24-21.pdf
https://static.toss.im/slash24/QR/slash24-22.pdf
https://static.toss.im/slash24/QR/slash24-23.pdf
https://static.toss.im/slash24/QR/slash24-24.pdf

이렇게 1부터 24까지의 URL 목록을 생성했습니다. 각 URL은 원본 링크에서 숫자 부분만 변경되었습니다.