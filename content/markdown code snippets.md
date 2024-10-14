---
title: markdown code snippets
date: 2024-10-14
tags:
  - seed
---
> [wagmi docs](https://wagmi.sh/react/getting-started)를 보고 이거 어떻게 했지하면서 연구하게되었다.
> 알고 보니 [vitepress](https://vitepress.dev/guide/markdown#import-code-snippets)에서 사용하는 커스텀 플러그인이었다.

```
<<< @/filepath
```

```
<<< @/snippets/snippet.js{2}
```

코드 원본:
https://github.com/vuejs/vitepress/blob/fb772acacf27b4c07096eb9374154c9ea4213d09/src/node/markdown/plugins/snippet.ts
