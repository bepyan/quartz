---
title: nanoid
date: 2024-10-14
tags:
  - seed
---
A tiny, secure, URL-friendly, unique string ID generator for JavaScript.
https://github.com/ai/nanoid

유닉한 ID를 부담없이 쉽게 생성할 수 있다.

```ts
import { nanoid } from 'nanoid/non-secure'
const id = nanoid() //=> "Uakgb_J5m9g-0JDMbcJqLJ"
```

### 영어

```ts
import { customAlphabet } from 'nanoid'

const nanoid = customAlphabet('abcdefghijklmnopqrstuvwxyz', 10);
```

### 영어 + 숫자

```ts
import { customAlphabet } from "nanoid";

const nanoid = customAlphabet("0123456789abcdefghijklmnopqrstuvwxyz", 5);
```
