---
title: Next.js shadcn-ui 세팅
date: 2024-09-11
tags:
  - seed
  - fe
---

```shell
pnpx shadcn-ui@latest init
```

`package.json`에 아래 script를 추가하자.
```
"ui": "pnpx shadcn-ui@latest add",
"ui:lint": "pnpx prettier src/components/ui/* --write"
```

component를 추가하고 lint를 수행해주면 된다.
```shell
pnpm ui avatar button card dropdown-menu input textarea label select separator sonner tabs tooltip dialog aspect-ratio accordion
pnpm ui:lint
```
