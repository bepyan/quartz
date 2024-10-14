---
title: Quartz 4 custom
date: 2024-10-02
tags:
  - seed
---
[[Quartz 4]]를 쓰면서 커스터 마이징한 것을 정리해보았다.

## `quartz.config.ts`

공백(` `) 3개 없이 바로 줄바꿈을 적용
```ts
plugins: {
  transformers: [
    // ...
    Plugin.HardLineBreaks(),
  ]
},
```

root에 작성된 글은 항시 draft로 인식
```ts
ignorePatterns: [..., "[!_]*"],
```

## `quartz.layout.ts`

좌측 사이드바 레이아웃 커스텀화
```ts
export const defaultContentPageLayout: PageLayout = {
  left: [
    // ...
	Component.DesktopOnly(
	  Component.RecentNotes({
		title: "Recent Writing",
		limit: 1,
		filter: (f) =>
		  !f.frontmatter?.noindex &&
		  !!f.frontmatter?.tags?.some((t) => t === "fruit" || t === "evergreen"),
		linkToMore: "tags/fruit/" as SimpleSlug,
		showTags: false,
	  }),
	),
	Component.DesktopOnly(
	  Component.RecentNotes({
		title: "Recent Notes",
		limit: 2,
		filter: (f) => !f.frontmatter?.noindex && !!f.frontmatter?.tags?.some((t) => t === "seed"),
		linkToMore: "tags/seed/" as SimpleSlug,
		showTags: false,
	  }),
	),
  ]
}
```

## `custom.scss`

좌측 사이드바 레이아웃 커스텀화
```scss
.left {
  display: grid !important;
  gap: 1.5rem !important;
  grid-template-columns: 1fr;
  grid-template-rows: min-content min-content min-content min-content;
  align-items: center;

  .page-title {
    grid-area: 1 / 1 / 2 / 3;
  }

  .search {
    grid-area: 2 / 1 / 3 / 2;
  }

  .darkmode {
    grid-area: 2 / 2 / 3 / 3;
  }

  .toc {
    grid-row: 3;
    grid-column: 1 / 3;
  }

  .recent-notes {
    .meta {
      font-size: 0.8em;
    }
  }

  .recent-notes:nth-last-child(2) {
    grid-area: 3 / 1 / 3 / 3;
  }

  .recent-notes:nth-last-child(1) {
    grid-area: 4 / 1 / 4 / 3;
  }

  @media all and (max-width: $fullPageWidth) {
    display: flex !important;
  }
}
```

구분선 커스텀화
```css
hr {
  overflow: visible;
  padding: 0;
  height: 0;
  margin: 4em auto;
  border: none;
  text-align: center;
  width: 100%;

  &:after {
    content: "* * *";
    display: inline-block;
    margin: -1em 0 0.5em;
    font-size: 1.5em;
    padding: 0.5em 1em;
    color: var(--gray);
  }
}
```

여백 추가
```css
article {
  h2 {
    margin-top: 5rem;
  }

  h3 {
    margin-top: 3.5rem;
  }
}
```

코드 블럭 스크롤바 숨기기
```css
pre > code {
  box-sizing: border-box;
  min-height: 36px;
  overflow: auto;
}
```
