---
layout: post
title: "React CRUD 비동기통신 params 이용여부 정리"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## 정리

- GET 요청은 params: {}로 감싸서 보내줘야한다.
- 그 외 요청은 감싸서 보내지 않아도 된다.
  > 이유? GET요청은 Header에 담겨져 보내지고, POST와 PUT은 Body에 담겨 보내지기 때문.

## GET

- 전달 파라미터는 꼭 params: {}로 감싸서 보내줘야한다.

  ```javascript
  axios
    .get("/user", {
      params: {
        ID: 12345,
      },
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
  ```

## POST

- params로 감싸서 보내지 않아도 된다.

  ```javascript
  axios
    .post("/user", {
      firstName: "Fred",
      lastName: "Flintstone",
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
  ```

## PUT

- params로 감싸서 보내지 않아도 된다.

  ```javascript
  axios
    .PUT("/user", {
      firstName: "Fred",
      lastName: "Flintstone",
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
  ```

## DELETE

    ```javascript
    axios.delete('/user?ID=12345')
    .then(function (response) {
    // handle success
    console.log(response);
    })
    .catch(function (error) {
    // handle error
    console.log(error);
    })
    .then(function () {
    // always executed
    });
    ```

## 참고자료 출처

- [[react] axios get, post, put, delete api 호출 하기.](https://firework-ham.tistory.com/74){:target="\_blank"}
- [React에서 Axios를 이용해 API 호출하기 (feat. fetch, ajax)](https://velog.io/@devstone/React%EC%97%90%EC%84%9C-Axios%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-API-%ED%98%B8%EC%B6%9C%ED%95%98%EA%B8%B0-feat.-fetch-ajax){:target="\_blank"}
