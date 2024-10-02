---
title: "@charset must precede all other statements"
date: 2024-10-02
tags:
  - seed
  - css
---

`@charset "UTF-8"`는 CSS 파일의 문자 인코딩을 명시적 UTF-8, 즉 다국어 지원에 적합한 유니코드 인코딩 방식으로 적용하는 코드이다.

브라우저가 CSS 파일을 올바르게 해석하기 위해, 파일의 인코딩을 먼저 알아야 한다. 최상단에 위치함으로써 브라우저가 파일을 읽기 시작할 때 즉시 인코딩 정보를 얻을 수 있다.

[CSS 명세](https://developer.mozilla.org/ko/docs/Web/CSS/@charset)에 따르면, @charset 규칙은 스타일시트의 첫 번째 요소여야 하며, 어떠한 공백이나 주석도 그 앞에 올 수 없다.

```css
@charset "UTF-8"; /* 스타일 시트의 인코딩을 Unicode UTF-8로 설정 */
 @charset "UTF-8"; /* 무효, at-규칙 앞에 문자(공백)가 있음 */
@charset UTF-8; /* 무효, ' 또는 " 없는 문자집합 CSS <string>이 아님 */
```
