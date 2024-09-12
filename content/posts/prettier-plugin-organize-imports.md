---
title: prettier-plugin-organize-imports
date: 2024-09-11
tags:
  - seed
  - fe
---

아주 단순하게 **알파벳 순서** `import` 구문을 정렬해주는 prettier 플러그인이다.
https://github.com/simonhaenisch/prettier-plugin-organize-imports#readme

```shell
pnpm add -D prettier-plugin-organize-imports
```

```json
{
  "plugins": [
	"prettier-plugin-organize-imports",
  ],
}
```

정렬을 무시하는 방법:
```
// organize-imports-ignore
```

더 정교한 정렬을 수행하고 싶다면 eslint 진영의 플러그인의 도움을 받아야 한다.
