
```shell
npm install -g pnpm
```

```shell
pnpm create astro@latest
```

[[VSCode 설정 세팅]]
[[Prettier 세팅]]

```shell
pnpm add -D prettier prettier-plugin-astro
touch .prettierrc.mjs
```

```js
/** @type {import("prettier").Config} */
export default {
  plugins: ['prettier-plugin-astro'],
  overrides: [
    {
      files: '*.astro',
      options: {
        parser: 'astro',
      },
    },
  ],
};
```

alias
https://docs.astro.build/en/guides/typescript/#import-aliases

```json
{
  "extends": "astro/tsconfigs/strict",
  "include": [".astro/types.d.ts", "**/*"],
  "exclude": ["dist"],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "~/*": ["src/*"]
    }
  }
}
```

eslint
```
pn add -D eslint @eslint/js eslint-plugin-astro eslint-plugin-simple-import-sort eslint-plugin-unused-imports typescript-eslint @typescript-eslint/parser
```

```
touch eslint.config.js
```

```
import pluginJs from "@eslint/js";
import eslintPluginAstro from "eslint-plugin-astro";
import simpleImportSort from "eslint-plugin-simple-import-sort";
import unusedImports from "eslint-plugin-unused-imports";
import globals from "globals";
import pluginTs from "typescript-eslint";

export default [
  { files: ["**/*.{js,mjs,cjs,ts,astro}"] },
  { ignores: [".astro/**/*", "dist/**/*", "**/static/"] },
  { languageOptions: { globals: globals.browser } },
  pluginJs.configs.recommended,
  ...pluginTs.configs.recommended,
  ...eslintPluginAstro.configs.recommended,
  {
    rules: {
      "no-undef": "off",
      "@typescript-eslint/ban-ts-comment": "off",
      "@typescript-eslint/no-unused-expressions": [
        "error",
        { allowShortCircuit: true },
      ],
    },
  },
  // @see https://github.com/lydell/eslint-plugin-simple-import-sort
  {
    plugins: {
      "simple-import-sort": simpleImportSort,
    },
    rules: {
      "simple-import-sort/imports": "error",
      "simple-import-sort/exports": "error",
    },
  },
  // @see https://github.com/sweepline/eslint-plugin-unused-imports
  {
    plugins: {
      "unused-imports": unusedImports,
    },
    rules: {
      "no-unused-vars": "off",
      "@typescript-eslint/no-unused-vars": "off",
      "unused-imports/no-unused-imports": "error",
      "unused-imports/no-unused-vars": [
        "warn",
        {
          vars: "all",
          varsIgnorePattern: "^_",
          args: "after-used",
          argsIgnorePattern: "^_",
        },
      ],
    },
  },
];

```


## tailwind v4

https://astro-tips.dev/tips/tailwind-v4/

```

```