---
title: ProseMirror vs Slate
date: 2025-02-01
tags:
  - seed
---

## 1. 개요
ProseMirror와 Slate는 복잡한 문서 편집 요구사항을 해결하기 위해 설계된 오픈소스 텍스트 에디터 라이브러리이다. 
두 라이브러리는 각기 다른 철학과 아키텍처를 기반으로 하며, 개발자와 프로젝트의 필요에 따라 선택할 수 있다.

## 2. 아키텍처 비교

### ProseMirror
- **DOM 기반 설계**: 직접 DOM 조작을 통해 고성능 편집 구현  
- **트랜잭션 시스템**: 문서 변경을 트랜잭션 단위로 관리하여 협업 편집 지원  
- **스키마 정의**: 사용자 정의 문서 구조를 명시적으로 지정

### Slate
- **가상 DOM 활용**: React 생태계에 최적화된 렌더링 방식  
- **불변성 원칙**: Immutable.js 기반의 상태 관리  
- **플러그인 아키텍처**: 데코레이터 패턴을 통한 확장 기능 구현

## 3. 핵심 기능 대조

| 기능 영역    | ProseMirror                         | Slate                             |
|--------------|-------------------------------------|-----------------------------------|
| 협업 편집    | 내장 Yjs 통합                      | 외부 라이브러리 필요              |
| 문서 스키마  | 명시적 정의 필수                    | 런타임 유연성                     |
| 확장성       | 100+ 공식 플러그인 제공              | 커뮤니티 기반 확장                |
| 테이블 지원  | advanced-table 확장                 | 기본 기능 미흡                    |
| 학습 곡선    | 가파름 (전문 개념 학습 필요)          | 완만 (React 친화적)               |

## 4. 생태계 현황
- **GitHub 활동**:  
  - [Slate](https://github.com/ianstormtaylor/slate): 30k★  
  - [ProseMirror](https://github.com/ProseMirror/prosemirror): 7.9k★
- **성능 벤치마크**:  
  - ProseMirror가 대용량 문서 처리 시 약 2.3배 빠른 성능 기록

## 5. 개발자 경험

### 코드 예시

**ProseMirror 기본 초기화**
```javascript
import { EditorView } from 'prosemirror-view'
const view = new EditorView(document.body, {
  state: EditorState.create({ schema }),
  dispatchTransaction(tr) {
    view.updateState(view.state.apply(tr))
  }
})
```

**Slate React 통합 예시**
```jsx
import { createEditor } from 'slate'
const [editor] = useState(() => withReact(createEditor()))
<Slate editor={editor} value={initialValue}>
  <Editable />
</Slate>
```

## 6. 선택 가이드라인

**ProseMirror 채택 시**
- 실시간 협업 편집이 필수인 경우
- 복잡한 계층형 문서 구조가 필요한 경우
- 기존 DOM 기반 애플리케이션과의 통합이 중요한 경우

**Slate 채택 시**
- React 생태계 기반 프로젝트에 최적화되어 있을 경우
- 빠른 프로토타이핑과 유연한 커스터마이징이 요구되는 경우
- 커스텀 블록 디자인을 강조하는 프로젝트


## **결론**

두 라이브러리는 지속적인 업데이트를 통해 기능이 보완되고 있다.

**ProseMirror**는 복잡한 엔터프라이즈 요구사항과 고성능 협업 편집이 필요한 프로젝트에 적합하다.
**Slate**는 React 기반의 신속한 개발과 유연한 커스터마이징을 원하는 프로젝트에 더 적합하다.

사이드 프로젝트에 에디터가 필요할 경우 [[Tiptap vs Plate]]를 더 참고해보면 좋을 것이다.