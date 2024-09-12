---
title: VSCode 설정 세팅
date: 2024-09-11
tags:
  - seed
---

```shell
touch .vscode/settings.json
```

`.vscode/settings.json` 

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": "explicit"
  },
  "css.lint.unknownAtRules": "ignore",
  "tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cn\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ],
  "typescript.updateImportsOnFileMove.enabled": "always",
  "typescript.preferences.importModuleSpecifier": "non-relative",
  "workbench.editor.customLabels.patterns": {
    "**/{layout,page,route,index}.ts{,x}": "${dirname}/${filename}"
  }
}
```

### editor

`defaultFormatter`는 `prettier`로 설정한다.

`formatOnSave`로 파일 저장시 포멧팅 되도록 한다.

`codeActionsOnSave`로 파일 저장시 eslint auto fix를 수행한다.


### css.lint.unknownAtRules

```
"css.lint.unknownAtRules": "ignore",
```

tailwind 관련 구문의 경고를 제거해줄 수 있다.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### tailwindCSS.experimental.classRegex

```
"tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cn\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ]
```

`class` `className` 외로 `cva`, `cn` 같은 함수로 감싼 문자열에도 tailwind를 적용할 수 있다.


### workbench.editor.customLabels

파일명을 더 직관적으로 보기 위한 기능이다.
특히 Next.js 같이 같은 파일명이 많은 프로젝트에서 유용하다.

```
  "workbench.editor.customLabels.patterns": {
	"**/{layout,page,route,index}.ts{,x}": "${dirname}/${filename}"
  }
```

참고: https://code.visualstudio.com/docs/getstarted/userinterface#_customize-tab-labels

IntellJ는 디폴트로 똑똑하게 알아서 제공해주는 기능이다.


### explorer.fileNesting

같은 depth에 있는 파일에 대해서 펼접할 수 있게 해준다.
특히 `index.ts`, `index.test.ts` 이렇게 사용하는 경우 유용하게 활용할 수 있다.

```
"*.ts": "$(capture).js, $(capture).d.ts.map, $(capture).*.ts, $(capture)_*.js, $(capture)_*.ts",
```

참고: https://github.com/antfu/vscode-file-nesting-config
