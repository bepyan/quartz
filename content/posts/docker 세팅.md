---
title: docker 세팅
date: 2025-03-06
tags:
  - seed
---

`homebrew`로 설치하는 방법이다.

```zsh
brew install --cask docker
```

설치 후 docker desktop 앱을 열어야 사용할 수 있다.
`cmd + space` `docker` 앱 실행한다.

이후 아래 명령어를 입력하면 도커 실행 현황이 보여지게 된다.

```zsh
docker ps 
```

## 트러블슈팅

만약 설치가 안된다면?

```zsh
brew list --cask | grep docker
```

여기에 docker가 뜬다면 설치가 안된 것이다.
따라서 아래 명령어로 docker를 제거하면 된다.

```zsh
brew uninstall docker
```
