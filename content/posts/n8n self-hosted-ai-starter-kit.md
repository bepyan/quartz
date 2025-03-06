---
title: n8n self-hosted-ai-starter-kit
date: 2025-03-06
tags:
  - seed
---

[[n8n]]을 빠르게 self hosting을 해보는 starter kit이다.
https://docs.n8n.io/hosting/starter-kits/ai-starter-kit/

## 시작하기

```zsh
git clone https://github.com/n8n-io/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
```

docker가 없다면 [[docker 세팅]]한다.

```zsh
# 맥 기준으로 명령어
docker compose --profile cpu up
```

이후 http://localhost:5678/setup 에 접속할 수 있게 된다.

