## ๐ N+1 Query Problem

## N+1 Problem ์ด๋?
- ์ฐ๊ด ๊ด๊ณ์์ ๋ฐ์ํ๋ ์ด์๋ก ์ฐ๊ด ๊ด๊ณ๊ฐ ์ค์ ๋ ์ํฐํฐ๋ฅผ ์กฐํํ  ๊ฒฝ์ฐ์ ์กฐํ๋ ๋ฐ์ดํฐ ๊ฐฏ์(n) ๋งํผ ์ฐ๊ด๊ด๊ณ์ ์กฐํ ์ฟผ๋ฆฌ๊ฐ ์ถ๊ฐ๋ก ๋ฐ์ํ์ฌ ๋ฐ์ดํฐ๋ฅผ ์ฝ์ด์ค๊ฒ ๋๋ค. ์ด๋ฅผ **N+1 ๋ฌธ์ **๋ผ๊ณ  ํ๋ค.
๐ ์ฝ๊ฒ ๋งํด์, ์ฟผ๋ฆฌ 1๋ฒ์ผ๋ก N๊ฑด์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์๋๋ฐ ์ํ๋ ๋ฐ์ดํฐ๋ฅผ ์ป๊ธฐ ์ํด ์ด N๊ฑด์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์ดํฐ ์ ๋งํผ ๋ฐ๋ณตํด์ 2์ฐจ์ ์ผ๋ก ์ฟผ๋ฆฌ๋ฅผ ์ํํ๋ ๋ฌธ์ ๋ค.

### โ Django์์์ N+1 Problem

#### **django ORM์ Lazy-Loading ๋ฐฉ์์ด๋ค**.
- Lazy-Loading ๋ฐฉ์์ ์ฌ์ฉํ๋ฉด ORM์์ ๋ช๋ น์ ์คํํ  ๋๋ง๋ค ๋ฐ์ดํฐ๋ฒ ์ด์ค์์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ค๋ ๊ฒ์ด ์๋๋ผ ๋ชจ๋  ๋ช๋ น ์ฒ๋ฆฌ๊ฐ ๋๋๊ณ  ์ค์ ๋ก ๋ฐ์ดํฐ๋ฅผ ๋ถ๋ฌ์์ผ ํ  ์์ ์ด ์์ ๋ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ฟผ๋ฆฌ๋ฅผ ์คํํ๋ค.

- ์ด ๋ฌธ์ ์ ํด๊ฒฐ ๋ฐฉ์์ผ๋ก **Eager-Loading** ๋ฐฉ์์ด ์๋ค. Eager-Loading๋ฐฉ์์ ์ฌ์ ์ ์ธ ๋ฐ์ดํฐ๋ฅผ ํฌํจํ์ฌ ์ฟผ๋ฆฌ๋ฅผ ์์ฒญํ๊ธฐ ๋๋ฌธ์ ๋นํจ์จ์ ์ผ๋ก ๋์ด๋๋ ์ฟผ๋ฆฌ ์์ฒญ์ ๋ฐฉ์งํ๋ค. 

### โ Django์์ Eager-Loading ๊ตฌํ์ ์ํ ๊ธฐ๋ฒ

๐ **select_related** 
- ์ฐธ์กฐํ๋ ๋์์ด ์ค๊ฐํ์ด๋ธ์ด ์๋ ์, Join ์ฟผ๋ฆฌ๋ฌธ์ ์ด์ฉํด์ data๋ฅผ ํธ์ถํ๋ค.

- ์ฆ, ๋ ํ์ด๋ธ๊ฐ join์ ํ  ์ ์๋ ๊ตฌ์กฐ์์ ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.
  join์ ํด์ ํธ์ถํ๊ธฐ ๋๋ฌธ์, ์ฟผ๋ฆฌ๊ฐ 1๋ฒ ์์ฒญ ๋๋ค. 

- ๋ฐ๋ผ์ ์ค๊ฐํ์ด๋ธ์ ์ด์ฉํด์ ๊ด๊ณ๋ฅผ ํ์ฑํ๋, many-to-many ๋ชจ๋ธ์์๋ ์ฌ์ฉํ  ์ ์๊ณ , foreign-key , one-to-one๊ณผ ๊ฐ์ single-valued relationships์์๋ง ์ฌ์ฉ์ด ๊ฐ๋ฅํ๋ค.

  
๐ **prefetch_related** 
- 2๊ฐ์ ํ์ด๋ธ์ ๊ฐ๊ฐ ํธ์ถํ์ฌ, django๋ด์์ ๋ณํฉํ๋ค.

- select_related์ ์ฌ์ฉํ  ์ ์๋ many-to-many๋ชจ๋ธ์์ ์ฌ์ฉํฉ๋๋ค. 

- foreign-key , one-to-one, ๊ทธ๋ฆฌ๊ณ  one-to-many ๋ฑ์ ๋ชจ๋  relationships์์ ์ฌ์ฉ ๊ฐ๋ฅํ๋ค. 

- SQL์ **WHERE โฆ IN **๊ตฌ๋ฌธ์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ์ด๋ค.

---

๐โโ๏ธ **์ฌ์ฉ ์์**

```python
        menus = Menu.objects.all()

        menu_data = [{
            'menu_id'   : menu.id,
            'menu_name' : menu.name,
            'image_url' : menu.image_url,
            'categories'  : [{
                'id'   : category.id,
                'name' : category.name,
                'subcategories'   : [{
                    'id'   : subcategory.id,
                    'name' : subcategory.name,
                } for subcategory in category.subcategory_set.all()],
            } for category in menu.category_set.all()],
        } for menu in menus]
```
- ๋ฉ๋ด -> ์นดํ๊ณ ๋ฆฌ -> ์๋ธ์นดํ๊ณ ๋ฆฌ ์์ผ๋ก ๋ฐ์ดํฐ๋ฅผ ํธ์ถํ๋ ์ฝ๋์ด๋ค. ๊ฐ๊ฐ์ ํ์ด๋ธ์ one-to-many ๊ด๊ณ๋ก ์ฐ๊ฒฐ๋์ด ์๋ค. 

- ๊ทธ๋ ๊ธฐ ๋๋ฌธ์ ์ด ๋ชจ๋  ๋ฐ์ดํฐ๋ฅผ ํธ์ถํ๊ธฐ ์ํด์๋ ์ฟผ๋ฆฌ ์์ฒญ ํ์๊ฐ ๋ง์์ง๋ ๊ตฌ์กฐ์ด๋ค. 

โ **์ฟผ๋ฆฌ ์์ฒญ ํ์ : 20ํ**

![](https://images.velog.io/images/lck0827/post/25ce8935-8479-4e3c-8ef4-8feb197f49de/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.01.09.png)

```python
        menus = Menu.objects.prefetch_related('category_set', 'category_set__subcategory_set')

        menu_data = [{
            'menu_id'   : menu.id,
            'menu_name' : menu.name,
            'image_url' : menu.image_url,
            'categories'  : [{
                'id'   : category.id,
                'name' : category.name,
                'subcategories'   : [{
                    'id'   : subcategory.id,
                    'name' : subcategory.name,
                } for subcategory in category.subcategory_set.all()],
            } for category in menu.category_set.all()],
        } for menu in menus]
```
- ์์ ์ฝ๋์์ prefetch_related()๋ฅผ ์ฌ์ฉํ์๋ค. ์นดํ๊ณ ๋ฆฌ์ ์๋ธ์นดํ๊ณ ๋ฆฌ๋ฅผ ์บ์ฑํ์ฌ ์ฟผ๋ฆฌ ์์ฒญ ํ์๋ฅผ ๋๋ผ๋งํฑํ๊ฒ ๊ฐ์์ํฌ ์ ์์๋ค.

โ **์ฟผ๋ฆฌ ์์ฒญ ํ์ : 3ํ**

![](https://images.velog.io/images/lck0827/post/9d4ce115-3d8b-4009-8023-def3e05ddc3b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.01.44.png)

---

### ๐ Reference
1. https://hckcksrl.medium.com/django-n-1-problem-d986b93f5d3e
2. https://incheol-jung.gitbook.io/docs/q-and-a/spring/n+1
3. https://velog.io/@burnkim61/Django-ORM-N1-%EB%AC%B8%EC%A0%9C