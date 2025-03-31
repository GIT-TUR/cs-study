# HTTP 세션과 인증 메커니즘

## Session

- 일반적으로 HTTP는 Stateless한 성질을 가지고 있는데, 인증과 인가 같은 기능을 구현하기 위해 state를 저장할 방법이 필요함
- 이를 위해 Session이라는 개념을 도입
- Session을 구현하기 위해 다양한 방법이 존재하며, 대표적으로 Cookie가 있음

## 왜 Cookie인가?

- HTTP 메시지는 Header와 Body로 구성되어 있음
- Body는 데이터를 포함하지만, 네트워크 전송 중 MITM(Man-In-The-Middle) 공격 등 다양한 위협에 취약할 수 있음
- Header에는 Authorization과 같은 인증 관련 정보가 포함될 수 있지만, Header 기반 방식은 사용이 제한적이고 직접 관리하기 어려움
- 이에 비해 Cookie는 브라우저와 서버 간에 자동으로 전송되며, 다양한 보안 옵션을 제공하여 안전하게 상태 정보를 유지할 수 있음

## Cookie의 이점

### 자동 전송 및 관리

- 브라우저는 HTTP 요청 시 Cookie를 자동으로 포함하여 서버에 전송함
- 이로 인해 XSS, CSRF와 같은 공격이 문제가 될 수 있음
- 따라서 HttpOnly, Secure, SameSite와 같은 옵션을 통해 설정할 필요가 있음
- XSS: 스크립트를 실행해서 쿠키 정보를 빼냄
- CSRF: 쿠키 정보를 악용해서 서버에 요청을 보냄

### 쿠키 보안 옵션

- **HttpOnly**: HTTP 요청에서만 Cookie가 전송될 수 있음 (JavaScript에서 접근 불가)
- **Secure**: HTTPS 연결에서만 Cookie가 전송될 수 있음
- 의문: Secure하면 HttpOnly 안해도 되는 것 아닌가?
- HTTPS 연결이 되어도 스크립트 실행을 막을 수 없음. 따라서 같이 활용해야 함
- **SameSite**: 같은 사이트의 요청에만 쿠키가 포함되도록 함
- 같은 사이트의 기준은 Domain임
- SOP(Same-Origin Policy)의 Origin과 구별됨

> 참고: Cookie는 버전0과 버전1이 존재함
>
> - 버전1은 버전0의 확장
> - 중요한 내용은 아닌 것 같음

## Token에 대해서

- 일반적으로 Session 방식이라면 Client의 정보를 Server에서 어찌되었든 저장해야 함
- 예를 들어 SessionID는 Redis와 같은 저장소를 활용해서 저장하는 방식을 생각해볼 수 있음
- JWT가 대표적임. JWT를 활용하면 서버에서 상태를 가지고 있지 않아도 검증할 수 있음

### 단점

- 무상태라는 특성으로 인해 탈취될 경우 무효화를 구현하기 까다로움
- 따라서 JWT + Session을 혼합해서 사용하는 하이브리드 방식도 일반적으로 사용됨

## JWT에 대해서 알아보기

JWT는 Header, Payload, Signature로 구성됨:

1. **Header**는 typ, alg로 구성

- 예를 들어 일반적인 JWT 구성에 의하면 access와 refresh로 typ를 나누고
- 암호화 알고리즘을 선택(SHA-256 등)해서 alg를 구성함

2. **Payload**에는 식별을 위한 유저 정보가 들어있음

3. **JWT Signature**

- 앞의 두 인코딩된 정보와 점(.)을 포함해서 secret key를 추가해 해싱함
- 공식문서에 보면 위 내용은 `base64UrlEncode(header) + "." + base64UrlEncode(payload)`로 표현됨
- 주의할 점: base64로 인코딩되어 있으므로 암호화되지 않았다는 점을 인지해야 함
