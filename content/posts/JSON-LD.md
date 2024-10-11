---
title: JSON-LD
date: 2024-10-11
tags:
  - seed
  - web
---

JSON-LD는 "JavaScript Object Notation for Linked Data"의 약자로, 구조화된 데이터를 표현하는 방식 중 하나이다.

JSON-LD의 활용은 검색결과에서의 가시성을 높이고, 클릭률(CTR)을 개선하는 데 도움을 줄 수 있다.

```html
<script type="application/ld+json">
{
	"@context": "http://schema.org",
	"@type": "Organization",
	"name": "브런치스토리",
	"url": "https://brunch.co.kr",
	"sameAs": [
		"https://play.google.com/store/apps/details?id=com.daumkakao.android.brunchapp",
		"https://apps.apple.com/kr/app/id1001388574"
	]
}
</script>
```

구글에서 JSON-LD을 권장하는 내용이 있다.
기본적으로 제품, 리뷰, 이벤트 등 다양한 유형의 정보를 표현할 수 있다.

- https://support.google.com/merchants/answer/6386198
- https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data
