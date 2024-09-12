---
title: 0902 Advance AI 교육
date: 2024-09-02
draft: true
tags:
  - seed
  - ai
---

> GenAI / LLM 활용 및 성능 개선


## Deep learning to LLM
https://docs.google.com/presentation/d/1j9LcRmwkX0MCnfJHExAJNGqWMM2jB1KHCeGySp0xSLM/edit?usp=sharing

확률적(Stochastic) vs 결정론적(Deterministic)

성능과 비용을 종합해서 고려해야 한다.
https://chat.lmsys.org/?leaderboard
어디에 쓸지에 따라 비용의 효율이 달라진다. 일반적으로 클라우드 기반 API 서비스을 사용하는 것이 훨씬 싸고 빠르다. 다만, 파인튜닝의 한계, 서비스로서의 안정성, 보안 등 제한이 있다.

큰 모델부터 써보고 작은 모델을 파인튜닝 해보자.
해당 솔루션에 대한 검증이 먼저이기 때문이다.

ChatGPT(3.5) 175B을 기준으로 연산 비용을 계산해보자.
→ Parameter 당 16bit 를 쓴다면, 350GB 크기의 모델이 필요하다.
→ 사용성의 하한선인 10 tokens/s을 기준으로, 350GB * 10/s = 3.5TB/s 성능이 필요하다.
→ 일반 DRAM의 Bandwidth로 모델 파라미터가 커버되지 않기 때문에 HBM을 사용한다. GPU를 빠르게 서빙할 NVLink 등 하드웨어도 필요하다.
→ 최소 5억 이상 하드웨어가 준비되어야 한다.

중국에서 만든 Qwen2가 잘 최적화 되어 있다.
https://arxiv.org/abs/2407.10671

보통 DRAM의 용량과 Bandwidth가 병목이 일어나는데, Bandwidth를 최적화하면 좋다.

**KV Caching**
Attention 연산 과정에서 입력 프롬프트 각 토큰에 대한 Key, Value는 출력이 끝날 때까지 계속해서 반복적으로 사용된다. 따라서 값을 매번 계산하지 않고, 이 값을 메모리에 ‘캐싱' 해두면 연산량과 bandwidth을 줄일 수 있다.

**Batching** strategies for LLM
비슷한 요청에 대해서 묶어서 연산하여 응답을 주는 전략이다.
Ex: Static Batching, Dynamic Batching, Continuous Batching.

**MoE** (Mixture of Experts)
모든 파라미터가 매번 다 필요하지 않다.
입력에 따라 8개 expert 중 2개를 선택해 계산하면, 훨씬 Bandwidth를 줄일 수 있다.

GQA(Group Query Attention), Flash Attention 

모델 평가, **Latency & Throughput**
Summarization, Generation, 결국 메모리 Bandwidth가 중요하다?

**On device AI**
성능이 낮아도 괜찮은 요소가 많다. 개인정보로부터 자유롭고, 비용이 낮다.
소비 전력이 너무 민감한다.

필요 기능에 따라 On device AI + Cloud AI를 함께 사용하는 것이 추세이다.

**LLM in a flash**
출력값이 0인 부분을 딥러닝을 통해서 예측하여 읽지 않는 접근으로 Bandwidth의 한계를 보완하려한다. 하지만 아직 공개된 부분이 적어 반신반의 상태이다.

**Quantization**
32 bit 을 16 bit 으로 줄이는 접근이다.

**Samba**
context가 길어지는 것에 대해서 `O(n^2)`을  `O(n)`로 줄이는 방법론이다.

**Route LLM**
LoRA-Guard

Understanding Transformer / Attention 
(추천: https://www.youtube.com/watch?v=wjZofJX0v4M&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=5)

Cloud API vs On premise vs On device 별 고려사항


## Prompt Engineering
https://docs.google.com/presentation/d/1EY4og1jqViMUAjj9Qv5gtBd8Xu4oASC0vkL6QqMkVkA/edit#slide=id.p

**[[Few-shot]]**, One-shot, Zero-shot
shot은 예시는 말한다.
몇몇 예시를 던져주면, In context learning 있기에 더 의미가 있다.

**[[CoT]]** (Chain of Thought)
페르소나, step by step ...이 중요한 이유이다.

**Self Consistency**
같은 질문에 대해 다양한 방법 / 여러 차례 반복을 통해 나온 답 중 가장 많이 나온 답을 선택한다.
다만 비용이 늘어난다.

**Least to Most**
Decomposition, 잘게 쪼갠다.
Subproblem solving, 순차적으로 푼다.
귀납법. 다만 요즘은 그냥 해도 성능이 잘 나온다.

**Tree of Thoughts**
**X of Thoughts**
**Graph of Thoughts**

**[[Program of Thoughts]]**
글로 컨텍스트를 전달하기 보단, 코드 포멧으로 전달하는 방법.

**[[Plan and Solve]]**
CoT에서 놓쳐지는 Step를 개선하는 방법이다.
플랜을 만들어서 실행하록하는데 아래 프롬프트를 참고해보도록 하자.
https://github.com/AGI-Edgerunners/Plan-and-Solve-Prompting

**ReAct**
Reason(CoT) + Act
보통 검색을 통해서 초기 프롬프트를 완성시키는 방법이다.

**Generated Knowledge Prompting**
지식을 많이 참고해야하는 경우 유용하다.
주어진 질문에 대한 관련 지식을 LLM 이 생성하고 질문과 지식을 조합하여 답변 생성한다.

**Prompt engineering write / update**

보여줄 예시나 참고할 자료가 있나?
few shot, web search, RAG

활용할 논리나 구조가 있나? 
CoT, ToT, Self consistency

문제를 더 잘게 쪼갤 수 있나?
least to most, plan and solve

스스로 결과 검증할 수 있나?
Self evaluation, self-redefine, chain of verification, system 2 attention etc.

포맷

클로드의 시스템 
https://docs.anthropic.com/en/release-notes/system-prompts#july-12th-2024

**Prompt Generator**

https://console.anthropic.com/dashboard