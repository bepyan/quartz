---
title: markdown code group
date: 2024-10-14
tags:
  - seed
---
[[VitePress|VitePress]]에서의 커스텀 플러그인이다.
https://vitepress.dev/guide/markdown#code-groups

`::: code-group`을 통해서 코드 블럭을 쌓을 수 있다.
자세한 사용 방법은 아래와 같다.

```
::: code-group

<<< 코드 블럭 1
```ts [index.ts]


<<< 코드 블럭 2
```ts [config.ts]
...

:::
```

소스 코드:
https://github.com/vuejs/vitepress/blob/fb772acacf27b4c07096eb9374154c9ea4213d09/src/node/markdown/plugins/containers.ts#L82
