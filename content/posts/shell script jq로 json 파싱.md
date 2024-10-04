---
title: shell script jq로 json 파싱
date: 2024-07-24
tags:
  - seed
  - snippet
---

https://jqlang.github.io/jq/
```shell
brew install jq
```

통신 코드 참고
```shell
request() {
    local method="$1"
    local endpoint="$2"
    local access_token="$3"
    local data="$4"
    local curl_cmd="curl -s -w '\n%{http_code}' -X $method"
    if [ -n "$access_token" ]; then
      curl_cmd="$curl_cmd -H \"Authorization: Bearer $access_token\""
    fi
    curl_cmd="$curl_cmd -H \"Content-Type: application/json\""
    if [ -n "$data" ]; then
        curl_cmd="$curl_cmd --data '$data'"
    fi
    curl_cmd="$curl_cmd \"$endpoint\""

    echo "✧ req: [$method] $endpoint $data"

    local response
    response=$(eval "$curl_cmd")
    local curl_exit_code=$?

    if [ $curl_exit_code -ne 0 ]; then
        echo "❌ curl 명령 실행 실패. 종료 코드: $curl_exit_code" >&2
        return $curl_exit_code
    fi

    local http_code
    http_code=$(echo "$response" | tail -n1)
    local response_body
    response_body=$(echo "$response" | sed '$d')
    echo "✦ res: [$http_code]"
    echo "$response_body"

    if [[ ! $http_code =~ ^2[0-9]{2}$ ]]; then
        echo "❌ API 요청 실패. HTTP 상태 코드: $http_code" >&2
        return "$http_code"
    fi

    return 0
}
```


```shell
res=$(request "...")
json_data=$(echo "$res" | sed '1,2d')
```

```shell
milestone_title=$(echo "$json_data" | jq -r '.milestone.title // empty')
```

`-r`
- 의미: "raw output"의 약자입니다.
- 기능: 이 옵션은 출력 결과에서 따옴표를 제거합니다. 문자열 값을 반환할 때 따옴표 없이 순수한 텍스트로 출력합니다.
- 사용 이유: 추출된 값을 변수에 할당할 때 따옴표 없이 깔끔한 문자열을 얻기 위해 사용됩니다.

`.milestone.title`
- 의미: JSON 객체에서 milestone 객체의 title 필드를 선택합니다.
- 기능: 중첩된 객체 구조에서 특정 필드를 추출합니다.

`// empty`
- 의미: "null 병합 연산자"라고 불리는 `jq`의 특별한 구문입니다.
- 기능: 만약 `.milestone.title`이 `null`이거나 존재하지 않는 경우, `empty`를 반환합니다.
- 사용 이유:
    - `milestone` 필드가 없거나 `null`일 경우 오류 대신 빈 문자열을 반환합니다.
    - 이는 스크립트의 안정성을 높이고, `milestone`이 설정되지 않은 경우를 우아하게 처리합니다.
