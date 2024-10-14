---
title: markdown code snippets
date: 2024-10-14
tags:
  - seed
---
> [wagmi docs](https://wagmi.sh/react/getting-started)를 보고 이거 어떻게 했지하면서 연구하게되었다.
> 알고 보니 [vitepress](https://vitepress.dev/guide/markdown#import-code-snippets)에서 사용하는 커스텀 플러그인이었다.

```
<<< @/snippets/snippet.js{2}
```

코드 원본:
https://github.com/vuejs/vitepress/blob/fb772acacf27b4c07096eb9374154c9ea4213d09/src/node/markdown/plugins/snippet.ts

동작 단계를 분석해보면 그렇게 복잡하지 않다.

### 0. fence에 커스텀 로직 적용

markdown-it는 `fence`을 활용해서 코드 블럭을 파싱한다.
따라서 `md.renderer.rules.fence` 을 활용해서 로직에 추가 기능을 구현할 수 있다.

### 1. `<<<` 문법 인식

우리만의 약속된 문법 `<<<`을 통해서 코드를 불러오도록 한다.

```
<<< @/filepath
```

### 2. 소스 코드 파일 읽기

```ts
const resolvedPath = path.resolve(path.dirname(realPath ?? _path), filepath)
```

### 3. html 파싱

소스 코드 파일 존재 유무를 파악하고 코드를 string으로 파싱한다.

```ts
let content = fs.readFileSync(src, 'utf8').replace(/\r\n/g, '\n')

if (regionName) {
  const lines = content.split('\n')
  const region = findRegion(lines, regionName)

  if (region) {
	content = dedent(
	  lines
		.slice(region.start, region.end)
		.filter((line) => !region.regexp.test(line.trim()))
		.join('\n')
	)
  }
}

token.content = content
```
