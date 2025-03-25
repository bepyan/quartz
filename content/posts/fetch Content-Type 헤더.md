---
title: fetch Content-Type 헤더
date: 2025-03-25
tags:
  - seed
---

Content-Type 헤더는 HTTP 메시지(요청이나 응답)에서 보내는 **콘텐츠의 형식(MIME type)** 을 나타내는 헤더이다.
  
즉, **내가 보내는 데이터가 어떤 타입인지** 서버나 클라이언트에게 알려주는 역할을 한다.

보통 보내는 데이터가 JSON 형태일 때 아래와 같이 명시하면 된다.

```js
fetch('/api/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ name: '홍길동' })
});
```

## 역사

**🕒 초기 웹 환경 (~1990년대)**

최초의 HTTP 프로토콜(RFC 1945, HTTP/1.0)부터 이미 존재하던 개념이다.
서버가 클라이언트에게 보내는 데이터의 형식을 알려주는 필수 헤더였다.

```
Content-Type: text/html
Content-Type: image/jpeg
```

**🕒 AJAX 시대 (2000년대 초반~2010년대)**

클라이언트가 서버에 보내는 요청에서도 **내가 보내는 데이터가 어떤 형태인지** 알릴 필요가 있었다.
폼 데이터를 보낼 때 `application/x-www-form-urlencoded`을 흔히 쓰였다.

```
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

파일 업로드를 위해선 multipart 요청을 보내야 하기 때문에 `multipart/form-data`를 사용하게 된다. 평문 데이터의 경우에는 `text/plain`을 사용한다.

```
Content-Type: multipart/form-data
Content-Type: text/plain
```

JSON이 점점 인기를 얻으면서 다음과 같은 형태가 추가되었다.

```
xhr.setRequestHeader('Content-Type', 'application/json');
```

**🕒 REST API & Fetch API (2015년~현재)**

REST API는 JSON 포맷을 표준으로 널리 활용하면서 Content-Type: application/json이 사실상 표준처럼 자리 잡았다.

```js
fetch('/api/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ username: '홍길동' })
});
```

## 만약 지정을 하지 않게 된다면?

만약 Content-Type을 지정하지 않고 데이터를 보낼 때, 브라우저에서 자동으로 설정한다.

텍스트일 경우 헤더가 생략되며, 서버에서 이를 어떻게 처리할지 결정할 수 있다.
이 경우 서버에서 보통 400 Bad Request 에러를 반환한다.

FormData일 경우 브라우저가 자동으로 `multipart/form-data`를 설정해준다.
오히려 직접 명시하면 **boundary**값이 없어져서 문제가 생길 수 있어서 생략하고전송하게 된다.

## vs Accept 헤더

[[fetch Accept 헤더]]

**내가 데이터를 보낼 때** → Content-Type
**내가 데이터를 받을 때** → Accept

