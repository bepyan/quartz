---
title: flex item에 ellipsis 적용하기
date: 2024-11-04
tags:
  - seed
---

말줄임 효과 `text-overflow: ellipsis`을 적용하기 위해서 아래 2속성이 적용 되어야 한다.

```css
overflow: hidden;
white-space: nowrap;
```

보통 `width: 200px` 같이 고정된 넓이를 지정함으로 ellipsis 효과를 줄 수 있다.

하지만 flex item의 경우 고정된 넓이를 쓰지 않고 `flex: 1` 으로 자동 레이아웃을 적용한다. 그럴 때 ellipsis 효과가 적용되지 않는 것을 발결할 수 있는데 `min-width`이 `auto`로 지정되기 때문이다.

따라서 `min-width: 0`을 적용하면 문제를 해결할 수 있다.

---

참고
https://velog.io/@eenaree/flex-item-ellipsis
