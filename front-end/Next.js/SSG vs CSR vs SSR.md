# 😼SSG vs CSR vs SSR

[참조1](https://nextjs.org/docs/basic-features/pages)   [참조2](https://www.youtube.com/watch?v=mWytwmxLKmo&t=22s)   [참조3](https://fauna.com/blog/comparing-spas-to-ssg-and-ssr)   [참조4](https://www.youtube.com/watch?v=vM_zQLnlyKw)   [참조5](https://kirillibrahim.medium.com/gray-area-on-when-to-use-different-rendering-modes-csr-ssr-ssg-214a636a24a4)

___



1. CSR와 SSR의 부분적인 장점들과 DX(developer experience) 를 등가교환 == SSG.

   ![image-20220623192431887](https://github.com/SPlCYWOLF/gitbook/blob/main/front-end/Next.js/SSG%20vs%20CSR%20vs%20SSR.assets/image-20220623192431887.png?raw=true)

   <br>

2. CSR & SSR & SSG의 활용 예시

   - CSR : 
     - 인터렉티브한 요소가 많음
     - 개발 리소스가 한정적임(특히 백앤드가)
     - FE에 빠른 정보 반영 필요
     - 예시 : 유저 대쉬보드, private content
   - SSR : 
     - 웹앱이 DB-reliant 하며 잦은 정보의 유동성으로 인해 정보의 실시간성이 필요함
     - 사용자의 인터넷 환경이 한정적임
     - SEO가 필요함
     - 예시 : e-commerce 플랫폼, SNS 사이트
   - SSG : 
     - 정보의 변화가 매우 적음
     - SEO가 필요함
     - 예시 : 블로그, public content