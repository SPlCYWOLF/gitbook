# 🥺 going production with Next.js

[참고1](https://nextjs.org/docs/going-to-production)

next.js 를 활용한 웹 어플리케이션을 상품화 하기위한 체크리스트

***

1. <mark style="color:green;">SSR 캐싱 적극 활용</mark>

   * 외부에 request 횟수를 줄임으로써 응답속도 향상 => UX up
   * Next.js는 `/_next/static` 경로의 에셋들 (JS, CSS, 정적이미지, 미디어 파일들)  + 은 자동으로 캐싱 헤더에 추가해줌.
   * 

   \

   