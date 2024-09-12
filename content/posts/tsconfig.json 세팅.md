---
title: tsconfig.json 세팅
date: 2024-09-12
tags:
  - seed
  - fe
---

`tsconfig.json`

```json
{
  "compilerOptions": {
    "lib": ["dom", "dom.iterable", "esnext"],
    "module": "esnext",
    "allowJs": true,
    "skipLibCheck": true,
    "incremental": true,

    /* Linting */
    "strict": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "verbatimModuleSyntax": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve",

    /* project setting */
    "plugins": [
      {
        "name": "next"
      }
    ],
    "outDir": "dist",
    "baseUrl": ".",
    "paths": {
      "~/*": ["./src/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

자세한 설명은 아래 gist 참고하면 좋다.
https://gist.github.com/SeonHyungJo/f93fd203f7dc5bb3657437a1cad29c48