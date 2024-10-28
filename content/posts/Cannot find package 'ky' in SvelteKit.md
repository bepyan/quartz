---
title: Cannot find package 'ky' in SvelteKit
date: 2024-10-28
tags:
  - seed
---

**TL;DR**
docker에서 `node_modules`를 복사해오지 않아 발생한 현상이었다.

[`ky`](https://github.com/sindresorhus/ky)는 `fetch`를 래핑한 통신 모듈이다.

SvelteKit SSR에서 사용하려면 [`ky-universal`](https://github.com/sindresorhus/ky-universal#readme) 라이브러리가 필요했다.

하지만 `ky` [v1.0.0](https://github.com/sindresorhus/ky/releases/tag/v1.0.0)가 릴리즈 되면서 `Node 18`이 fetch를 공식지원되면서 해당 라이브러리가 필요 없다고 한다.
