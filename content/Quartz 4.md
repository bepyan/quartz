---
title: Quartz 4
date: 2024-08-05
tags:
  - seed
---

옵시디언 타겟 오픈소스 블로그 템플릿이다.
https://quartz.jzhao.xyz/

웹에서 [digital gardens](https://jzhao.xyz/posts/networked-thought) 을 만들고자하는 철학이 감명이 깊었다.
- 상호 연결된 아이디어와 생각의 네트워크
- 정돈된 파일 캐비닛이나 색인이 아니라, 엉켜 있는 성장의 집합체
옵시디언 **제2의 뇌**의 철학과 대이상동하다.

[해커뉴스](https://news.hada.io/topic?id=16070)에서 [옵시디언 노트 작성 워크플로우](https://www.ssp.sh/brain/public-second-brain-with-quartz/)를 소개해주는 글로 접하게 되었다.

공식문서에 들어가자마자 나는 곧장 매료되었다.
- 옵시디언의 그래프가 그대로 연동 됨
- 링크에 hover시 페이지 Preview가 뜸
- 완성도가 높은 디자인 시스템
- 빠른 페이지 라우팅
- ...
오픈소스 주인장이신 [jzhao](https://github.com/jackyzha0)는 정말이지 찐 개발자이다.

```
                                                                                ## #
                         ^                             ^                       # #                      
      ^    ^            /|\            ^    ^         /|\ ^                   ##         ^              
  ^  /|\  /|\  ^        /|\  ^     ^  /|\  /|\  ^     /|\/|\    ^          __||         /|\ ^    ^   ^ 
 /|\ /|\  /|\ /|\       /|\ /|\   /|\ /|\  /|\ /|\    /|\/|\   /|\        /.\__\        /|\/|\  /|\ /|\
 .|  #|.. .|& /|\        | #&|.   .|  #|.. .|& /|\     | #|.   /|\        |O | |        .| #|.. .|& /|\
```

기술 스택을 정리해보면, `preact` + `spa router` + `esbuild` + `sass` + `shiki` 로 정적 웹사이트를 만드는 것이다. 다른 말로 디테일한 동작은 모두 자체 구현했다는 것이다. 블로그 제작에 몸 좀 담궈본 사람으로서 존경심을 갖지 않을 수 없었다.

참지 못하고 바로 레포 만들어서 도메인까지 연동을 해버렸다.

옵시디언 플러그인
- Note Folder Autorename
- 노트와 이미지를 폴더로 자동 정리
- Remember cursor position

[[Quartz 4 custom]]
