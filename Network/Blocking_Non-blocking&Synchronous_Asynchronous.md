## ๐ Blocking/Non-blocking & Synchronous & Asynchronous

> ๐ง **์ด์ ์ ์๋ฐ์คํฌ๋ฆฝํธ, Node.js๋ฅผ ๊ณต๋ถํ์๋๋ ๊ทธ๋ ๊ณ  ๋น๋๊ธฐ ๊ฐ๋์ ๋งค์ฐ ์ค์ํ๊ฒ ๋ค๋ค์ง๋ค. ๋น๋๊ธฐ์ ๋ํ ๊ฐ๋์ ์ด์  ์ด๋์ ๋ ํ์คํ๊ฒ ์๊ณ ์์ง๋ง Blocking๊ณผ Synchronous, Non-blocking๊ณผ Asynchronous์ ๊ฐ๋์ด ํผ๋๋๋ ๊ฒฝ์ฐ๊ฐ ๋ง์ ์ ๋ฆฌํด ๋ณด๊ณ ์ ํ๋ค. **

---

## Blocking vs Non-blocking
- Blocking๊ณผ Non-blocking์ **'์ ์ด๊ถ'**์ ๊ด์ ์์ ์ ๊ทผํ๋ ๋ฐฉ์์ด๋ค. 

- Blocking์ด๋ผ๋ ๊ฒ์ ํ๊ตญ์ด๋ก '๋งํ ์๋ค' ๋ผ๋ ๋ป์ผ๋ก, ํธ์ถ๋ ํจ์๊ฐ ์ ์ด๊ถ์ ๋๊ฒจ์ฃผ์ง ์์ ํธ์ถํ ํจ์์ธก์์๋ ๋ค๋ฅธ ์์์ ์ํํ  ์ ์์ด ์ ์ด๊ถ์ด ๋์์ค๊ธฐ๋ฅผ ๊ธฐ๋ค๋ฆฌ๋ ๊ฒ์ ๋งํ๋ค. 

- ๋ฐ๋๋ก Non-Blocking์, ์ ์ด๊ถ์ด ๋๊ฒจ ์ง์ง ์์ผ๋ฏ๋ก, ๋์์ ์์ ์ฒ๋ฆฌ ์ฌ๋ถ์ ์๊ด์ด ์์ด ํธ์ถํ ํจ์ ์ธก์์ ์ ์ด๊ถ์ ๊ฐ์ง๊ณ  ๋ค์ ์์๋ค์ ์ํํ  ์ ์๋ค.

- ๋ค์๋งํด Non-Blocking ์ผ๋ก ์๋ํ๋ค๋ ๊ฒ์, ์ ์ด๊ถ์ ํธ์ถํ ํจ์ ์ธก์์ ๊ณ์ํด์ ๊ฐ์ง๊ณ  ์๊ธฐ ๋๋ฌธ์, ๋ง์ฝ์ ๋ค๋ฅธ ํจ์๊ฐ ์คํ๋๋ค๋ฉด ๊ทธ ํจ์์ ๋ํ ๊ฒฐ๊ณผ๊ฐ์ ๋ฐ์ ์ ์๋ ์ํฉ์ธ์ง ์ฒดํฌํ๋ ๊ณผ์ ์ด ํ์ํ ๊ฒ์ด๋ค. 


## Synchronous vs Asynchronous
- Synchronous, Asynchronous๋ '์๊ฐ'์ ๊ด์ ์์ ์ ๊ทผํด์ผ ํ๋ค.

- ํธ์ถ๋ ํจ์์ ํธ์ถํ ํจ์ ๋ ํจ์ ๊ด์ ์์ ๋ฐ๋ผ๋ณด๋ฉด, Synchronous ๋ ๋ ํจ์์ ์์๊ณผ ์ข๋ฃ ์๊ฐ์ ๋ํด ๋ง์ถฐ์ ธ์ผํ๋ค๋ ๋ป์ด๋ค. ์คํ์์ ํจ์ ํ๋๊ฐ ๋น ์ ธ ๋๊ฐ๊ณ , ๋ค์ ํจ์๊ฐ ์คํ์ด ๋๊ณ , ์ด๋ฐ ๋๋์ผ๋ก ์๊ฐ์ด ์ง์ผ์ง๋ฉด์ ์์ฐจ์ ์ผ๋ก ์ผ์ด๋  ์ ์๋ ๊ฒ์ ์๋ฏธํ๋ค. ์ค์ ๋ก ํ๊ตญ์ด๋ก ๋๊ธฐํ ๋ํ ๊ทธ๋ฐ ๋งฅ๋ฝ์์ ๋ค์ด๋ง๋๋ค๊ณ  ๋ณผ ์ ์๋ค. 

- Asynchronous๋ ๋ ํจ์์ ์์๊ณผ ์ข๋ฃ ์๊ฐ์ด ์์ ํ ๋ง์ถฐ์ง์ง๊ฐ ์๋๋ค๋ ๋ป์ด๋ค. ํธ์ถํ ํจ์๋ ํธ์ถ๋ ํจ์์ ๊ฒฐ๊ณผ๋ฅผ ๊ธฐ๋ค๋ฆฌ์ง๋ง, ์ ์ด๊ถ์ด ์ด๋ป๊ฒ ๋ ์ง๋ ๊ด์ฌ์ด ์๋ค. ๋น๋๊ธฐ์ ์ผ๋ก ๋ค๋ฅธ ํจ์๊ฐ ์คํ์ด ๋๋ค๋ ๋ฐ์ ์๋ฏธ๊ฐ ์๊ณ  ํธ์ถ๋ ํจ์์ ๊ฒฐ๊ณผ๊ฐ์ ๋ฐ๊ฒ ๋๋๋ฐ ๋ค๋ฅธ ๋น๋๊ธฐ ํจ์๋ก ๋ถํฐ ๋ฐ์ ๊ฒฐ๊ณผ๊ฐ์ ๋ํด ๋ชจ๋  ์์๊ฐ ์์ ํ ๋ณด์ฅ์ด ๋  ์ ์๋ค๋ ์๋ฏธ์ด๋ค. Ajax ๊ฐ ๋ํ์ ์ธ ๊ทธ ์์์ด๋ค.

---

## Blocking/Non-blocking & Synchronous/Asynchronous

- ์์์ ๊ฐ๊ฐ์ ๊ฐ๋๋ค์ ์ดํด๋ณด์๋ฏ์ด, Blocking์ด๋ผ๊ณ  ๋ฐ๋์ Sync๊ฐ ๋๋ ๊ฒ์ด ์๋๋ค. ๊ทธ๋ฆฌ๊ณ  Non-blocking์ด๋ผ๊ณ  ๋ฐ๋์ Async์ธ ๊ฒ๋ ์๋๋ค. 
- ์ฆ Blocking/Non-blocking๊ณผ Sync/Async๋ ๋ณ๊ฐ์ ๊ฐ๋์ด๋ค. 

![](https://images.velog.io/images/lck0827/post/fba374d9-957e-4f1e-b035-dfbc48974155/image.png)
์ถ์ฒ: [homoefficio๋ ๋ธ๋ก๊ทธ](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)

- ๋ช ๊ฐ์ง ๋ชจ๋ธ์ ์ดํด ๋ณด๋๋ก ํ์.


### Non-blocking + Synchronous

![](https://images.velog.io/images/lck0827/post/54ec115b-a016-431c-a687-2c532f77a745/image.png)

- **์ ์ด๊ถ์ ํธ์ถ๋ ํจ์์๊ฒ ๋๊ฒจ์ฃผ์ง ์๋๋ค (Non-blocking)**

- **But, ๊ฒฐ๊ณผ๊ฐ์ ์์๋ ๋ณด์ฅ๋๋ค (Synchronous)
**

- ์ ์ด๊ถ์ ํธ์ถ๋ ํจ์์๊ฒ ๋๊ฒจ์ฃผ์ง ์๊ธฐ ๋๋ฌธ์ (Non-blocking), ํ๋ก๊ทธ๋จ ์ธก์์๋ ํธ์ถํ ํจ์๊ฐ ๋๋๊ธฐ๋ฅผ ๊ธฐ๋ค๋ฆฌ๋ฉด์ ๋ค๋ฅธ ์์๋ค์ ์ํํ  ์๊ฐ ์๋ ๊ฒ์ด ํต์ฌ์ด๋ค. 
ํ์ง๋ง Synchronous์ ํน์ฑ ๋๋ฌธ์, ์๊ฐ์ ๋ง์ถฐ์ฃผ๊ธฐ ์ํด ๋งค ์๊ฐ ํธ์ถ๋ ํจ์๊ฐ ๋๋ฌ๋์ง ํ์คํํ๋ ์์ฒญ์ด ํ์ํ๋ค.

### Blocking + Asynchronous
![](https://images.velog.io/images/lck0827/post/db0e53b8-2a18-4791-9c6b-e08af60d6ef6/image.png)

- **์ ์ด๊ถ์ ํธ์ถ๋ ํจ์์๊ฒ ๋๊ฒจ์ฃผ๊ฒ ๋๋ค (Blocking)**

- **But, ๊ฒฐ๊ณผ๊ฐ์ ์์๋ ๋ณด์ฅ๋์ง ์์ผ๋ฉฐ ๊ฒฐ๊ณผ๋ฅผ ๋ฐํ์ผ๋ก ์ด๋ฃจ์ด์ง๋ค (Asynchronous)**

- ํธ์ถํ ํจ์๋ ์ ์ด๊ถ์ ํธ์ถ๋ ํจ์์๊ฒ ๋๊ฒจ์ฃผ์ด ๋ค๋ฅธ ์์๋ค์ ํ  ์ ์๊ฒ ๋๋ค. ํธ์ถ๋ ํจ์์ ๋ํ ๊ฒฐ๊ณผ๊ฐ์ ์๋ต์ ๋ฐ์ ํ, ์ ์ด๊ถ ๋ํ ๋๊ฒจ๋ฐ๊ฒ ๋์ด ๋ค๋ฅธ ์์๋ค์ด ์คํ๋๋ค. ๊ทธ๋ฆฌ๊ณ  Asynchronous์ ํน์ฑ์ ๊ฐ์ง๋ค. ์ฌ์ค ์ด๋ฐ ์ผ์ด์ค๋ ๋นํจ์จ์ ์ด๊ธฐ ๋๋ฌธ์ ๊ฑฐ์ ์ฌ์ฉ๋์ง ์๋๋ค. ํ๊ฒฝ์ด ๋ค๋ฅธ ๋ ํ๋ก๊ทธ๋จ์ ํผํฉ์์ ์ฌ์ฉํ๋ฉด์ ๊ฒช๊ฒ ๋๋ ํฌ๊ทํ ๊ฒฝ์ฐ (ex. Node.js์ MySQL์ ํจ๊ป ์ฌ์ฉํ๋ ๊ฒฝ์ฐ)์ ์ฌ์ฉ๋์ด์ง๋ค๊ณ  ํ๋ค.

---

### ๐ Reference
1. http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/
2. https://programming119.tistory.com/238
3. https://jh-7.tistory.com/25