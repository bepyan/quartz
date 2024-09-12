---
title: prettier-plugin-tailwindcss
date: 2024-09-11
tags:
  - seed
---

tailwind 팀에서 만든 공식 prettier 플러그인이다.
https://github.com/tailwindlabs/prettier-plugin-tailwindcss

클래스명을 [our recommended class order](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier#how-classes-are-sorted) 기준으로 자동으로 정렬해준다.

```shell
pnpm add -D prettier-plugin-tailwindcss
```

```json
{
  "plugins": [
	"prettier-plugin-tailwindcss"
  ],
  "tailwindFunctions": ["cn", "cva"]
}
```

[`tailwindFunctions`](https://github.com/tailwindlabs/prettier-plugin-tailwindcss?tab=readme-ov-file#sorting-classes-in-function-calls)

`let className = cn("px-4 py-2 ...")` 같은 환경에서도 정렬이 진행할 수 있도록 해준다.
