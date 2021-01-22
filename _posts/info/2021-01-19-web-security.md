---
title: "주요 웹 보안 취약점 정리"
description: "주요 웹 보안 취약점 정리"
last_modified_at: 2021-01-12
toc: true
toc_sticky: true
categories:
  - info 
tags:
  - web
  - security
---

**OWASP**(The Open Web Application Security Project - 국제 웹 보안 표준 기구) 에서 위험도가 높거나 발생 빈도가 높은 취약점 10가지 순위를 발표함.

## OWASP TOP 10
- A1 - Injection(인젝션)
- A2 - Broken Authentication and Session Management (인증 및 세션 관리 취약점)
- A3 - Sensitive Data Exposure (민감한 데이터 노출)
- A4 - XML External Entities (XXE) (XML 외부 개체 (XXE))
- A5 - Broken Access Control (취약한 접근 통제)
- A6 - Security Misconfiguration (잘못된 보안 구성)
- A7 - Cross-Site Scripting (XSS) (크로스 사이트 스크립팅 (XSS))
- A8 - Insecure Deserialization(안전하지 않은 역직렬화)
- A9 - Using Components with Known Vulnerabilities (알려진 취약점이 있는 구성요소 사용)
- A10 - Insufficient Logging & Monitoring(불충분한 로깅 및 모니터링)

#### A1. Injection
SQL, OS, XXE(Xml eXternal Entity), LDAP 인젝션 취약점은 신뢰할 수 없는 데이터가 명령어나 쿼리문의 일부분으로써, 인터프리터로 보내질 때 발생한다. 공격자의 악의적인 데이터는 예상하지 못하는 명령을 실행하거나 적절한 권한 없이 데이터에 접근하도록 인터프리터를 속일 수 있다.
<br><br>
```sql
SELECT * FROM admin where email = {email} and password = {password}
```
이러한 코드가 있을때 사용자는 아래처럼 파라미터를 보내 데이터에 바로 접글할수 있음 `'test' or 1=1`
```sql
SELECT * FROM admin where email = 'test' and password = 'test' or 1=1
```
<br>
**해결방법**
- 동적 쿼리 대신 parameter bind 사용..
- 서버단에서 SQL 특수문자 검증..
- LIMIT 같은걸 이용해서 제한두기..

#### A5. Broken Access Control
취약한 접근 제어는 인증된 사용자가 수행할 수 있는 것에 대한 제한이 제대로 적용되지 않는 것을 의미한다. 공격자는 이러한 취약점을 악용하여 사용자의 계정 액세스, 중요한 파일 보기, 사용자의 데이터 수정, 액세스 권한 변경 등과 같은 권한 없는 기능, 또는 데이터에 액세스할 수 있다.
<br><br>
```
http://example.com/admin/?role=user
http://example.com/bbs/view/12345
```
이런식으로 파라미터를 조작하고 URL을 탐색할수 있을때
```
http://example.com/admin/?role=admin
http://example.com/bbs/modify/12345
```
이렇게 권한에 접근 할 수 있는지 확인해 볼 수 있다.
<br><br>
**해결방법**
- 인증 프로세스를 잘 구축하자.. 


#### A7. XSS
XSS 취약점은 애플리케이션이 신뢰할 수 없는 데이터를 가져와 적절한 검증이나 제한 없이 웹 브라우저로 보낼 때 발생한다. XSS는 공격자가 피해자의 브라우저에 스크립트를 실행하여 사용자 세션 탈취, 웹 사이트 변조, 악의적인 사이트로 이동할 수 있다.
<br><br>

<a href="/assets/images/post/web-security-exp-1.png">
    <img src='/assets/images/post/web-security-exp-1.png'> 
</a>
<br>
게시판 등록같은 기능이 있을때 위에처럼 값이 그대로 DB에 들어가고
<br><br>
```html
{content}
```
이런식으로 화면에 저장된 값을 그대로 보여준다면
<br><br>
<a href="/assets/images/post/web-security-exp-2.png">
    <img src='/assets/images/post/web-security-exp-2.png'> 
</a>
<br>
스크립트가 그대로 실행됩니다. 이런식으로 스크립트가 실행되버리면 여러 이상한 짓을 할 수 있습니다.
<br><br>
**해결방법**
- XSS방어 라이브러리 사용..
- 보통 서버언어에 XSS방어해주는 함수가 있음..
- react 같은 프레임워크는 방어기능 있음..
- 엔티티로 인코딩해서 저장되도록.. `&lt;`

#### Cross-Site Request Forgery (CSRF)
사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격을 말한다.
<br><br>

```html
<form action="/password/modify">
    <input type="password" name="password">
    <input type="password" name="passwordCheck">    
</form>
```
이러한 비밀번호 변경 사이트가 있다고 했을때..
```
http://example.com/password/modify?password=1234&passwordCheck=1234
```
이렇게 요청하면 비밀번호가 변경된다는걸 유추 할 수 있다.  
```
<a href="http://example.com/password/modify?password=1234&passwordCheck=1234">클릭해봐</a>
```
게시판같은곳에 저런 a 태그를 등록하고 다른 사용자가 누른다면 자기의 의도와 상관없이 비밀번호가 변경될수 있다.
<br><br>
**해결방법**

Security Token
1. 사용자의 세션에 임의의 난수값을 저장하고 사용자의 요청에도 난수값을 넘겨줌
2. 서버에서 request 받을때 해당 난수값이 일치해야만 적상작동 하도록 셋팅
<br><br>
<a href="/assets/images/post/web-security-exp-3.png">
   <img src='/assets/images/post/web-security-exp-3.png'>
</a>
<br><br>
<a href="/assets/images/post/web-security-exp-4.png">
    <img src='/assets/images/post/web-security-exp-4.png'>
</a>
<br><br>
<a href="/assets/images/post/web-security-exp-5.png">
    <img src='/assets/images/post/web-security-exp-5.png'>
</a>
