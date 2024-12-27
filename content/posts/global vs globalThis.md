---
title: global vs globalThis
date: 2024-12-27
tags:
  - seed
  - node.js
---

Node.js 환경에서 글로벌 객체에 접근하는 두 가지 주요 방법인 globalThis와 global을 비교해보자.

## 글로벌 객체란?

자바스크립트 환경에서 최상위 스코프를 제공하는 객체이다.

브라우저: `window`
Node.js: `global`

## global 객체

Node.js 전용 환경

특징:
- Node.js 내장 모듈 및 글로벌 변수 접근 가능
- ECMAScript 표준에 포함되지 않음

## globalThis 객체

모든 자바스크립트 환경 (브라우저, Node.js, 웹 워커 등)

특징:
- ECMAScript 2020 (ES2020) 표준
- 일관된 글로벌 객체 접근 방법 제공
- 이식성 높은 코드 작성 가능 (모든 환경에서 일관된 접근 방식)

## 결론

가능하면 globalThis를 사용하여 코드의 이식성과 호환성을 높이면 좋을 것 같다.

