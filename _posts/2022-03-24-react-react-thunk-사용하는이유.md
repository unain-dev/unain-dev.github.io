---
layout: post
title: "[React] react-thunk 사용하는 이유"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## react-thunk
> Redux Thunk 미들웨어는 당신이 액션 대신 함수를 반환하는 액션 크리에이터를 쓸 수 있게 해준다.  
Thunk는 action의 dispatch를 지연시키는데 사용될 수 있으며, 특정 조건이 충족되는 경우에만 dispatch할 수 있다. 내부 함수는 dispatch와 getState를 매개변수로 둔다.  

## redux-thunk를 사용하는 이유, redux는 왜 API 호출이 안되는가?
redux-thunk라는 미들웨어는 API 호출이 필요할 때 쓴다.  
근데 Redux는 왜 API 호출을 하면 안되는가?
### async / await 로 호출하면?(src/actions/index.js)
```javascript
export const fetchData = async () => {
  //임의의 api 주소에 async await으로 (get) 요청을 하였다.
  const response = await APIadress.get('/data')
 
  return {
    type: 'FETCH_DATA',
    payload: response
  }
}
```
위와 같이 action을 작성하면 다음과 같은 에러 코드가 뜬다.  
`action must be plain objects. Use custom middleware for async actions`
response는 plain objects라고 생각되기 때문이다.(console에 찍어보니까 객체 맞는데?)  
하지만 사실 async await 은 엄청나게 큰 함수이다.  
그 함수가 종료되고 return 되는 것이 내가 console에서 보는 plain objects 형태의 데이터다.  
따라서, reducer로 dispatch 되는 최초의 action 형태는 plain이 아니라 async await의 함수의 형태이다.  
그래서 오류가 난다.  

### promise 로 호출하면?(src/actions/index.js)
```javascript
export const fetchData = async () => {
  //임의의 api 주소에 (get) 요청을 promise 형태로 하였다.
  const promise = await APIadress.get('/data')
 
  return {
    type: 'FETCH_DATA',
    payload: response
  }
}
```
redux가 실행될 때, action creator를 호출하고 action이 dispatch 되어 reducer로 이동할 때 이 모든 단계는 순식간에 실행된다고 한다.  
Promise를 사용하면 순식간에 실행된 reducer에서 '반환된 데이터가 아직 없다'(객체에 아무것도 없다!)라고 판단한다.  
따라서 Promise도 사용할 수 없다.

## redux-thunk를 쓰면 어떻게 되는가?
> Redux Thunk 미들웨어는 당신이 액션 대신 함수를 반환하는 액션 크리에이터를 쓸 수 있게 해준다.
redux-thunk는 액션을 반환할 때 객체가 아니라 함수를 반환할 수 있게 해준다.  
다른 말로 액션이 함수의 형태일 때 그 함수를 실행하고 또 실행하여 객체가 되었을 때 reducer로 dispatch 한다.  

dispatch 이후에 Redux thunk가 실행된다.  
> action creator -> action -> dispatch -> Redux Thunk

Redux thunk에서 dispatch 된 액션이 함수인지 아닌지 판단한다.
> Redux Thunk -> 함수인가? -> 아니요.(Plain Object) -> dispatch -> Reducer
> Redux Thunk -> 함수인가? -> 예 -> 함수실행 -> dispatch -> 함수인가? -> 아니요(Plain Object) -> Reducer


### async await를 사용한 올바른 코드(src/actions/index.js)
```javascript
export const fetchData = () => {
  // 이 액션 생성자(fetchData)는 함수를 반환한다.
  // 함수는 dispatch와 getState를 매개변수로 가진다.
  return async function(dispatch, getState) {
    const response = await APIadress.get('/data')
   
    // 요청이 완료되면 여기서 직접 dispatch 한다.
    dispatch ({ type: 'FETCH_DATE', payload: response })
  }
}
```
위의 코드를 리팩토링하면(이러한 형태의 코드로 많이 작성한다.)
```javascript
export const fetchData = () => async dispatch => {
  const response = await APIadress.get('/data');
 
  dispatch({ type: 'FETCH_DATA', payload: response })
}
```

## 일반적인 Redux의 Data Loading 순서
redux-thunk를 사용한 redux의 data loading은 다음과 같은 순서로 작동한다.

> [컴포넌트 마운트에서(라이프사이클) 액션 생성자를 호출한다.]
> 1. 컴포넌트가 화면에 렌더링 됨
> 2. 컴포넌트에서 'ComoponentDidMount()' 라이프사이클 메서드를 호출
> 3. 'ComponentDidMount()' 에서 action creator를 호출함
> 
> [API 요청은 Action Creator에서 담당하며, Redux-thunk가 여기서 작동한다.]  
> 4. Action creator가 코드를 실행하며 API 요청  
> 5. API가 데이터를 응답  
> 6. Action creator는 'payload'에 가져온 데이터를 할당하고 action을 반환한다.  
> 
> [redux store에서 새로운 state가 생성된다.(dispatch 된 action의 payload(데이터))>]  
> 7. reducer는 action을 보고 'payload'에 할당된 데이터를 가져온다.  
> 8. 새로운 state가 생성되었기 때문에 react 앱은 리렌더링 된다.  
>



## 참고자료 출처
- [](https://velog.io/@mokyoungg/Redux-Redux-thunk){:target="\_blank"}
