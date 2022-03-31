---
layout: post
title: "[Web] Closer란?"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## Closer란?
> 클로저는 주변의 상태 (lexical environment)의 참조와 함께 번들로 묶인 함수의 조합입니다.  
> 즉, 클로져는 우리에게 inner함수에서 outer함수의 스코프에 접근을 가능하게 해줍니다. 자바스크립트에서 클로저는 함수가 생성될 때마다 생성됩니다.

간단히 말하자면 함수가 선언될 때(실행X) 외부의 lexcial environment를 참조?하게 되는 현상?이다.  

함수의 실행컨텍스트를 간단히 알고 이해해야한다.   
함수는 호출 될 때 함수의 실행컨텍스트가 생성됐다가 실행이 끝나면 실행컨텍스트가 종료된다. (힘수의 실행 컨텍스트가 생성될 때 함수의 lexical environment도 생성된다.) 이 실행컨텍스트의 lexical environment에는 함수의 지역변수의 정보& 이 함수의 상위 스코프의 대한 정보가 들어있다.

## Closer의 예시
```javascript
function outer(){
  const name = 'kyle';
  console.log(name)
  return function inner(){
    const greeting = 'hello!'
    console.log(greeting,name)
  }
}

const getKyle = outer() //kyle 
getKyle() //hello!kyle
```
outer 함수가 위와 같이 종료됐다.  
우리의 예상대로라면, outer함수가 종료 됐으니 name은 아무데서도 접근할 수 없다!  
하지만 inner함수에서 접근 가능하다. 이것이 바로 closer이다.

> 클로져의 특성상 inner함수가 선언될 때 그 주변의 lexical enviroment(여기서는 outer의 lexical enviroment)와 함께 번들로 묶였기 때문이다!  
그렇기 때문에 inner가 실행이 되어서 lexical environment를 만든 뒤 참조 하지 않아도, 선언할 때 이미 묶여버리게 된다.  
> 때문에 변수 name을 사용할 수 있게 된다.


## Closer를 사용하는 이유
### 1. 전역변수를 줄일 수 있다.
전역변수가 많으면 어디에서든 실수로라도 접근을 할 수 있기 때문에 최대한 전역변수를 줄여서 코드를 해야합니다.  
하지만 프로그램을 구현하다보면 이 함수 하나에서만 사용하는데 전역변수가 필요한 순간이 있죠. 이럴 때 클로저가 유용하게 사용됩니다.  

예를들어 클릭할 때 마다 count를 세주는 함수가 있다고 생각해봅시다.
```javascript
const btn = document.querySelector('button')

btn.addEventListener('click',handleClick)

let count = 0
function handleCilck(){
  count++
  return count
}
```
위와 같은 경우에 count를 전역변수로 사용해줘야 count가 증가를 해줄 수 있습니다.
이럴경우 클로져를 사용해서 해결할 수 있습니다.

```javascript
const btn = document.querySelector('button')

btn.addEventListener('click',handleClick())

function handleCilck(){
  let count = 0
  return function (){
    count++
    return count
  }
}
```
위와 같이 작성해 준다면 외부함수(handleClick)의 lexical environment를 참조하는 함수를 btn의 콜백함수로 이용해 전역객체 없이 구현할 수 있습니다.

### 2. 비슷한 형태의 코드를 재사용률을 높일 수 있습니다.
말 만으로는 무슨 뜻인지 이해가 잘 안갈 수 있습니다.   
아래 코드를 보면서 이해해보겠습니다.
```javascript
const newTag = function(open, close) {
    return function(content) {
        return open + content + close
    }
}

const bold = newTag('<b>', '</b>')
const italic = newTag('<i>', '</i>')

console.log(bold(italic("This is my content!")))
//<b><i>This is my content!</i></b>
```
코드를 보면 bold,itealic 등등의 새로운 태그를 만들 수 있는 함수 newTag를 클로져를 이용해 간단하게 구현했습니다.
인자에 open,close,content를 한번에 다 받는다면,This is my content! 와 같은 값을 출력을 하고 싶을 때 가독성이 떨어질 수 있습니다.

하지만 클로져로 구현하면 코드의 가독성도 좋은 재사용하기 편한 코드를 구현할 수 있습니다.


## Closer를 사용하며 주의해야할 점
### 착각하기 쉬운 Closer
아래의 코드가 클로저인지 생각해보자
```javascript
function outer() {
  let name = 'kyle';
  if (true) {
    let city = 'seoul';
    return function inner() {
      console.log(city);
    };
  }
}
```
클로저를 정확하게 파악하지 않았을 때 위와 같은 코드를 클로저라고 착각할 수 있다. 마치 함수를 리턴하는 것 자체가 클로저라고 오해하는 경우가 생길 수 있다.

![image](https://user-images.githubusercontent.com/28949166/161071052-cebd2f97-de29-4f0e-86a4-bae1adb3c82a.png)

하지만 위의 코드의 스코프를 보면 그렇지 않다는 것을 알 수 있다.

그렇다. 클로저는 내부에 선언된 함수가 외부함수의 지역변수를 사용해 줬을 때만 클로저라고 선언된다.
inner 함수에도 클로저를 사용하고 싶으면 name변수를 사용해주면 된다.
```javascript
function outer() {
  let name = 'kyle';
  if (true) {
    let city = 'seoul';
    return function inner() {
      console.log(city);
     console.log(name);
    };
  }
}
```
![image](https://user-images.githubusercontent.com/28949166/161071178-144a535d-a2f3-431f-aaf8-b9292f6f0981.png)

> 클로저란 내부함수에서 외부함수의 지역변수를 사용할 때 외부함수의 lexcial environment와 함께 bundled 되는 것?(mdn에서는 combination이라고 표현했다.) 이라고 생각하면 될 것이다.


## 참고자료 출처

- [[JS]클로져(closure)와 클로져의 사용 예제](https://velog.io/@proshy/JS%ED%81%B4%EB%A1%9C%EC%A0%B8closure%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%B8%EC%9D%98-%EC%82%AC%EC%9A%A9-%EC%98%88%EC%A0%9C){:target="\_blank"}
