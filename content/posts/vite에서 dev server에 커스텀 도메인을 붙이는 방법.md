---
title: vite에서 dev server에 커스텀 도메인을 붙이는 방법
date: 2025-01-14
tags:
  - seed
---

로컬 DNS에서 특정 도메인에 대해 라우팅을 설정할 수 있다.
이는 `/etc/hosts`에서 설정할 수 있다.

```shell
sudo vi ~/etc/hosts
```

```shell
127.0.0.1 local.bepyan.me
```

이후 vite 설정에서 관련 도메인을 설정할 수 있다.
Astro도 똑같이 설정해도 된다.

```json
server: {
  host: 'local.bepyan.me',
  port: 4321,
},
```

여기까지 설정했다면, 아래 도메인으로 개발서버를 접근할 수 있을 것이다.

```
http://local.bepyan.me:4321
```

만약 `https`를 적용하고 싶다면?
[[vite에서 dev server에 https를 붙이는 방법]]

참고:
https://github.com/vitejs/vite/discussions/5406
