---
title: Astro 서버 사이드에서 url hash를 취급하지 않는 이유
date: 2025-03-17
tags:
  - seed
---

해시값이 있는 url로 접근해도 `Astro.url.hash`가 항상 빈 문자열로 출력되는 현상이 있다.

이는 `hash`는 브라우저를 위한 것으로 대신 `query/search param`을 사용하라고 권고하고 있다.
https://github.com/withastro/astro/issues/3775

https://stackoverflow.com/questions/14462218/is-the-url-fragment-identifier-sent-to-the-server#:~:text=Fragment%20identifiers%20are%20not%20sent,elements%20within%20the%20same%20page