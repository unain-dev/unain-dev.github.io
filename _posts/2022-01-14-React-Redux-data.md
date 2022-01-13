---
layout: post
title: "React Redux 참고자료"
# date: 2021-12-10 12:34:43 +0900
categories: React
---

## Redux

![image](https://user-images.githubusercontent.com/28949166/149366231-1267a040-b385-4dde-a648-ded4bfd78f6c.png)

- [리액트 용어 정리](https://kyun2da.dev/%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/Redux-%EC%A0%95%EB%A6%AC/)
- Store : 전역으로 공유하는 상태의 저장소. 하나의 어플리케이션에는 하나의 sotre만 존재해야 한다.
- Action : 객체. 상태에 변화를 일으켜야할 때 이 action을 일으켜야한다.
- Action Creator : Action 객체를 만들어주는 함수.
- Reducer : 현재 상태와 액션 객체를 받아, 필요하다면 새로운 상태를 리턴하는 함수이다. 액션 유형을 기반으로 이벤트를 처리하는 이벤트 리스너.
- dispatch : Store의 내장함수. action 객체를 넘겨줘서 상태를 업데이트 할 수 있도록 함. 그리고 이 dispatch를 사용을 해서 store의 상태를 변경해야한다.(반드시! store에 직접 접근해 상태를 변경하면 안된다! - immutable)
  > vuex의 mutation.
- subscribe : store의 내장함수. 리스너 함수를 파라미터로 넣어 호출하면 상태가 업데이트될 때마다 호출된다. 일종의 이벤트 리스너.
- selector : store의 상태 값을 가져올 때 사용
  > vuex의 getter?

### 참고자료

- [React Immutable](https://velopert.com/3486)
- [Redux 실습](https://react.vlpt.us/redux/03-prepare.html)
- [로그인에서의 Redux 활용](https://joonganglib.tistory.com/m/11)
