---
layout: post
title: "forEach문에 break 걸기"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## forEach에서의 break문
Array.forEach() 는 기본적으로 break 문을 따로 지원하지 않는다.

만일 일반 for문의 break 구문을 forEach에 구현하고 싶다면 다음 3가지 방법이 존재한다.
1. try catch문 안에서 forEach를 돌리고, 강제 throw에러로 루프를 벗어나는 방법
2. Array.some() 메소드를 쓰는 방법
3. Array.every() 메소드를 쓰는 방법

### try catch를 이용한 방법
- forEach는 return true / false 둘 다 continue로 작동된다.
- forEach 자체의 return은 undefined 이다.
- 따라서 리턴으로 break를 걸수가 없어 아예 예외처리를 통해서 예외를 throw하여 강제로 루프문을 벗어나게 하는 방법을 쓴다.
```javascript
  var arr = [1,2,3,4,5,6,7,8,9,10];
  try{
    arr.forEach(function(c){
      console.log(c);
      if(c==3) throw new Error("stop loop"); // 에러를 throw하면 강제로 루프에서 벗어나서 catch로 가게 된다.
    })
  }catch(e){

  } 

  // 결과 : 1, 2, 3
```




## 참고자료 출처

- [[JS] 📚 자바스크립트 forEach()에 break거는 방법](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-forEach%EC%97%90-break%EA%B1%B0%EB%8A%94-%EB%B0%A9%EB%B2%95){:target="\_blank"}
