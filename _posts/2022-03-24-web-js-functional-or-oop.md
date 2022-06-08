---
layout: post
title: "[Web] js는 함수형 언어인가, 객체지향형 언어인가?"
categories: Web
---

## JS에서의 객체지향형 프로그래밍
자바스크립트에서 객체를 정의하는 방법은 매우 많은데 그중 function 키워드를 이용한 객체 정의 방법이 있다.  
주의할 점은 function 키워드를 이용한다 해도 function이 아니라는 것이다.

- JS에서의 OOP
  - 객체 선언
  - 객체 상속
  - 프로토타입 사용
 
 ```javascript
function Car() {
  this.power = false;
  this.position = 0;
}
 
Car.prototype.start = function() {
  this.power = true;
  console.log('자동차 시동');
}

Car.prototype.moveTo = function(position) {
  console.log(`자동차 이동 = 현재 위치: {${this.position}}`);
  if (!this.power) {
    console.log('자동차의 시동이 꺼져있습니다.');
    return;
  }
  this.position = position;
  console.log(`자동차 이동 = 이동 위치: {${this.position}}`);
}

const car = new Car();
car.start();
car.moveTo(10);

 ```
> 예제 코드는 Javascript에서 지원하는 prototype을 이용해서 객체를 정의하고 사용하는 내용입니다.  
> 결과적으로 객체지향 프로그래밍은 객체를 정의(변수와 메서드)하고 객체를 생성해서 만들어진 객체를 사용하는 것을 의미합니다.

> ES6에서 JS의 클래스 내용이 추가되었습니다. ES6 문법을 통해, 이제는 프로토타입을 사용하지 않고도 클래스 선언 및 사용이 가능합니다.

## JS에서의 함수형 프로그래밍
- JS에서의 객체는 1급 객체

```javascript
function start(car) {
  car.power = true;
  console.log('자동차 시동');
}

function moveTo(car, position) {
  console.log(`자동차 이동 = 현재 위치: {${car.position}}`);
  if (!car.power) {
    console.log('자동차의 시동이 꺼져있습니다.');
    return;
  }
  car.position += position;
  console.log(`자동차 이동 = 이동 위치: {${car.position}}`);
}

const car = { power: false, position: 0 };
start(car);
moveTo(car, 10);
```

> 객체지향에서 제시했던 예제 코드와 달리 객체가 가진 기능을 사용하지 않고 오롯이 함수를 정의하고 함수를 조합함으로써 결과를 만들어냈음을 알 수 있습니다.  
> Car는 정의하지 않고 JSON 값과 함수를 정의하고 사용할 뿐입니다.

## 객체지향형 vs 함수형
- 객체지향은 객체 안에 상태를 저장하고, 이 상태를 이용해 메소드를 추가하고, 상태변화를 설정하고 조정하기위해 다양한 기능을 사용한다.
- 이에 반해 함수형은 상태를 제어하는 것보다 상태를 저장하지 않고 없애는데에 포인트를 쥐고 있다. 그래서 함수형은 간결한 프로그래밍에 더 적합하다.

```javascript
// 객체지향 프로그래밍
car.start();
car.moveTo(10);

// 함수형 프로그래밍
start(car);
moveTo(car, 10);
```

## 자바스크립트는 객체지향? 함수형?
- 자바스크립트는 여러가지 스타일로 프로그래밍이 가능한 멀티 패러다임 언어(multiparadigm programming language) 이다.
- 명령형 프로그래밍(함수형에 속한)도 가능하고 ,객체지향도 가능하다.
- 하지만 함수형 프로그래밍의 중요한 개념인 순수함수를 완벽하게 표현(?)을 할 수 없다.

## 참고자료 출처
- [[javascript] 함수형 프로그래밍 과 자바스크립트와 객체지향](https://koras02.tistory.com/98)
- [Javascript - 객체지향 프로그래밍과 함수형 프로그래밍의 차이](https://7942yongdae.tistory.com/156)
