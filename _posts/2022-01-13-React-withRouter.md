---
layout: post
title: "React withRouter"
# date: 2021-12-10 12:34:43 +0900
categories: React
---

## withRouter

- location, match, history의 기능을 사용하기 위해 사용한다.
  `import { withRouter } from 'react-router-dom';`
- 사용
  `const ShowPageInfo = withRouter(({ match, location }) => { return <div>현재 위치: {location.pathname}</div>;});`
- [참고자료](https://react-router.vlpt.us/1/05.html)
- [로그인 후 이전 페이지로 이동](https://velog.io/@ziyoonee/react-router-dom-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%ED%9B%84-%EC%9D%B4%EC%A0%84%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A1%9C-%EC%9D%B4%EB%8F%99%ED%95%98%EA%B8%B0)
