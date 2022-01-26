---
layout: post
title: "React Router V6 Navigator"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

> React Router v6 install이 완료 되었다는 가정 하에 진행.
> Navigator는 React Router v5의 history를 대신합니다.

## Navigator 적용

1. import

   ```javascript
   import { useNavigate } from "react-router-dom";
   ```

2. 사용

   ```javascript
   const navigate = useNavigate();

   navigate("/");
   navigate(-1);
   navigate(-2);
   navigate(`/user/${user._id}`);
   ```

## 참고자료 출처

- [React Router v6 업데이트 정리](https://velog.io/@ksmfou98/React-Router-v6-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%A0%95%EB%A6%AC){:target="\_blank"}
