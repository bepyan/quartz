---
title: bun에서 쉽게 package 업데이트하는 방법
date: 2024-11-12
tags:
  - seed
---

Node.js 생태계의 새로운 런타임이자 패키지 매니저인 Bun을 사용할 때 프로젝트의 의존성을 업데이트하는 방법은 여러 가지가 있다. 오늘은 가장 많이 사용되는 세 가지 방법을 알아보았다.

## bun update

가장 기본적인 방법은 Bun의 내장 명령어를 사용하는 것이다.

```shell
bun update
```

이 명령어는 `package.json`의 의존성을 현재 버전 규칙에 맞춰 최신 버전으로 업데이트한다.

원래 `package.json`에 반영이 안되는 버그가 있었으나 해결이 되었다.
https://github.com/oven-sh/bun/issues/4312

## npm-check-updates

더 세밀한 제어가 필요할 때는 `npm-check-updates`를 사용할 수 있다.

```shell
bunx npm-check-updates -ui 
```

또는 긴 형식으로,

```shell
bunx npm-check-updates --upgrade --interactive
```

이 도구는 대화형 인터페이스를 제공하여, 업데이트하고 싶은 패키지를 선택적으로 골라서 업데이트할 수 있다.

## taze

[`taze`](https://github.com/antfu-collective/taze)는 Anthony Fu가 만든 도구로, 간단하면서도 강력한 기능을 제공한다. 특히 모노레포 환경에서의 의존성 관리를 효율적으로 할 수 있게 해준다.

```shell
bunx taze
```

패키지를 바로 설치하고 싶다면 `-w` 플래그를 추가하면 된다.

모노레포 프로젝트의 경우 `-r` 플래그를 사용하여 모든 하위 패키지를 재귀적으로 업데이트할 수 있다.

```shell
bunx taze -r
```

디폴트로 마이너 버전(0.x) 업데이트를 진행하나 만약 메이저 버전(x.x) 업데이트 하려면 아래 명령어를 실행하면 된다.

```shell
bunx taze major
```