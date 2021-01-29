---
title: "[JavaScript] Request Content-Type"
description: "Request content-type"
search: true
comments: true
categories:
  - info
tags:
  - request
  - content-type
last_modified_at: 2021-01-12
---


## Content-Type
AJAX를 사용할때 Content-Type을 설정할수 있다.
<br>
<br>
```javascript
$.ajax({
    url: url,
    data: data,
    contentType: 'application/x-www-form-urlencoded; charset=UTF-8'
})
```
contentType의 default값 이며, QueryString 형태로 데이터 전송. <form>으로 보내는 것도 이 형식.
<br>
<br>
```javascript
$.ajax({
    url: url,
    data: JSON.stringify(data),
    contentType: 'application/json; charset=UTF-8'
})
```
JSON 형태로 데이터전송, JSON.stringify(data) 로 JSON타입으로 바꾼후 전송필요
<br>
<br>

서버단 에서는 Content-Type에 따라 받는 방식이 달라진다.
{: .notice--info}
