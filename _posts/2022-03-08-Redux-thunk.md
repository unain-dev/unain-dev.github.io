---
layout: post
title: "redux-thunk 개념 이해"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## redux-thunk란?

- 비동기 작업을 처리할 때 많이 사용하는 미들웨어다. 객체가 아닌 함수 형태의 액션을 디스패치할 수 있게 해준다.

## redux-thunk 실행 사이클 이해하기

### 일반적인 redux 실행 사이클

![image](https://user-images.githubusercontent.com/28949166/157150268-48e81755-8a57-42cc-bf45-b31032523ddc.png)

> event -> action creator -> action 생성 -> dispatch(action) -> reducer -> new state

1. user event 발생
2. action creator를 통해 event에 부합하는 action object가 생성됨.
3. 2에서 생성한 action object를 dispatch를 통해 reducer로 보냄.
4. reducer가 action과 이 전의 state를 인자로 받아 new State를 생성.

### redux-thunk (redux-middleware) 실행 사이클

![image](https://user-images.githubusercontent.com/28949166/157150990-2f065da7-26e1-4513-ae6f-9ce7a3421fb7.png)

> event -> action creator -> action 생성 -> dispatch(action) -> <b>Redux Middleware(Rdux Thunk)</b>-> reducer -> new state

### redux-thunk 내부 실행 사이클

- action이 함수가 아닐 경우
  > Redux Thunk -> 함수가 아닐 경우 -> dispatch -> Reducer
- action이 함수일 경우
  > Redux Thunk -> 함수가 맞다 -> <b>함수실행</b> -> <b>dispatch(수동)</b> -> Reducer

## Redux Data Loading 사이클

>

    <컴포넌트 마운트에서(라이프사이클) 액션 생성자를 호출한다.>
    1. 컴포넌트가 화면에 렌더링 됨
    2. useEffect에서 action creator 호출

    <API 요청은 Action Creator에서 담당하며, Redux-thunk가 여기서 작동한다.>
    3. Action creator가 코드를 실행하며 API 요청
    4. API가 데이터를 응답
    5. Action creator는 'payload'에 가져온 데이터를 할당하고 action을 반환한다.

    <redux store에서 새로운 state가 생성된다.(dispatch 된 action의 payload(데이터))>
    6. reducer는 action을 보고 'payload'에 할당된 데이터를 가져온다.
    7. 새로운 state가 생성되었기 때문에 react 앱은 리렌더링 된다.

## redux-thunk Example

- 렌더링 컴포넌트

  ```javascript

  ```

- reducer

  ```javascript
  export const initialState = {
    isLogin: false,
    username: "",
  };

  const userReducer = (state = initialState, action) => {
    switch (action.type) {
      case "LOGIN_SUCCESS":
        return {
          ...state, // es6 spread 문법
          isLogin: true,
          username: action.payload.username,
        };
      default:
        return state;
    }
  };

  export default userReducer;
  ```

- action 생성 함수

  ```javascript
  // action 생성 함수
  const loginSuccess = (response) => {
    return {
      type: "LOGIN_SUCCESS",
      payload: response,
    };
  };

  const loginFail = (error) => {
    return {
      type: "LOGIN_FAIL",
      payload: error,
    };
  };

  //
  const loginTry = (someValue) => async (dispatch, getState) => {
    dispatch({ type: "LOGIN_REQUEST" });
    try {
      const response = await myAjaxLib.post("/someEndpoint", {
        data: someValue,
      });
      dispatch(loginSuccess(response));
    } catch (error) {
      dispatch(loginFail(error));
    }
  };
  ```

<!--

- index.js에서 action으로 API 호출

  ```javascript
  // async await 사용 예제
  export const fetchData = () => async (dispatch) => {
    const response = await APIadress.get("/data");

    // 요청이 완료되면 여기서 직접 dispatch 한다.
    dispatch({ type: "FETCH_DATA", payload: response });
  };
  ```

  ```javascript
  // api를 따로 선언해서 then, catch 사용 예제
  const getComments = () => (dispatch, getState) => {
    // 이 안에서는 액션을 dispatch 할 수도 있고
    // getState를 사용하여 현재 상태도 조회 할 수 있습니다.
    const id = getState().post.activeId;

    // 요청이 시작했음을 알리는 액션
    dispatch({ type: "GET_COMMENTS" });

    // 댓글을 조회하는 프로미스를 반환하는 getComments 가 있다고 가정해봅시다.
    api
      .getComments(id) // 요청을 하고
      .then((comments) =>
        dispatch({ type: "GET_COMMENTS_SUCCESS", id, comments })
      ) // 성공시 success dispatch
      .catch((e) => dispatch({ type: "GET_COMMENTS_ERROR", error: e })); // 실패시 fail dispatch
  };
  ```

- reducer 설정(reducers/index.js)

  ```javascript
  1
  //redux에서 combineReducers 를 가져옴
  import { combineReducers } from 'redux'

  2
  // switch 구문을 사용한 reducer -> redux-actions로 간편화 가능
  // 최초의 state는 빈 배열이다.([])
  const datasReducer (state=[], action) => {
    switch(action.type){
        // action의 type의 값이 'FETCH_DATA' 인가?
        case 'FETCH_DATA':
        // 참(true)이면 그 액션의 payload를 반환한다.
        return action.payload;
        // 해당되는 액션 type이 없으면
        default:
        // 기존의 state를 반환한다.
        return state;
    }
  }

  3
  // createStore를 위한 reducer로 넘어간다.
  export default combineReducers({
    datas: datasReducer,
  })

  ```
-->

## 참고자료 출처

- redux-thunk 이론 : [(Redux) Redux-thunk](https://velog.io/@mokyoungg/Redux-Redux-thunk){:target="\_blank"}
- 예제 코드 참고 : [미들웨어 이해하기(1) : redux-thunk](https://lovecode.tistory.com/144){:target="\_blank"}
- redux-actions 참고 1(요약본) : [redux-actions로 가독성 높이기](https://juhi.tistory.com/24){:target="\_blank"}
- redux-actions 참고 2 : [Redux 를 통한 React 어플리케이션 상태 관리 :: 4장. Ducks 구조와 redux-actions 사용하기](https://velopert.com/3358){:target="\_blank"}
- 찐 예제!!! : [redux-thunk 를 사용하여 웹 요청 비동기 작업 처리하기](https://jammanboo.tistory.com/36){:target="\_blank"}
