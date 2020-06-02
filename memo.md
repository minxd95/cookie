# NodeJs 에서의 Cookie

## 쿠키의 생성

```javascript
res.writeHead(200, {
  // 객체형태의 인자로 헤더값을 넘겨준다.
  "Set-Cookie": [
    // Set-Cookie : 헤더에서 쿠키를 전달하는 속성
    "yummy_cookie=choco",
    "tasty_cookie=strawberry", // Session 쿠키(웹브라우저 종료시 소멸)
  ],
});
```

## 쿠키 사용하기

parsing 모듈 설치

```
npm install cookie
```

소스코드

```javascript
const http = require("http");
const cookie = require("cookie"); // 모듈 임포트
const app = http.createServer((req, res) => {
  let cookies = {};

  if (req.headers.cookie != undefined)
    // 쿠키가 있으면
    cookies = cookie.parse(req.headers.cookie); // cookie 모듈을 이용해여 parsing
  console.log(cookies.yummy_cookie); // parsing 된 객체를 [.쿠키명] 하여 사용

  /*              생략             */
});
app.listen(3000);
```

## 쿠키의 옵션

Permanent Cookie : 지정한 기간동안 쿠키 생존

Max-Age(초), Expires(구체적 날짜)

```javascript
`Permanent=cookies; Max-Age=${60 * 60 * 24 * 30}`;
```

Secure : https 를 이용한 통신에서만 쿠키를 서버로 전송

```javascript
`Secure=Secure; Secure`;
```

HttpOnly : 웹브라우저와 서버간의 통신에서만 쿠키 제어 가능

```javascript
`HttpOnly=HttpOnly; HttpOnly`;
```

Path : 해당되는 경로에서만 쿠키를 서버로 전송

```javascript
`Path=Path; Path=/cookie`;
```

Domain : 어떤 도메인에서 동작할 것인가
ex) o2.org 의 모든 서브 도메인에서도 살아 남는다.

```javascript
`Domain=Domain; Domain=o2.org`;
```
