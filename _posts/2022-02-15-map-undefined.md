---
layout: post
title: "React Error) Cannot read property 'map' of undefined"
# date: 2021-12-10 12:34:43 +0900
categories: React.js
---

## 문제 원인

- 리액트는 렌더링이 되어야 모든 효과를 실행하기 때문.
- 즉, 문제는 렌더링이 될 때 map 함수로 돌릴 대상(배열)이 할당되지 않아 대상을 찾지 못해 생기는 오류이다!

## 해결 방법

- map 함수로 돌릴 대상(배열)이 컴포넌트에 할당이 되면 그 다음에 렌더링이 되도록 한다.

```javascript
        return(
            <div>
                <h2>코로나 관련 뉴스<h2>
                <div className="news">
                    {articles && articles.map(item => {
                        return <p><a href={item.link}> {item.title} </a></p>;
                    })}
                </div>
            </div>
            );
```

## 참고자료 출처

- [문제상황 TypeError: Cannot read property 'map' of undefined](https://devbirdfeet.tistory.com/47){:target="\_blank"}
