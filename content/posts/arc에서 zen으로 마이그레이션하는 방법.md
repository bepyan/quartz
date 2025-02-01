---
title: arc에서 zen으로 마이그레이션하는 방법
date: 2025-01-31
tags:
  - seed
---

arc에서 성능, 배터리 소모 이슈로 zen으로 마이그레이션을 해보기로 했다.
([[zen에서 arc로 넘어가야하는 이유]])

arc는 자체적으로 북마크, 히스토리 등 데이터를 추출할 수 없게 되어 있다. 따라서 chrome 프로필을 활용하여 데이터를 옮길 수 있다.

아래 글을 참고하여 arc 프로필 데이터를 chrome 프로필로 넘길 수 있다.
https://gist.github.com/clouedoc/4acc8355782f394152d8ce19ceaf53ba

이후 zen 설정에서 `Import Browser Data`를 검색하여 해당프로필 데이터를 옮기면 된다.

`Import` 시 `Import all available data`  클릭해서 `Payment methods`는 체크 해제해야 한다.

다만 기존 워크스페이스와 북마크를 옮길 수 없다.
