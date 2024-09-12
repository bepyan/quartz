---
title: Pretendard 세팅
date: 2024-09-11
tags:
  - seed
---

한국에서 개발의 표준이 되어 버린 프리텐다드.
https://github.com/orioncactus/pretendard

쉽게 적용하려면 `head`에 [[dynamic-subset]] css을 추가하면 된다.

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

외부 cdn이 아닌 회사 내부 cdn을 활용하고 싶다면,
https://github.com/orioncactus/pretendard/tree/main/dist/web/static 여기 파일들을 다운 받아서 원하는 곳에 배치하면 된다.

만약 한자도 표기하고 싶다면 [Pretendard JP](https://github.com/orioncactus/pretendard/tree/main/packages/pretendard-jp) 폰트를 사용해야 한다.

## tailwind + css variable로 세팅하기

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
