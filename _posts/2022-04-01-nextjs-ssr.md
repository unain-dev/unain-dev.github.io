---
layout: post
title: "[Web] Next.js"
# date: 2021-12-10 12:34:43 +0900
categories: Web React.js
---

## Next.js
SSR을 쉽게 구현하도록 도와주는 프레임워크. 

Next.js는 React의 SSR(Server Side Rendering)을 쉽게 구현할 수 있게 도와주는 프레임워크다. 그렇다고 React에서 SSR이 불가능하다고 묻는다면, 대답은 'React에서도 구현 가능하다'이다. 하지만, React로 개발환경을 구현하는 것은 굉장히 복잡한 일이었다.  
(React와 Next.js의 차이를 경험해보기 위해 사전에 예제 코드를 적용하며 경험해 보았다...). 
이런 문제를 해결하기 위해 등장한 것이 바로 Next.js 되겠다.  

<br/>

## SSR과 SEO
결론부터 말하면, CSR에선 검색 엔진 최적화에 불리한 특징이 있으므로 SSR을 구현하여 검색 엔진 최적화를 하는데, 지금부터 검색 엔진 작동원리를 간단하게 알아보자.  

### 검색 엔진 작동원리
검색 엔진 봇들은 사이트의 데이터를 크롤링할 때, JavaScript 파일을 해석할 수 없다는 특징을 가졌다. 때문에 HTML 파일에서 크롤링을 하게 된다.  

- CSR방식은 Client 측에서 페이지를 구성하기 전까지 HTML에 아무것도 없으므로 데이터를 수집할 수 없는 상태이기 때문에 검색 엔진에 노출이 어렵다.
- SSR은 Server 측에서 화면을 그려서 보내주는 방식이다. 때문에 HTML 안에 이미 컨텐츠들을 포함하고 있는 상태이며, 크롤러 봇들이 데이터를 수집하는데 수월하다.

<br/>

## Next.js의 작동 원리
React는 SPA를 만들기 위한 라이브러리므로 CSR 방식을 채택한 SPA라고 할 수 있는데, React를 기반으로 한 Next.js에서 SSR을 구현할 수 있을까?  

### Next.js 작동 원리
> 1. 초기에 사용자가 Server에 페이지 접속을 요청하면, SSR방식으로 렌더링 될 HTML을 보냄.
> 2. 브라우저에서 JavaScript를 다운로드하고 React를 실행함.
> 3. 사용자, 페이지가 서로 상호작용하여 다른 페이지로 이동할 땐, Server가 아닌 CSR방식으로 브라우저에서 처리함.

<br/>

### 정리하면, 일석이조인 Next.js ?!
Next.js는 React를 기반으로 한 Framework이며, SSR를 구현하고 SEO에 유리하기 때문에 사용한다.  
Next.js는 Server에서 받은 사용자의 접속 요청을 초기에 SSR방식으로 렌더링 될 HTML을 보내고, 브라우저에서 JavaScript를 다운로드하고 React를 실행하기 때문에 SEO가 가능하다.  
또한 다른 페이지로 이동할 경우 CSR방식으로 Server가 아닌 브라우저에서 처리함으로써 SPA장점도 유지할 수 있다.

<br/>

## 정리
- Next.js를 사용하는 주된 이유는 SSR을 구현하기 위함이다.

- 초기에 SSR로 렌더링항 HTML을 보내기에 SEO에 유리해지고, 페이지를 변경할 때마다 CSR방식으로 처리하기 때문에 SPA장점도 유지할 수 있다.

- 코드 분할을 통해 초기 구동 속도를 빠르게 할 수 있다.

- Webpack 기반 환경을 통해 HMR을 적용하여 실시간 reload를 적용하는 등, 작업 환경을 커스터마이징하여 개발할 수 있다.

<br/>

## 참고자료 출처
- [Next.js를 사용하는 이유](https://ivorycode.tistory.com/19){:target="\_blank"}
