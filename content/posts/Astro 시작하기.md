---
title: Astro 시작하기
date: 2024-12-24
tags:
  - seed
---

```shell
npm install -g pnpm
```

```shell
pnpm create astro@latest
```

[[VSCode 설정 세팅]]
[[Prettier 세팅]]

```shell
pnpm add -D prettier prettier-plugin-astro
touch .prettierrc.mjs
```

```js
/** @type {import("prettier").Config} */
export default {
  plugins: ['prettier-plugin-astro'],
  overrides: [
    {
      files: '*.astro',
      options: {
        parser: 'astro',
      },
    },
  ],
};
```

alias
https://docs.astro.build/en/guides/typescript/#import-aliases

```json
{
  "extends": "astro/tsconfigs/strict",
  "include": [".astro/types.d.ts", "**/*"],
  "exclude": ["dist"],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "~/*": ["src/*"]
    }
  }
}
```

eslint

[[Eslint 세팅]]

```js
import eslintPluginAstro from "eslint-plugin-astro";

export default [
  ...eslintPluginAstro.configs.recommended,
  // ...
];

```


## tailwind v4

https://astro-tips.dev/tips/tailwind-v4/
