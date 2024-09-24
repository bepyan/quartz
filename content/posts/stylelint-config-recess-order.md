---
title: stylelint-config-recess-order
date: 2024-09-24
tags:
  - seed
---

> twiter, Bootstrap에서 채용한 CSS 정렬 방식
> https://github.com/stormwarning/stylelint-config-recess-order

[stylelint-order](https://github.com/hudochenkov/stylelint-order?tab=readme-ov-file)을 활용하여 구현되었다.

```shell
pnpm add -D stylelint-config-recess-order
```

```json
{
	extends: ['stylelint-config-recess-order'],
	rules: {
		// Add overrides and additional rules here
	},
}
```

개인적으로 이전에 [`stylelint-config-idiomatic-order`](https://github.com/ream88/stylelint-config-idiomatic-order)을 사용했으나, 더이상 유지보수가 되지 않다.
