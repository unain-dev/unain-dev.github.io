---
layout: post
title: "redux-thunk 예제 이해"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## redux-thunk란?

- 비동기 작업을 처리할 때 많이 사용하는 미들웨어다. 객체가 아닌 함수 형태의 액션을 디스패치할 수 있게 해준다.

## redux-thunk (redux-middleware) 실행 사이클

![image](https://user-images.githubusercontent.com/28949166/157150990-2f065da7-26e1-4513-ae6f-9ce7a3421fb7.png)

> event -> action creator -> action 생성 -> dispatch(action) -> <b>Redux Middleware(Rdux Thunk)</b>-> reducer -> new state

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

- api 통신 함수 : lib/api

  ```javascript
  import axios from "axios";

  export const getPost = (id) => axios.get(`api 주소 /${id}`);
  ```

- reducer : modules/sample.js

  ```javascript
  import { handleActions } from "redux-actions";
  import * as api from "../lib/api";
  import createRequestThunk from "../lib/createRequestThunk";

  //액션타입 선언

  const GET_POST = "sample/GET_POST";
  const GET_POST_SUCCESS = "sample/GET_POST_SUCCESS";
  const GET_POST_FAILURE = "sample/GET_POST_FAILURE";

  //thunk 함수 생성
  //thunk 함수 내부에서 시작, 성공, 실패에 따라 각각 다른 액션 디스패치

  export const getPost = createRequestThunk(GET_POST, api.getPost);

  const initialState = {
    loading: {
      GET_POST: false,
    },
    post: null,
  };

  // redux-actions 라이브러리에서 handleActions 사용. -> reducer를 switch 문 없이 사용.
  const sample = handleActions(
    {
      [GET_POST]: (state) => ({
        ...state,
        loading: {
          ...state.loading,
          GET_POST: true, //요청 시작
        },
      }),
      [GET_POST_SUCCESS]: (state, action) => ({
        ...state,
        loading: {
          ...state.loading,
          GET_POST: false, // 요청 완료
        },
        post: action.payload,
      }),
      [GET_POST_FAILURE]: (state, action) => ({
        ...state,
        loading: {
          ...state.loading,
          GET_POST: false, // 요청 완료
        },
      }),
    },
    initialState
  );

  export default sample;
  ```

- reducer 통합 해주는 rootReducer : modules/index.js

  ```javascript
  import { combineReducers } from "redux";
  import counter from "./counter";
  import sample from "./sample";

  const rootReducer = combineReducers({
    counter,
    sample,
  });

  export default rootReducer;
  ```

- createRequestThunk 함수 - 매번 다른 thunk 함수를 작성하는 걸 방지하기 위해 분리한 함수

  ```javascript
  export default function createRequestThunk(type, request) {
    //성공 및 실패 액션 타입 정의
    const SUCCESS = `${type}_SUCCESS`;
    const FAILURE = `${type}_FAILURE`;
    return (params) => async (dispatch) => {
      dispatch({ type }); //시작
      try {
        const response = await request(params);
        dispatch({
          type: SUCCESS,
          payload: response.data,
        }); //성공
      } catch (e) {
        dispatch({
          type: FAILURE,
          payload: e,
          error: true,
        }); //에러 발생
        throw e;
      }
    };
  }

  //사용법 : createRequestThunk('GET_USERS', api.getUsers);
  ```

- 데이터 표현 Presenter 컴포넌트 : components/Sample.js

  ```javascript
  import React from "react";

  const Sample = ({ loadingPost, post }) => {
    return (
      <div>
        <section>
          <h1>포스트</h1>
          {loadingPost && "로딩 중..."}
          {!loadingPost && post && (
            <div>
              <h3>{post.title}</h3>
              <h3>{post.body}</h3>
            </div>
          )}
        </section>
      </div>
    );
  };

  export default Sample;
  ```

- 데이터 표현 Container 컴포넌트 : containers/SampleContainer.js

  ```javascript
  import React from "react";
  import { connect } from "react-redux";
  import Sample from "../components/Sample";
  import { getPost } from "../modules/sample";

  const { useEffect } = React;
  const SampleContainer = ({ getPost, post, loadingPost }) => {
    // 2번.
    useEffect(() => {
      getPost(1);
    }, [getPost]);

    return <Sample post={post} loadingPost={loadingPost} />;
  };

  // 이 부분을 useSelector로 대체 가능!!!
  //-> useSelector로 대신하면 SampleContainer 컴포넌트에 props로 내려주지 않고 사용 가능.
  export default connect(
    //비구조화 할당을 통해 state 를 분리 -> state.sample.post 대신 sample.post 사용
    ({ sample }) => ({
      post: sample.post,
      loadingPost: sample.loading.GET_POST,
    }),
    {
      getPost,
    }
  )(SampleContainer);
  ```

- App.js

  ```javascript
  import logo from "./logo.svg";
  import "./App.css";
  import SampleContainer from "./containers/SampleContainer";

  const App = () => {
    return (
      <div>
        <SampleContainer />
      </div>
    );
  };
  ```

## 참고자료 출처

- redux-thunk 전반적인 예제 : [redux-thunk 를 사용하여 웹 요청 비동기 작업 처리하기](https://jammanboo.tistory.com/36){:target="\_blank"}
- connect 함수 이해 예제 : [connect]](https://selfish-developer.com/entry/connect){:target="\_blank"}
- connect vs useSelector : [hooks에서 redux 사용하기 connect와 useSelector 비교](https://m.blog.naver.com/bunggl/221729399996){:target="\_blank"}
