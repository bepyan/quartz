---
title: tailwindcss 난독화
date: 2023-11-25
tags:
  - seed
---

## 방법 1. prefix
https://tailwindcss.com/docs/configuration#prefix
- no prefix will be added to your own custom classes.
- 문제는 직접 prefix을 붙여줘야 한다.
```html
<div class="tw-text-lg"></div>
```
- `cn` 유틸에 추가하는 형태로도 임의로 붙일 수도 있다.
```js
export function cn(...inputs: ClassValue[]) {
	const className = clsx(inputs);
	const prefixedClassName = className.split(' ').map(name => `tw-${name}`).join(' ');
  return twMerge(prefixedClassName);
}
```
- 다만 모든 class에 cn을 붙여써야하는 문제가 있다.


## 방법2. postcss 활용
[unplugin-tailwindcss-mangle](https://github.com/sonofmagic/tailwindcss-mangle/tree/main/packages/unplugin-tailwindcss-mangle)
- This plugin only transform those classes which name contain `-` or `:`
- `flex` 같은 클래스를 변환할 수 없다.

✨ [postcss-obfuscator](https://github.com/n4j1Br4ch1D/postcss-obfuscator) 
- https://github.com/n4j1Br4ch1D/postcss-obfuscator/issues/2
- [[postcss-obfuscator로 클래스명 난독화]]

[postcss-modules](https://github.com/madyankin/postcss-modules)

[postcss-rename](https://github.com/google/postcss-rename#usage)


## 방법3. 우회
tailwind 대신 unocss 사용하기?
- https://github.com/unocss/unocss
- [tagify](https://unocss.dev/presets/tagify) 옵션을 통해서 class를 태그로 만들 수 있다.
