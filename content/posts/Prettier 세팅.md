---
title: Prettier 세팅
date: 2024-09-11
tags:
  - seed
  - fe
---

```shell
pnpm add -D prettier prettier-plugin-organize-imports prettier-plugin-tailwindcss
```

```shell
touch .prettierrc
```

`.prettierrc`

```json
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80,
  "arrowParens": "always",
  "bracketSpacing": true,
}
```

`useTabs: false`
환경에 따라 `tab` 길이가 2칸일 수 있고 4칸일 수 있기 때문에 아예 허용하지 않는 것이 좋다.

`trailingComma: all`
객체, 배열 요소 마지막에 항시 `,`를 붙임으로 새로운 요소를 쉽게 추가할 수 있도록 한다.

나머지는 그냥 눈에 보기 편한 설정들이다.

특별한 이유가 없다면 그냥 [prettier 기본 세팅](https://prettier.io/docs/en/configuration.html)에 모두 위임하여 업계 표준을 따르는 것이 좋아 보인다.

자세한 설정 명세는 [공식문서](https://prettier.io/docs/en/options)를 참고해보자.

더 나아가 추가해보면 좋을 플러그인을 정리해보았다.

[[prettier-plugin-organize-imports]]
[[prettier-plugin-tailwindcss]]
[[prettier-plugin-svelte]]
[[prettier-plugin-astro]]

추가로 [[VSCode 설정 세팅]]에서 `formatOnSave` 설정을 진행하자.
