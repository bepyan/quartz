---
title: (svelte) dropdown
date: 2024-09-09
tags:
  - seed
  - fe
  - snippet
---

## Svelte에서 Dropdown 컴포넌트 구현하기

웹 애플리케이션에서 자주 사용되는 UI 요소 중 하나가 드롭다운 메뉴다. 이전 글에서 다룬 clickOutside 기능과 결합하면 사용성 높은 드롭다운 컴포넌트를 만들 수 있다. 이번에는 Svelte를 사용해 재사용 가능한 드롭다운 컴포넌트를 구현해보자.

## 1. 컴포넌트 구조

먼저 드롭다운 아이템의 인터페이스를 정의하고, 필요한 모듈들을 import 한다.

```svelte
<script lang="ts" context="module">
  export interface DropdownItem {
    label: string;
    value: string;
  }
</script>

<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { cn } from '~/libs/utils';
  import { buttonVariants } from '~/components/ui/button';
  import clickOutside from '~/libs/svelte/use-click-outside';

  // props 정의
  export let items: DropdownItem[] = [];
  export let selectedValue: string | null = null;
  export let buttonClass: string = '';
  export let menuClass: string = '';
  export let align: 'start' | 'end' = 'start';

  // 내부 상태 및 로직
  let isOpen: boolean = false;
  const dispatch = createEventDispatcher<{ select: { item: DropdownItem } }>();

  $: selectedItem = items.find(
    (item) =>
      item.value === selectedValue ||
      (selectedValue === null && item.value === undefined)
  ) ?? null;

  function toggleDropdown(): void {
    isOpen = !isOpen;
  }

  function selectItem(item: DropdownItem): void {
    selectedValue = item.value;
    isOpen = false;
    dispatch('select', { item });
  }

  // 드롭다운 애니메이션
  function dropdownTransition(node: HTMLElement) {
    return {
      delay: 0,
      duration: 100,
      css: (t: number, u: number) => `
        opacity: ${t};
        transform: scale(${0.95 + 0.05 * t}) translateY(-${2 * u}px);
      `,
    };
  }
</script>
```

여기서 주목할 점은 `clickOutside` 모듈을 import 하고 있다는 것이다. 이는 이전 글에서 구현한 [[(svelte) use-click-outside]] 기능을 그대로 활용하는 것이다.

## 2. 컴포넌트 마크업

다음은 드롭다운의 HTML 구조다.

```svelte
<div
  class="relative font-sans"
  use:clickOutside={{ enabled: isOpen, callback: () => (isOpen = false) }}
>
  <button
    class={cn(
      buttonVariants({
        variant: 'ghost',
        size: 'icon',
        className: buttonClass,
      })
    )}
    on:click={toggleDropdown}
  >
    <slot name="button">{selectedItem ? selectedItem.label : 'Select'}</slot>
  </button>
  {#if isOpen}
    <div
      transition:dropdownTransition
      class={cn(
        'absolute top-full z-50 mt-1 flex min-w-[8rem] flex-col overflow-hidden rounded-md border bg-page p-1 shadow-md',
        align === 'end' ? 'right-0' : 'left-0',
        menuClass
      )}
    >
      {#each items as item}
        <button
          class="inline-flex w-full items-center justify-between rounded-sm px-2 py-1.5 text-left text-sm capitalize text-heading hover:bg-selection"
          on:click={() => selectItem(item)}
        >
          {item.label}
          {#if selectedItem === item}
            <!-- dot icon -->
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="1em"
              height="1em"
              viewBox="0 0 256 256"
            >
              <path
                fill="currentColor"
                d="M156 128a28 28 0 1 1-28-28a28 28 0 0 1 28 28Z"
              />
            </svg>
          {/if}
        </button>
      {/each}
    </div>
  {/if}
</div>
```

이 마크업에서 `use:clickOutside`를 사용하고 있는 것을 볼 수 있다. 이는 이전에 구현한 clickOutside 액션을 드롭다운 컴포넌트에 적용한 것이다. 드롭다운이 열려있을 때(`isOpen === true`) 외부를 클릭하면 드롭다운이 닫히도록 설정되어 있다.

## 3. 주요 기능 설명

1. **상태 관리**: `isOpen` 변수로 드롭다운의 열림/닫힘 상태를 관리한다.
2. **선택된 아이템 추적**: `selectedValue`와 `selectedItem`을 사용해 현재 선택된 아이템을 추적한다.
3. **이벤트 디스패치**: Svelte의 `createEventDispatcher`를 사용해 아이템 선택 시 이벤트를 발생시킨다.
4. **스타일링**: `cn` 함수와 `buttonVariants`를 사용해 동적으로 클래스를 적용한다.
5. **애니메이션**: `dropdownTransition` 함수로 드롭다운 메뉴에 간단한 애니메이션을 적용한다.
6. **clickOutside 적용**: 드롭다운 외부 클릭 시 메뉴가 닫히도록 `clickOutside` 액션을 사용한다.

## 4. 사용 예시

이 드롭다운 컴포넌트는 다음과 같이 사용할 수 있다:

```svelte
<script>
  import Dropdown from './Dropdown.svelte';

  const items = [
    { label: 'Option 1', value: '1' },
    { label: 'Option 2', value: '2' },
    { label: 'Option 3', value: '3' },
  ];

  let selectedValue = null;

  function handleSelect(event) {
    console.log('Selected:', event.detail.item);
  }
</script>

<Dropdown {items} bind:selectedValue on:select={handleSelect} />
```

## 결론

이렇게 구현한 드롭다운 컴포넌트는 재사용성이 높고, clickOutside 기능이 통합되어 있어 사용자 경험이 좋다. Svelte의 반응성과 결합하여 상태 관리가 간편하고, 커스터마이징도 쉽게 할 수 있다.

이전 글에서 다룬 clickOutside 기능을 실제 컴포넌트에 적용하는 방법을 보여줌으로써, 재사용 가능한 기능을 만들고 이를 실제 UI 컴포넌트에 통합하는 과정을 이해할 수 있다. 이런 방식으로 코드를 구조화하면 유지보수가 쉽고 확장성 있는 애플리케이션을 만들 수 있다.

추가로, 접근성을 고려하여 키보드 네비게이션을 지원하거나, 다양한 스타일 옵션을 제공하는 등의 개선을 할 수 있다. 프로젝트의 요구사항에 맞게 이 컴포넌트를 확장하고 커스터마이징하여 사용하면 된다.