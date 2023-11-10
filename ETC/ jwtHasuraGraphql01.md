# JWT 프런트엔드 클라이언트에서 처리 (GraphQL)

<h1>JWT란?</h1>

JWT에 대한 자세한 기술 설명은 이 문서를 참조하세요 .

인증을 위해 JWT는 서버에서 발급한 토큰입니다.<br/>
토큰에는 사용자별 정보가 포함된 JSON Payload가 있습니다.<br/>
이 토큰은 클라이언트가 API와 통신할 때(HTTP 헤더로 전송하여) API가 토큰으로 표시되는 사용자를 식별하고 사용자별 작업을 수행할 수 있도록 사용할 수 있습니다.

<h1>JWT 구조</h1>

JWT가 직렬화되면 다음과 같습니다.<br/>
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.XbPfbIHMI6arZ3Y922BhjWgQzWXcXNrz0ogtVhfEd2oM<br/>

해당 base64를 디코딩하면(https://jwt.io/#debugger-io), Header, Payload, Signature로 구성된 JSON을 얻게 됩니다.

직렬화된 형식은 다음 형식입니다.

```
[ base64UrlEncode(header) ] . [ base64UrlEncode(payload) ] . [ signature ]
```

 JWT는 암호화되지 않습니다. 이는 64 기반으로 인코딩되고 서명됩니다.<br/>
 따라서 누구나 토큰을 디코딩하고 해당 데이터를 사용할 수 있습니다.<br/>
 JWT의 서명은 그것이 실제로 합법적인 소스에서 나온 것인지 확인하는 데 사용됩니다.

 <h2>로그인</h2>

로그인 프로세스는 일반적으로 수행하는 프로세스와 실제로 변경되지 않습니다.<br/>
예를 들어, 인증 엔드포인트에 사용자 이름/비밀번호를 제출하고 응답에서 JWT 토큰을 가져오는 로그인 양식은 다음과 같습니다.<br/>
이는 외부 공급자를 통한 로그인, OAuth 또는 OAuth2 단계일 수 있습니다.<br/>
클라이언트가 최종 로그인 성공 단계의 응답으로 최종적으로 JWT 토큰을 얻는 한 실제로는 중요하지 않습니다.<br/>

먼저, 로그인 서버에 사용자 이름과 비밀번호를 보내는 간단한 로그인 양식을 작성하겠습니다.<br/>
서버는 JWT 토큰을 발행하고 이를 메모리에 저장합니다.<br/>
이 튜토리얼에서는 인증 서버 백엔드에 중점을 두지 않지만 이 블로그 게시물의 예제 저장소에서 확인해 보세요.

handleSubmit 로그인 버튼의 핸들러는 다음과 같습니다.

```ts
async function handleSubmit () {
  //...
  // Make the login API call
  const response = await fetch(`/auth/login`, {
    method: 'POST',
    body: JSON.stringify({ username, password })
  })
  //...
  // Extract the JWT from the response
  const { jwt_token } = await response.json()
  //...
  // Do something the token in the login method
  await login({ jwt_token })
}
```

로그인 API는 토큰을 반환 한 다음 이 토큰을 일단 얻은 토큰으로 무엇을 할지 결정할 수 있는 login함수 에 이 토큰을 전달합니다. /utils/auth

```ts
import { login } from '../utils/auth'
await login({ jwt_token })
```

이제 토큰이 생겼는데 localstorage 에 보관하면 안됩니다. 보안에 취약합니다.

쿠키에 저장하는 방법도 좋지 않습니다.

JWT를 저장하기 위해 클라이언트에서 쿠키를 만드는 것도 XSS에 취약합니다.<br/>
앱 외부의 Javascript를 통해 클라이언트에서 읽을 수 있는 경우 도난당할 수 있습니다.<br/>
HttpOnly 쿠키(클라이언트 대신 서버에 의해 생성됨)가 도움이 될 것이라고 생각할 수도 있지만 쿠키는 CSRF 공격 에 취약합니다.<br/>
HttpOnly 및 합리적인 CORS 정책은 CSRF 양식 제출 공격을 방지할 수 없으며 쿠키를 사용하려면 적절한 CSRF 완화 전략이 필요하다는 점에 유의하는 것이 중요합니다.

SameSite cookie는 쿠키 기반 접근 방식을 CSRF 공격으로부터 안전하게 만들어줍니다.<br/>
인증 서버와 API 서버가 서로 다른 도메인에서 호스팅되는 경우 솔루션이 아닐 수도 있지만 그렇지 않은 경우에는 정말 잘 작동합니다.

<h2>토큰을 저장하는곳</h2>

The OWASP JWT Cheatsheet and OWASP ASVS (Application Security Verification Standard) prescribe guidelines for handling and storing tokens.<br/>
OWASP JWT 치트시트 및 OWASP ASVS(애플리케이션 보안 검증 표준)는 토큰 처리 및 저장에 대한 지침을 규정합니다.

https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.md<br/>
https://github.com/OWASP/ASVS

이와 관련된 섹션은 JWT Cheatsheet의 Token Storage on Client Side 이슈와 ASVS의 3장 및 8 장입니다. Token SidejackingSession ManagementData Protection

"이는 애플리케이션이 다음 동작을 나타내는 방식으로 토큰을 저장할 때 발생합니다."

```
브라우저(쿠키 저장)에 의해 자동으로 전송됩니다.
브라우저를 다시 시작해도 검색됩니다(브라우저 localStorage 컨테이너 사용).
XSS 문제(JavaScript 코드에 액세스할 수 있는 쿠키 또는 브라우저 로컬/세션 저장소에 저장된 토큰)가 있는 경우 검색됩니다.
```

예방방법

```
브라우저 sessionStorage 컨테이너를 사용하여 토큰을 저장합니다.
서비스를 호출할 때 JavaScript를 사용하여 Bearer HTTP 헤더로 추가합니다 Authentication.
finger print토큰에 정보를 추가합니다 .
```

브라우저 sessionStorage 컨테이너에 토큰을 저장하면 XSS 공격을 통해 토큰이 도난당할 수 있습니다.<br/>
그러나 토큰에 추가된 지문은 공격자가 자신의 컴퓨터에서 훔친 토큰을 재사용하는 것을 방지합니다.<br/>
공격자의 악용 표면을 최대한 차단하려면 브라우저를 추가하여 Content Security Policy 컨텍스트를 강화하세요.

fingerprint 문제 에서 다음 지침을 구현하는 경우는 다음과 같습니다 Token Sidejacking.

징후

```
이 공격은 공격자가 토큰을 가로채거나 도난당하고 이를 사용하여 대상 사용자 ID를 사용하여 시스템에 액세스할 때 발생합니다.
```

예방하는 방법

이를 방지하는 방법은 토큰에 "user context"를 추가하는 것입니다. 사용자 컨텍스트는 다음 정보로 구성됩니다.

```
인증 단계에서 생성되는 임의의 문자열입니다.
HttpOnly는 강화된 쿠키(플래그: + Secure+ + 쿠키 접두사) 로 클라이언트에 전송됩니다.
임의 문자열의 SHA256 해시는 공격자가 임의 문자열 값을 읽고 예상 쿠키를 설정할 수 있는 XSS 문제를 방지하기 위해 원시 값 대신 토큰에 저장됩니다.
```

동일한 세션 중에 IP 주소가 변경될 수 있는 합법적인 상황이 있으므로 IP 주소를 사용해서는 안 됩니다.<br/>
예를 들어, 사용자가 모바일 장치를 통해 애플리케이션에 액세스하고 교환 중에 이동통신사가 변경되면 IP 주소가 (종종) 변경될 수 있습니다.<br/>
또한 IP 주소를 사용하면 유럽 GDPR 규정 준수에 문제가 발생할 가능성이 있습니다.

토큰 검증 중에 수신된 토큰에 올바른 컨텍스트가 포함되어 있지 않으면 거부되어야 합니다.