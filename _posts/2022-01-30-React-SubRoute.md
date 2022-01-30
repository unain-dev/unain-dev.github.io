---
layout: post
title: "Redux 서브라우트(서브라우팅)"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## 문제 상황

- 홈 화면에서는 Nav+Content+Footer만 보이고
- 마이페이지 화면에서는 Nav+Content+Footer에다가 +Sidebar가 보여야함.
- 또한 mypage 내부에는 userInfo, myBooklog 등으로 서브라우팅 시켜야함.

## 해결 방법

- src/index.js : 전체 라우팅 담당. 라우팅의 루트.

  ```javascript
  const rootElement = document.getElementById("root");
  render(
    <Provider store={store}>
      <PersistGate persistor={persistor}>
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<App />} />
            <Route path="/login" element={<Login />} />
            <Route path="/signup" element={<Signup />} />

            {/* 서브라우팅 시작. */}
            <Route path="/mypage" element={<MyPage />}>
              {/* index가 꼭 붙어야함. */}
              <Route index element={<UserInfoContainer />} />
              <Route path="mybooklog" />
              <Route path="mybookclub" />
              <Route path="mychallenge" />
            </Route>
            {/* 서브라우팅 끝. */}
          </Routes>
        </BrowserRouter>
      </PersistGate>
    </Provider>,
    rootElement
  );
  ```

- src/views/user/myPage/index.js : mypage의 서브라우팅 루트 파일.

  ```javascript
  import UserInfoContainer from "./userInfo/UserInfoContainer";
  import UserBooklogPresenter from "./userBooklog/UserBooklogPresenter";
  import UserBookclubPresenter from "./userBookclub/UserBookclubPresenter";
  import UserChallengePresenter from "./userChallenge/UserChallengePresenter";
  import { Route, Routes } from "react-router-dom";
  import Sidebar from "../../main/Sidebar";
  import styled from "styled-components";
  import Login from "../login/LoginContainer";

  const Center = styled.div`
    height: 90vh;
    display: flex;
    flex-direction: row;
  `;

  function Mypage() {
    return (
      <Center>
        <Sidebar />
        <Routes>
          {/* 이렇게 어떤 컴포넌트로 분기시켜주는지, path 어딘지 안적어주면 렌더링 되지 못함. 라우터가 경로 찾지 못해서.... */}
          <Route index path="/" element={<UserInfoContainer />} />
          <Route path="/mybooklog" exact element={<UserBooklogPresenter />} />
          <Route path="/mybookclub" exact element={<UserBookclubPresenter />} />
          <Route
            path="/mychallenge"
            exact
            element={<UserChallengePresenter />}
          />
        </Routes>
      </Center>
    );
  }

  export default Mypage;
  ```

<!-- ## 참고자료 출처

- [[#. React] redux-persist 설치 후 새로고침해도 state 유지하기](https://developer0809.tistory.com/108){:target="\_blank"}

- [Redux-Persist 사용하여 Store 유지하기](https://velog.io/@tunakim/Redux-Persist-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-Store-%EC%9C%A0%EC%A7%80%ED%95%98%EA%B8%B0){:target="\_blank"} -->

```

```
