---
layout: post
title: "[JS] for in vs for of"
categories: JS
---
## for in vs for of
- for in : 객체 순환
- for of : 배열 순환
한 마디로 정리하자면, 위처럼 정리 할 수 있습니다.

한번 예시를 통해 좀 더 자세히 살펴 볼게요!

## for in
### 기본
```
var obj = {
  a: 1,
  b: 2,
  c: 3
};

for (var item in obj) {
  console.log(item) // a, b, c
}
```

### 활용
```
var obj = {
  a: 1,
  b: 2,
  c: 3
};

for (var item, idx in obj) {
  console.log(idx, " : ", item) // 0 : a, 1 : b, 2 : c
}
```
> index를 받아오고 싶다면, 두번째 인자로 받아오면 된다(순서는 변수명과 상관 없이 첫번째 변수가 value, 두번째 변수가 key이다.)

## for of
### 기본 사용
```
var arr = [1, 2, 3];

for (var item of arr) {
  console.log(item); // 1, 2, 3
}
```

### 객체에 for of를 사용한다면?
```
var arr = [1, 2, 3];

for (var item in arr) {
  console.log(item); // 0, 1, 2
}
```
> 객체를 for of로 돌려도 오류가 나지 않는 이유는?
> js는 객체 = 배열로 취급한다. 그래서 for of로 객체를 순환해도 오류가 나지 않는 것이다.

### 하지만!!! for in으로 객체를 돌리는 것과 for of로 객체를 순환하는 것은 사용새가 다르다.
```
var obj = {
  a: 1,
  b: 2,
  c: 3
};

for (var item in obj) {
  console.log(item) // a, b, c
}
```
```
var arr = [1, 2, 3];

for (var item in arr) {
  console.log(item); // 0, 1, 2
}
```
위 예제를 보면 알 수 있듯이
- for in : 객체의 value 순환
- for of : 객체의 key 순환, 배열의 value 순환

## 참고자료 출처
- [for ...in, for ...of 차이](https://velog.io/@eomttt/for-...in-for-...of-%EC%B0%A8%EC%9D%B4){:target="\_blank"}
