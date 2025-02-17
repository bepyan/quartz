---
title: vscode에서 svelte 컴포넌트 import이 자동완성이 안되는 현상 대응
date: 2025-02-17
tags:
  - seed
---


`tsconfig.json` 설정 문제로 보인다.
`include`에 `svelte` 파일이 포함되어 있지 않으면 자동완성을 지원해주지 않는다.

```json
{
  "include": ["**/*"],
  "exclude": ["dist"]
}
```

아래 같이 모든 파일을 포함시키고, 불필요한 빌드 번들을 제외하는 설정이 간편해 보인다.

참고:
https://docs.astro.build/en/guides/typescript/#tsconfig-templates


## index.svelte 지양

`button/index.svelte` 이 있을 경우, `<Button />`로 import 자동완성을 지원 받지 못한다.

