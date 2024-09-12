---
title: plan and solve
date: 2024-09-04
tags:
  - seed
  - ai
---

[[LLM]]에게 문제 해결 과정을 체계적으로 접근하도록 유도하여, 더 정확하고 논리적인 결과를 얻을 수 있게 하는 [[프롬프트]] 기법이다.

[[Zero-Shot]] 상황에서 문제를 해결하고 싶을 때 아주 유용하다.

예시 참고:
https://github.com/AGI-Edgerunners/Plan-and-Solve-Prompting

```
Let's devise a plan and solve the problem step by step.
```

```
Let's first understand the problem and devise a plan to solve the problem. Then, let's carry out the plan to solve the problem step by step.
```

```
Let's first prepare relevant information and make a plan. Then, let's answer the question step by step (pay attention to commonsense and logical coherence).
```

```
Let's first understand the problem, extract relevant variables and their corresponding numerals, and make and devise a complete plan. Then, let's carry out the plan, calculate intermediate variables (pay attention to correct numerical calculation and commonsense), solve the problem step by step, and show the answer.
```
