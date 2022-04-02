---
layout: post
title: "[React] filter와 map의 혼합 사용"
categories: React.js ES6
---

## 문제 상황
- props로 내려오는 인자 중 조건에 해당하는 몇가지만 필터링해 map으로 컴포넌트 반복을 시켜야 함.
- 그러나, filter 함수는 컴포넌트로 리턴이 불가.
- 그런데 export 컴포넌트 function 내에서 if(..){...}으로 해주면 렌더링이 매번 일어나기 때문에 too may re-render 오류가 발생!
- 그래서 filter와 map을 혼합해서 사용.


## 해결 예시

```javascript
import React from "react";
import Img from "../../atoms/Img/Img/Img";
import InfoText from "../../atoms/Text/InfoText/InfoText";

...

const LongGameCard = ({ info, onClick }) => {
  return (
    <div onClick={onClick}>
      <div>
        {info.genres
          .filter((g, index) => index < 3)
          .map((genre, index) => (
            <TagText key={index} size="small">
              #{genre}
            </TagText>
          ))}
      </div>
    </div>
  );
};

export default LongGameCard;

```
