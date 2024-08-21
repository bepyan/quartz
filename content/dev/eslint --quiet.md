---
title: eslint --quiet
date: 2024-08-21
tags:
  - seed
  - eslint
---

ESLint에서 warning을 무시하고 error만 출력되게 설정할 수 있다.

```shell
eslint --quiet .
```

또는

```shell
eslint -q .
```

추가로, 특정 디랙토리에 대해서만 error를 출력하게 할 수 있다.

```shell
eslint --quiet src/
```
