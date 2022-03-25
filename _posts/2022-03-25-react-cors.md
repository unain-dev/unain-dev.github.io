---
layout: post
title: "React 에서의 CORS 에러 해결 방법"
# date: 2021-12-10 12:34:43 +0900
categories: Web React.js
---

## 특정 사이트의 CORS만 처리하기
1. package.json에 맨 아래쪽에 다음과 같이 m.serach.naver.com(접근 URL)에 대한 프록시를 추가한다. 
    ```
    //package.json
    {
      ..., 
      ..., 
      "proxy": "https://m.search.naver.com" 
    }
    ```
2. 호출할때 url의 호스트를 지워준다.
    ```
    export function test() { 
      axios.get('/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query=%EC%BD%94%EC%8A%A4%ED%94%BC')
      .then(data => {
        console.log(data.data)
      }) 
    }
    ```

이렇게 호출하면 브라우저에서는 localhost:3000 (나의 리액트 서버)로 부터 api응답 받아온것마냥 인식하기때문에 CORS가 해결된다.

## 여러가지 api로부터 CORS 처리를 관리하기
일단 도로 package.json에 해둔 프록시 설정을 제거하자.
1. http-proxy-middleware 라이브러리를 설치
    `npm install http-proxy-middleware`
2. src에 setupProxy.js 파일을 하나 생성하자. (이 루트의 파일명으로 자동으로 설정되니 다른 설정은 필요없다.
    ```
    //setupProxy.js
    
    const { createProxyMiddleware } = require('http-proxy-middleware');
    module.exports = function(app){
      app.use( 
        createProxyMiddleware('/naver', {
          target: 'https://m.search.naver.com',
          pathRewrite: {
            '^/naver':''
          }, 
          changeOrigin: true 
        })
      )
      
      app.use(
        createProxyMiddleware('/다른context', {
          target: 'https://다른호스트', 
          pathRewrite: { 
            '^/지우려는패스':''
          }, 
          changeOrigin: true 
        })
      )
      
      ...
    };
    ```
위처럼 설정하면 '/naver'로 시작되는 url을 자동으로 인식하여 프록시 처리해주고, /naver라는 패스는 pathRewrite에서 설정한 것처럼 제거가 가능하다.

그래서 이렇게 호출하면 관리가 가능하다.
```
export function test() {
  axios.get('naver/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query=%EC%BD%94%EC%8A%A4%ED%94%BC')
    .then(data => {
      console.log(data.data)
    })
}
```

## 참고자료 출처

- [리액트(React) CORS처리](https://woochan-dev.tistory.com/94){:target="\_blank"}
