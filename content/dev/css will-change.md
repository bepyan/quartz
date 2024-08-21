---
title: css will-change
date: 2024-08-21
tags:
  - seed
  - css
---

`will-change`는 CSS 속성으로, 브라우저에게 요소가 곧 변형될 것이라는 힌트를 준다. 

```css
.my-element {
  will-change: transform;
}
```

이를 적용하면, 브라우저는 [[Compositing Layers|별도의 레이어]]를 생성하거나 추가적인 리소스를 할당한다.
이는 GPU 가속을 활용하여 브라우저 성능 최적화할 수 있다.

따라서 과도한 사용은 오히려 성능 저하를 일으킬 수 있다.

대규모 DOM 요소가 한 번에 변경될 때 사용하면 좋고,
변화가 끝나면 해당 속성을 제거되도록 설계하는 것이 좋다.

```css
.button {
  transition: transform 0.3s ease-out;
}

.button:hover {
  will-change: transform;
}

.button:active {
  transform: scale(1.1);
}
```
