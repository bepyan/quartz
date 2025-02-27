---
title: OpenAPI 3.0 vs 2.0(Swagger)
date: 2025-02-27
tags:
  - seed
---

기존 명칭을 [[Swagger Specification]]에서 [[Open API Specification (OAS)]]으로 변경되었다.

이는 SmartBear가 Swagger를 인수하여 Linux Foundation에 기부하면서 대대적인 업데이트와 함께 명칭을 바꿔줬다. 단일 기업 소유에서 오픈소스 커뮤니티 주도 표준으로 발전하고자하는 의미가 담겨져 있다.

## 구체적인 변경점

현대 API의 복잡한 요구사항를 수용하기 위해 스팩이 변경되었다.

- 업계 표준인 JSON Schema와의 호환성 강화
- 파편화된 구조(`definitions`, `parameters` 등)를 개선하기 위해 `components` 개념 도입
- `produces/consumes` 대신 더 유연한 `content` 객체 도입
- `oneOf`, `anyOf`, `allOf` 도입으로 복잡한 데이터 구조 표현 가능

```yaml
# 2.0
responses:
  200:
    description: "성공"
    schema:
      $ref: "#/definitions/User"

# 3.0
responses:
  200:
    description: "성공"
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/User"
```

## 마이그레이션

많은 조직이 2.0과 3.0을 병행 사용하는 과도기 경험하게 되었다.
근래에는 많은 자동화 도구가 나오면서 마이그레이션 복잡성이 해소되었다.

## 미래 방향성

- JSON Schema 완전 통합: 향후 버전에서 더 완벽한 JSON Schema 호환성 추구
- GraphQL과의 공존: REST와 GraphQL 간 상호운용성 향상
- 비동기 API 지원: 이벤트 기반 API를 위한 AsyncAPI와의 통합 가능성
