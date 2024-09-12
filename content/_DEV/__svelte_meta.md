---
title: __svelte_meta
date: 2024-08-13
tags:
  - seed
  - svelte
---

`__svelte_meta`는 Svelte DOM의 소스코드 위치를 담은 메타 데이터이다.

```json
{
	"loc": {
		"char": 1548,
		"column": 16,
        "file": "src/components/button.tsx",
        "line": 34,
	}
}
```

무려 2018년도 초기에 추가된 기능이다.   
https://github.com/sveltejs/svelte/issues/1499

크롬 콘솔에서 아래 명령어로 위 데이터를 확인해볼 수 있다.

```shell
$0.__svelte_meta
```

[vite-plugin-svelte-inspector](https://github.com/sveltejs/vite-plugin-svelte/tree/main/packages/vite-plugin-svelte-inspector)에서 이를 활용하여 svelte 파일을 열어주는 기능을 제공해준다.

관련 메타정보를 남기고 싶지 않을 땐,   
svelte compilerOptions에서 `dev: false` 옵션을 적용하면 된다.

```js
compilerOptions : {
  dev: false,
}
```

참고:   
https://www.petermekhaeil.com/til/svelte-components-have-file-location-meta-data/
