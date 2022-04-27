---
layout: post
title: "Redux 용어 정리"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---
## Redux의 3가지 원칙
1. Store는 무조건 하나만 존재한다.
2. 상태(State)는 읽기 전용이다.
    - 리액트에서는 setState 메소드를 활용해야만 상태 변경이 가능하다.
    - 리덕스에서도 액션이라는 객체를 통해서만 상태를 변경할 수 있다.
3. 변경은 순수함수로만 가능하다.
    - 리듀서와 연관되는 개념이다.
    - Store(스토어) – Action(액션) – Reducer(리듀서)

![image](https://user-images.githubusercontent.com/28949166/159769442-2a70b01f-33a9-4eb6-bb66-28c646063cee.png)
## Redux 용어 정리
### Store
> Store(스토어)는 상태가 관리되는 오직 하나의 공간이다.
- 컴포넌트와는 별개로 스토어라는 공간이 있어서 그 스토어 안에 앱에서 필요한 상태를 담는다.
- 컴포넌트에서 상태 정보가 필요할 때 스토어에 접근한다.

### Action
> Action(액션)은 앱에서 스토어에 운반할 데이터를 말한다. (주문서)  
Action(액션)은 자바스크립트 객체 형식으로 되어있다.
```javascript
{
  type: 'ACTION_CHANGE_USER', // 필수
  payload: { // 옵션
    name: '하나몬',
    age: 100
  }
}
```

## Reducer의 사용
### Dispatch
- Action(액션)을 Store(스토어)에 바로 전달하는 것이 아니다. Action(액션)을 Reducer(리듀서)에 전달해야한다.
- Reducer(리듀서)가 주문을 보고 Store(스토어)의 상태를 업데이트하는 것이다.
- Action(액션)을 Reducer(리듀서)에 전달하기 위해서는 dispatch() 메소드를 사용해야한다.
```javascript
// reducer
export const START_LOADING = "START_LOADING";
export const FINISH_LOADING = "FINISH_LOADING";

const initialState = {
  isLoading: false, // 로딩 중인지 여부를 표시.
};

const loading = (state = initialState, action) => {
  switch (action.type) {
    case START_LOADING:
      return {
        ...state,
        isLoading: true,
      };
    case FINISH_LOADING:
      return {
        ...state,
        isLoading: false,
      };
    default:
      return state;
  }
};
```

```javascript
export const startLoading = () => ({ type: START_LOADING }); // action

...
import { useDispatch } from 'react-redux'; // 리덕스 훅 가져오기

dispatch(startLoading());
```

### useSelector
- 하위 컴포넌트에서 store에 접근하는 방법
```javascript
import { useSelector } from 'react-redux';

const isLoading = useSelector((state) => state.loading.isLoading);
```

## Redux 동작 사이클
![image](https://user-images.githubusercontent.com/28949166/159770299-6fe4daa7-848f-4cf7-8d9b-cff59ae7c706.png)
> 1. Action(액션) 객체가 dispatch() 메소드에 전달된다.
> 2. dispatch(액션)를 통해 Reducer를 호출한다.
> 3. Reducer는 새로운 Store 를 생성한다.
### 왜 이런 공식을 따를까?
- 이유는 데이터가 한 방향으로만 흘러야하기 때문이다.

## Redux를 사용하는 이유?
### Redux의 장점
- 상태를 예측 가능하게 만든다. (순수함수를 사용하기 때문)
- 유지보수 (복잡한 상태 관리와 비교)
- 데이터 전달을 위한 복잡한 계층 구조가 필요하지 않게 되었음. 즉, props drilling을 방지!
- 상태 업데이트를 위한 함수들로 인해 컴포넌트가 필요 이상으로 커지는 것을 막을 수 있음
- 애플리케이션에서 액션과 리듀서 등을 각각 모아 분리함으로써 개발자들이 비즈니스 로직에 대해 파악하기에도 더 쉬워짐

## 참고자료 출처

- [Redux(리덕스)란? (상태 관리 라이브러리)](https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/){:target="\_blank"}
- [Redux는 무엇이고, 어떤 장점이 있는가?](https://jjy0821.tistory.com/40){:target="\_blank"}
