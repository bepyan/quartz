---
title: ToT
date: 2024-09-04
tags:
  - seed
---

Tree of Thoughts 의 약자로, 문제 해결하기 위해 여러 가능한 경로를 트리 형태로 탐색한다. [[CoT]]와 [[ReAct]]을 더욱 발전시킨 [[프롬프트]] 기법이다.

CoT와 다르게 여러 가능한 경로를 동시에 고려한다.

특히 전략 게임, 복잡한 계획 수립, 다단계 의사결정 등의 분야에서 강력한 성능을 보일 수 있다.

프롬프트 예시: 

```
Imagine three different experts are answering this question.
All experts will write down 1 step of their thinking,
then share it with the group.
Then all experts will go on to the next step, etc.
If any expert realises they're wrong at any point then they leave.
The question is...
```

```
문제: [복잡한 문제 설명]

사고 트리:
1. 초기 접근:
   1.1 방법 A
       - 장점: ...
       - 단점: ...
   1.2 방법 B
       - 장점: ...
       - 단점: ...

2. 선택된 접근 (예: 1.2)의 세부 단계:
   2.1 단계 1
       - 결과: ...
       - 다음 선택: ...
   2.2 단계 2
       - 결과: ...
       - 다음 선택: ...

3. 최종 해결책:
   [선택된 경로를 따라 도출된 최종 해결책]

평가 및 결론:
[최종 해결책에 대한 평가와 결론]
```

참고:
https://www.promptingguide.ai/techniques/tot