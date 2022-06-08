---
layout: post
title: "[JS] 이벤트 루프(Event Loop)"
# date: 2021-12-10 12:34:43 +0900
categories: JS
---

![image](https://user-images.githubusercontent.com/28949166/159767964-f8d962f8-331f-4246-8c3d-c70a4d5baede.png)

## JS Engine
자바스크립트 엔진은 Memory Heap 과 Call Stack 으로 구성되어 있다.(그림 왼쪽!)  
가장 유명한 것이 구글의 V8 Engine이다.  
자바스크립트는 단일 스레드 (sigle thread) 프로그래밍 언어인데,  
이 의미는 Call Stack이 하나 라는 이야기이다.  
(멀티가 되지 않고, 하나씩 하나씩 처리한다는 의미!)


### Memory Heap : 메모리 할당이 일어나는 곳
(ex, 우리가 프로그램에 선언한 변수, 함수 등이 담겨져 있음)  
Call Stack : 코드가 실행될 때 쌓이는 곳. stack 형태로 쌓임.  
Stack(스택) : 자료구조 중 하나, 선입후출(LIFO, Last In First Out)의 룰을 따른다.  
### Web API
그림의 오른쪽에 있는 Wep API는 JS Engine의 밖에 그려져 있다.  
즉, 자바스크립트 엔진이 아니다.  
Web API 는 브라우저에서 제공하는 API 로, DOM, Ajax, Timeout 등이 있다.  
Call Stack에서 실행된 비동기 함수는 Web API를 호출하고,  
Web API는 콜백함수를 Callback Queue에 밀어 넣는다.  

## Callback Queue
비동기적으로 실행된 콜백함수가 보관 되는 영역이다.  
예를 들어 setTimeout에서 타이머 완료 후 실행되는 함수(1st 인자),  
addEventListener에서 click 이벤트가 발생했을 때 실행되는 함수(2nd 인자) 등이 보관된다.  
Queue(큐) : 자료 구조 중 하나, 선입선출(FIFO, Frist In Frist OUT)의 룰을 따른다.  

## Event Loop
Event Loop는 Call Stack과 Callback Queue의 상태를 체크하여,  
Call Stack이 빈 상태가 되면, Callback Queue의 첫번째 콜백을 Call Stack으로 밀어넣는다.  
이러한 반복적인 행동을 틱(tick) 이라 부른다.  


> 정리하면,  
V8 엔진에서 코드가 실행되면, Call Stack에 쌓인다.  
Stack의 선입후출의 룰에 따라 제일 마지막에 들어온 함수가 먼저 실행되며,  
Stack에 쌓여진 함수가 모두 실행된다.  
비동기함수가 실행된다면, Web API가 호출된다.  
Web API는 비동기함수의 콜백함수를 Callback Queue에 밀어넣는다.  
Event Loop는 Call Stack이 빈 상태가 되면  
Callback Queue에 있는 첫번째 콜백을 Call Stack으로 이동시킨다.  
(이러한 반복적인 행동을 틱(tick)이라 한다.)  
자바스크립트를 단일 스레드 프로그래밍 언어라 한번에 하나씩 밖에 실행할 수 없다.  
그러나 Web API, Callback Queue, Event Loop 덕분에 멀티 스레드 처럼 보여진다.   
>

## 참고자료 및 출처
- [Event Loop (이벤트 루프)](https://velog.io/@thms200/Event-Loop-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84)
