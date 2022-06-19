---
layout: post
title: "[React] dependencies vs devDependencies"
categories: React.js
---
## dependencies vs devDependencies
- dependencies: 프로덕션 환경에서 응용 프로그램에 필요한 패키지.
- devDependencies: 로컬 개발 및 테스트에만 필요한 패키지.

## 설치
- dependencies: `npm install 라이브러리명`
- devDependencies: `npm install 라이브러리명 --save-dev` 혹은 `npm install 라이브러리명 -D`

## 둘을 구분하는 이유
이렇게 구분해주는 이유는 결국 배포할 때 어떤 라이브러리가 포함될 것인가를 명시적으로 하기 위해서.

dependencies 에 설치된 라이브러리는 배포할 때 포함되지만 devDependencies 에 설치된 라이브러리는 개발할 때 필요한 라이브러리기 때문에 배포할 때 포함되지는 않음.

이렇게 잘 구분을 해서 설치해줘야 빌드시간도 줄이고, 배포할 때 불필요한 라이브러리를 포함시키지 않아도 됨.

## 참고자료 출처
- [dependencies와 devDependencies 차이](https://velog.io/@vewevteen/dependencies%EC%99%80-devDependencies-%EC%B0%A8%EC%9D%B4){:target="\_blank"}
- [dependencies 와 devDependencies 차이](https://www.codeit.kr/community/threads/29051){:target="\_blank"}
