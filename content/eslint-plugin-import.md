---
title: eslint-plugin-import
date: 2024-09-24
tags:
  - seed
---

아직 eslint 9을 지원하지 않는 것으로 보인다.
https://github.com/import-js/eslint-plugin-import/issues/2948

```json
    // https://github.com/import-js/eslint-plugin-import/blob/main/docs/rules/order.md
    'import/order': [
        'error',
        {
            'groups': ['builtin', 'external', 'internal', ['parent', 'sibling', 'index']],
            'alphabetize': {
                order: 'asc',
                caseInsensitive: true,
            },
            'newlines-between': 'always',
        },
    ],
    'import/first': 'error',
    'import/newline-after-import': 'error',
    'import/prefer-default-export': 'off',
    'import/no-useless-path-segments': ['error', { noUselessIndex: true }],
```
