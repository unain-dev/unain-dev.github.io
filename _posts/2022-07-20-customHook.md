---
layout: post
title: "[React] Custom Hook"
categories: React.js
---
## Custom hook?
React에서 기본적으로 제공하는 hook(useState, useEffect 등...)과는 달리, 사용자가 직접 생성하여 사용할 수 있는 hook을 칭한다.

반복되는 훅 활용 메소드들을 하나로 줄여줌으로써 더 간결하고 보기 좋은 코드를 만들 수 있다.

일반적인 function처럼 컴포넌트를 렌더링하는 역할은 수행하지 않지만, function과는 다르게 useEffect, useState 등 기본 React hook을 활용하여 구성이 가능하다.

다만, hook으로 만들어야할 때와 아닐 때를 잘 구분하고 판단하여 사용해야한다.

## Custom Hook의 장점
- 컴포넌트보다 적은 양의 코드로 동일한 로직을 구현 할 수 있다.
- 일반 function과는 다르게 useEffect, useState 등 기본 React hook을 활용한 로직 구성이 가능하다.
- 상태 관리 로직의 재활용이 가능하다.
- 동일한 로직을 별도로 관리하여 재사용성을 증가시킬 수 있다.

## Hooks의 규칙
1. 최상위 레벨에서만 Hook을 호출해야한다.
  - 반복문, 조건문 혹은 중척된 함수 내에서 hook을 호출하지 않아야한다.
  - 이 규칙을 따르면 컴포넌트가 렌더링 될 때마다 동일한 순서로 hook이 호출 되는 것이 보장된다. 이러한 점은 React가 useState와 useEffect가 여러 번 호출되는 중에도 Hook의 상태를 올바르게 유지할 수 있도록 해준다.
2. 오직 React함수 내에서 Hook을 호출해야한다.
   - 이 규칙을 지키면 컴포넌트의 모든 상태 관련 로직을 소스코드에서 명확하게 보이도록 할 수 있다.
3. 네이밍은 prefix `use`로 시작해야한다.

## Exapmle of Custom Hook
> 버튼을 클릭하면, 각각의 숫자가 증가하는 컴포넌트

### App.js
```javascript
import { useEffect } from "react";
import "./styles.css";
import useTestHook from "./useTestHook";

export default function App() {
  const num1 = useTestHook();
  const num2 = useTestHook();

  useEffect(() => {}, []);

  return (
    <div className="App">
      <h1>num1 : {num1.num}</h1>
      <button onClick={num1.onClick}>num1 증가</button>
      <h1>num2 : {num2.num}</h1>
      <button onClick={num2.onClick}>num2 증가</button>
    </div>
  );
}
```

### useTestHook.js
```javascript
import { useState } from "react";

export default function useTestHook(command) {
  const [num, setNum] = useState(0);

  const onClick = () => {
    setNum(num + 1);
  };
  return { num, onClick };
}
```

## Custom Hook은 언제 만들어야할까?
### 합성
한마디로, 동시에 다른 hook을 사용할 수 있어야 하고, 서로 간의 사용하는 자원에 대해 영향을 주면 안된다.

### 디버깅


## 참고자료 출처
- [Custom Hook을 만들기 전에 고려해야 할 것들](https://leego.tistory.com/entry/React-Custom-hook%EC%9D%84-%EB%A7%8C%EB%93%A4%EA%B8%B0-%EC%A0%84%EC%97%90-%EA%B3%A0%EB%A0%A4%ED%95%B4%EC%95%BC-%ED%95%A0-%EA%B2%83%EB%93%A4#%EB%--%A-%EC%--%B-%EA%B-%--%EB%A-%B-%EC%--%-C%F-%-F%-A%AA){:target="\_blank"}
- [핀다에서 쓰는 React Custom Hooks](https://medium.com/finda-tech/%ED%95%80%EB%8B%A4%EC%97%90%EC%84%9C-%EC%93%B0%EB%8A%94-react-custom-hooks-1a732ce949a5){:target="\_blank"}
- [간단한 리액트 커스텀 훅 만들어보기](https://nukw0n-dev.tistory.com/29){:target="\_blank"}
