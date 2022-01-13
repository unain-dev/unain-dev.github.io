---
layout: post
title: "React 로그인 구현"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

### 공통사항

- 라우터에서 진입 전, session 에서 userInfo 가져와서 userInfo 있으면 로그인 된 상태로 인식.

### Vue.js에서의 로그인 동작 순서

1. 로그인 폼에서 입력을 받는다.
2. 입력 받은 값들을 store의 action 메소드(?)를 사용해 비동기통신으로 request 던짐.
3. store의 action에서 동작이 일어남. : request에 대한 response를 받아 response가 success면 commit으로 mutation을 호출해서 store의 state에 backend에서 받아온 userInfo를 저장함.
4. 3번 동작에 이어서, response가 success면 response에 같이 온 token을 sessionStorage에 sessioStorage.setItem("access-token", token)함.
5. 로그인 컴포넌트에서는 2~3번 과정이 끝나면, sessionStorage.getItem("access-token") 해와서 토큰이 있는지 없는지 검사.
6. 토큰이 있으면, home으로 분기시키고 없으면 회원가입페이지로 분기.
   -> 앞으로 계속 sessionStorage를 getItem해와서 로그인 여부 확인하는 듯.
