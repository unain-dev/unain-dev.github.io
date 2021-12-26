---
layout: post
title: "useState setState 일부만 상태 업데이트하기"
date: 2021-12-26 20:34:43 +0900
categories: ES6
---

### useState setState 일부만 상태 업데이트하기

- spread operator를 사용한다.

  ```
  const [state, setState] = useState({
    history: [
      {
        squares: Array(9).fill(null),
      },
    ],
    stepNumber: 0,
    xIsNext: true,
  });

  function jumpTo(step) {
    setState({
      //   history: state.history, // 이 라인 삭제시 오류
      ...state, // 바로 윗 라인 history : state.history와 같은 뜻. spread operator
      stepNumber: step,
      xIsNext: step % 2 === 0,
    });
  }
  ```
