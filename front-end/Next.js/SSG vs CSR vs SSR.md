# ๐ผSSG vs CSR vs SSR

[์ฐธ์กฐ1](https://nextjs.org/docs/basic-features/pages)   [์ฐธ์กฐ2](https://www.youtube.com/watch?v=mWytwmxLKmo&t=22s)   [์ฐธ์กฐ3](https://fauna.com/blog/comparing-spas-to-ssg-and-ssr)   [์ฐธ์กฐ4](https://www.youtube.com/watch?v=vM_zQLnlyKw)   [์ฐธ์กฐ5](https://kirillibrahim.medium.com/gray-area-on-when-to-use-different-rendering-modes-csr-ssr-ssg-214a636a24a4)

___



1. CSR์ SSR์ ๋ถ๋ถ์ ์ธ ์ฅ์ ๋ค๊ณผ DX(developer experience) ๋ฅผ ๋ฑ๊ฐ๊ตํ == SSG.

   ![image-20220623192431887](https://github.com/SPlCYWOLF/gitbook/blob/main/front-end/Next.js/SSG%20vs%20CSR%20vs%20SSR.assets/image-20220623192431887.png?raw=true)

   <br>

2. CSR & SSR & SSG์ ํ์ฉ ์์

   - CSR : 
     - ์ธํฐ๋ ํฐ๋ธํ ์์๊ฐ ๋ง์
     - ๊ฐ๋ฐ ๋ฆฌ์์ค๊ฐ ํ์ ์ ์(ํนํ ๋ฐฑ์ค๋๊ฐ)
     - FE์ ๋น ๋ฅธ ์ ๋ณด ๋ฐ์ ํ์
     - ์์ : ์ ์  ๋์ฌ๋ณด๋, private content
   - SSR : 
     - ์น์ฑ์ด DB-reliant ํ๋ฉฐ ์ฆ์ ์ ๋ณด์ ์ ๋์ฑ์ผ๋ก ์ธํด ์ ๋ณด์ ์ค์๊ฐ์ฑ์ด ํ์ํจ
     - ์ฌ์ฉ์์ ์ธํฐ๋ท ํ๊ฒฝ์ด ํ์ ์ ์
     - SEO๊ฐ ํ์ํจ
     - ์์ : e-commerce ํ๋ซํผ, SNS ์ฌ์ดํธ
   - SSG : 
     - ์ ๋ณด์ ๋ณํ๊ฐ ๋งค์ฐ ์ ์
     - SEO๊ฐ ํ์ํจ
     - ์์ : ๋ธ๋ก๊ทธ, public content