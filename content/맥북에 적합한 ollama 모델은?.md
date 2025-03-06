---
title: 맥북에 적합한 ollama 모델은?
date: 2025-03-06
tags:
  - seed
---

내 맥북 스펙은 아래와 같다.

```
MacBook Pro 16 (M3 Max, 36GB RAM) 
```

빠른 응답을 위해선 7B를 추천한다.
복잡한 논리 전개나 긴 맥락 이해에서는 한계가 있다.

```zsh
ollama run deepseek-r1:7b
```

사실 M3 Max 정도 스팩이면 13B 파라미터 모델도 무난한게 돌릴 수 있다.

```zsh
ollama run deepseek-r1:14b
```

30B 이상은 긴 대기 시간이 발생될 수 있기에 대신 웹 서비스를 사용하는 것이 좋아 보인다.