---
title: (TS) export =
date: 2024-01-12
tags:
  - seed
---
TypeScript 모듈에서 단일 내보내기를 제공한다.
CommonJS 모듈 형식과의 호환성을 위해 사용된다.

```ts
class MyClass {
    // 클래스 구현
}

export = MyClass;
```

```ts
import MyClass = require("./MyClass");
```
