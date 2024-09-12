---
title: N개의 탭, 단 하난의 웹소켓 SharedWorker
date: 2024-09-12
tags:
  - seed
  - 강의
---

> [[TOSS SLASH 24]]
> WebSocket을 SharedWorker에 올려 연결 개수 최적화

박건영 토스증권 Frontend Developer
https://static.toss.im/slash24/QR/slash24-12.pdf

**문제 인식:**
모바일 환경에서는 WebSocket으로 서버와 연결하는 것이 일반적이다.
PC 환경에서는 여러 탭과 브라우저를 사용할 수 있어, WebSocket 연결이 과도하게 생성되어 서버에 부하가 걸린다.

**기존 해결 방안의 한계:**
Visibility Change 이벤트를 기준으로 보이지 않는 탭의 WebSocket 연결을 차단하는 방법이 있다.
하지만 여전히 보이는 탭의 수만큼 연결이 유지되어 완전한 해결책이 되지 못한다.

**Web Worker API 소개:**
브라우저에서 별도의 스레드를 생성할 수 있는 [[Web Worker API]]를 활용할 수 있다.
[[Dedicated Worker]]와 [[Shared Worker]] 두 가지 유형이 있다.

**Shared Worker 활용:**
여러 탭에서 하나의 [[Shared Worker]]를 공유할 수 있다.
같은 Origin과 같은 JS 파일을 사용하는 경우에만 공유가 가능하다.
`postMessage`를 통해 메인 스레드와 워커 스레드 간 통신이 가능하다.

**SharedWorker + WebSocket 구현:**
Shared Worker 내에서 [[WebSocket]] 연결을 생성하고 관리한다.
여러 탭에서 하나의 [[WebSocket]] 연결을 공유하여 서버 부하를 줄일 수 있게 된다.

**브라우저 호환성 고려:**
[Shared Worker를 지원하지 않는 브라우저](https://caniuse.com/sharedworkers)를 위해 [[Dedicated Worker]]를 fallback으로 사용하면 된다.
결국 탭별로 WebSocket 연결을 관리하게 되는데 PC의 모던 브라우저는 거의 이를 지원하기에 부담이 작다.

**구현 시 난관과 해결책:**
a. 번들링 문제:
모던 번들러에선 `new URL`을 사용하여 Worker 파일 경로를 자동으로 처리할 수 있다.

```js
const worker = new SharedWorker(new URL("./worker.ts", import.meta))
```

b. 메모리 누수 문제:
탭이 닫힐 때 리소스 정리가 필요하다.
`BeforeUnload` 이벤트는 신뢰성이 낮아 사용하기 어렵다.
`WeakRef`와 `MessagePort`를 조합하여 가비지 컬렉션을 활용한 탭 종료 감지 방법을 사용했다.

```js
const weakPort = new WeakRef(port);

portList.push(weakPort);

if (!weakPort.deref()) {
 // undefined 라면 탭이 닫혔다고 판단
}
```

**마무리:**
1. 데스크톱 환경 WebSocket 연결 개수 문제
2. WebSocket을 SharedWorker에 올려 연결 개수 최적화

---

**나의 한줄평:**
문제를 해결하기 위해선 브라우저에 대해서 잘 알아야 한다.
