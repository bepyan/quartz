---
title: git fetch과 git pull의 차이
date: 2024-08-20
tags:
  - seed
---

둘 다 원격 저장소의 변경사항을 로컬로 가져오는 명령어이다.

다만 `fetch`는 변경사항을 확인만 하고, `pull`은 변경사항을 가져와 즉시 통합한다.

```
fetch + merge(또는 rebase) = pull
```

빠르게 origin과 통합하고 싶다면 아래 같이 `pull` 명령어를 수행하면 된다.

```shell
git pull --rebase origin main
```
