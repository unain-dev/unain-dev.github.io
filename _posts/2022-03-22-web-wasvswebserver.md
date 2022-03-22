---
layout: post
title: "[Web] WAS vs WebServer"
# date: 2021-12-10 12:34:43 +0900
categories: Web
---

## Static Page & Dynamic Page
- Static Pages
  - Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.
  - 항상 동일한 페이지를 반환한다.
  - 정적 웹페이지(static web page)는 서버에 저장되어있는 HTML+CSS 파일 그대로 보여주는 것이다.
  - Ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 파일들
- Dynamic Pages
  - 인자의 내용에 맞게 동적인 contents를 반환한다.
  - 동적 웹페이지(dynamic web page)는 상황에 따라 서버에 저장되어있는 HTML에 데이터 추가/가공을 해서 보여주는 방법이다.
- Static Page vs Dynamic Page
  - 정적 웹페이지는 추가적인 통신&계산이 필요 없기 때문에 속도가 빠르고 서버에 부담이 적은 반면, 추가/수정/삭제 등 내용 변경이 필요할 때 HTML 자체를 수정해야 하기 때문에 번거롭다는 단점이 있다.
  - 동적 웹페이지는 한 페이지에서 상황/시간/사용자요청에 따라 다른 모습을 보여줄 수 있다는 장점이 있지만 상대적으로 보안에 취약하고 모습이 계속 변하기 때문에 (많은 경우 주소도 같이 변하죠!) 검색 엔진 최적화(search engine optimazation, SEO)가 어렵다.


## WebServer vs WAS
![image](https://user-images.githubusercontent.com/28949166/159486842-38c9764e-eb77-4d9e-acd6-eb90a0a4cfbe.png)
![image](https://user-images.githubusercontent.com/28949166/159488988-bd6cc440-f1c3-4017-9c67-397a4afa1d83.png)

### WebServer
> 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램

- Web Server의 기능
  > HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당한다.
요청에 따라 아래의 두 가지 기능 중 적절하게 선택하여 수행한다.
  1. 정적인 컨텐츠 제공.
      - WAS를 거치지 않고 바로 자원을 제공한다.
  2. 동적인 컨텐츠 제공을 위한 요청 전달
      - 클라이언트의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.
      - 클라이언트는 일반적으로 웹 브라우저를 의미한다.
- Web Server의 예
  > Ex) Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등

### WAS
- WAS의 개념
  - DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
  - HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다.
  - 데이터베이스의 조회나 다양한 로직 처리가 필요한 컨텐츠를 제공.
- WAS의 역할
  - WAS = Web Server + Web Container
  - Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시되었다.
  - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.
  - 주로 DB 서버와 같이 수행된다.
  - 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.
- WAS의 주요 기능
  - 프로그램 실행 환경과 DB 접속 기능 제공
  - 여러 개의 트랜잭션(논리적인 작업 단위) 관리 기능
  - 업무를 처리하는 비즈니스 로직 수행
- WAS의 예
  > Ex) Tomcat, JBoss, Jeus, Web Sphere 등

## 참고자료 출처

- [[Web] Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html){:target="\_blank"}
- [동적 웹 페이지란?](https://velog.io/@uvula6921/%EB%8F%99%EC%A0%81-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80%EB%9E%80){:target="\_blank"}
- [웹서버와 WAS 서버의 차이점을 알아보자](https://codechasseur.tistory.com/25){:target="\_blank"}
