---
title:  "[기술면접 질문] 웹"
search: true
last_modified_at: 2020-12-30
categories:
  - tech-interview
tags:
  - web
toc: true
toc_sticky: true
---

## 웹브라우저에서 서버로 요청했을 때, 흐름을 설명해주세요.

###### 1. URL 입력하면 브라우저가 분석시작
인터넷은 쉽게 말하면 글로벌 케이블 네트워크다
지구 전역의 모든 데이터를 전달하는 심해 케이블을 통해 세계가 연결되는 방법이다.
IP 주소를 이용하는 것이지 도메인네임을 이용하지 않는다.

###### 2. DNS 서버에 붙고, 도메의의 IP주소를 물어본다.
Root server - TLD server - Authoriative server

###### 3. ARP를 통해 IP주소를 MAC주소로 변환
실질적인 통신을 하기 위해서는 논리 주소인 IP주소를 물리 주소인 MAC 주소로 변환

###### 4. 대상 서버와 TCP 소켓 연결
3-way Handshaking<br>
4-way Handshaking

###### 5. HTTP(HTTPS) 프로토콜로 요청, 응답
Request, Response ...

###### 6. 브라우저에서 응답을 해석
HTML, CSS, JavaScript ...

<a href="https://deveric.tistory.com/97" target="_blank">https://deveric.tistory.com/97</a>

<a href="/assets/images/post/url-exp.png">
    <img src="/assets/images/post/url-exp.png" alt="URL 설명">
</a>

<a href="/assets/images/post/url-process.jpg">
    <img src="/assets/images/post/url-process.jpg" alt="URL 과정">
</a>



## CORS란 무엇인가요?


## 웹 서버와 웹 어플리케이션 서버(WAS)의 차이는 무엇인가요?


## REST API에 대해서 설명해 주세요.


## API Gateway란 무엇인가요?


## API Gateway가 다운되면 모든 API를 사용 못할지도 모르는데, 어떤 방안을 마련해야 할까요?
