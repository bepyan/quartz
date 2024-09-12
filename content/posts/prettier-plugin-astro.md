---
title: Prettier 세팅 with Astro
date: 2024-09-11
tags:
  - seed
  - fe
---

```shell
pnpm add -D prettier-plugin-astro
```

```json
{
	plugins: ['prettier-plugin-astro'],
  // https://github.com/withastro/prettier-plugin-astro
  overrides: [
    {
      files: '*.astro',
      options: {
        parser: 'astro',
      },
    },
  ],
}
```

https://github.com/withastro/prettier-plugin-astro
