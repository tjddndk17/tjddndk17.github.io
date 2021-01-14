---
title: "Request Content-Type"
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


### Content-Type

AJAX를 사용할때 Content-Type을 설정할수 있다.

**application/x-www-form-urlencode** (기본값)<br><br>
QueryString 형태로 보냄<br>
form으로 보내는것도 이 형식이다
{: .notice--info}

**application/json**<br><br>
JSON 형태로 보냄<br>
JSON.stringify(data) 로 JSON타입으로 바꾼후 전송필요
{: .notice--info}

서버쪽에서는 Content-Type에 따라 받는 방식이 달라진다.
