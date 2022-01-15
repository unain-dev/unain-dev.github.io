---
layout: post
title: "React Redux 예제(로그인)"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

- [github source](https://github.com/unain-dev/react-base-practice/tree/main/login-practice){:target="\_blank"}

### Redux 설치

- redux toolkit

  ```
  npm install @reduxjs/toolkit
  ```

- redux 보조 패키지
  ```
  npm install react-redux
  ```

## 방법 1

> dispatch에 파라미터로 action 생성함수 결과값(리턴값)을 전달시킴.

1.  모듈로 store(state), reducer, action 생성함수 작성

- src/common/store/modules/auth.js

  ```javascript
  // 모듈이 많은 경우 이렇게 나눠두면 좋음. store 조회 경로는 state.auth가 됨.
  const LOGIN = "auth/LOGIN";

  // action 생성함수
  export const setUserInfo = (info) => ({
    type: LOGIN,
    userInfo: {
      id: info,
    },
  });

  const initialState = {
    type: "",
    userInfo: {
      id: "",
    },
  };

  export default function auth(state = initialState, action) {
    switch (action.type) {
      case LOGIN:
        return {
          ...state,
          userInfo: action.userInfo,
        };
      default:
        return state;
    }
  }
  ```

2. reducer 모듈을 하나로 묶음

   - src/common/store

     ```javascript
     import { combineReducers } from "redux";
     import auth from "./modules/auth";

     const rootReducer = combineReducers({
       auth,
     });

     export default rootReducer;
     ```

3. store를 provider를 이용해 어플리케이션에 등록(하위 컴포넌트들에서 store 접근 가능하게)

- src/index.js

  ```javascript
  import React from "react";
  import ReactDOM from "react-dom";
  import "./index.css";
  import App from "./App";
  import { Provider } from "react-redux";
  import { createStore } from "redux";
  import rootReducer from "./common/store";

  // store 선언
  const store = createStore(rootReducer);

  ReactDOM.render(
    <React.StrictMode>
      {/* store를 어플리케이션에 등록 */}
      <Provider store={store}>
        <App />
      </Provider>
    </React.StrictMode>,
    document.getElementById("root")
  );
  ```

4. redux store 등록 & 조회

- src/views/base/login/login-container.js

  ```javascript
  import { useSelector, useDispatch } from "react-redux";
  import Login from "./login-dialog";
  import { setUserInfo } from "../../../common/store/modules/auth";

  function LoginContainer() {
    const userInfo = useSelector((state) => state.auth.userInfo);
    const dispatch = useDispatch();

    const onClickLogin = (id) => {
      console.log("in onLogin");
      // 이 부분은 비동기 통신의 success 부분(then)에서 처리해줘야함. 임시로 이렇게 처리.
      const token = {
        id: id,
      };
      sessionStorage.setItem("access-token", JSON.stringify(token));

      dispatch(setUserInfo(id));
      console.log("store에 있는 id : ", userInfo);
    };

    return (
      <>
        <Login onLogin={onClickLogin}></Login>
      </>
    );
  }

  export default LoginContainer;
  ```

- src/views/base/login/login-dialog.js

  ```javascript
  import Modal from "../modals/Modal";
  import { useState } from "react";
  import { useHistory } from "react-router-dom";
  import store from "../../../common/store/modules/auth";

  // 모달창 만들기 : https://phrygia.github.io/react/2021-09-21-react-modal/
  // history 사용해 이 전 페이지로 이동 :https://velog.io/@leemember/React-Router-dom%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%EC%9D%B4%EC%A0%84-%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A1%9C-%EC%9D%B4%EB%8F%99%ED%95%98%EA%B8%B0
  const Login = ({ onLogin }) => {
    const history = useHistory();
    const goBack = () => {
      history.goBack();
    };

    // useState를 사용하여 open상태를 변경한다. (open일때 true로 만들어 열리는 방식)
    const [modalOpen, setModalOpen] = useState(true);

    const closeModal = () => {
      setModalOpen(false);
      sessionStorage.removeItem("access-token");
      goBack();
    };

    // react hook에서 state 사용
    const [id, setId] = useState("");
    const [pw, setPw] = useState("");

    // handler 함수들
    const onIdHandler = (event) => {
      setId(event.currentTarget.value);
    };

    const onPwHandler = (event) => {
      setPw(event.currentTarget.value);
    };

    const onSubmit = (e) => {
      // e.preventDefault();
      console.log(id);
      onLogin(id); // store에 userInfo 저장.
    };

    return (
      <>
        {/* //header 부분에 텍스트를 입력한다. */}
        <Modal open={modalOpen} close={closeModal} header="Login">
          {/* // Modal.js <main> {props.children} </main>에 내용이 입력된다. 리액트 */}
          <form>
            <div>
              <input placeholder="ID" value={id} onChange={onIdHandler}></input>
            </div>
            <div>
              <input placeholder="PW" value={pw} onChange={onPwHandler}></input>
            </div>
            <button type="button" onClick={onSubmit}>
              로그인
            </button>
          </form>
        </Modal>
      </>
    );
  };

  export default Login;
  ```

## 방법 2

> dispatch에 type만 파라미터로 전달해 action 생성함수를 거치지 않고 그냥 reducer에서 바로 바뀐 값을 return시켜서 state를 변환.(맞는 방법인지 확인 필요)

- [간단한 예제를 통해 Redux를 이해하기](https://velog.io/@qf9ar8nv/%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%98%88%EC%A0%9C%EB%A5%BC-%ED%86%B5%ED%95%B4-Redux%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0){:target="\_blank"}

## 참고

- 방법 1 : [Redux 실습](https://react.vlpt.us/redux/03-prepare.html){:target="\_blank"}
- 방법 2 : [간단한 예제를 통해 Redux를 이해하기](https://velog.io/@qf9ar8nv/%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%98%88%EC%A0%9C%EB%A5%BC-%ED%86%B5%ED%95%B4-Redux%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0){:target="\_blank"}
