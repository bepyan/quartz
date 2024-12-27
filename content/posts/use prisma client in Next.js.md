---
title: use prisma client in Next.js
date: 2024-12-27
tags:
  - seed
  - prisma
  - next.js
---

```ts
const prismaClientSingleton = () => {
  return new PrismaClient();
};

declare const globalThis: {
  __db__: ReturnType<typeof prismaClientSingleton>;
} & typeof global;

const db = globalThis.__db__ ?? prismaClientSingleton();

if (process.env.NODE_ENV === 'development') {
  globalThis.__db__ = db;
}

export default db;
```

`globalThis`에 대해서 더 알고 싶다면 [[global vs globalThis]].
