---
title: "웹브라우저에서 서버로 요청했을 때, 흐름"
description: "웹브라우저에서 서버로 요청했을 때, 흐름 Flow when requested from web browser to server"
search: true
toc: true
toc_sticky: true
comments: true
categories:
  - info
tags:
  - web
  - browser
last_modified_at: 2020-12-30
---

<!-- https://www.itworld.co.kr/news -->
<!-- https://aws.amazon.com/ko/events/builders-online-series/ -->

### 1. URL 입력하면 브라우저가 분석시작
인터넷은 쉽게 말하면 글로벌 케이블 네트워크다.
지구 전역의 모든 데이터를 전달하는 심해 케이블을 통해 세계가 연결되는 방법이다.
IP 주소를 이용하는 것이지 도메인네임을 이용하지 않는다.

URL 구조<br>
<a href="/assets/images/post/url-exp.png">
    <img src="/assets/images/post/url-exp.png" alt="URL 설명">
</a>

<br>
### 2. DNS 서버에 붙고, 도메의의 IP주소를 물어본다.
Root server - TLD server - Name server
<a href="/assets/images/post/dns-info.png">
    <img src="/assets/images/post/dns-info.png" alt="dns server 정보">
</a>

<br>
### 3. ARP를 통해 IP주소를 MAC주소로 변환
실질적인 통신을 하기 위해서는 **ARP**(Address Resolution Protocol)프로토콜을 이용하여 IP주소를 MAC주소로 변환

IP주소 : 논리적 주소 / 32bit<br>
MAC주소 : 물리적 주소 / 48bit 
{: .notice--info}

<br>
### 4. 대상 서버와 TCP 소켓 연결
3-way Handshaking<br>
연결하여 데이터를 전송하기 위해서 다음 3가지 과정을 거친다.

1 - 접속 요청 프로세스가 연결요청 메시지 전송 (SYN)<br>
2 - 접속 요청을 받은 프로세스가 수락 (SYN + ACK)<br>
3 - 마지막으로 접속 요청 프로세스가 수락 확인을 보내 연결을 맺음 (ACK)
{: .notice--info}

4-way Handshaking<br>
연결을 종료하기 위해서도 다음 4가지 과정을 거친다.

1 - 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송한다.<br>
2 - 서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAT 상태<br>
3 - 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN 플래그를 전송<br>
4 - 클라이언트는 확인했다는 메시지를 보냄
{: .notice--info}

<br>
### 5. HTTP(HTTPS) 프로토콜로 요청, 응답
Request, Response ...

<br>
### 6. 브라우저에서 응답을 해석
HTML, CSS, JavaScript ...

**그림으로 보자면..**
<a href="/assets/images/post/url-process.jpg">
    <img src="/assets/images/post/url-process.jpg" alt="URL 과정">
</a>

<br>
### 도메인은 어떻게 연결하나요?

① 도메인을 사이트에서 구매한다.<br>
② 도메인 네임서버를 설정한다.(기본은 도메인 구매사이트의 네임서버로 되어있을거임)<br>
③ 네임서버 홈페이지에서 A레코드와 CNAME을 설정한다<br>

**A레코드** : www.naver.com -> 23.201.36.188<br>
**CNAME** : aaa.naver.com -> www.naver.com -> 23.201.36.188<br>
**MX** : {id}@luvd.co.kr -> 메일플러그 MX값 -> 메일플러그 서버
{: .notice--info}




<!--
## CORS란 무엇인가요?

## 웹 서버와 웹 어플리케이션 서버(WAS)의 차이는 무엇인가요?

## REST API에 대해서 설명해 주세요.

## API Gateway란 무엇인가요?

## API Gateway가 다운되면 모든 API를 사용 못할지도 모르는데, 어떤 방안을 마련해야 할까요?
-->