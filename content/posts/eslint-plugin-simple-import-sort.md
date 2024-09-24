---
title: eslint-plugin-simple-import-sort
date: 2024-09-24
tags:
  - seed
---

커스텀 자유도를 낮춤으로 쉽게 import를 정렬할 수 있는 eslint plugin이다.

기본 정렬 순서:

1. Side effect imports. (These are not sorted internally.)
2. Node.js builtins prefixed with `node:`.
3. Packages.
4. Absolute imports and other imports.
5. Relative imports.

eslint 9 버전:

```json
import simpleImportSort from 'eslint-plugin-simple-import-sort';

export default [
  // ...
  {
    plugins: {
      'simple-import-sort': simpleImportSort,
    },
    rules: {
      'simple-import-sort/imports': 'error',
      'simple-import-sort/exports': 'error',
    },
  },
]
```

커스텀 버전:

```json
"simple-import-sort/imports": ["error", {
  "groups": [
    // `react` related packages, External packages
    ["^react", "^@?\\w"],
    [
      // Internal packages
      "^(constant)(/.*|$)", "^(store)(/.*|$)", "^(utils)(/.*|$)", "^(api)(/.*|$)", "^(contexts)(/.*|$)", "^(hooks)(/.*|$)", "^(components/layout)(/.*|$)", "^(components/common)(/.*|$)", "^(components/pages)(/.*|$)", "^(pages)(/.*|$)",
      // Side effect imports
      "^\\u0000",
      // Parent imports (..): ../depth  >  ..
      "^\\.\\.(?!\\/?$)", "^\\.\\.\\/?$",
      // Same-folder imports(.): ./depth/  >  ./depth  >  .
      "^\\.\\/(?=.*\\/)(?!\\/?$)", "^\\.(?!\\/?$)", "^\\.\\/?$"
    ],
    // Style imports
    ["(?=.*react)(?=.*css).*", "^.+\\.?(scss)$", "^.+\\.?(css)$"]
  ]
}]
```
