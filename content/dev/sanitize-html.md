---
title: sanitize-html
date: 2024-08-22
tags:
  - seed
---

[sanitize-html](https://www.npmjs.com/package/sanitize-html?ref=blixt-dev)을 활용하여 허용되지 않는 HTML 태그을 제거할 수 있다.

이는 [XSS 공격]을 방어하기도 한다.
HTML 랜딩시, HTML 저장시에 `<script>` 같은 위험성 있는 태그를 제거해야한다.
