## ๐ ํ๋ก์ธ์ค & ์ค๋ ๋

## ํ๋ก์ธ์ค๋?
- ํ๋ก๊ทธ๋จ์ ๋ฉ๋ชจ๋ฆฌ ์์์ ์คํ์ค์ธ ์์
- ๋ฉ๋ชจ๋ฆฌ์ ์ฌ๋ผ์ CPU๋ฅผ ํ ๋น ๋ฐ๊ณ  ์คํ๋๊ณ  ์๋ ํ๋ก๊ทธ๋จ์ ์ธ์คํด์ค(๋๋ฆฝ์ ์ธ ๊ฐ์ฒด)
- ์ด์์ฒด์ ๋ก๋ถํฐ ์์คํ ์์์ ํ ๋น๋ฐ๋ ์์์ ๋จ์
- ํ๋ก๊ทธ๋จ์ ์ ์ ์ธ ๊ฐ๋, ํ๋ก์ธ์ค๋ ๋์ ์ธ ๊ฐ๋์ด๋ค

### ํ๋ก์ธ์ค์ ํน์ง
- ํ๋ก์ธ์ค๋ ๊ฐ๊ฐ ๋๋ฆฝ๋ ๋ฉ๋ชจ๋ฆฌ ์์ญ(Code, Data, Stack, Heap์ ๊ตฌ์กฐ)์ ํ ๋น๋ฐ๋๋ค.
- ํ๋ก์ธ์ค๋ง๋ค ์ต์ 1๊ฐ์ ์ค๋ ๋(๋ฉ์ธ์ค๋ ๋)๋ฅผ ์์ ํ๊ณ  ์๋ค.
- ๊ฐ ํ๋ก์ธ์ค๋ ๋ณ๋์ ์ฃผ์ ๊ณต๊ฐ์์ ์คํ๋๋ฉฐ, ํ ํ๋ก์ธ์ค๋ ๋ค๋ฅธ ํ๋ก์ธ์ค์ ๋ณ์๋ ์๋ฃ๊ตฌ์กฐ์ ์ ๊ทผํ  ์ ์๋ค.
- ํ ํ๋ก์ธ์ค๊ฐ ๋ค๋ฅธ ํ๋ก์ธ์ค์ ์์์ ์ ๊ทผํ๋ ค๋ฉด ํ๋ก์ธ์ค ๊ฐ์ ํต์ (IPC, inter-process communication)์ ์ฌ์ฉํด์ผ ํ๋ค.
  - ex) ํ์ดํ, ํ์ผ, ์์ผ ๋ฑ์ ์ด์ฉํ ํต์  ๋ฐฉ๋ฒ ์ด์ฉ


![](https://images.velog.io/images/lck0827/post/2fcf9f60-dc55-4f62-beb3-f1d3e29cb360/image.png)

โ Code
- text ์์ญ์ด๋ผ๊ณ ๋ ๋ถ๋ฆผ
- ์คํํ  ํ๋ก๊ทธ๋จ์ ์ฝ๋๊ฐ ์ ์ฅ๋๋ ์์ญ
- CPU๋ ์ด ์์ญ์ ์ ์ฅ๋ ๋ช๋ น์ด๋ฅผ ํ๋์ฉ ๊ฐ์ ธ์ ์ํ
- ํ๋ก๊ทธ๋จ์ด ์์๋๊ณ  ๋๋ ๋๊น์ง ๋ฉ๋ชจ๋ฆฌ ์์ญ์ ์ ์ง

โ Data
- ์ ์ญ(global) ๋ณ์์ ์ ์ (static)๋ณ์๊ฐ ์ ์ฅ๋๋ ์์ญ
- ํ๋ก๊ทธ๋จ ์์๋ ํ ๋น๋๊ณ  ์ข๋ฃ๋ ๋ ํด์ ๋๋ค
- BSS์ GVAR์์ญ์ ํตํ์ด data์์ญ์ด๋ผ ํ๋ค
  - BSS : ์ด๊ธฐํ๊ฐ ๋์ง ์์ ๋ฐ์ดํฐ๋ฅผ ์ ์ฅํ๊ธฐ ์ํ ์์ญ (RAM์ ์ ์ฅ)
  - GVAR : ์ด๊ธฐํ๊ฐ ๋ ๋ฐ์ดํฐ๋ฅผ ์ ์ฅํ๊ธฐ ์ํ ์์ญ (ROM์ ์ ์ฅ)
(์ด๊ธฐํ ๋ ๋ฐ์ดํฐ๋ ๊ฐ์ ์ ์ฅํด์ผํ๊ธฐ์ ๋นํ๋ฐ์ฑ ๋ฉ๋ชจ๋ฆฌ์ธ ROM์ ์ ์ฅ)

โ Stack
- ํ๋ก๊ทธ๋จ์ ์ํด ์ฌ์ฉ๋๋ ์์ ๋ฐ์ดํฐ ์์ญ
- ํจ์ ํธ์ถ์ ์์ฑ๋๋ ์ง์ญ๋ณ์, ๋งค๊ฐ๋ณ์๋ฅผ ์ ์ฅ, ํจ์ ์ข๋ฃ์ ํด์ 
- ๋ฉ๋ชจ๋ฆฌ ์ฃผ์๋ ๋์ ๊ณณ์์ ๋ฎ์ ๊ณณ์ ๋ฐฉํฅ์ผ๋ก ํ ๋น

โ Heap
- ํ๋ก๊ทธ๋๋จธ์ ์ํด ํ ๋น๋๊ณ  ํด์ ๋๋ค
- ๋ฉ๋ชจ๋ฆฌ๋ฅผ ๋์ ์ผ๋ก ํ ๋นํ๊ณ  ํ  ๋ ์ฌ์ฉ๋๋ ๋ฉ๋ชจ๋ฆฌ ์์ญ (ex. c์ธ์ด๋ฅผ ์๋ก ๋ค๋ฉด malloc, calloc, ...)
- ์คํ๊ณผ ๋ฐ๋๋ก ๋ฉ๋ชจ๋ฆฌ ์ฃผ์๊ฐ ๋ฎ์ ๊ณณ์์ ๋์ ๊ณณ์ ๋ฐฉํฅ์ผ๋ก ํ ๋น

---

## ์ค๋ ๋๋?
- โํ๋ก์ธ์ค ๋ด์์ ์คํ๋๋ ์ฌ๋ฌ ํ๋ฆ์ ๋จ์โ
- ํ๋ก์ธ์ค์ ํน์ ํ ์ํ ๊ฒฝ๋ก
- ํ๋ก์ธ์ค๊ฐ ํ ๋น๋ฐ์ ์์์ ์ด์ฉํ๋ ์คํ์ ๋จ์

### ์ค๋ ๋์ ํน์ง
- ์ค๋ ๋๋ ํ๋ก์ธ์ค ๋ด์์ ๊ฐ๊ฐ Stack๋ง ๋ฐ๋ก ํ ๋น๋ฐ๊ณ  Code, Data, Heap ์์ญ์ ๊ณต์ ํ๋ค.
  
- ์ค๋ ๋๋ ํ ํ๋ก์ธ์ค ๋ด์์ ๋์๋๋ ์ฌ๋ฌ ์คํ์ ํ๋ฆ์ผ๋ก, ํ๋ก์ธ์ค ๋ด์ ์ฃผ์ ๊ณต๊ฐ์ด๋ ์์๋ค(ํ ๊ณต๊ฐ ๋ฑ)์ ๊ฐ์ ํ๋ก์ธ์ค ๋ด์ ์ค๋ ๋๋ผ๋ฆฌ ๊ณต์ ํ๋ฉด์ ์คํ๋๋ค.
- ๊ฐ์ ํ๋ก์ธ์ค ์์ ์๋ ์ฌ๋ฌ ์ค๋ ๋๋ค์ ๊ฐ์ ํ ๊ณต๊ฐ์ ๊ณต์ ํ๋ค. ๋ฐ๋ฉด์ ํ๋ก์ธ์ค๋ ๋ค๋ฅธ ํ๋ก์ธ์ค์ ๋ฉ๋ชจ๋ฆฌ์ ์ง์  ์ ๊ทผํ  ์ ์๋ค.
- ๊ฐ๊ฐ์ ์ค๋ ๋๋ ๋ณ๋์ ๋ ์ง์คํฐ์ ์คํ์ ๊ฐ๊ณ  ์์ง๋ง, ํ ๋ฉ๋ชจ๋ฆฌ๋ ์๋ก ์ฝ๊ณ  ์ธ ์ ์๋ค.
- ํ ์ค๋ ๋๊ฐ ํ๋ก์ธ์ค ์์์ ๋ณ๊ฒฝํ๋ฉด, ๋ค๋ฅธ ์ด์ ์ค๋ ๋(sibling thread)๋ ๊ทธ ๋ณ๊ฒฝ ๊ฒฐ๊ณผ๋ฅผ ์ฆ์ ๋ณผ ์ ์๋ค.

> ๐ **ํ๋ก์ธ์ค๋ ์์ ๋ง์ ๊ณ ์  ๊ณต๊ฐ๊ณผ ์์์ ํ ๋น๋ฐ์ ์ฌ์ฉํ๋๋ฐ ๋ฐํด, ์ค๋ ๋๋ ๋ค๋ฅธ ์ค๋ ๋์ ๊ณต๊ฐ, ์์์ ๊ณต์ ํ๋ฉด์ ์ฌ์ฉํ๋ ์ฐจ์ด๊ฐ ์กด์ฌํจ
**

![](https://images.velog.io/images/lck0827/post/fe4c2813-348b-4624-a027-1a9e3a458be3/image.png)

---

## ๋ฉํฐ ํ๋ก์ธ์ค
- ๋๊ฐ ์ด์ ๋ค์์ ํ๋ก์ธ์(CPU)๊ฐ ํ๋ ฅ์ ์ผ๋ก ํ๋ ์ด์์ ์์(Task)์ ๋์์ ์ฒ๋ฆฌํ๋ ๊ฒ. (๋ณ๋ ฌ์ฒ๋ฆฌ)
- ๊ฐ ํ๋ก์ธ์ค ๊ฐ ๋ฉ๋ชจ๋ฆฌ ๊ตฌ๋ถ์ด ํ์ํ๊ฑฐ๋ ๋๋ฆฝ๋ ์ฃผ์ ๊ณต๊ฐ์ ๊ฐ์ ธ์ผ ํ  ๊ฒฝ์ฐ ์ฌ์ฉํ๋ค.

โ **์ฅ์  ** 
   - ์์ ์ฑ (๋ฉ๋ชจ๋ฆฌ ์นจ๋ฒ ๋ฌธ์ ๋ฅผ OS ์ฐจ์์์ ํด๊ฒฐ)
   - ์ฌ๋ฌ ๊ฐ์ ์์ ํ๋ก์ธ์ค ์ค ํ๋์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ๋ฉด ๊ทธ ์์ ํ๋ก์ธ์ค๋ง ์ฃฝ๋ ๊ฒ ์ด์์ผ๋ก ๋ค๋ฅธ ์ํฅ์ด ํ์ฐ๋์ง ์๋๋ค.

โ **๋จ์  **
- ๊ฐ๊ฐ ๋๋ฆฝ๋ ๋ฉ๋ชจ๋ฆฌ ์์ญ์ ๊ฐ๊ณ  ์์ด, ์์๋ ๋ง์ ์๋ก ์ค๋ฒํค๋ ๋ฐ์. Context Switching์ผ๋ก ์ธํ ์ฑ๋ฅ ์ ํ
- ํ๋ก์ธ์ค ์ฌ์ด์ ์ด๋ ต๊ณ  ๋ณต์กํ ํต์  ๊ธฐ๋ฒ(IPC)
ํ๋ก์ธ์ค๋ ๊ฐ๊ฐ์ ๋๋ฆฝ๋ ๋ฉ๋ชจ๋ฆฌ ์์ญ์ ํ ๋น๋ฐ์๊ธฐ ๋๋ฌธ์ ํ๋์ ํ๋ก๊ทธ๋จ์ ์ํ๋ ํ๋ก์ธ์ค๋ค ์ฌ์ด์ ๋ณ์๋ฅผ ๊ณต์ ํ  ์ ์๋ค.

---

## ๋ฉํฐ ์ค๋ ๋
- ํ๋์ ์์ฉ ํ๋ก๊ทธ๋จ์์ ์ฌ๋ฌ ์ค๋ ๋๋ฅผ ๊ตฌ์ฑํด ๊ฐ ์ค๋ ๋๊ฐ ํ๋์ ์์์ ์ฒ๋ฆฌํ๋ ๊ฒ
- ์ค๋ ๋๋ค์ด ๊ณต์  ๋ฉ๋ชจ๋ฆฌ๋ฅผ ํตํด ๋ค์์ ์์์ ๋์์ ์ฒ๋ฆฌํ๋๋ก ํด์ค

โ **์ฅ์  ** 
- ๋๋ฆฝ์ ์ธ ํ๋ก์ธ์ค์ ๋นํด ๊ณต์  ๋ฉ๋ชจ๋ฆฌ๋งํผ์ ์๊ฐ, ์์ ์์ค์ด ๊ฐ์ ์ ์ญ ๋ณ์์ ์ ์  ๋ณ์์ ๋ํ ์๋ฃ ๊ณต์  ๊ฐ๋ฅ
- ์์คํ ์์ ์๋ชจ ๊ฐ์
   - ํ๋ก์ธ์ค๋ฅผ ์์ฑํ์ฌ ์์์ ํ ๋นํ๋ ์์คํ ์ฝ์ด ์ค์ด๋ค์ด ์์์ ํจ์จ์ ์ผ๋ก ๊ด๋ฆฌํ  ์ ์๋ค.
- ์์คํ ์ฒ๋ฆฌ๋ ์ฆ๊ฐ (์ฒ๋ฆฌ ๋น์ฉ ๊ฐ์)
  - ์ค๋ ๋ ๊ฐ ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ  ๋ฐ๋ ๊ฒ์ด ๊ฐ๋จํด์ง๊ณ  ์์คํ ์์ ์๋ชจ๊ฐ ์ค์ด๋ค๊ฒ ๋๋ค.
  - ์ค๋ ๋ ์ฌ์ด์ ์์๋์ด ์์ Context Switching์ด ๋น ๋ฅด๋ค.
- ๊ฐ๋จํ ํต์  ๋ฐฉ๋ฒ์ผ๋ก ์ธํ ํ๋ก๊ทธ๋จ ์๋ต ์๊ฐ ๋จ์ถ
  - ์ค๋ ๋๋ ํ๋ก์ธ์ค ๋ด์ Stack ์์ญ์ ์ ์ธํ ๋ชจ๋  ๋ฉ๋ชจ๋ฆฌ๋ฅผ ๊ณต์ ํ๊ธฐ ๋๋ฌธ์ ํต์ ์ ๋ถ๋ด์ด ์ ๋ค.

โ **๋จ์ ** 
- ์์ ์ฑ ๋ฌธ์ . ํ๋์ ์ค๋ ๋๊ฐ ๋ฐ์ดํฐ ๊ณต๊ฐ ๋ง๊ฐ๋จ๋ฆฌ๋ฉด, ๋ชจ๋  ์ค๋ ๋๊ฐ ์๋ ๋ถ๋ฅ ์ํ (๊ณต์  ๋ฉ๋ชจ๋ฆฌ๋ฅผ ๊ฐ๊ธฐ ๋๋ฌธ)
- ์ฃผ์ ๊น์ ์ค๊ณ๊ฐ ํ์ํ๋ค.
- ๋๋ฒ๊น์ด ๊น๋ค๋กญ๋ค.
- ๋จ์ผ ํ๋ก์ธ์ค ์์คํ์ ๊ฒฝ์ฐ ํจ๊ณผ๋ฅผ ๊ธฐ๋ํ๊ธฐ ์ด๋ ต๋ค.
- ๋ค๋ฅธ ํ๋ก์ธ์ค์์ ์ค๋ ๋๋ฅผ ์ ์ดํ  ์ ์๋ค. (์ฆ, ํ๋ก์ธ์ค ๋ฐ์์ ์ค๋ ๋ ๊ฐ๊ฐ์ ์ ์ดํ  ์ ์๋ค.)
- ๋ฉํฐ ์ค๋ ๋์ ๊ฒฝ์ฐ ์์ ๊ณต์ ์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ๋ค. (๋๊ธฐํ ๋ฌธ์ )
- ํ๋์ ์ค๋ ๋์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ๋ฉด ์ ์ฒด ํ๋ก์ธ์ค๊ฐ ์ํฅ์ ๋ฐ๋๋ค.

---

### ๋ฉํฐ ํ๋ก์ธ์ค ๋์  ๋ฉํฐ ์ค๋ ๋๋ฅผ ์ฌ์ฉํ๋ ์ด์ 

- ์์์ ํจ์จ์ฑ ์ฆ๋
  - ๋ฉํฐ ํ๋ก์ธ์ค๋ก ์คํ๋๋ ์์์ ๋ฉํฐ ์ค๋ ๋๋ก ์คํํ  ๊ฒฝ์ฐ, ํ๋ก์ธ์ค๋ฅผ ์์ฑํ์ฌ ์์์ ํ ๋นํ๋ ์์คํ ์ฝ์ด ์ค์ด๋ค์ด ์์์ ํจ์จ์ ์ผ๋ก ๊ด๋ฆฌ ๊ฐ๋ฅํ๋ค.
  -> ํ๋ก์ธ์ค ๊ฐ์ Context Switching์ ๋จ์ํ CPU ๋ ์ง์คํฐ ๊ต์ฒด ๋ฟ๋ง ์๋๋ผ RAM๊ณผ CPU ์ฌ์ด์ ์บ์ฌ ๋ฉ๋ชจ๋ฆฌ์ ๋ํ ๋ฐ์ดํฐ๊น์ง ์ด๊ธฐํ๋๋ฏ๋ก ์ค๋ฒํค๋๊ฐ ํฌ๊ธฐ ๋๋ฌธ
  - ์ค๋ ๋๋ ํ๋ก์ธ์ค ๋ด์ ๋ฉ๋ชจ๋ฆฌ๋ฅผ ๊ณต์ ํ๊ธฐ ๋๋ฌธ์ ๋๋ฆฝ์ ์ธ ํ๋ก์ธ์ค์ ๋ฌ๋ฆฌ ์ค๋ ๋ ๊ฐ ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ  ๋ฐ๋ ๊ฒ์ด ๊ฐ๋จํด์ง๊ณ  ์์คํ ์์ ์๋ชจ๊ฐ ์ค์ด๋ค๊ฒ ๋๋ค.
- ์ฒ๋ฆฌ ๋น์ฉ ๊ฐ์ ๋ฐ ์๋ต ์๊ฐ ๋จ์ถ
  - ํ๋ก์ธ์ค ๊ฐ์ ํต์ (IPC)๋ณด๋ค ์ค๋ ๋ ๊ฐ์ ํต์ ์ ๋น์ฉ์ด ์ ์ผ๋ฏ๋ก ์์๋ค ๊ฐ์ ํต์ ์ ๋ถ๋ด์ด ์ค์ด๋ ๋ค.
  -> ์ค๋ ๋๋ Stack ์์ญ์ ์ ์ธํ ๋ชจ๋  ๋ฉ๋ชจ๋ฆฌ๋ฅผ ๊ณต์ ํ๊ธฐ ๋๋ฌธ
 - ํ๋ก์ธ์ค ๊ฐ์ ์ ํ ์๋๋ณด๋ค ์ค๋ ๋ ๊ฐ์ ์ ํ ์๋๊ฐ ๋น ๋ฅด๋ค.
   โ> Context Switching์ ์ค๋ ๋๋ Stack ์์ญ๋ง ์ฒ๋ฆฌํ๊ธฐ ๋๋ฌธ


![](https://images.velog.io/images/lck0827/post/22601ed1-2e01-4bc2-a4ac-4cc4e470359d/image.png)

---

### ๐ Reference
1. https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html
2. https://velog.io/@raejoonee/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98-%EC%B0%A8%EC%9D%B4
3. byfuls.com/programming/read?id=61
4. https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Process%20vs%20Thread.md