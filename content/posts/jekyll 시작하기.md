---
title: jekyll 시작하기
date: 2025-03-13
tags:
  - seed
---

https://jekyllrb-ko.github.io/docs/

먼저 [[ruby 개발환경 세팅]]한다.

이후 jekyll 개발 환경을 설치한다.

```shell
gem install jekyll bundler
```

이제 특정 레포 가서 번들 설치 후 실행하면 된다.

```shell
bundle install
```

```shell
bundle exec jekyll serve
```

디폴트로 https://localhost:4000/ 에서 페이지를 접근할 수 있게 된다.

페이지 번들 생성물에 대해서 `.gitignore`도 추가해줘야 한다.

```
_site
.jekyll-cache
```