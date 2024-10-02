---
title: import order 뽀개기
date: 2024-09-13
tags:
  - fruit
  - dev
---
일관된 코드를 작성하기 위해선 import 구문을 특정 규칙을 갖고 정렬해야 한다.

어떤 솔루션이 있는지 살펴보도록 하자.
https://github.com/topics/sort-imports

## prettier 진영

[[prettier-plugin-organize-imports]]
단순하게 알파벳 순서로 정렬할 수 있다.

뭔가 특별한 규칙을 부여하고 싶다면 eslint 진영으로 접근해야 한다.

## eslint 진영

[[eslint-plugin-simple-import-sort]]
[[eslint-plugin-import]]

## 번외

[[stylelint-config-recess-order]]
import order는 아니지만 css attribute order를 보장해주는 도구도 있다.

