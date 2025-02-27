---
title: OpenAPI Typescript
date: 2025-02-27
tags:
  - seed
---

openapi-typescript turns OpenAPI 3.0 & 3.1 schemas into TypeScript quickly using Node.js. No Java/node-gyp/running OpenAPI servers necessary.

https://openapi-ts.dev/introduction

[work with hono](https://www.speakeasy.com/openapi/frameworks/hono)

## 워킹 방식

yaml 파일로 type 파일을 생성하여 `TYPE SAFE`를 제공해준다!!

```
npm i openapi-fetch
npm i -D openapi-typescript typescript
```

```shell
npx openapi-typescript ./path/to/api/v1.yaml -o ./src/lib/api/v1.d.ts
```

https://openapi-ts.dev/openapi-fetch/
