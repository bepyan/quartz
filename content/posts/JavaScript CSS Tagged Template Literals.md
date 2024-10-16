---
title: JavaScript CSS Tagged Template Literals
date: 2024-10-16
tags:
  - seed
---

```js
/**
 * CSS 문자열을 생성하는 태그된 템플릿 함수입니다.
 * 이 함수는 템플릿 리터럴의 정적 부분과 동적 부분을 결합하여 하나의 CSS 문자열을 만듭니다.
 *
 * @param {TemplateStringsArray} strings - 템플릿 리터럴의 정적 부분을 포함하는 문자열 배열
 * @param {...*} values - 템플릿 리터럴에 삽입될 동적 값들
 * @returns {string} 생성된 CSS 문자열
 *
 * @example
 * const backgroundColor = 'red';
 * const fontSize = '16px';
 *
 * const styles = css`
 *   .myClass {
 *     background-color: ${backgroundColor};
 *     font-size: ${fontSize};
 *   }
 * `;
 *
 * console.log(styles);
 * // 출력: .myClass { background-color: red; font-size: 16px; }
 *
 * @performance 이 함수는 런타임에 문자열 연산을 수행하므로, 대규모 CSS 블록이나
 * 빈번한 호출 시 성능에 영향을 줄 수 있습니다. 가능하면 정적 CSS를 사용하거나,
 * 결과를 캐싱하여 재사용하는 것이 좋습니다.
 */
export const css = (strings, ...values) => {
    return strings.reduce((acc, str, i) => {
        return acc + str + (values[i] || '');
    }, '');
};
```
