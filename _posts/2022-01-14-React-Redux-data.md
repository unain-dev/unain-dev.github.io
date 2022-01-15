---
layout: post
title: "React Redux 기초"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## Redux 설치 패키지

- redux toolkit

  ```
  npm install @reduxjs/toolkit

  ```

- redux 보조 패키지
  ```
  npm install react-redux
  ```

## Redux 기초개념

![image](https://user-images.githubusercontent.com/28949166/149366231-1267a040-b385-4dde-a648-ded4bfd78f6c.png)

- [리액트 용어 정리](https://kyun2da.dev/%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/Redux-%EC%A0%95%EB%A6%AC/)
- Store : 전역으로 공유하는 상태의 저장소. 하나의 어플리케이션에는 하나의 sotre만 존재해야 한다.
- Action : 객체. 상태에 변화를 일으켜야할 때 이 action을 일으켜야한다.
- Action Creator : Action 객체를 만들어주는 함수.
- Reducer : 현재 상태와 액션 객체를 받아, 필요하다면 새로운 상태를 리턴하는 함수. 액션 유형을 기반으로 이벤트를 처리하는 이벤트 리스너.
- dispatch : Store의 내장함수. action 객체를 넘겨줘서 상태를 업데이트 할 수 있도록 함. 그리고 이 dispatch를 사용을 해서 store의 상태를 변경해야한다.(반드시! store에 직접 접근해 상태를 변경하면 안된다! - immutable)
  > vuex의 mutation.
- Subscribe : store의 내장함수. 리스너 함수를 파라미터로 넣어 호출하면 상태가 업데이트될 때마다 호출된다. 일종의 이벤트 리스너.
- Selector : store의 상태 값을 가져올 때 사용
  > vuex의 getter?

### ⭐ Redux 동작

![image](https://user-images.githubusercontent.com/28949166/149377508-71f09364-2356-4b5a-b239-7beb59a5190f.png)

- [Redux(리덕스)란? (상태 관리 라이브러리)](https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/)

1. user의 행동메 맞는 action 객체(정확하게는 action 객체를 리턴하는 action 생성함수)가 dispatch() 메소드에 전달된다.
2. dispatch(action)을 통해 reducer가 호출된다.
3. reducer는 새로운 store를 생성하여 저장한다(갈아끼운다.)

   ```javascript
   import { createStore } from "redux";

   /* 리덕스에서 관리 할 상태 정의 */
   const initialState = {
     counter: 0,
     text: "",
     list: [],
   };

   /_ 액션 타입 정의 _/;
   // 액션 타입은 주로 대문자로 작성합니다.
   const INCREASE = "INCREASE";
   const DECREASE = "DECREASE";

   /_ 액션 생성함수 정의 _/;
   // 액션 생성함수는 주로 camelCase 로 작성합니다.
   // 화살표 함수로 작성하는 것이 더욱 코드가 간단하기에,
   // 이렇게 쓰는 것을 추천합니다.
   // 2번.
   const increase = () => ({
     type: Increase,
   });
   const decrease = () => ({
     type: DECREASE,
   });

   /_ reducer 정의 _/;
   function reducer(state = initialState, action) {
     // state 의 초깃값을 initialState 로 지정했습니다.
     switch (action.type) {
       case INCREASE: // 3번.
         return {
           ...state,
           counter: state.counter + 1,
         };
       case DECREASE:
         return {
           ...state,
           counter: state.counter - 1,
         };
       default:
         return state;
     }
   }

   /_ 스토어 만들기 _/;
   const store = createStore(reducer);

   console.log(store.getState()); // 현재 store 안에 들어있는 상태를 조회합니다.

   // 스토어안에 들어있는 상태가 바뀔 때 마다 호출되는 listener 함수
   const listener = () => {
     const state = store.getState();
     console.log(state);
   };

   const unsubscribe = store.subscribe(listener);
   // 구독을 해제하고 싶을 때는 unsubscribe() 를 호출하면 됩니다.

   // 액션들을 디스패치 해봅시다.
   store.dispatch(increase()); // 1번.
   store.dispatch(decrease());
   ```

   - 위 예제에서의 작동 순서
     1. store.dispatch(action 생성함수())로, 발생한 action에 대한 객체를 action 생성함수()를 파라미터로 전달해 사실상 파라미터로는 action 객체가 인가 될 수 있도록 함.
     2. reducer에서 이 전 값(store에 저장되어 있던)과 action을 받아 action type에 따라 새로운 객체를 생성시킴
     3. reducer에서 action.type에 따라 달리 만든 새로운 객체를 리턴시킴으로써 store에 갈아끼움.

### 참고자료

- ⭐[React Immutable](https://velopert.com/3486)
- ⭐[Redux(리덕스)란? (상태 관리 라이브러리)](https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/)\
- [리덕스는 무엇이고, 왜 사용하는가?](https://velog.io/@youthfulhps/What-is-Redux-and-why-use-it)
- ⭐[Redux 실습](https://react.vlpt.us/redux/03-prepare.html)
- [로그인에서의 Redux 활용](https://joonganglib.tistory.com/m/11)
- ⭐[간단한 예제를 통해 Redux를 이해하기](https://velog.io/@qf9ar8nv/%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%98%88%EC%A0%9C%EB%A5%BC-%ED%86%B5%ED%95%B4-Redux%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
