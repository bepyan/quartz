---
title: Github Action 기본 세팅
date: 2023-10-31
tags:
  - seed
  - dev
---

## `CODEOWNERS`

```
* @bepyan
```

## `auto_assign.yml`

1. [Install the app](https://github.com/apps/auto-assign).
2. Create `.github/auto_assign.yml` in your repository with the following.

```yml
addReviewers: false
addAssignees: author
```

https://github.com/kentaro-m/auto-assign/

## Github PR Issue 라벨 자동 부착

`./github/workflows/labeler.yml`

```yml
name: 'Pull Request Labeler'
on:
  - pull_request_target

jobs:
  labeler:
    permissions:
      contents: read
      pull-requests: write
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v4
        with:
          repo-token: '${{ secrets.GITHUB_TOKEN }}'
```

`./github/labeler.yml`

```yml
workflow:
  - .github/workflows/*

ci:
  - .github/workflows/ci.yml

style:
  - src/styles/*
  - src/styles/**/*

'test: e2e':
  - e2e/*
  - e2e/**/*

'test: unit':
  - src/**/*.test.{js,jsx,ts,tsx}
  - src/__test__/*
  - src/__test__/**/*

docs:
  - '*.md'
  - '**/*.md'
```
