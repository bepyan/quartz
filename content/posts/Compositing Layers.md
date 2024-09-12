---
title: Compositing Layers
date: 2024-08-21
tags:
  - seed
  - web
---

Compositing Layers(합성 레이어)는 웹 페이지 렌더링 과정에서 중요한 역할을 한다.
이 레이어는 GPU에서 독립적으로 관리되며, 메인 스레드의 부하를 줄인다.

합성 레이어 생성 조건은 아래와 같다.

- `transform: translateZ()` 같은 3D 변형된 요소
- `<video>`, `<canvas>`, `<iframe>` 요소
- CSS 애니메이션을 사용하는 요소
- `will-change` 속성을 사용하는 요소
- `opacity` 값이 1이 아닌 요소

Chrome 개발자 도구의 'Layers' 패널을 사용하여 이 레이어들이 어떻게 처리되는지 확인할 수 있다.
