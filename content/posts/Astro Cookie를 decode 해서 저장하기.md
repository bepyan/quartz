---
title: Astro Cookie를 decode 해서 저장하기
date: 2025-01-15
tags:
  - seed
  - astro
---

Astro에서 Cookie를 저장할 때 `encode`되어 저장된다.

이 때 Astro.Cookie의 encode 속성을 활용하면 된다.
https://docs.astro.build/en/reference/api-reference/#encode

```js
Astro.cookies.set('example', 'test value', {
  encode: (value) => value,
});
```

참고:
https://github.com/withastro/astro/issues/10711#issuecomment-2041795251
