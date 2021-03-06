---
layout: post
title: "[JS] var vs let vs const"
# date: 2021-12-10 12:34:43 +0900
categories: Web JS
---

## 변수 선언
- var
  - var 키워드를 이용한 변수 선언은 선언 단계와 초기화 단계가 동시에 진행되어, var에 암묵적으로 undefined를 할당해 초기화한다.
  - 즉, 선언만 해도 자동으로 undefined로 초기화 된다.
  - 호이스팅의 대상이 됨.
- const, let
  - 선언 단계와 초기화 단계가 분리되어 진행된다.
  - 호이스팅의 대상이 되지 않는다. -> 호이스팅으로 인한 혼란을 방지.

## var의 문제점
1. 변수 중복 선언 가능하여, 예기치 못한 값을 반환할 수 있다.
2. 함수 레벨 스코프로 인해 함수 외부에서 선언한 변수는 모두 전역 변수로 된다.
3. 변수 선언문 이전에 변수를 참조하면 언제나 undefined를 반환한다.
> 이러한 단점을 보완하기 위해 ES6에서 const, let이 등장했다.

## 새로운 const, let의 등장
1. 변수 호이스팅
  - let : let 키워드로는 변수 중복 선언이 불가하지만, 재할당은 가능하다
  - const : const가 let과 다른 점이 있다면, 반드시 선언과 초기화를 동시에 진행되어야 한다.
    > const도 let과 마찬가지로 재선언이 불가하며, 더 나아가 재할당도 불가하다. 재할당의 경우, 원시 값은 불가능하지만, 객체는 가능하다. const 키워드는 재할당을 금지할 뿐, ‘불변’을 의미하지 않는다.
2. 블록 레벨 스코프
  - let, const 키워드로 선언한 변수는 모두 코드 블록(ex. 함수, if, for, while, try/catch 문 등)을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.
3. 변수 호이스팅
  - let : 선언 단계와 초기화 단계가 분리되어 진행
    >  즉, 런타임 이전에 자바스크립트 엔진에 의해 선언 단계가 먼저 실행되지만, 초기화 단계가 실행되지 않았을 때 해당 변수에 접근하려고 하면 참조 에러가 뜬다.
    >  따라서 let 키워드로 선언한 변수는 스코프의 시작 지점부터 초기화 단계 시작 지점까지 변수를 참조할 수 없는 일시적 사각지대(Temporal Dead Zone: TDZ) 구간에 존재한다.
  - const : 선언 단계와 초기화 단계가 동시에 진행
    > let 키워드로 선언한 경우, 런타임 이전에 선언이 되어 자바스크립트 엔진에 이미 존재하지만 초기화가 되지 않았기 때문에 name is not defined라는 문구가 떴다. 하지만 const 키워드로 선언한 경우, 선언과 초기화가 동시에 이루어져야 하지만 런타임 이전에는 실행될 수 없다. 따라서 초기화가 진행되지 않은 상태이기 때문에 Cannot access 'name' before initialization 에러 문구가 뜬다.

## 참고자료 출처
- [호이스팅(Hoisting)이란](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html){:target="\_blank"}
