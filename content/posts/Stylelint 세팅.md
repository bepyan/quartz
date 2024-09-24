---
title: Stylelint 세팅
date: 2024-09-24
tags:
  - seed
---

> A mighty CSS linter that helps you avoid errors and enforce conventions.
> https://stylelint.io/

```shell
pnpm add -D stylelint stylelint-config-recess-order stylelint-config-recommended-scss
```

- [[stylelint-config-recess-order]]: css 속성 정렬
- stylelint-config-recommended-scss: sass 지원

```json
{
  "extends": ["stylelint-config-recess-order"],
  "overrides": [
    {
      "files": ["*.scss"],
      "extends": ["stylelint-config-recommended-scss"],
      "rules": {
        "no-descending-specificity": null
      }
    }
  ]
}
```

디폴트로 scss 파일에 대해서 검사가 안되기에(?) `.vscode/settings.json` 에 설정을 추가해야 한다.

```json
{
  // ...
  "stylelint.validate": ["css", "scss"],
}
```
