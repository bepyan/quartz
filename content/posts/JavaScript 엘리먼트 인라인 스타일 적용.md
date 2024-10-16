---
title: JavaScript 엘리먼트 인라인 스타일 적용
date: 2024-10-16
tags:
  - seed
---

```js
/**
 * 요소에 스타일을 설정하는 함수,
 * @param {HTMLElement} el 스타일을 설정할 HTML 요소
 * @param {Object} styles CSS 스타일 객체.
 * 카멜 케이스만 지원되며 케밥 케이스는 지원하지 않습니다.
 * 같은 속성이 여러 번 나타나면, 마지막으로 지정된 값이 최종적으로 적용됩니다.
 * @example
 * setElementStyles(document.body, {
 *     backgroundColor: 'red',
 *     fontSize: '16px',
 *     marginTop: 20  // 숫자는 자동으로 'px'로 변환됩니다
 * });
 */
export const setElementStyles = (el, styles) => {
    Object.assign(el.style, styles);
};
```
