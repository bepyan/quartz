---
title: clearLocationHash
date: 2024-09-26
tags:
  - seed
  - snippet
---

웹 개발을 하다 보면 URL의 해시(#) 부분을 제거해야 할 때가 있다. 
단순히 `location.hash = ''`를 적용할 경우URL에  `#`이 남게 된다.

이를 해결하기 위해선 `history.replaceState`를 활용하면 된다.

```js
export const clearLocationHash = () => {
    const uri = window.location.toString();

    if (uri.indexOf('#') > 0) {
        const cleanUri = uri.substring(0, uri.indexOf('#'));
        window.history.replaceState({}, document.title, cleanUri);
    }
};
```

사용 예:

```js
// URL이 "https://example.com/page#section1" 일 때
clearLocationHash();
// URL이 "https://example.com/page"로 변경됩니다.
```
