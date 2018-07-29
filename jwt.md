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

