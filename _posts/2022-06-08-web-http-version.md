---
layout: post
title: "[Web] HTTP 1.1 vs 2.0"
categories: Web
---
## HTTP 1.1 특징
- Connection 한 개당 하나의 요청을 처리하도록 설계됨

    -> 동시에 리소스를 주고 받는 것이 불가능
    
    -> 요청과 응답이 순차적으로 이루어짐
    
    -> HTTP 문서 내에 포함된 다수의 리소스(image, css, script)를 처리하려면 요청할 리소스의 개수에 비례하여 Latency(대기시간)이 길어짐
- HOL(Head Of Line) Blocking이 발생할 수 있다.
    HOL 블로킹이란 네트워크에서 같은 큐에 있는 패킷이 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상을 말한다.
- RTT(Round Trip Time) 증가
   Connection 하나에 요청 한 개를 처리하는 특성때문에 매번 요청 별로 Connection을 만들게 되고 TCP상에서 동작하는 HTTP의 특성상 3-way handshake가 반복적으로 일어나며, 불필요한 RTT 증가와 네트워크 지연을 초래하여 성능을 지연시킨다.
- 무거운 Header 구조
    매 요청마다 중복된 헤더 값을 전송하게 되며, 서버 도메인에 관련된 쿠키 정보도 헤더에 함께 포함되어 전송된다. 이러한 반복적인 헤더 전송, 쿠키 정보로 인해 헤더 크기가 증가한다.

### HTTP1.1 개선방법
1. Image Spriting

    웹 페이지를 구성하는 다양한 아이콘 이미지 파일의 요청 횟수를 줄이기 위해 아이콘을 하나의 큰 이미지로 만든 다음 CSS에서 해당 이미지의 좌표 값을 지정하여 표시하는 방법이다.

2. Domain Sharding
  
    브라우저들이 HTTP1.1의 단점을 극복하기 위해 여러 개의 Connection을 생성해서 병렬로 요청을 보내기도 한다. 하지만 브라우저 별로 도메인당 Connection 개수 제한이 존재하기 때문에 근복적인 해결은 어렵다.

3. Minified CSS/Javascript
  
    HTTP를 통해 전송되는 데이터의 용량을 줄이기 위해 CSS, Javascript를 축소한다. (ex. name.min.js)

4. Load Faster
  
    head 태그에 자바스크립트를 삽입하고 async나 defer 옵션을 사용해 브라우저의 파싱을 block 하지 않고 로드한다.

5. Data URI Scheme
  
    HTML 문서 내 이미지 리소스를 Base64로 인코딩된 이미지 데이터로 직접 기술하는 방법으로, 서버로의 요청을 줄인다.

6. 구글의 SPDY
  
    위에서 언급된 노력들로는 근본적인 단점을 해결할 수 없었다. 그래서 구글은 더 빠른 웹을 실행하기 위해 Throughtput 관점이 아닌 Latency 관점에서 HTTP를 고속화한 SPDY(스피티)라 불리는 새로운 프로토콜을 구현했다.
  
    다만 SPDY는 HTTP를 대체하는 프로토콜이 아니고 HTTP를 통한 전송을 재정의하는 형태로 구현되었다. 이는 HTTP2.0 초안의 참고 규격이 된다.

## HTTP 2.0 특징
![image](https://user-images.githubusercontent.com/28949166/172598927-9204bb9b-4557-41b5-8989-ef29e3b1ee3e.png)

> HTTP2.0은 HTTP1.1을 완전하게 재작성한 것이 아니라 프로토콜의 성능에 초첨을 맞춰 수정한 버전이라고 생각하면 된다. 특히 End-user가 느끼는 Latency나 네트워크, 서버 리소스 사용량 등과 같은 성능 위주로 개선되었다.

- Multiplexed Streams
    
    connection 한 개로 동시에 여러 개의 메시지를 주고 받을 수 있으며, 응답은 순서에 상관없이 stream으로 주고 받는다.

- Stream Prioritization

  리소스 간의 의존관계에 따른 우선순위를 설정하여 리소스 로드 문제를 해결함
  
  ex. 문서 내에 CSS파일 1개와 이미지 파일 2개가 존재하고 이를 클라리언트가 요청하는 상황에서 이미지 파일보다 CSS 파일의 수신이 늦어진다면 렌더링에 문제가 생기게 되는데 이를 해결함.

- Server Push

    클라이언트가 요청하지 않은 리소스를 서버가 사전에 푸쉬를 통해 전송할 수 있다.
    
    ex. 푸쉬가 가능하면 클라이언트가 추후에 HTML문서를 요청할 때 해당 문서 내의 리소스를 사전에 클라이언트에서 다운로드할 수 있도록 하여 클라이언트의 요청을 최소화할 수 있음

- Header Compression
    
    헤더 정보를 HPACK 방식으로 압축한다.

## 참고자료 출처
- [HTTP1.1과 HTTP2.0의 차이](https://velog.io/@wiostz98kr/HTTP1.1%EA%B3%BC-HTTP2.0%EC%9D%98-%EC%B0%A8%EC%9D%B4-e2v4x4t1){:target="\_blank"}
