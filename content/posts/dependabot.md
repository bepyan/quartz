---
title: dependabot
date: 2024-04-08
tags:
  - seed
---

`dependabot.yml`
```
version: 2
updates:
  - package-ecosystem: 'npm'
    directory: '/'
    schedule:
      interval: 'daily'

```

```
    labels:
      - "change:chore"
      - "impact:internal"
```

https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuring-dependabot-version-updates

## with bun

`dependabot-update-package-lock.yaml`
```
name: 'Dependabot: Update bun.lockb'
on:
  pull_request:
    paths:
      - 'package.json'

permissions:
  contents: write

jobs:
  update-bun-lockb:
    name: 'Update bun.lockb'
    if: github.actor == 'dependabot[bot]'
    runs-on: ubuntu-latest
    steps:
      - uses: oven-sh/setup-bun@v1
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
          ref: ${{ github.event.pull_request.head.ref }}
      - run: |
          bun install
          git add bun.lockb
          git config --global user.name 'dependabot[bot]'
          git config --global user.email 'dependabot[bot]@users.noreply.github.com'
          git commit --amend --no-edit 
          git push --force

```
https://github.com/dependabot/dependabot-core/issues/6528


## auto-merge

`auto-merge-dependabot.yaml`
```
name: Auto Merge Dependabot PRs
on:
  pull_request:
    branches:
      - main

permissions:
  contents: write
  pull-requests: write

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - name: Dependabot metadata
        id: metadata
        uses: dependabot/fetch-metadata@v1.1.1
        with:
          github-token: '${{ secrets.GITHUB_TOKEN }}'
      - name: Enable auto-merge for Dependabot PRs
        if: ${{ steps.metadata.outputs.update-type == 'version-update:semver-patch' }}
        run: gh pr merge --auto --merge "$PR_URL"
        env:
          PR_URL: ${{ github.event.pull_request.html_url }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```


## PR이 너무 많이 생성된다면..?
`open-pull-requests-limit` 설정 추가
https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#open-pull-requests-limit

패치 업데이트 무시
```
ignore:
  - dependency-name: 'github-linguist'
	update-types: ['version-update:semver-patch']
```


## PR 다루기
따로 해결해야할 패키지 버전 업데이트는 댓글을 작성
```
@dependabot ignore this major version
```

