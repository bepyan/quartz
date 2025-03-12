---
title: ruby 개발환경 세팅
date: 2025-03-13
tags:
  - seed
---

Mac의 경우 시스템에서 ruby를 사용하고 있어 개발단에서 권한 이슈가 발생될 수 있다.

rbenv를 통해서 특정 ruby 버전을 다운 받아서 사용해보자.
brew를 통해서 설치한다.

```zsh
brew install rbenv ruby-build
```

ruby 버전을 확인 후 원하는 버전을 다운 받는다.

```zsh
rbenv install -list
```

```zsh
rbenv install 3.4.2
rbenv global 3.4.2
```

`~/.zshrc`에 관련 경로 설정도 추가한다.

```zsh
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
```

이제 이를 통해서 
