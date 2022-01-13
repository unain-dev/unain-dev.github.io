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
