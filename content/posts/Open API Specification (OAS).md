---
title: OpenAPI
date: 2025-02-27
tags:
  - seed
---

## 개요

Open API Specification는 **RESTful API를 정의하고 문서화하기 위한 표준 명세**입니다. 

이전에는 [[Swagger Specification | Swagger]]라고 불렸으며, API의 엔드포인트, 요청 매개변수, 응답 형식 등을 JSON 또는 YAML 형식으로 기술합니다.

## 핵심 특징

**언어 독립적**
JSON 또는 YAML 형식으로 작성되어 어떤 프로그래밍 언어와도 호환

**표준화된 문서**
API 엔드포인트, 요청/응답 형식, 인증 방법 등을 일관된 방식으로 기술

**자동화 지원**
문서 생성, 클라이언트 코드 생성, 서버 스텁 생성 등 자동화 가능

## 기본 구조

```yaml
openapi: 3.0.0
info:
  title: Sample API
  description: API 설명
  version: 0.1.9
servers:
  - url: http://api.example.com/v1
    description: 프로덕션 서버
paths:
  /users:
    get:
      summary: 사용자 목록 반환
      responses:
        '200':
          description: 사용자 이름 배열
          content:
            application/json:
              schema:
                type: array
                items:
                  type: string
```

## 활용 사례

- 명확한 커뮤니케이션
	- 팀 간, 회사 간 API 이해를 위한 공통 언어 제공
- 개발 생산성 향상
	- 문서 자동화
	- 테스트 자동화
	- 도구 생태계
		- Swagger UI, ReDoc 등 다양한 도구와 통합


## 더 공부해보면 좋을 주제

[[OpenAPI 3.0 vs 2.0(Swagger)]]
[[OpenAPI Typescript]]

https://tech.kakaopay.com/post/openapi-documentation/
https://docs.tosspayments.com/resources/glossary/oas

https://www.speakeasy.com/openapi
https://www.speakeasy.com/openapi/frameworks/springboot

https://www.udemy.com/course/swagger-tools-openapi/?couponCode=ST10MT30325G1
https://product.kyobobook.co.kr/detail/S000211655004

