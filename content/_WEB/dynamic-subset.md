---
title: dynamic-subset
date: 2024-09-12
tags:
  - seed
---

**다이나믹 서브셋**은 웹 폰트 최적화 기술 중 하나로, **웹 페이지에 실제로 사용되는 글자만 선별적으로 로드하는 방식**이다.

주요 특징은 아래와 같다.

- 페이지에 실제로 사용되는 글자만 서버에서 클라이언트로 전송한다.
- 전체 폰트 파일이 아닌 필요한 부분만 다운로드하므로 **초기 페이지 로드 시간이 단축**된다.
- 불필요한 데이터 전송을 줄여 서버와 클라이언트 모두의 리소스를 절약한다.
- 특히 한중일(CJK) 폰트와 같이 글자 수가 많은 언어에 매우 효과적이다.

다이나믹 서브셋을 구현하기 위해서는 특별한 서버 설정이나 폰트 서비스(Google Fonts, cloudflare cdn 등)의 지원이 필요하다.

구체적인 동작 과정은 아래와 같다.

### 1. CSS 파일 로딩

`pretendard-dynamic-subset.min.css` 파일을 로드하게 되면 아래 코드처럼 스타일이 적용된다.

```css
/* [0] */
@font-face {
	font-family: 'Pretendard Variable';
	font-style: normal;
	font-display: swap;
	font-weight: 45 920;
	src: url(../../../packages/pretendard/dist/web/variable/woff2-dynamic-subset/PretendardVariable.subset.0.woff2) format('woff2-variations');
	unicode-range: U+f9ca-fa0b, U+ff03-ff05, U+ff07, U+ff0a-ff0b, U+ff0d-ff19, U+ff1b, U+ff1d, U+ff20-ff5b, U+ff5d, U+ffe0-ffe3, U+ffe5-ffe6;
}

/* [1] */
@font-face {
	font-family: 'Pretendard Variable';
	font-style: normal;
	font-display: swap;
	font-weight: 45 920;
	src: url(../../../packages/pretendard/dist/web/variable/woff2-dynamic-subset/PretendardVariable.subset.1.woff2) format('woff2-variations');
	unicode-range: U+d723-d728, U+d72a-d733, U+d735-d748, U+d74a-d74f, U+d752-d753, U+d755-d757, U+d75a-d75f, U+d762-d764, U+d766-d768, U+d76a-d76b, U+d76d-d76f, U+d771-d787, U+d789-d78b, U+d78d-d78f, U+d791-d797, U+d79a, U+d79c, U+d79e-d7a3, U+f900-f909, U+f90b-f92e;
}
```

### 2. 폰트 로딩

브라우저에서 `unicode-range` 범위에 있는 문자를 발견하게 되면 `src`에 명시된 폰트 파일을 참조하게 된다.



따라서 [[Pretendard 세팅]]할 땐 일반 폰트보다는 다이나믹 서브셋의 css를 활용하면 좋다.
