---
layout: post
title: "React Router V6 tutorial"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## React Router install

```
    npm intall react-router-dom --save
```

## Router 적용

1. index.js

   ```javascript
   import React from "react";
   import ReactDOM from "react-dom";
   import "./index.css";
   import App from "./App";
   import { BrowserRouter } from "react-router-dom";

   ReactDOM.render(
     <BrowserRouter>
       <App />
     </BrowserRouter>,
     document.getElementById("root")
   );
   ```

2. App.js(Route page)

   - 규칙

   > <Route path="주소규칙" element={보여 줄 컴포넌트 JSX} />

   - 예시

     ```javascript
     import { Route, Routes } from "react-router-dom";
     import About from "./pages/About";
     import Home from "./pages/Home";

     const App = () => {
       return (
         <Routes>
           <Route path="/" element={<Home />} />
           <Route path="/about" element={<About />} />
         </Routes>
       );
     };
     ```

## 참고자료 출처

- [React Router v6 튜토리얼](https://velog.io/@velopert/react-router-v6-tutorial){:target="\_blank"}
