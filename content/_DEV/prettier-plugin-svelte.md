---
title: Prettier 세팅 with Svelte
date: 2024-09-11
tags:
  - seed
---

```shell
pnpm add -D prettier-plugin-svelte
```

```json
{
	plugins: ['prettier-plugin-svelte'],
	// https://github.com/sveltejs/prettier-plugin-svelte#prettierrc-example
  svelteSortOrder: 'options-scripts-markup-styles',
  svelteStrictMode: false,
  svelteAllowShorthand: true,
  svelteIndentScriptAndStyle: true,
}
```

참고: https://github.com/sveltejs/prettier-plugin-svelte#prettierrc-example

