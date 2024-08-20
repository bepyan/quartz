---
title: (TS) enum vs const enum
date: 2024-02-02
tags:
  - seed
  - typescript
---

종종 명확한 타입을 

```ts
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT',
}
```

## enum

enum은 트리쉐이킹 되지 않는다.   
js로 트랜스파일링 될때 즉시실행함수가 생성된다.

```js
'use strict'
var Direction
;(function (Direction) {
  Direction['Up'] = 'UP'
  Direction['Down'] = 'DOWN'
  Direction['Left'] = 'LEFT'
  Direction['Right'] = 'RIGHT'
})(Direction || (Direction = {}))
```

enum은 위험하다.   
enum은 선언되지 않는 key값의 접근을 허용한다.

## const enum

트리쉐이킹 문제가 없다.

```ts
'use strict'
const left = 'LEFT' /* Left */
```

## as const

```ts
const Direction = {
  Up: 'UP',
  Left: 'LEFT',
  Right: 'RIGHT',
  Down: 'DOWN',
} as const

type Direction = (typeof Direction)[keyof typeof Direction]
```
 
 추가로 기존 변수에 `read only`를 강제하는 효과가 있다.

## 참고

- https://yceffort.kr/2020/09/typescript-enum-not-treeshaked
- https://mugglim.tistory.com/9
- https://xpectation.tistory.com/218

