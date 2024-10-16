---
title: 브라우저 timezone 테스트하는 방법
date: 2024-10-16
tags:
  - seed
---

브라우저에서 [[KST 시간 변환]] 같은 i18n 작업을 진행하면 관련 테스트를 잘 수행해야 한다.

크롬 개발자 도구(DevTools)를 통해서 브라우저의 timezone을 설정할 수 있다.
https://www.browserstack.com/guide/change-time-zone-in-chrome-for-testing

### 1. 개발자 도구에서 콘솔탭으로 이동한다.

### 2. 우상단에 세로 `...` > `More tools` > `Sensors`를 클릭한다.

![](https://browserstack.wpenginepowered.com/wp-content/uploads/2021/11/Devtools-bs.png)

### 3. 콘솔창 하단 `Sensor` 탭에서 시간대를 설정한다.

![](https://browserstack.wpenginepowered.com/wp-content/uploads/2021/11/Sensor-timezone.png)
