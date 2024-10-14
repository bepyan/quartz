---
title: VitePress 분석
date: 2024-10-14
tags:
  - fruit
---
VitePress는 Vite & Vue 기반의 문서 생성 프레임워크이다.
https://vitepress.dev/

[VuePress](https://github.com/vuejs/vuepress)에서 새롭게 브랜딩되었다.
Vite, Vue 진영의 오픈소스 메인테이너가 만든 프레임워크이다보니 DX도 무척 좋다.
UI가 매우 깔끔하며 기능도 풍부하다.

기본적으로 [markdown-it](https://github.com/markdown-it/markdown-it) 으로 마크다운을 파싱하며, [shiki](https://github.com/shikijs/shiki)로 코드 하이라이트한다.
front-matter는 [gray-matter](https://github.com/jonschlinkert/gray-matter)로 구현했다.

디테일한 기능은 markdown-it 기반의 커스텀 플러그인으로 구현했다.

- [[markdown code focus]]
- [[markdown code group]]
- [[markdown code snippets]]

Vue 기반이라 React 컴폰넌트를 사용하지 못하는 아쉬움이 있다.

대안으로,
Svelte 커뮤니티에서 따라 만든 [SveltePress](https://github.com/SveltePress/sveltepress)가 있지만 퀄리티 차이가 크다.
React 진영은 [Docusaurus](https://github.com/facebook/docusaurus),
Next.js 진영은 [Nextra](https://nextra.site/),
Astro 진영은 [Starlight](https://github.com/withastro/starlight),
하지만 개인적으로 VitePress의 완성도가 가장 좋은 것 같다.