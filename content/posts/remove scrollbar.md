---
title: remove scrollbar
date: 2024-09-10
tags:
  - evergeeen
  - fe
---

스크롤바를 제거하는 방법에 대해서 기록해보자.

### radix-ui

radix-ui에서 사용하는 패턴은 아래와 같다.
https://github.com/radix-ui/primitives/blob/main/packages/react/scroll-area/src/ScrollArea.tsx

```css
[data-radix-scroll-area-viewport] {
  scrollbar-width: none;
  -ms-overflow-style: none;
  -webkit-overflow-scrolling: touch;
}
[data-radix-scroll-area-viewport]::-webkit-scrollbar {
  display: none;
}
:where([data-radix-scroll-area-viewport]) {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
:where([data-radix-scroll-area-content]) {
  flex-grow: 1;
}
```
