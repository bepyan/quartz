---
title: LangGraph
date: 2024-09-04
tags:
  - seed
  - ai
---

[[LangChain]]의 확장 기능으로, 복잡한 AI 워크플로우를 구축하기 위한 도구이다. 이는 다단계 추론과 의사결정이 필요한 작업에 유용하다.

내부적으로 Directed Graph(유향 그래프) 구조를 사용한다. 그래프의 각 `Node`는 특정 작업을 수행하고, `Edge`는 작업 간의 흐름을 나타낸다. 이는 알고리즘에 따라 노드를 순회하면서 작업을 수행하게 된다.

초기 보일러 플레이트가 무겁지만 복잡한 [[AI Agent]]를 더욱 쉽게 구축할 수 있게 된다. 워크플로우에서 특정 작업을 유연하게 첨삭할 수 있다.

Node기반으로 이를 세팅하는 코드:
https://langchain-ai.github.io/langgraphjs/tutorials/rag/langgraph_agentic_rag/