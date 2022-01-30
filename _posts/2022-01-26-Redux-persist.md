---
layout: post
title: "Redux redux-persist"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## 문제 상황

- 페이지 이동 시, redux의 store들이 초기화 되는 현상.

## 해결 방법

- redux-persist 설치

  ```
    npm install --save redux-persist
  ```

- redux-persist store(reducers)에 적용시키기

  - src/reducers/index.js : src/reducers/modules 내에 auth.js있음.

    ```javascript
    import { combineReducers } from "redux";
    import authReducer from "./modules/auth";

    // Redcer-Persist
    import { persistReducer } from "redux-persist";
    import storage from "redux-persist/lib/storage";

    //redux-persist 적용
    const persistConfig = {
      key: "root",
      storage: storage,
    };

    const rootReducer = combineReducers({
      authReducer,
    });

    export default persistReducer(persistConfig, rootReducer);
    ```

- redux-persist index.js에 적용시키기

  - src/index.js

    ```javascript
    import React from "react";
    import ReactDOM from "react-dom";
    import App from "./App";
    import { Provider } from "react-redux";
    import { createStore } from "redux";
    import rootReducer from "./common/reducers/index";
    import { composeWithDevTools } from "redux-devtools-extension"; // 리덕스 개발자 도구
    import { BrowserRouter, Routes, Route } from "react-router-dom";
    import { render } from "react-dom";
    import Login from "./views/user/login/LoginContainer";
    import Signup from "./views/user/signup/SignupContainer";

    // Redux-Persist
    import { persistStore } from "redux-persist";
    import { PersistGate } from "redux-persist/integration/react";

    const store = createStore(rootReducer, composeWithDevTools()); // 스토어를 만듭니다.
    const listener = () => {
      const state = store.getState();
      console.log(state);
    };
    const unsubscribe = store.subscribe(listener);

    // redux-persist를 store에 적용.
    const persistor = persistStore(store);

    const rootElement = document.getElementById("root");
    render(
      <Provider store={store}>
        {/* redux-persist를 적용시킨 store를 전체 컴포넌트에 내려줌. */}
        <PersistGate persistor={persistor}>
          <BrowserRouter>
            <Routes>
              <Route path="/" element={<App />} />
              <Route path="/login" element={<Login />} />
              <Route path="/signup" element={<Signup />} />
            </Routes>
          </BrowserRouter>
        </PersistGate>
      </Provider>,
      rootElement
    );
    ```

## 참고자료 출처

- [[#. React] redux-persist 설치 후 새로고침해도 state 유지하기](https://developer0809.tistory.com/108){:target="\_blank"}

- ⭐[Redux-Persist 사용하여 Store 유지하기](https://velog.io/@tunakim/Redux-Persist-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-Store-%EC%9C%A0%EC%A7%80%ED%95%98%EA%B8%B0){:target="\_blank"}
