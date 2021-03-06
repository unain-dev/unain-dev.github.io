---
layout: post
title: "[JS] Hoisting"
# date: 2021-12-10 12:34:43 +0900
categories: JS
---

## Hoisting
- 정의
  - 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것

## Hoisting 대상
- var 변수 선언과 함수선언문에서만 호이스팅이 일어난다.
  - var 변수/함수의 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.
  - let/const 변수 선언과 함수표현식에서는 호이스팅이 발생하지 않는다.
### 함수 선언문과 함수 표현식에서의 호이스팅
- 함수 선언문에서의 호이스팅
  - 함수선언문은 코드를 구현한 위치와 관계없이 자바스크립트의 특징인 호이스팅에 따라 브라우저가 자바스크립트를 해석할 때 맨 위로 끌어 올려진다.
- 함수 표현식에서의 호이스팅
  - 함수표현식은 함수선언문과 달리 선언과 호출 순서에 따라서 정상적으로 함수가 실행되지 않을 수 있다.

## 참고자료 출처
- [호이스팅(Hoisting)이란](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html){:target="\_blank"}
