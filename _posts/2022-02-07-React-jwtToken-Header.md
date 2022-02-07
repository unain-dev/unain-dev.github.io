---
layout: post
title: "React axios 요청 시 헤더에 변수 넣어 보내기"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## 사용하는 경우

- BE에서 헤더에 jwtToken 등을 넣어서 보낼 것을 요구하는 경우 헤더에 감싸서 보내야한다.

## axios 요청 시 헤더에 변수 넣어 보내는 방법

- 비동기 통신 모듈(GET)

  ```javascript
  async function booklogDetail(booklogSeq, header, success, fail) {
    await api
      .get(`/api/v1/booklogs/${booklogSeq}`, header)
      .then(success)
      .catch(fail);
  }
  ```

  - 원래에는 axios.get(`URL`, params, header) 순으로, 3번째 파라미터가 헤더에 해당하지만 params가 없으면 header를 2번째 요소로 넣어야한다.(빈 요소를 2번째 파라미터로 넣으면 오류 발생)

- 비동기 통신 요청 부(POST, PUT, DELETE)

  ```javascript
  async function setLikeBooklog(booklogSeq, header, success, fail) {
    await api
      .post(`/api/v1/booklogs/${booklogSeq}/like`, {}, header)
      .then(success)
      .catch(fail);
  }
  ```

  - POST, PUT, DELETE는 GET과 달리, 요청 바디에 담기기 때문에 헤더를 전달하기 위해서는 axios.get(`URL`, params, header) 순으로, 3번째 파라미터로 헤더를 맞춰줘야 한다. 즉, 파라미터가 없으면 빈 값이라도 2번째 파라미터에 넣어야 동작 한다.

- 비동기 통신 요청 부

  ```javascript
  booklogDetail(
    params.booklogSeq,
    {
      headers: {
        Authorization: `Bearer ` + jwtToken,
      },
    },
    (response) => {
      if (response.data.status === 200) {
        setBooklog(response.data.data.booklog);
      } else {
        alert("접근이 불가능한 페이지입니다.");
        navigate("/");
      }
    },
    (error) => {
      alert("접근이 불가능한 페이지입니다.");
      navigate("/");
    }
  );
  ```

  - 아래 부분에서 `Bearer `의 띄어쓰기를 빼면 동작 오류!
    ```javascript
    {
        headers: {
          Authorization: `Bearer ` + jwtToken,
        },
      },
    ```
