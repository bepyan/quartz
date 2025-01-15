---
title: vite에서 dev server에 https를 붙이는 방법
date: 2025-01-14
tags:
  - seed
---

`@vitejs/plugin-basic-ssl`  `vite-plugin-mkcert`등 라이브러리를 사용할 수도 있지만, vite에서는 직접 cert를 설정하는 것을 권장하고 있다.

:::
In most scenarios, it is recommended to generate a secure trusted certificate instead and use it to configure [`server.https`](https://vitejs.dev/config/server-options.html#server-https)
:::

그럼 직접 설정하는 방법을 알아보자면,
`mkcert`로 자체 TLS 인증서를 발급하는 것이 가장 편하다.

```bash
brew install mkcert
mkcert -install
```

```bash
mkcert local.bepyan.me
```

Astro에서는 아래 같이 설정하면 된다.
참고로 Astro는 vite 기반이다.

```json
import { defineConfig } from 'astro/config';
import fs from 'fs';

const HOST_URL = 'local.bepyan.me';

export default defineConfig({
	server: {
		host: HOST_URL,
		port: 443,
	},
	vite: {
	  server: {
	    https: {
	      key: fs.readFileSync(`./cert/${HOST_URL}-key.pem`),
	      cert: fs.readFileSync(`./cert/${HOST_URL}.pem`),
	    },
	  },
	},
}
```

`443` 포트는 특권 포트로, 관리자 권한이 필요하다.
따라서 관리자 권한으로 개발서버를 실행하면 된다.

```bash
sudo npm run dev
```

만약 브라우저에서 "개인 정보 보호" 관련 경고가 뜬다면, `cert` 파일이 제대로 로드되지 않았기 때문이다. `vite.config`이 있는 디랙토리 기준으로 파일을 읽기에 경로를 잘 설정해줘야 한다.

참고:
https://vite.dev/config/server-options.html#server-https
https://nodejs.org/api/https.html#https_https_createserver_options_requestlistener
https://web.dev/articles/how-to-use-local-https?hl=ko
