---
layout: post
title: "[ES6] spread operator vs concat in merge to array"
date: 2021-12-26 20:34:43 +0900
categories: JS
---

### spread operator vs concat in merge to array

- many items에 single item을 합칠 때 : concat 사용
- single item에 many items를 합칠 때 : spread operator 사용
- concat은 string을 합칠 때, 하나의 string을 하나의 item으로 보지 않고, 한 글자씩 쪼개서 merge한다.

  ```
  a = [1, 2, 3]
  x = 'hello';

  console.log(a.concat(x));  // [ 1, 2, 3, 'hello' ]
  console.log([...a, ...x]); // [ 1, 2, 3, 'h', 'e', 'l', 'l', 'o' ]
  ```

  ```
  [...a, ...b] // bad :-(
  a.concat(b) // good :-)

  [x, y].concat(a) // bad :-(
  [x, y, ...a]    // good :-)
  ```
