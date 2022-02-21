## 🌈 N+1 Query Problem

## N+1 Problem 이란?
- 연관 관계에서 발생하는 이슈로 연관 관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오게 된다. 이를 **N+1 문제**라고 한다.
👉 쉽게 말해서, 쿼리 1번으로 N건의 데이터를 가져왔는데 원하는 데이터를 얻기 위해 이 N건의 데이터를 데이터 수 만큼 반복해서 2차적으로 쿼리를 수행하는 문제다.

### ✔ Django에서의 N+1 Problem

#### **django ORM은 Lazy-Loading 방식이다**.
- Lazy-Loading 방식을 사용하면 ORM에서 명령을 실행할 때마다 데이터베이스에서 데이터를 가져오는 것이 아니라 모든 명령 처리가 끝나고 실제로 데이터를 불러와야 할 시점이 왔을 때 데이터베이스에 쿼리를 실행한다.

- 이 문제의 해결 방식으로 **Eager-Loading** 방식이 있다. Eager-Loading방식은 사전에 쓸 데이터를 포함하여 쿼리를 요청하기 때문에 비효율적으로 늘어나는 쿼리 요청을 방지한다. 

### ✔ Django에서 Eager-Loading 구현을 위한 기법

😃 **select_related** 
- 참조하는 대상이 중간테이블이 아닐 시, Join 쿼리문을 이용해서 data를 호출한다.

- 즉, 두 테이블간 join을 할 수 있는 구조에서 사용 가능하다.
  join을 해서 호출하기 때문에, 쿼리가 1번 요청 된다. 

- 따라서 중간테이블을 이용해서 관계를 형성하는, many-to-many 모델에서는 사용할 수 없고, foreign-key , one-to-one과 같은 single-valued relationships에서만 사용이 가능하다.

  
😃 **prefetch_related** 
- 2개의 테이블을 각각 호출하여, django내에서 병합한다.

- select_related을 사용할 수 없는 many-to-many모델에서 사용합니다. 

- foreign-key , one-to-one, 그리고 one-to-many 등의 모든 relationships에서 사용 가능하다. 

- SQL의 **WHERE … IN **구문을 사용하는 방법이다.

---

🙆‍♂️ **사용 예시**

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
- 메뉴 -> 카테고리 -> 서브카테고리 순으로 데이터를 호출하는 코드이다. 각각의 테이블은 one-to-many 관계로 연결되어 있다. 

- 그렇기 때문에 이 모든 데이터를 호출하기 위해서는 쿼리 요청 횟수가 많아지는 구조이다. 

❗ **쿼리 요청 횟수 : 20회**

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
- 위의 코드에서 prefetch_related()를 사용하였다. 카테고리와 서브카테고리를 캐싱하여 쿼리 요청 횟수를 드라마틱하게 감소시킬 수 있었다.

❗ **쿼리 요청 횟수 : 3회**

![](https://images.velog.io/images/lck0827/post/9d4ce115-3d8b-4009-8023-def3e05ddc3b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.01.44.png)

---

### 📝 Reference
1. https://hckcksrl.medium.com/django-n-1-problem-d986b93f5d3e
2. https://incheol-jung.gitbook.io/docs/q-and-a/spring/n+1
3. https://velog.io/@burnkim61/Django-ORM-N1-%EB%AC%B8%EC%A0%9C