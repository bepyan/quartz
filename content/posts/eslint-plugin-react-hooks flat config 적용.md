---
title: eslint-plugin-react-hooks flat config 적용
date: 2025-02-17
tags:
  - seed
---

https://github.com/facebook/react/pull/30774
https://github.com/facebook/react/tree/main/packages/eslint-plugin-react-hooks#flat-config-eslintconfigjs

```js
import pluginReactHooks from 'eslint-plugin-react-hooks';

export default [
    pluginReactHooks.configs['recommended-latest'],
];
```

만약 오류가 발생된다면,

```js
import pluginReactHooks from 'eslint-plugin-react-hooks';

export default [
  {
    files: ['**/**/*.{js,ts,jsx,tsx}'],
    plugins: {
      'react-hooks': pluginReactHooks,
    },
    rules: {
      ...pluginReactHooks.configs.recommended.rules,
    },
  },
];
```
