---
layout: post
title: "[Web] 브라우저 렌더링 과정"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---
## 브라우저 렌더링 과정
1. Parsing : HTML 파일과 CSS 파일을 파싱해서 각각 DOM Tree, CSSOM Tree를 만든다.
    > 파싱 중 HTML에 CSS가 포함되어 있다면 CSSOM(CSS Object Model) Tree 구성 작업도 함께 진행한다.
2. Style : Parsing 단계에서 생성된 DOM Tree와 CSSOM Tree를 매칭시켜서 Render Tree를 구성한다
3. Layout : Rendering Tree에서 각 노드의 위치와 크기를 계산한다.
    > 만약 크기 값을 %로 지정하였다면, Layout 단계에서 % 값을 계산해서 픽셀 단위로 변환한다. 
4. Paint : 계산된 값을 이용해 각 노드를 화면상의 실제 픽셀로 변환하고, 레이어를 만든다.
    >  스타일이 복잡할수록 Paint 시간도 늘어난다. 예를 들어, 단색 배경의 경우 시간과 작업이 적게 필요하지만, 그림자 효과는 시간과 작업이 더 많이 필요하다.
5. Composite : Paint 단계에서 생성된 레이어를 합성하여 실제 화면에 나타낸다.

## 참고자료 출처
- [브라우저 렌더링 과정 이해하기](https://tecoble.techcourse.co.kr/post/2021-10-24-browser-rendering/){:target="\_blank"}
