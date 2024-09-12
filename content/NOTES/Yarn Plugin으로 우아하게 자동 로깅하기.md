---
title: Yarn Plugin으로 우아하게 자동 로깅하기
date: 2024-09-12
tags:
  - seed
---

> [[240912 TOSS SLASH 24]]
> Yarn Plugin으로 TDS 컴포넌트에 로깅 HOC 씌우기

전성 토스 Frontend Platform Engineer
https://static.toss.im/slash24/QR/slash24-09.pdf

**문제 인식:**
토스는 많은 로그를 남기며, 이는 다양한 분석에 사용된다.
수동으로 로그를 처리하기에는 양이 너무 많고 복잡하다.

**초기 접근 방식:**
TDS(Toss Design System)에 직접 로그를 추가하려 했으나, 여러 협력사와 공유하는 TDS의 특성상 어렵다. [[HOC]] 형태로 로그를 감싸는 방식을 시도했지만, 이는 많은 코드 수정을 필요하다. 특히 TDS 버전과 로깅 시스템 버전과 맞추기 어렵다.

```js
import { withLogging } from "@tossteam/v3-logger";
import { Button as TDSButton } from "@toss/tds";

export * from "@toss/tds";
export const Button = withLogging(TDSButton, props => ({
 text: getTextContent(props.children),
}));
```

```js
// import { Button } from "@toss/tds"
import { Button } from "@toss/logging-tds";
```

**핵심 아이디어:**
기존 코드를 그대로 유지하면서 TDS와 로깅을 독립적으로 배포할 수 있는 방법을 모색했다.
Yarn의 패키지 설치 과정(Resolution → Fetch → Link)에 개입하여 TDS 패키지를 가로채는 방식을 고안했다.

**Yarn Plugin 구현:**
Resolution 단계에서 TDS 패키지 대신 로깅 TDS 패키지를 참조하도록 했다.
Fetch 단계에서는 로깅 TDS 패키지를 다운로드하고 메타데이터를 수정한다.
Link 단계는 기존과 동일하게 진행된다.

```json
{
  "dependencies": {
    "@toss/tds": "logging:^1::__version=^1.2",
    "@toss/v3-logger": "^1.2"
  }
}
```

**구현 결과:**
개발자는 기존 TDS 임포트 구문을 그대로 사용하여 로깅할 수 있다.
TDS와 로깅 시스템의 버전을 독립적으로 관리할 있게 되었다.

---

**나의 한줄평:**
패키지를 가로챈다는 접근은 정말 듣도보지 못한 참신한 접근법이다.
