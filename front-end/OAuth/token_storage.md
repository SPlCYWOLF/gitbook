# 🐧 Token storage

[ref 1](https://blog.bitsrc.io/sessionstorage-and-localstorage-a-ux-security-comparison-a05c486413e0) ,   [ref 2](https://www.youtube.com/watch?v=occfnVaZOXI) ,   [ref 3](https://auth0.com/docs/secure/security-guidance/data-security/token-storage) ,    [ref4](https://community.auth0.com/t/why-is-storing-tokens-in-memory-recommended/17742) ,   [ref5](https://blog.ropnop.com/storing-tokens-in-browser/#global-variable:~:text=or%20new%20page-,Closure%20Variable,-PoC%20Page%3A) ,   [ref6](https://dev-dain.tistory.com/m/46#:~:text=%EC%82%AC%EC%9D%B4%ED%8A%B8%20%EC%83%9D%EC%84%B1%EA%B8%B0%EC%99%80%20%EC%B0%B0%EB%96%A1%EA%B6%81%ED%95%A9%EC%9D%B4%EB%8B%A4.-,SPA%20%EA%B5%AC%ED%98%84%20%EB%B0%A9%EC%8B%9D%EB%93%A4,-SPA%20%EA%B5%AC%ED%98%84%20%EB%B0%A9%EC%8B%9D%EC%9D%80)

---

*토큰 = 액세스 토큰

## 1. store in the Cookie

- 자동으로 `request`와 함께 보내진다 -> `authorization header` 신경 안써도 된다 -> 구현 상대적으로 간편.
- `Cross-site-request-forgery`에 취약하다.
  - 이에 대한 해결책 :
    1. `csrf token` 활용
       - `request`마다 새롭게 생생되어 쿠키와 함께 보내지는 랜덤 문자열.

    2. `http only flag` 활용
       - 특정 데이터를 `server-side`에서만 열람 가능하게 만듬.
         고로, `JS document`의 쿠키 `api`에 접근 불가능하게 만듬.


<br>

## 2. store in the Local storage

- 로컬 스토리지와 세션 스토리지 중 선택 가능.
- 쿠키와는 다르게 특정 도메인에 종속되어있음.
  고로, 서브도메인을 포함한 타 도메인으로부터 접근 불가능.
  고로, `csrf` 에 내성이 있음.
- 하지만 `cross-site-scripting` 에는 노출되어있음.
  - 이에 대한 해결책 :
    1. 저장 전에 추가적으로 토큰 암호화 -> but.. 해독과정에 추가 토큰 유사한게 필요한데, 결국 이걸 또 어떻게 안전하게 보관할지.. 재귀..? 버근가?


<br>

## 3. store in the Memory (JS closure variable)

- 상대적으로 가장 안전한 방법

  - why ? :
    마찬가지로 `cross-site-scripting`위험에 노출되어있지만,
    `JS`의 `closure`에 저장하게 됨 (`class`내부의 `private`변수에 저장하는 느낌).

    **토큰값을 변수에 저장하는 함수**와, **저장된 토큰값을 헤더에 추가하는 함수**만 보여줌 (상세 내용은 예시 코드 참고).
    고로, `JS`로 토큰값 자체에 접근하는건 매우 어렵고,
    `auth.fetch`를 활용하려해도 `whitelist origin`을 지정해 놓을 수 있기 때문에 요청자 식별이 가능.

- 인지도 높은 OAuth 프레임워크인  `AuthO`에서 추천하는 토큰 저장 방식.

- JS 변수에 토큰을 저장하는 방법.

- 크롬의 경우, 탭 마다 고유의 메모리 공간을 가짐 == 새로운 탭 마다 새롭게 로그인 필요.
  - 이에 대한 해결책 :
    1. `Refresh Token ` 
       - 새로운 `access token` 을 얻기위한 토큰
       - 하지만 해당 토큰의 lifetime 이 길면 위험
         - 해결책 : `refresh token rotation`
           1. 매번 `refresh token`으로 `access token` 이 발행될 때 마다 새로운 `refresh token` 생성..
           1. 사용자 경험 위해서도 탭마다 이런게 있으면 불-편

- 페이지 새로고침 되면 지워짐 === 새롭게 로그인 필요.

  - 이에 대한 해결책 :
    1. SPA로 웹 서비스 구현
       - SPA === 페이지 새로고침 없이 데이터가 교환되고 업데이트되는 원리 === 토큰의 variable 값 보존 가능

- 예시 : 

  ```javascript
  function authModule() {
      // prevents overwriting the normal fetch operation to steal the authorization cookie
      const fetch = window.fetch;
      
      const authOrigins = ["https://tokenstorage.ropnop.dev", "http://localhost:3000"]; // 화이트 리스트
      let token = '';
      
      this.setToken = (value) => {  // 토큰값을 변수에 저장하는 함수
          token = value
      }
  
      this.fetch = (resource, options) => {  // 저장된 토큰값을 http 요청 헤더에 추가하는 함수
          let req = new Request(resource, options);
          destOrigin = new URL(req.url).origin;
          if (token && authOrigins.includes(destOrigin)) {
              req.headers.set('Authorization', token);
          }
          return fetch(req)
      }
  }
  
  
  const auth = new authModule();
  
  function login() {  // 로그인 요청 함수
      fetch("/api/login")
          .then((res) => {
              if (res.status == 200) {
                  return res.json()
              } else {
                  throw Error(res.statusText)
              }
          })
          .then(data => {
              auth.setToken(data.token)  // 토큰값을 JS closure 변수에 저장
              // logResponse("loginResponse", `Private auth object set with token value: ${data.token}`)
          })
          .catch(console.error)
  }
  
  
  function makeRequest() {
      auth.fetch("/api/echo", {headers: {"CustomHeader1": "foobar"}})
          .then((res) => {
              if (res.status == 200) {
                  return res.text()
              } else {
                  throw Error(res.statusText)
              }
          }).then(responseText => logResponse("requestResponse", responseText))
          .catch(console.error)
  }
  ```

<br>

## 결론

- 결국 얼마나 꼬느냐의 차이일 뿐.
- 완벽한 보안은 이상론이다.