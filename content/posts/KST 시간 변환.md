---
title: KST 시간 변환
date: 2024-09-30
tags:
  - seed
---

JS에서 `new Date`는 기본적으로 실행 환경의 로컬 시간대를 사용한다.
어디에서나 한국 시간을 보여주려면 무언가 작업이 필요하다.

가장 기본적인 방법은 국제 표준 시간대인 [**UTC**](https://namu.wiki/w/%ED%98%91%EC%A0%95%20%EC%84%B8%EA%B3%84%EC%8B%9C)를 기준으로 상대적 연산을 하는 것이다.

```js
const kstTimestamp = new Date().getTime() + (9 * 60 * 60 * 1000);
```

`new Date().getTime()`는 UTC 시간대로 반환하고, 한국시간은 UTC 기준으로 9시간이 빠르기에 그 만큼 더해주면 된다. 하지만 `new Date().getTime()`은 `ms` 단위를 사용하기에 계산식이 조금 지저분하다.

이 때, `toLocaleString`의 `timezone`를 활용하여 계산식을 피할 수 있다.

```js
new Date(new Date().toLocaleString('en', { timeZone: 'Asia/Seoul' }));
```

이를 유틸로 만들어 활용해보자.

```js
export const getKSTDate = (date = new Date()) => {
    return new Date(date.toLocaleString('en', { timeZone: 'Asia/Seoul' }));
};
```
