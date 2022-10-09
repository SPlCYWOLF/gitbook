# 🐧 Token storage

[ref 1](https://blog.bitsrc.io/sessionstorage-and-localstorage-a-ux-security-comparison-a05c486413e0) ,   [ref 2](https://www.youtube.com/watch?v=occfnVaZOXI) ,   [ref 3](https://auth0.com/docs/secure/security-guidance/data-security/token-storage)

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

## 3. store in the Memory

- `SPA` 기준, 상대적으로 가장 안전한 방법 (왜?)
- 인지도 높은 OAuth 프레임워크인  `AuthO`에서 추천하는 토큰 저장 방식.
- JS 변수에 토큰을 저장하는 방법.
- 마찬가지로 `cross-site-scripting`위험에 노출되어있음.
- 크롬의 경우, 탭 마다 고유의 메모리 공간을 가짐 == 새로운 탭 마다 새롭게 로그인 필요.
  - 이에 대한 해결책 :
    1. `Refresh Token `  (but 어떻게? 추가 검색 필요)
       - 새로운 `access token` 을 얻기위한 토큰
       - 하지만 해당 토큰의 lifetime 이 길면 위험
         - 해결책 : `refresh token rotation`
           1. 매번 `refresh token`으로 `access token` 이 발행될 때 마다 새로운 `refresh token` 생성..

<br>

## 결론

- 결국 얼마나 꼬느냐의 차이일 뿐.
- 완벽한 보안은 이상론이다.