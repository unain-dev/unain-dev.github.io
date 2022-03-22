---
layout: post
title: "[Web] async/await"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## async await
- async/await 키워드를 사용하면 비동기 코드를 마치 동기 코드처럼 보이게 작성할 수 있음.
- await 키워드는 async 키워드가 붙어있는 함수 내부에서만 사용할 수 있으며 비동기 함수가 리턴하는 Promise로 부터 결과값을 추출해줌.
-  즉, await 키워드를 사용하면 일반 비동기 처리처럼 바로 실행이 다음 라인으로 넘어가는 것이 아니라 결과값을 얻을 수 있을 때까지 기다려줍니다. 따라서 일반적인 동기 코드 처리와 동일한 흐름으로 (함수 호출 후 결과값을 변수에 할당하는 식으로) 코드를 작성할 수 있으며, 따라서 코드를 읽기도 한결 수월해집니다.
- 예시
  ```javascript
  async function fetchAuthorName(postId) {
    const postResponse = await fetch(
      `https://jsonplaceholder.typicode.com/posts/${postId}`
    );
    const post = await postResponse.json();
    const userId = post.userId;
    const userResponse = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    const user = await userResponse.json();
    return user.name;
  }

  fetchAuthorName(1).then((name) => console.log("name:", name));
  ```
  > async 키워드가 function 앞에 붙었다는 것을 알 수 있습니다. 그리고 Promise를 리턴하는 모든 비동기 함수 호출부 앞에는 await 키워드가 추가되었습니다.


## 예외처리
- 동기/비동기 구분없이 try/catch로 일관되게 예외 처리를 할 수 있는 부분도 async/await를 사용해서 코딩했을 때의 큰 이점 중 하나
- 예시
  ```javascript
  async function fetchAuthorName(postId) {
    const postResponse = await fetch(
      `https://jsonplaceholder.typicode.com/posts/${postId}`
    );
    const post = await postResponse.json();
    const userId = post.userId;

    try {
      const userResponse = await fetch(
        `https://jsonplaceholder.typicode.com/users/${userId}`
      );
      const user = await userResponse.json();
      return user.name;
    } catch (err) {
      console.log("Faile to fetch user:", err);
      return "Unknown";
    }
  }

  fetchAuthorName(1).then((name) => console.log("name:", name));
  ```

## 주의점
- 주의할 점은 async 키워드가 붙어있는 함수를 호출하면 명시적으로 Promise 객체를 생성하여 리턴하지 않아도 Promise 객체가 리턴됩니다.

## 참고자료 출처
- [[자바스크립트] 비동기 처리 3부 - async/await](https://www.daleseo.com/js-async-async-await/){:target="\_blank"}
