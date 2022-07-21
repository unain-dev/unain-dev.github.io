---
layout: post
title: "[React] useRef & custom Hook 예제"
categories: React.js
---
## Case 1 : 값의 기억 - 리렌더링 방지
> custom hook 내부에서 useRef로 값을 기억
- App.js
    ```javascript
      import { useRef } from "react";
      import "./styles.css";
      import useTestHook from "./useTestHook";

      export default function App() {
        const num1 = useTestHook();
        const num2 = useTestHook();
        
        return (
          <div className="App">
            <h1>num1 : {num1.num.current}</h1>
            <button onClick={num1.onClick}>num1 증가</button>
            <h1>num2 : {num2.num.current}</h1>
            <button onClick={num2.onClick}>num2 증가</button>
          </div>
        );
      }

    ```
- useTestHook.js
    ```javascript
    import { useRef } from "react";

    export default function useTestHook(command) {
      const num = useRef(0);

      const onClick = () => {
        num.current += 1;
        console.log(num.current);
      };

      return { num, onClick };
    }

    ```
### 결과
https://user-images.githubusercontent.com/28949166/180121932-b5b77050-d07b-42b4-b205-3a2c1283ac90.mp4

    



## Case 2 : DOM 선택
> App.js에서 직접 div를 ref로 지정 후, 이 지정한 ref를 파라미터로 넘겨줘서 custom Hook 내부에서 스타일 핸들링
- App.js
    ```javascript
      import { useRef } from "react";
      import "./styles.css";
      import useMoveHook from "./useMoveHook";
      import useTestHook from "./useTestHook";

      export default function App() {
        const num1 = useTestHook();
        const num2 = useTestHook();

        const objRef = useRef();

        const moveHook = useMoveHook;

        const move = () => {
          moveHook(objRef);
        };

        return (
          <div className="App">
            <h1>num1 : {num1.num.current}</h1>
            <button onClick={num1.onClick}>num1 증가</button>
            <h1>num2 : {num2.num.current}</h1>
            <button onClick={num2.onClick}>num2 증가</button>
            <div
              style={{ width: "200px", height: "200px", backgroundColor: "red" }}
              ref={objRef}
              onClick={move}
            ></div>
          </div>
        );
      }

    ```
    
- useMoveHook.js
    ```javascript
      const useMoveHook = (ref) => {
        console.log(ref);
        if (ref !== undefined) {
          switch (ref.current.style.backgroundColor) {
            case "blue":
              ref.current.style.backgroundColor = "red";
              break;
            case "red":
              ref.current.style.backgroundColor = "blue";
              break;
            default:
              break;
          }
        }
      };

      export default useMoveHook;

    ```

### 결과
https://user-images.githubusercontent.com/28949166/180122038-9571c6c1-ca7d-4c0c-8dbe-64c14d91009b.mp4



## 참고자료 출처
- [How to target an element child (with useRef) with a variable declaration outside of useEffect?](https://stackoverflow.com/questions/60503263/react-hooks-how-to-target-an-element-child-with-useref-with-a-variable-decla){:target="\_blank"}
- [useRef는 처음이라 :: 개념부터 활용 예시까지](https://mnxmnz.vercel.app/react/what-is-use-ref/){:target="\_blank"}
