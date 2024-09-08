---
title: switch (true) 패턴
date: 2024-08-06
tags:
  - seed
  - javascript
---

일련의 조건을 평가할 때 유용하다.

```js
function getGrade(score: number): string {
  switch (true) {
    case score >= 90:
      return 'A';
    case score >= 80:
      return 'B';
    case score >= 70:
      return 'C';
    case score >= 60:
      return 'D';
    default:
      return 'F';
  }
}
```

### 장점

- 복잡한 if-else 체인을 더 읽기 쉬운 형태로 구조화할 수 있다.
- 각 case에 여러 조건을 묶을 수 있어 유연성이 높다.
- break 문을 생략하면 fall-through 동작을 활용할 수 있다.

### 단점

- 일반적인 switch 문 사용법이 아니어서 다른 개발자들이 혼란스러워할 수 있다.
- 성능 면에서 일반적인 if-else 문과 큰 차이가 없다.

### 주의점

- 첫 번째로 true가 되는 case만 실행되므로, 조건의 순서가 중요하다.

### 참고

- https://ui.toast.com/posts/ko_20210603
- https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-3.html#switch-true-narrowing
