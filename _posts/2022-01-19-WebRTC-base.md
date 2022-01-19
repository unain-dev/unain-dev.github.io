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

### 2번. 서로의 주소 공유

- 서버와 같은 중간자를 거치지 않고 브라우저 간 P2P로 연결하기 전! Peer 끼리의 정보를 교환할 때에는 서버가 필요하다! 그리고 그게 바로 2번 과정.
  ![image](https://user-images.githubusercontent.com/28949166/150143476-af17ea88-9c2a-4df9-9ef8-d51621080eff.png)
  - 주소 교환 : NAT(공유기)를 사용한 경우, 공인 IP를 여러개로 서브네팅해 분산시키므로 STUN 서버를 이용해서 주소를 알아내야한다. -> 만약, STUN으로 해결하지 못하는 경우, TURN 서버가 필요! -> Peer Connection Complete!

### 3번. 방화벽 우회

#### ICE

- 브라우저가 Peer를 통한 연결(2번)이 가능하도록 해주는 프레임워크.

- peer간 단순 연결 시 작동하지 않는 이유들
  1. 연결을 시도하는 방화벽을 통과해야 함
  2. 단말에 Public IP가 없다면 유일한 주소값을 할당해야 한다.
  3. 라우터가 peer간의 직접 연결을 허용하지 않을 때 데이터를 릴레이해야 하는 경우

> 이렇게 peer간 단순 연결을 허용하지 않을 때 STUN or TURN or 둘 다를 사용한다!

#### STUN

![image](https://user-images.githubusercontent.com/28949166/150144269-032520f7-b9f3-43e2-b4db-a07a95e03bce.png)

- 클라이언트 자신의 Public IP를 알려준다.
<!-- - 현재 다른 Peer가 클라이언트 자신으로 접근이 가능하도록 할건지 여부를 결정. -->
- 클라이언트는 인터넷을 통해 클라이언트의 Public Address와 라우터의 NAT 뒤에 있는 클라이언트가 접근 가능한지에 대한 답변을 STUN서버에 요청한다.

#### NAT

![image](https://user-images.githubusercontent.com/28949166/150144753-74b6b2a0-e354-4ece-98c2-460043b668b5.png)

- 단말에 Public IP 주소를 할당.
- Private IP를 Public IP와 Port로 번역한다.
  > 그러나, peer들이 오직 이전에 연결한 적 있는 연결들만 허용한다. 따라서 STUN서버에 의해 공개 IP주소를 발견한다고 해도 모두가 연결을 할수 있다는 것은 아니다.

#### TURN

![image](https://user-images.githubusercontent.com/28949166/150144801-de5e4684-ae8c-4491-bdbf-7dfb9434d433.png)

- TURN 서버와 연결해 모든 정보를 TURN 서버에 전달하도록해 Symmetric NAT 제한을 우회! -> 즉, STUN에서 막혀서 통신하지 못할 때 사용해야한다.
- TURN 서버와 연결하고, 모든 peer들이 저 서버에 모든 패킷을 보낸다음 TURN 서버에게 나에게 전달하라고 해야한다.

> TURN 서버를 사용하는 것은 오버헤드가 명확하게 존재하므로, 마지막 보루로 사용해야함!

## 참고자료 출처

- [1. WebRTC 정리하기](https://surprisecomputer.tistory.com/7?category=909008){:target="\_blank"}
- [WebRTC 파헤치기(1) - WebRTC 이론](https://velog.io/@happyjarban/WebRTC-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B01-WebRTC-%EC%9D%B4%EB%A1%A0){:target="\_blank"}
