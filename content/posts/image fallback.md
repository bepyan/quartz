---
title: image fallback
date: 2024-08-21
tags:
  - seed
  - fe
---

서버 부하를 줄이기 위해서 이미지 리소스를 줄이는 것이 필수적이다.
이미지 포멧 중 avif과 webp이 상당히 성능이 좋다.

그러나 IE에선 avif, webp을 지원하지 않는다.
이를 대응하기 위한 방법을 알아보자.

기본적인 전략은 최신 이미지 포멧에 대한 fallback을 지정해주는 것이다.

### `picture`

HTML의 `picture` 태그을 활용해서 fallback을 지정할 수 있다.

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="이미지 설명">
</picture>
```


### `image-set`

CSS 단에서는 `image-set`을 활용해 fallback을 제공할 수 있다.

```css
.image {
  background-image: url('image.jpg');
  background-image: image-set(url('image.avif') type('image/avif'), url('image.jpg') type('image/jpeg'));
}
```

IE는 [`image-set`](https://caniuse.com/css-image-set)을 지원하지 않기에 첫 라인의 `image.jpg`가 적용이 될 것이다.
반면, 최신 브라우저는 가장 나중에 정의된 구문으로 `image.avif`가 적용된다.
