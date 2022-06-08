---
layout: post
title: "[Web] 화면 렌더링 속도를 향상 시킬 수 있는 방법"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## 화면 렌터더링 속도를 향상 시킬 수 있는 방법
### 1. 트리 쉐이킹
트리 쉐이킹이란, 나무를 흔들면 몇 몇 가지들이 떨어지는 것 처럼, 외부 모듈에서 필요한 기능들만 import 하는 것을 의미한다.  
- 예시 : 거대한 lodash 파일을 한번에 import 시켜오는 것 보다, lodash의 일정 기능만 import 해오는 것이 파일 용량이 작아져 렌더링 속도를 빠르게 할 수 있다.
  ```javascript
   import _ from "lodash" // :( BAD
   import array from "lodash/array" // :) GOOD
  ```

### 2. 이미지 용량 조절
이미지의 경우, png -> jpg -> jpeg의 순서로 용량이 작으므로, 이미지 용량을 작게 하면 렌더링 속도를 향상 시킬 수 있다.

### 3. 애니메이션 mp4, video 태그 사용
애니메이션이 적용 된 경우, gif 보다 video 태그에서 mp4를 사용하면 적은 용량의 리소스를 요청 할 수 있다.

### 4. 모듈 번들러로 css와 js 번들링 하기
webpack과 같은 모듈 번들러로 여러 개의 js 파일을 하나의 파일로 번들링 할 수 있다.

### 5. CSS에서, 복잡한 셀렉터 지양하기


## 참고자료 출처
- [[프론트엔드] 성능 최적화 정리](https://coffeeandcakeandnewjeong.tistory.com/34){:target="\_blank"}
