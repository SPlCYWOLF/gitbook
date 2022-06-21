# 🚀 going production with Next.js

[참고1](https://nextjs.org/docs/going-to-production)

next.js 를 활용한 웹 어플리케이션을 상품화 하기위한 체크리스트

***

1. <mark style="color:green;">SSR 캐싱 적극 활용</mark>

   * 외부에 request 횟수를 줄임으로써 응답속도 향상 => UX up

   * Next.js는 `/_next/static` 경로의 에셋들 (JS, CSS, 정적이미지, 미디어 파일들)  + 정적 페이지는 
     자동으로 캐싱 헤더에 추가해줌.

   * 정적 페이지를 `revalidate` 하고싶다면, `getStaticProps()` 함수에 `revalidate` 값을 설정.
     revalidate : 최신 정보를 캐싱 헤더에 추가하는 작업

   * `stale-while-revalidate` 를 활용하면, `getServerSideProps()` 함수로 SSR 캐싱 커스터마이즈 가능.

     ```jsx
     export async function getServerSideProps({ req, res }) {
       res.setHeader(
         'Cache-Control',
         'public, s-maxage=10, stale-while-revalidate=59'
       )
     
       return {
         props: {},
       }
     }
     ```

   * **BUT**
     SSR 캐싱을 활용하기 위해선 배포 provider가 캐싱된 데이터를 동적으로 response 해줘야 하는데,
     Redis 와 같은 key/value DB를 활용하거나, 호스팅 프로그램으로 Vercel을 활용하는 방법이 있다.

   \

2. <mark style="color:green;">최소한의 Javascript를 정적 페이지에 포함</mark>

   * `dynamic import(lazy-load)` 를 활용하여 특정 상황에서만 cliend-side에서 Javascript import => 
     정적 Javascript 파일 크기를 최소화 => 페이지 로드 속도 향상 & 배포 속도 향상 => UX & DX up

   \

3. <mark style="color:green;">Lighthouse 를 활용하여 웹 페이지의 성능, 접근성, SEO 상태를 최적화</mark>

   * next.js 를 프로덕션 빌드 => incognito 모드에서 lighthouse 점수 확인 => 타 브라우저 익스텐션의 영향 안받음 => 더 정확한 진단

   \
   
4. <mark style="color:green;">퍼포먼스 향상</mark>

   - next/image 활용하여 이미지 최적화
   - 자동 폰트 최적화
   - 스크립트 최적화