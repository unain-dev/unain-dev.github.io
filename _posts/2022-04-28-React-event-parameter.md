---
layout: post
title: "[React] 이벤트 리스너에 파라미터 전달하기"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---
## 벤트 리스너에 파라미터 전달하는 방법
### Wrong!
```javascript
const clickHandler = (e, params) => {
  console.log(params); // error
  e.preventDefault();
  // do someting...
}

return (
	<button onClick={clickHandler}> Do Something!</button>
)
```
> onClick은 1개의 파라미터만 전달하기 때문에 params는 undefined로 전달된다.

## Good :)
```javascript
const clickHandler = (params, e) => {
  console.log(params); // error
  e.preventDefault();
  // do someting...
}

return (
	<button onClick={(e)=>{clickHandler(params, e)}}> Do Something!</button>
)
```

## 참고자료 출처
- [[React] onClick함수에 파라미터 전달하기](https://velog.io/@albaneo0724/React-onClick%EC%97%90-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0-%EC%A0%84%EB%8B%AC%ED%95%98%EA%B8%B0){:target="\_blank"}
