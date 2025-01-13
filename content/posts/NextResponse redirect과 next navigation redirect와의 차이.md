---
title: NextResponse redirect과 next navigation redirect와의 차이
date: 2024-12-24
tags:
  - seed
---

action, page에선 `navigation`, api 에서는 `NextResponse.redirect`를 사용해야 한다.

`NextResponse.redirect` 은 절대경로로 해야 한다. 
이를 쉽게 적용하는 방법은 아래와 같다.
```ts
const redirectTo = new URL(request.url);
redirectTo.pathname = '/';
return NextResponse.redirect(redirectTo);
```
