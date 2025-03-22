---
title: Typescript에서 undefined 타입을 nullable 타입으로 변환하기
date: 2025-03-21
tags:
  - seed
---

- 객체인 경우 객체의 모든 속성에 대해 재귀적으로 변환을 적용합니다.
- 값 타입에 undefined가 포함된 경우 null 타입을 추가합니다.
- 배열과 같은 다른 객체 타입에도 적용됩니다.
- 중첩된 객체 구조의 모든 레벨에서 동작합니다.

```ts
/**
 * Record 타입에서 undefined가 포함된 필드를 undefined | null로 변환하는 재귀적 유틸리티 타입
 */
type DeepUndefinedToNullable<T> = T extends object
  ? {
      [K in keyof T]: DeepUndefinedToNullable<T[K]>;
    } & (undefined extends T ? null : unknown)
  : undefined extends T
  ? T | null
  : T;
```

중첩이 아닌 상황에서는 아래 같이 사용해도 됩니다.

```ts
/**
 * Record 타입에서 undefined가 포함된 필드를 undefined | null로 변환하는 유틸리티 타입
 */
type UndefinedToNullable<T> = {
  [K in keyof T]: undefined extends T[K] ? T[K] | null : T[K];
};
```