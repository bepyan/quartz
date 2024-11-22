---
title: 왜 Error 타입은 unknown 일까?
date: 2024-11-21
tags:
  - seed
---

보통 우린 `try catch`를 통해서 에러를 다루곤 한다.
`catch`의 인자를 활용해서 말이다.

```ts
try {
  aFunctionThatMightFail();
} catch (e) {
  console.error(e);
}
```

하지만 `e` 의 타입이 `unknown`으로 잡히기에 `e.message` 같이 `Error`의 속성을 접근할 수 없게 된다.

왜 `unknown`으로 잡힐까?

답은 말그대로 **무엇이 나올지 모르기 때문**이다.
보통은 런타임 에러가 발행되어 `catch` 되겠지만 명시적으로 무언가를 던질 수 도 있다.

```ts
try {
	throw 'hello world'
} catch (e) {
  console.log(e); // hello world
}
```

따라서 `catch`된 런타임 에러를 다루기 위해서 [`instanceof`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/instanceof)을 활용해 타입을 체크해야 한다.

```ts
try {
  aFunctionThatMightFail();
} catch (e) {
  if (e instanceof Error) {
    console.log(e.message)
  }
}
```

더 많은 내용은 [[Node.js Error Handling 가이드]] 참고.