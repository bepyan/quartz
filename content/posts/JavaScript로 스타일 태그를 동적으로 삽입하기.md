---
title: JavaScript로 스타일 태그를 동적으로 삽입하기
date: 2024-10-16
tags:
  - seed
---

현대에 널리 쓰이는 `CSS-in-JS` 라이브러리는 스타일을 동적으로 삽입한다.
초기 CSS 파일의 용량을 최소화할 수 있다.
([CSS-in-JS-라이브러리에-대한-고찰](https://velog.io/@bepyan/CSS-in-JS-라이브러리에-대한-고찰) 참고)

프로젝트에서 해당 기능을 가볍게 사용하고 싶지만, 라이브러리를 추가하기엔 부담스러울 때가 있다.
이때 JavaScript으로 직접 구현해 볼 수 있다. 

방법은 간단하다.
`<style>` 태그를 만들고 `<head>` 태그에 삽입하면 된다.

```js
const styleEl = document.createElement('style');
styleEl.textContent = `
/* ... */
`;
document.head.appendChild(styleEl);
```

하지만 현실에서는 여러가지에 대해서 대응을 해야 한다.

## 1. CSS 압축

브라우저 렌더링 성능을 개선하기 위함이다.
브라우저가 CSS를 파싱해서 화면을 그리기 때문에 압축된 CSS는 파싱에 유리하다.

```js
export const compressCSS = (styleSheet) => {  
    return styleSheet  
        .replace(/\s+/g, ' ') // 연속된 공백을 단일 공백으로 변경
        .replace(/:\s+/g, ':') // 콜론(:) 주변의 공백 제거
        .replace(/\s*{\s*/g, '{') // 중괄호({}) 주변의 공백 제거
        .replace(/\s*}\s*/g, '}') 
        .replace(/\s*;\s*/g, ';') // 세미콜론(;) 주변의 공백 제거
        .replace(/\s*,\s*/g, ',') // 쉼표(,) 주변의 공백 제거
        .trim(); // 문자열 앞뒤의 공백 제거
};
```

## 2. 중복 스타일 로드 방지

스타일이 중복으로 로드되는 것 자체가 비효율적이다.
여러가지 방법으로 이 문제에 접근할 수 있지만, 여기서는 기존 스타일을 덮어씌워지도록 하자.

```js
const styleId = "uniqueID";

const existStyleEl = document.getElementById(styleId);

if (existStyleEl) {
	existStyleEl.remove(); // 기존 스타일 태그 제거
}

const styleEl = document.createElement('style');
styleEl.id = styleId;
```

## 최종 코드

이제 이를 `appendStyles`로 유틸화하여 쉽게 활용 할 수 있다.

```js
/**  
 * CSS 문자열을 압축합니다.  
 * 이 함수는 불필요한 공백을 제거하고 CSS 구문을 최소화하여 문자열의 크기를 줄입니다.  
 * @param {string} styleSheet - 압축할 CSS 문자열  
 * @returns {string} 압축된 CSS 문자열  
 */  
export const compressCSS = (styleSheet) => {  
    return styleSheet  
        .replace(/\s+/g, ' ') // 연속된 공백을 단일 공백으로 변경
        .replace(/:\s+/g, ':') // 콜론(:) 주변의 공백 제거
        .replace(/\s*{\s*/g, '{') // 중괄호({}) 주변의 공백 제거
        .replace(/\s*}\s*/g, '}') 
        .replace(/\s*;\s*/g, ';') // 세미콜론(;) 주변의 공백 제거
        .replace(/\s*,\s*/g, ',') // 쉼표(,) 주변의 공백 제거
        .trim(); // 문자열 앞뒤의 공백 제거
};

/**
 * 스타일을 문서의 <head> 요소에 추가합니다.
 * 만약 같은 ID를 가진 스타일 요소가 이미 존재한다면, 기존 요소를 제거하고 새로운 요소로 대체합니다.
 *
 * @param {string} styleId - 스타일 요소의 고유 ID
 * @param {string} styleSheet - 추가할 CSS 스타일 문자열
 * @returns {HTMLStyleElement} 새로 생성되어 문서에 추가된 스타일 요소
 *
 * @example
 * const styles = `
 *   .my-class {
 *     color: red;
 *     font-size: 16px;
 *   }
 * `;
 * appendStyles('my-styles', styles);
 *
 */
export const appendStyles = (styleId, styleSheet) => {
    const existStyleEl = document.getElementById(styleId);

    if (existStyleEl) {
        existStyleEl.remove();
    }

    const styleEl = document.createElement('style');
    styleEl.id = styleId;
    styleEl.textContent = compressCSS(styleSheet);
    document.head.appendChild(styleEl);

    return styleEl;
};
```

