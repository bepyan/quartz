---
title: git rebase reset
date: 2024-09-23
tags:
  - seed
---

> [[git fetch과 git pull의 차이]]

git merge 혹은 git pull을 하다보면 브랜치가 충돌되는데 엄청 꼬일 때가 있다.

해당 브랜치를 완전 초기화하고 싶다면 아래 명령어를 수행하면 된다.

```shell
git reset --hard origin/xxx
```
