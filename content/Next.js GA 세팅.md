---
title: Next.js GA 세팅
date: 2024-12-15
tags:
  - seed
---

https://nextjs.org/docs/messages/next-script-for-ga

```shell
pnpm add @next/third-parties
```

```tsx
import { GoogleAnalytics } from '@next/third-parties/google'
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <GoogleAnalytics gaId="G-XYZ" />
    </html>
  )
}
```