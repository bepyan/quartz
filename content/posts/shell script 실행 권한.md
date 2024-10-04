---
title: shell script 실행 권한
date: 2024-07-23
tags:
  - seed
---

특정 파일 권한
```
chmod +x .kode/jira/test.sh
```

디랙토리 권한
```
chmod -R 777 example_folder
chmod -R 111 .kode/jira
```

각 비트는 읽기(4), 쓰기(2), 실행(1) 권한을 나타낸다.
7 = 4 + 2 + 1, 즉 모든 권한이 부여됨을 의미한다.
