---
title: (svelte) use-click-outside
date: 2024-09-09
tags:
  - seed
  - fe
  - snippet
---

## Svelte에서 clickOutside 기능 구현하기

웹 애플리케이션을 개발하다 보면 특정 영역 외부를 클릭했을 때 동작을 처리해야 하는 경우가 자주 있다. 이런 기능을 'clickOutside'라고 부르는데, 주로 모달이나 드롭다운 메뉴를 닫을 때 사용한다. Svelte에서는 이 기능을 간단하고 효율적으로 구현할 수 있다. 여기서는 두 가지 방식의 clickOutside 구현을 살펴보자.


## 1. 기본 버전

가장 기본적인 형태의 clickOutside 함수는 이렇다.

```ts
export default function clickOutside(node: HTMLElement, handler: () => void) {
  const onClick = (event: MouseEvent) =>
    node &&
    !node.contains(event.target as HTMLElement) &&
    !event.defaultPrevented &&
    handler();

  document.addEventListener('click', onClick, true);

  return {
    destroy() {
      document.removeEventListener('click', onClick, true);
    },
  };
}

```

이 버전은 간단하지만 효과적이다. 함수는 두 개의 매개변수를 받는다:

- `node`: clickOutside를 적용할 HTML 요소
- `handler`: 외부 클릭 시 실행할 콜백 함수

함수는 문서 전체에 클릭 이벤트 리스너를 추가하고, 클릭된 요소가 지정된 노드의 외부에 있는지 확인한다. 외부 클릭이 감지되면 핸들러 함수를 호출한다.

## 2. 고급 버전

더 많은 제어가 필요한 경우, 다음과 같은 버전을 사용할 수 있다.

```ts
export default function clickOutside(
  node: HTMLElement,
  {
    enabled: initialEnabled,
    callback,
  }: {
    enabled: boolean;
    callback: () => void;
  },
) {
  const handleOutsideClick = (event: MouseEvent) => {
    if (!node.contains(event.target as Node)) {
      callback();
    }
  };

  function update({ enabled }: { enabled: boolean }) {
    if (enabled) {
      document.addEventListener('click', handleOutsideClick);
    } else {
      document.removeEventListener('click', handleOutsideClick);
    }
  }

  update({ enabled: initialEnabled });

  return {
    update,
    destroy() {
      document.removeEventListener('click', handleOutsideClick);
    },
  };
}
```

이 버전은 추가적인 기능을 제공한다:

- `enabled` 옵션으로 clickOutside 기능을 동적으로 켜고 끌 수 있다.
- `update` 함수로 컴포넌트의 프로퍼티가 변경될 때 동작을 조절할 수 있다.

## 사용 예시

Svelte 컴포넌트에서 이 기능을 사용하는 방법은 다음과 같다:

```svelte
<script>
  import clickOutside from '~/libs/svelte/use-click-outside';
  
  let isOpen = false;
</script>

<div use:clickOutside={{ enabled: isOpen, callback: () => (isOpen = false) }}>
  <button>열기/닫기</button>
  {#if isOpen}
    <div>이 영역 외부를 클릭하면 닫힙니다.</div>
  {/if}
</div>
```

이 예시에서는 `isOpen` 상태에 따라 clickOutside 기능이 활성화되며, 외부 클릭 시 `isOpen`을 `false`로 설정하여 영역을 닫는다.

더 구체적인 예시는 [[(svelte) dropdown]]을 참고해봐도 좋을 것 같다.

## 결론

Svelte의 액션(action) 기능을 활용한 clickOutside 구현은 코드의 재사용성을 높이고 컴포넌트의 로직을 간결하게 유지하는 데 도움이 된다. 초 간단 버전은 간단한 사용 사례에 적합하고, 조금 더 복잡한 버전은 더 복잡한 상황에서 유연성을 제공한다.

이 패턴을 활용하면 사용자 경험을 향상시키고 인터페이스를 더욱 직관적으로 만들 수 있다. 그냥 `innerText` 혹은 `innerHTML`을 사용하는 것보다 이런 방식으로 구현하면 Svelte의 라이프사이클이 제대로 반영되어 예상치 못한 동작을 방지할 수 있다.

clickOutside 기능을 구현할 때는 성능과 사용성을 고려해야 한다. 불필요한 이벤트 리스너 추가를 피하고, 필요한 경우에만 활성화하는 것이 좋다. 또한, 접근성을 고려하여 키보드 사용자를 위한 대체 방법도 함께 제공하는 것이 좋다.

이 구현을 바탕으로 프로젝트의 요구사항에 맞게 커스터마이징하여 사용하면 된다. Svelte의 반응성과 결합하여 사용하면 더욱 강력한 UI 컴포넌트를 만들 수 있을 것이다.