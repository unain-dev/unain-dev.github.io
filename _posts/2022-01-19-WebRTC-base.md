---
layout: post
title: "Web RTC 개념"
# date: 2021-12-10 12:34:43 +0900
categories: Web RTC
---

## Web RTC

### Web RTC란?

- 웹 브라우저만 있으면, 별도의 설치 없이 리얼타임 커뮤니케이션이 가능할 수 있게 만들어주는 기술.
- 리얼타임에 근사한 라이브 스트리밍 포맷.
- JS API로 제공되는, P2P간 실시간 전송이 되도록 지원하는 오픈소스.
- 서버와 같은 중간자를 거치지 않고 브라우저 간을 P2P로 연결하는 기술.서버와 같은 중간자를 거치지 않고 브라우저 간을 P2P로 연결하는 기술

### Web RTC 동작 원리

![image](https://user-images.githubusercontent.com/28949166/150143357-af6b8c96-8032-418a-adf4-bf8d0a6b3588.png)

1. 각 브라우저 P2P 커뮤니케이션
2. 서로의 주소 공유
3. 보안 사항 및 방화벽 우회
4. 실시간 데이터 공유

- 서버와 같은 중간자를 거치지 않고 브라우저 간 P2P로 연결하기 전! Peer 끼리의 정보를 교환할 때에는 서버가 필요하다! 그리고 그게 바로 2번 과정.
  ![image](https://user-images.githubusercontent.com/28949166/150143476-af17ea88-9c2a-4df9-9ef8-d51621080eff.png)
  - 주소 교환 : NAT(공유기)를 사용한 경우, 공인 IP를 여러개로 서브네팅해 분산시키므로 STUN 서버를 이용해서 주소를 알아내야한다. -> 만약, STUN으로 해결하지 못하는 경우, TURN 서버가 필요! -> Peer Connection Complete!

## 참고자료 출처

- [1. WebRTC 정리하기](https://surprisecomputer.tistory.com/7?category=909008){:target="\_blank"}
- [WebRTC 파헤치기(1) - WebRTC 이론](https://velog.io/@happyjarban/WebRTC-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B01-WebRTC-%EC%9D%B4%EB%A1%A0){:target="\_blank"}
