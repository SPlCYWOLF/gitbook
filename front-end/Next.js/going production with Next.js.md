# ๐ going production with Next.js

[์ถ์ฒ1](https://nextjs.org/docs/going-to-production) : next.js ๋ฅผ ํ์ฉํ ์น ์ดํ๋ฆฌ์ผ์ด์์ ์ํํ ํ๊ธฐ์ํ ์ฒดํฌ๋ฆฌ์คํธ

___



1. <mark style="color:green;">SSR ์บ์ฑ ์ ๊ทน ํ์ฉ</mark>

   * ์ธ๋ถ์ request ํ์๋ฅผ ์ค์์ผ๋ก์จ ์๋ต์๋ ํฅ์ => UX up

   * Next.js๋ `/_next/static` ๊ฒฝ๋ก์ ์์๋ค (JS, CSS, ์ ์ ์ด๋ฏธ์ง, ๋ฏธ๋์ด ํ์ผ๋ค)  + ์ ์  ํ์ด์ง๋ 
     ์๋์ผ๋ก ์บ์ฑ ํค๋์ ์ถ๊ฐํด์ค.

   * ์ ์  ํ์ด์ง๋ฅผ `revalidate` ํ๊ณ ์ถ๋ค๋ฉด, `getStaticProps()` ํจ์์ `revalidate` ๊ฐ์ ์ค์ .
     revalidate : ์ต์  ์ ๋ณด๋ฅผ ์บ์ฑ ํค๋์ ์ถ๊ฐํ๋ ์์

   * `stale-while-revalidate` ๋ฅผ ํ์ฉํ๋ฉด, `getServerSideProps()` ํจ์๋ก SSR ์บ์ฑ ์ปค์คํฐ๋ง์ด์ฆ ๊ฐ๋ฅ.

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
     SSR ์บ์ฑ์ ํ์ฉํ๊ธฐ ์ํด์  ๋ฐฐํฌ provider๊ฐ ์บ์ฑ๋ ๋ฐ์ดํฐ๋ฅผ ๋์ ์ผ๋ก response ํด์ค์ผ ํ๋๋ฐ,
     Redis ์ ๊ฐ์ key/value DB๋ฅผ ํ์ฉํ๊ฑฐ๋, ํธ์คํ ํ๋ก๊ทธ๋จ์ผ๋ก Vercel์ ํ์ฉํ๋ ๋ฐฉ๋ฒ์ด ์๋ค.

   \

2. <mark style="color:green;">์ต์ํ์ Javascript๋ฅผ ์ ์  ํ์ด์ง์ ํฌํจ</mark>

   * `dynamic import(lazy-load)` ๋ฅผ ํ์ฉํ์ฌ ํน์  ์ํฉ์์๋ง cliend-side์์ Javascript import => 
     ์ ์  Javascript ํ์ผ ํฌ๊ธฐ๋ฅผ ์ต์ํ => ํ์ด์ง ๋ก๋ ์๋ ํฅ์ & ๋ฐฐํฌ ์๋ ํฅ์ => UX & DX up

   \

3. <mark style="color:green;">Lighthouse ๋ฅผ ํ์ฉํ์ฌ ์น ํ์ด์ง์ ์ฑ๋ฅ, ์ ๊ทผ์ฑ, SEO ์ํ๋ฅผ ์ต์ ํ</mark>

   * next.js ๋ฅผ ํ๋ก๋์ ๋น๋ => incognito ๋ชจ๋์์ lighthouse ์ ์ ํ์ธ => ํ ๋ธ๋ผ์ฐ์  ์ต์คํ์์ ์ํฅ ์๋ฐ์ => ๋ ์ ํํ ์ง๋จ

   \
   
4. <mark style="color:green;">ํผํฌ๋จผ์ค ํฅ์</mark>

   - next/image ํ์ฉํ์ฌ ์ด๋ฏธ์ง ์ต์ ํ
   - ์๋ ํฐํธ ์ต์ ํ
   - ์คํฌ๋ฆฝํธ ์ต์ ํ