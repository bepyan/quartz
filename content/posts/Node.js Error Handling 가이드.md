---
title: Node.js Error Handling 가이드
date: 2024-11-21
tags:
  - seed
---

노드 런타임에는 여러 에러타입이 있다.
타입에 따라 특정 동작을 수행을 해야 하는데, 기본 `Error` 객체를 확장해야 한다.

## HTTP Error

기본적으로 HTTP Error가 있다.

```ts
export class HTTPError extends Error {
  constructor(
    public status: number,
    public message: string,
    public code?: string,
  ) {
    super(message);
    this.status = status;
    this.name = 'HTTPError';
    // constructor code won't show up in the stack trace in V8
    Error.captureStackTrace?.(this, this.constructor);
  }
}
```

요청에 대한 에러 응답 포멧이 있으니, mdn을 참고해보면 된다.
https://developer.mozilla.org/ko/docs/Web/HTTP/Status/500

```ts
export class RequestError extends HTTPError {
  constructor(message: string = '요청 오류', code: string = 'B_REQUEST_ERROR') {
    super(400, message, code);
    this.name = 'RequestError';
    Error.captureStackTrace?.(this, this.constructor);
  }
}

export class AuthError extends HTTPError {
  constructor(message: string = '인증 오류', code: string = 'B_AUTH_ERROR') {
    super(401, message, code);
    this.name = 'AuthError';
    Error.captureStackTrace?.(this, this.constructor);
  }
}

export class ForbiddenError extends HTTPError {
  constructor(message: string = '권한 오류', code: string = 'B_FORBIDDEN') {
    super(403, message, code);
    this.name = 'ForbiddenError';
    Error.captureStackTrace?.(this, this.constructor);
  }
}

export class NotFoundError extends HTTPError {
  constructor(message: string = '리소스 오류', code: string = 'B_NOT_FOUND') {
    super(404, message, code);
    this.name = 'NotFoundError';
    Error.captureStackTrace?.(this, this.constructor);
  }
}

export class InternalError extends HTTPError {
  constructor(message: string = '서버 오류', code: string = 'B_INTERNAL_ERROR') {
    super(500, message, code);
    this.name = 'InternalError';
    Error.captureStackTrace?.(this, this.constructor);
  }
}
```

에러 타입을 확인하는 유틸도 작성해줘도 좋다.

```ts
export function isHTTPError(error: unknown): error is HTTPError {
  return error instanceof HTTPError;
}

export function isRequestError(error: unknown): error is RequestError {
  return error instanceof RequestError;
}

export function isAuthError(error: unknown): error is AuthError {
  return error instanceof AuthError;
}

export function isForbiddenError(error: unknown): error is AuthError {
  return error instanceof ForbiddenError;
}

export function isNotFoundError(error: unknown): error is NotFoundError {
  return error instanceof NotFoundError;
}

export function isInternalError(error: unknown): error is InternalError {
  return error instanceof InternalError;
}
```

그럼 우리가 정의한 에러 클래스를 통해 쉽게 에러 라우팅을 할 수 있다.

```ts
try {
    // 요청 처리
    return await next();
} catch (error: unknown) {
    if (!isHTTPError(error)) {
      console.error(error);
      // ... sentry logging
      return context.rewrite('/500');
    }

    if (isRequestError(error)) {
      return context.rewrite('/500');
    }

    if (isAuthError(error)) {
      return context.rewrite('/401');
    }

    if (isForbiddenError(error)) {
      return context.rewrite('/403');
    }

    if (isNotFoundError(error)) {
      return context.rewrite('/404');
    }

    return context.rewrite('/500');
}
```

서버 로직에서는 이렇게 throw하기만 하면 된다.

```ts
throw new RequestError('[TEST] 400 Error');
```


## 참고

https://thecodersblog.com/practices-extending-error-javascript-enhancing-error-handling?t
https://adamcoster.com/blog/javascript-custom-errors?t
https://javascript.info/custom-errors?t
https://nodejs.org/docs/latest-v22.x/api/errors.html
https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-%EC%A0%84%EB%AC%B8%EA%B0%80%EC%B2%98%EB%9F%BC-%EC%97%90%EB%9F%AC-%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0-39d14f5cc6a2