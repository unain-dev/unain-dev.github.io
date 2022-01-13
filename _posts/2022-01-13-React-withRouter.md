---
layout: post
title: "React withRouter, history 사용"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## withRouter

- location, match, history의 기능을 사용하기 위해 사용한다.
  `import { withRouter } from 'react-router-dom';`
- 사용
  `const ShowPageInfo = withRouter(({ match, location }) => { return <div>현재 위치: {location.pathname}</div>;});`
- [참고자료](https://react-router.vlpt.us/1/05.html)
- [react에서 history 사용](https://meanbymin.tistory.com/132)
- [CRA, React Router dom를 이용하여 이전 페이지로 이동하기](https://velog.io/@leemember/React-Router-dom%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%EC%9D%B4%EC%A0%84-%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A1%9C-%EC%9D%B4%EB%8F%99%ED%95%98%EA%B8%B0)
  > 이 방법을 사용함.
- [로그인 후 이전 페이지로 이동](https://velog.io/@ziyoonee/react-router-dom-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%ED%9B%84-%EC%9D%B4%EC%A0%84%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A1%9C-%EC%9D%B4%EB%8F%99%ED%95%98%EA%B8%B0)
