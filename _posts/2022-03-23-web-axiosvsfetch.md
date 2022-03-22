---
layout: post
title: "[Web] axios vs fetch"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## axios
- 비동기로 HTTP 통신을 가능하게 해주며 return을 promise 객체로 해주기 때문에 response 데이터를 다루기도 쉽습니다.
- 예시
  ```javascript
  axios({
    method: 'post',
    url: '/user/12345',
    data: {
      firstName: 'Yongseong',
      lastName: 'Kim'
    }
  });
  ```

## fetch
- fetch는 ES6부터 JavaScript의 내장 라이브러리로 들어왔습니다.
- 예시
  ```javascript
  const url ='http://localhost3000/test`
  const option ={
     method:'POST',
     header:{
       'Accept':'application/json',
       'Content-Type':'application/json';charset=UTP-8'
    },
    body:JSON.stringify({
      name:'sewon',
        age:20
    })

    fetch(url,options)
      .then(response => console.log(response))
  ```
- 장점

### axios vs fetch
- axios
  - 장점 
    - response timeout 처리 방법이 있다. (fetch에는 존재하지 않는 기능)
    - promise 기반으로 다루기가 쉽다.(json형식으로 promise 객체를 리턴해줌!)
    - 크로스 브라우징에 신경을 많이썼기에 브라우저 호환성이 뛰어나다.
  - 단점
    - 모듈 설치를 해줘야한다.
- fetch
  - 장점 
    - 내장 라이브러리이기에 별도의 import를 해줄 필요가 없다.
    - promise 기반으로 다루기가 쉽다.
    - 내장 라이브러리이기에 사용하는 프레임워크가 안정적이지 않을 때 사용하기 좋다.
  - 단점
    - internet explorer의 경우에는 fetch를 지원하지 않는 버전도 존재한다. (브라우저 호환성이 상대적으로 떨어진다.)
    - 기능이 부족하다.
      ![image](https://user-images.githubusercontent.com/28949166/159515825-a06f6c78-7e5c-4e15-926b-d9b052fa9b21.png)


## 참고자료 출처
- [[개발상식] Ajax와 Axios 그리고 fetch](https://velog.io/@kysung95/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-Ajax%EC%99%80-Axios-%EA%B7%B8%EB%A6%AC%EA%B3%A0-fetch){:target="\_blank"}
- [[React] axios vs fetch](https://kimtongting.tistory.com/entry/React-axios-vs-fetch-axios-fetch-%EC%B0%A8%EC%9D%B4-axios-fetch-%EC%B0%A8%EC%9D%B4%EC%A0%90){:target="\_blank"}
