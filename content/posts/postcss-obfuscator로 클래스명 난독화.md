---
title: postcss-obfuscator로 클래스명 난독화
date: 2023-11-20
tags:
  - seed
---

`package.json`
```json
{
    "build:cleanup": "rm -rf out dist",
    "build:css:prepare": "mkdir -p out/src",
    "build:css:obfuscation": "NODE_ENV=obfuscation postcss src/styles/tailwind.css  --dir out/src/styles",
    "build:css": "yarn build:css:prepare && yarn build:css:obfuscation",
    "build:js": "yarn vite build",
    "build": "yarn build:cleanup && yarn build:css && yarn build:js",
}
```

`postcss.config.js`
```js
const isProd = process.env.NODE_ENV === 'production';
const isObfuscation = process.env.NODE_ENV === 'obfuscation';

module.exports = {
  plugins: [
    (!isProd || isObfuscation) && require('tailwindcss'),
    (!isProd || isObfuscation) && require('autoprefixer'),
    isObfuscation &&
      // @see https://github.com/n4j1Br4ch1D/postcss-obfuscator
      require('postcss-obfuscator')({
        enable: true,
        srcPath: 'src',
        desPath: 'out/src',
        jsonsPath: 'out/css-obfuscator',
        formatJson: true,
        extensions: ['.svelte'],
        classIgnore: ['resize', 'translate', 'transform', 'ease-out', 'ease-in-out'],
      }),
  ],
};
```

`vite.config.ts`
```js
import * as path from 'path';

import { defineConfig } from 'vite';

const isProd = process.env.NODE_ENV === 'production';

// https://vitejs.dev/config/
export default defineConfig({
  //...
  resolve: {
    alias: {
      '~': path.resolve(__dirname, isProd ? './out/src' : './src'),
    },
  },
  build: {
    copyPublicDir: true,
    lib: {
      name: 'phocus',
      entry: path.resolve(__dirname, './out/src/index.ts'),
    },
  },
});

```

문제점

- `class:*`  문법을 제대로 파싱하지 못함...
- `style:transition="transform ..."` `style` 안을 파싱해버림
