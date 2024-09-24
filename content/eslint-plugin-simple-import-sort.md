---
title: eslint-plugin-simple-import-sort
date: 2024-09-24
tags:
  - seed
---

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
