#JSON Web Tokens (JWT)

## Definition
```
A JSON Web Token (JWT) is a JSON object that is defined in RFC 7519 as a safe way 
to represent a set of information between two parties. 
The token is composed of a header, a payload, and a signature.
```
- JWT 시스템에서 발급된 토큰은, 토큰에 대한 정보와 전달할 정보, 그리고 토큰에 대한 signature를 포함한다. 
- 이런 토큰은 서버와의 통신에서 HTTP헤더나, url파라미터로 쉽게 전달된다.

## The Reason why using JWT
- Authorization : 유저가 로그인을 하면, 서버는 유저의 정보를 바탕으로 토큰을 발급하여 유저에게 전달. 유저는 서버에 요청을 할때마다 발급받은 JWT를 같이 서버로 보낸다.
서버는 전달 받은 JWT를 검증하고 유저의 요청에 대한 권한체크 후 작업을 처리한다. 이런 방식을 사용하면, 서버는 유저의 세션을 유지 할 필요가 없이,
토큰에 대한 검증만을 바탕으로 유저의 요청에 대한 처리를 하면 되므로 서버자원을 아낄 수 있다.

- Information Exchange: : JWT public/private key방식으로 signature되어 있으므로 안정성있게 정보를 교환하기에 좋은 방법. 

## Structure of JWT
```
header.payload.signature
```
It should be noted that a double quoted string is actually considered a valid JSON object.

### Header
```
{
  "typ": "JWT",
  "alg": "HS256"
}
```
- typ : 토큰 타입을 지정.
- alg : 해싱 알고리즘을 지정하며, 주로 HMAC SHA256 혹은 RSA 가 사용된다. 토큰 검증을 위한 signature에서 사용

### Payload
```
{
    "userId": "b08f86af-35da-48f2-8fab-cef3904660bd"
}
```
- payload에서 각각의 데이터(프로퍼티)는 "claims"라고 명시된다.
- payload에 클레임은 원하는 만큼 추가 가능하나, 비례해서 사이즈가 커짐을 유의한다.
- payload는 암호화(encrypted)가 되는게 아닌. encoded되는 것이므로 password등의 정보를 추가하진 않아야한다.

### Signature
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
- Header, Payload 정보를 "."으로 이어서 인코딩을 한다.

### Putting all Together
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJ2ZWxvcGVydC5jb20iLCJleHAiOiIxNDg1MjcwMDAwMDAwIiwiaHR0cHM6Ly92ZWxvcGVydC5jb20vand0X2NsYWltcy9pc19hZG1pbiI6dHJ1ZSwidXNlcklkIjoiMTEwMjgzNzM3MjcxMDIiLCJ1c2VybmFtZSI6InZlbG9wZXJ0In0.WE5fMufM0NDSVGJ8cAolXGkyB5RmYwCto1pQwDIqo2w
```

- 각 단계에서 생성된 데이터를 인코딩하여 .으로 이어준다.


## How does JWT protect our data?
- JWT의 목적은 데이터를 숨기거나 보호하는게 아니라 인증된 정보가 제대로 주고 받아졌는지를 검증하는 것이다.
- JWT는 데이터를 암호화가 아닌 인코딩을 하여 두 개체간에 서로 올바른 데이터가 주고 받아졌는지를 확인한다.


# TOKEN
API를 이용하는 웹서비스에서 token기반 인증 방식이 많이 사용된다.

## 토큰 사용 이유
- Stateless 서버 : 세션을 사용하여 stateful 하게 유저 정보를 서버에 저장하여, 클라이언트의 요청을 받을때마다 인증하여 처리하는 방식은 메모리 혹은 데이터베이스에 많은 자원을 소비하게 된다. 반면 token방식으로 stateless서버를 사용하면 유저의 요청을 인증을 통하여 처리하므로 서버의 확장성 (Scalability) 이 높아진다.

- 모바일 어플리케이션에 적합 : 모바일에서는 쿠키등을 통한 인증보다는 토큰을 이용한 인증이 이상적이다.
- 인증정보를 다른 어플리케이션으로 전달 : OAuth등과 같은 인증정보를 다른 웹서비스에 공유하여 사용 가능하다.( 페이스북/구글 같은 sns 인증정보 공유 )

## 서버기반 인증의 문제
-  유저가 인증을 할 때에는, 서버에 저장된 세션정보를 바탕으로 이루어진다. 대부분의 경우에는 메모리에 저장하며 유저의 수가 늘어남에 따라 서버에 부담이 된다.
- 확장을 위해 서버나 데이터베이스를 분산하거나 여러대의 서버를 사용하게 되면, 세션 정보를 이러한 분산시스템에 싱크 되도록 설계해야하며, 이는 어려움을 야기시킨다.
- 쿠키는 단일 도메인 및 서브 도메인에서만 사용 가능하며, 웹 어플리케이션 세션을 여러 도메인에서 공용으로 사용하려하면 CORS (Cross-Origin Resource Sharing)문제가 생긴다.


## 토큰 기반 시스템 작동 원리
- 유저가 로그인을 시도하면, 서버는 이 정보를 검증하고 signed된 토큰을 발급하여 클라이언트로 보낸다.
- 유저는 이 토큰을 저장해두고, 서버에 요청을 할 때마다 HTTP 헤더에 토큰값을 포함시켜서 전달한다.
- 서버는 이 토큰값을 검증하고, 요청에 응답한다.



Referencing

[https://velopert.com/2350](https://velopert.com/2350)

[https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec](https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec)