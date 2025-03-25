---
title: fetch header accept
date: 2025-03-25
tags:
  - seed
---

Accept 헤더는 HTTP 요청(Request)을 보낼 때 클라이언트가 **서버에게 받고자 하는 콘텐츠 타입**(MIME type)을 알려주는 역할을 한다.

가장 기본적으로는 JSON 형식의 응답을 받는다.

```js
fetch('https://example.com/api/users', {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
});
```

## 역사적 배경

**🕒 초기 웹의 등장 (~1990년대)**

당시 웹은 HTML 페이지가 중심이었지만, 이미지나 문서 등 다양한 콘텐츠를 제공하기 위해 클라이언트가 원하는 콘텐츠 형식을 명시적으로 서버에 전달할 필요가 있었다.

**🕒 REST API의 등장 (2000년대 초반~2010년대)**

서버가 하나의 URI를 통해 JSON, XML, HTML 등 여러 형식을 제공할 수 있게 되자 클라이언트가 원하는 포맷을 요청하는 방식으로 사용되었다.

**🕒 Fetch API의 등장과 활용 (2015년~현재)**

JavaScript의 Fetch API가 웹 표준으로 등장(2015년 이후, ES6 시대)하면서 Accept 헤더 사용이 더 쉬워졌다.

## 다양한 헤더

### 