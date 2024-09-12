---
title: 240912 toss slash 24
date: 2024-09-12
tags:
  - seed
---

세션 노트

## Yarn Plugin으로 우아하게 자동 로깅하기

hoc로 클릭 이벤트를 주입.
hoc tds 패키지를 별도로 관리하기엔 코드 변경을 대응하기 어려움.

TDS와 logger의 버전을 독립적으로 운영?

yarn plugin으로 tds 컴포넌트를 가로채기
resolution → fetch → link
TDS을 resolution step에서 로깅 TDS 패키지를
코드 단에서는 TDS 패키지를 그대로 사용할 수 있게 된다.


## N개의 탭, 단 하난의 웹소켓: SharedWorker
박건영

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
박정웅

playwright + nodejs
vscode에서 테스트를 쉽게 실행할 수 있음.
결과 리포트.

컴퓨팅 리소스
테스트에 따라 필요한 리소스의 크기가 동적으로 변함.

Playwright.config에 리포트 청크 적용.


## 웹뷰로 시작되는 Nest.js 프레임워크로 똑똑하게 서류 스크립핑하기
박진수

Message 방식 vs API 방식

Nest.js
컴포넌트 기반 개발
Custom HTTP Adapter로 express, festify를 쉽게 교체할 수 있다?



