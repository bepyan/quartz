---
title: Astro에서 TanstackQuery를 사용하는 방법
date: 2025-02-27
tags:
  - seed
---

ReactQuery를 사용할 땐 QueryClientProvider를 사용하는데, Astro환경에서는 어떻게 사용해보면 좋을까?

## Provider

아주 간단한 방식은 기존 방식대로 `App` 컴포넌트에 `QueryClientProvider`를 씌우는 것이다.

```html
<body>
	<App client:lony />
</body>
```

하지만 [[Astro Islands]]을 활용할 수 없다는 치명적인 단점이 있다.

## 전역 상태 

`nanostores`를 통해서 `queryClient`를 전역 상태화를 하면 된다.

```ts
// src/stores/query.ts

import { QueryClient } from "@tanstack/react-query";
import { atom } from "nanostores";

export const queryClient = atom(new QueryClient());
```

```tsx
// src/components/Example.tsx

import { useStore } from "@nanostores/react";
import { useQuery } from "@tanstack/react-query";
import { queryClient } from "../stores/query";

export default function Example() {
  const client = useStore(queryClient);
  const { data } = useQuery({
      queryKey: ["example"],
      queryFn: async () => "Hello, world!",
  }, client);

  return (
    <div>
      <h1>{data}</h1>
    </div>
  );
}
```

단 `SSR`을 할 수 없어, `client:only`를 해야한다.

```html
<Example client:only="react" />
```

고도화할 수 있는 방법을 찾아 보자.

## nanostores

```ts
import { QueryClient, QueryObserver } from '@tanstack/query-core';
import { atom, onMount } from 'nanostores';

export const queryClient = atom(new QueryClient());

export const posts = atom<object | null>(null);

onMount(posts, () => {
  const observer = new QueryObserver<object>(queryClient.get(), {
    queryKey: ['posts'],
    queryFn: () => fetch(`https://dummyjson.com/posts`).then((res) => res.json()),
  });
  const unsubscribe = observer.subscribe(({ data }) => data && posts.set(data));

  return async () => {
    unsubscribe();
  };
});
```

https://github.com/TanStack/query/discussions/5152#discussioncomment-5399784

To be continue...


## 참고

https://hounie.me/writings/how-to-use-react-query-with-astro/
