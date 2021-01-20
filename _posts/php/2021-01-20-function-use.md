---
title: "[PHP] function use"
description: "php function use 사용방법"
last_modified_at: 2021-01-20
categories:
  - php
tags:
  - function
---

PHP 함수에서 `use` 사용방법 정리<br><br>

```php
$msg = '안녕하세요';

$exp = function() {
    return $msg;
};

echo $exp(); // error
```
해당 코드는 에러가 발생합니다.  
PHP 함수는 외부변수를 사용할 수 없기 때문입니다.  
`use`를 사용하면 외부변수도 함수 안에서 사용할 수 있습니다.

<br>

```php
$msg = '안녕하세요';

$exp = function() use($msg) {
    return $msg;
};

echo $exp(); // 안녕하세요
```
이렇게 `use`를 사용하여 외부변수를 사용할 수 있습니다.  
`use`에 들어가는 변수값은 **함수선언시에** 설정되어있는 변수값이 들어가는 것이기 때문에 나중에 변수값을 변경하고 싶다면 <u>참조 연산자</u>를 사용해야 합니다. 

<br>

```php
$msg = '안녕하세요';

$exp = function() use($msg) {
    return $msg;
};

$msg = 'hello';

echo exp(); // 안녕하세요
```

```php
$msg = '안녕하세요';

$exp = function() use(&$msg) {
    return $msg;
};

$msg = 'hello';

echo exp(); // hello
```
첫 번째 경우를 보면 **$msg**값이 변경되지 않은것을 알 수 있습니다.   
두 번째 경우처럼 <u>참조 연산자</u>를 사용하면 나중에도 변수값을 변경할 수 있습니다.  
`변수명 앞에 '&' 붙이기`