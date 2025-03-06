---
title: Swagger Specification
date: 2025-02-27
tags:
  - seed
---

Swagger는 REST API를 설계, 구축, 문서화, 사용하기 위한 도구 모음과 명세 형식이다. 
현재 OpenAPI 명세를 지원하는 도구 브랜드명으로 사용되었다.

## 역사

2010년 [Wordnik](https://en.wikipedia.org/wiki/Wordnik)에서 API 문서화 문제를 해결하기 위해 개발되었다. 2.0 버전에서 널리 채택되며 사실상의 API 표준으로 자리를 차지했다.

2015년 SmartBear가 인수 후, Linux Foundation에 기부하여 OpenAPI Specification으로 이름 변경되었다.

2017년에 OpenAPI 3.0이 출시되었다.

현재는 대부분의 경우 OpenAPI 3.0+를 사용하지만, 여전히 "Swagger"라는 용어가 도구와 명세를 지칭하는 데 통용되고 있다. Swagger 도구들은 계속해서 발전하며 현대 API 개발 워크플로우의 핵심 부분으로 남아있다.

## 명세

```
swagger: "2.0"
info:
  title: "샘플 API"
  version: "1.0.0"
host: "api.example.com"
basePath: "/v1"
schemes:
  - "https"
paths:
  /users:
    get:
      summary: "사용자 목록 조회"
      produces:
        - "application/json"
      responses:
        200:
          description: "성공적인 응답"
          schema:
            type: "array"
            items:
              $ref: "#/definitions/User"
definitions:
  User:
    type: "object"
    properties:
      id:
        type: "integer"
      name:
        type: "string"
```

## Swagger 도구 생태계

Swagger Editor: 명세를 작성하고 실시간으로 검증하는 에디터
Swagger UI: API 문서를 자동으로 생성하고 테스트할 수 있는 인터페이스
Swagger Codegen: 명세로부터 클라이언트 및 서버 코드 자동 생성
Swagger Inspector: API 테스트 도구

