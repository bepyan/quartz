---
title: markdown code focus
date: 2024-10-14
tags:
  - seed
---

[[shiki]]의 코드 하이라이트 기능 중에 하나이다.
https://shiki.style/packages/transformers#transformernotationfocus

```ts
console.log('Not focused');
console.log('Focused') // [!code focus]
console.log('Not focused');
```

주석으로 `code focus`할 곳을 명시하면 된다.
https://shiki.style/packages/transformers#transformernotationfocus

## VitePress에서의 사용법

VitePress에서 이를 사용하고 있다.
https://vitepress.dev/guide/markdown#focus-in-code-blocks

소스코드:
https://github.com/vuejs/vitepress/blob/fb772acacf27b4c07096eb9374154c9ea4213d09/src/node/markdown/plugins/highlight.ts#L73-L76

```ts
const transformers: ShikiTransformer[] = [
    //...
    transformerNotationFocus({
      classActiveLine: 'has-focus',
      classActivePre: 'has-focused-lines'
    }),
]
```

https://github.com/vuejs/vitepress/blob/fb772acacf27b4c07096eb9374154c9ea4213d09/src/client/theme-default/styles/components/vp-doc.css#L375-L393

```css
.vp-doc [class*='language-'] .has-focused-lines .line:not(.has-focus) {
  filter: blur(0.095rem);
  opacity: 0.4;
  transition:
    filter 0.35s,
    opacity 0.35s;
}

.vp-doc [class*='language-'] .has-focused-lines .line:not(.has-focus) {
  opacity: 0.7;
  transition:
    filter 0.35s,
    opacity 0.35s;
}

.vp-doc [class*='language-']:hover .has-focused-lines .line:not(.has-focus) {
  filter: blur(0);
  opacity: 1;
}
```
