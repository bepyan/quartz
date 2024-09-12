---
title: export =
date: 2024-08-21
tags:
  - seed
  - fe
  - typescript
---

TypeScript 모듈에서 단일 내보내기를 제공한다.
**CommonJS 모듈 형식과의 호환성**을 위해 사용된다.

```ts
class MyClass {
  // 클래스 구현
}

export = MyClass
```

```ts
import MyClass = require("./MyClass")
```
