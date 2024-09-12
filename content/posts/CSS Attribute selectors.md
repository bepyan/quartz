---
title: CSS Attribute selectors
date: 2024-08-27
tags:
  - seed
  - css
  - fe
---

`ico_`로 시작하는 클래스에 스타일을 적용하고 싶다면 바로 [attribute selectors](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Attribute_selectors)을 활용하면 좋다.

```css
li[class^="box-"]
```

IE7부터 지원되기에 맘편히 쓰면 된다.

참고
https://stackoverflow.com/questions/13352080/match-all-elements-having-class-name-starting-with-a-specific-string
