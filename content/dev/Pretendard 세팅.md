---
title: Pretendard 세팅
date: 2024-09-11
tags:
  - seed
---

한국에서 개발의 표준이 되어 버린 프리텐다드.
https://github.com/orioncactus/pretendard

쉽게 적용하려면 `head`에 `dynamic-subset`을 추가하면 된다.

```html
<head>
  <link
    rel="stylesheet"
    as="style"
    crossOrigin="anonymous"
    href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css"
  />
</head>
```

tailwind + css variable로 세팅하기

```css
@layer base {
  :root {
    --font-sans: "Pretendard Variable", Pretendard;
  }
  ...
}
```

```json
theme: {
    fontFamily: {
      sans: ['var(--font-sans)', 'sans'],
      // ...
    }
}
```
