---
title: (bash) 터미널 echo에 색상을 넣기
date: 2023-12-18
tags:
  - seed
---

## 폰트 색상 적용

```bash
echo "\u001b[1;31m Hello \u001b[0m"
```

`31m`의 `1`부분을 아래 코드로 수정할 수 있다.

```bash
0 - black
1 - red
2 - green
3 - yellow
4 - blue
5 - magenta
6 - cyan
7 - white
```

## 배경 적용

```bash
echo "\u001b[1;42;1;37m   *** PHOCUS ***   \u001b[0m"
```

```
Code:
0 - normal
1 - bold
2 - normal again
3 - background color
4 - underline the text
5 - blinking

You can also specify both a foreground and a background color.

Code:
```

https://gist.github.com/mauriciopazpp/6a01f015c7598b6eb4ce367cc7d590bc
