## 🌈 Garbage Collection

> 🧐 **지난 TIL-080글에서 파이썬의 GIL개념을 공부하며 파이썬의 가비지 컬렉션 방식에 대해 언급을 했었다. 이번 글에서는 가비지 컬렉션에 대해 좀 더 자세히 알아보고자 한다. **

## 가비지 컬렉션 (Garbage Collection,GC)란?

- 메모리 관리 기법 중의 하나로, 시스템에서 더이상 사용하지 않는 동적 할당된 메모리 블록을 찾아 자동으로 사용 가능한 자원으로 회수하는 것을 뜻한다.  

- 더 이상 필요없어진 메모리를 쓰레기(Garbage), 시스템에서 가비지 컬렉션을 수행하는 부분을 가비지 컬렉터(Garbage Collector)라 부른다. 

---

### 메모리 누수(Memory Leak)란?

- 메모리의 힙(Heap) 영역에 할당된 부분이 참조되지 않는데도 해제되지 않은 채로 메모리를 계속 점유하고 있는 것이다. 

![](https://images.velog.io/images/lck0827/post/2a07dac4-ee5b-45a8-80e9-ea3b3a1fa3c4/image.png)

---

### 가비지 컬렉터의 원리
- 가비지 컬렉션 작업을 하는 가비지 컬렉터는 아래와 같은 일을 한다.
  - 메모리 할당
  - 사용 중인 메모리 인식
  - 사용하지 않는 메모리 인식
  
- 프로그램을 실행할 때 메모리를 관리하는 OS에 프로그램 실행에 필요한 메모리를 요청하게 되는데, 이때 할당하게 되는 메모리 저장 주소를 offset 주소라고 한다. 

- 할당된 메모리들은 프로그램이 작동하면 필연적으로 가비지가 발생하게된다. 
기존에 가리키고 있던 메모리가 새롭게 선언 혹은 형변환이 되면, 다른 곳을 가리키게 되면서 주소를 잃어버리게 되고 다시 찾을 수 없게 되면서 정리되지 않은 메모리가 생겨버리기 때문이다. 
- 이때 가비지 컬렉터는 가비지를 다른 용도로 사용할 수 있도록 메모리 해제를 시킨다.


---

### 파이썬의 Garbage Collector
- CPython에서 메모리를 관리하는 방법에는 크게 2가지가 있다. 
1) Generational Garbage Collection(세대별 가비지 컬렉션)
2) Reference Counting (레퍼런스 카운팅)
👉 이중에서 **레퍼런스 카운팅 **방법을 주로 사용한다. (지난 TIL-080 글에도 설명이 되어 있다.)

- 레퍼런스 카운팅은, 객체를 만들때마다 얼마나 그 객체가 사용되고 있는지 카운팅하고 객체가 참조될때마다 증가되고 참조가 해제되면 감소한다. 그리고 0이되면 메모리 할당을 릴리즈 하는 방법이다. 

- `sys` 라이브러리의 `getrefcount` 함수로 객체의 참조 횟수를 알 수 있다. 

```python
import sys

text = '백엔드 개발자 CK!'
print(sys.getrefcount(text))

lst = [text]
print(sys.getrefcount(text))

tup = (text)
print(sys.getrefcount(text))

dic = {'text': text}
print(sys.getrefcount(text))

a = text
print(sys.getrefcount(text))

>>> 2
>>> 3
>>> 4
>>> 5
>>> 6
```

✔ 변수로 지정되는 순간부터가 참조 횟수 1회이다. 
✔ 첫 print 작동하며 1회 추가
✔ 리스트에 인용되며 1회 추가
✔ 두번째 print 부터는 횟수 추가 안됨
✔ tuple에 인용되며 1회 추가
✔ 딕셔너리에 인용되며 1회 추가
✔ 다른 변수에 할당되며 1회 추가


> 🙆‍♂️ **같은 기능의 프로그램이더라도 메모리 관리에 따라 성능이 극명하게 다를 수 있다. 한정된 메모리를 효율적으로 사용할 수 있는 코드를 작성하는 것은 개발자의 몫이기 때문에 가비지 컬렉션과 같은 개념의 동작원리, 내부 구조를 좀 더 확실히 공부할 필요가 있는 것 같다. **

---

### 📝 Reference
1. https://ko.wikipedia.org/wiki/%EC%93%B0%EB%A0%88%EA%B8%B0_%EC%88%98%EC%A7%91_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)
2. https://blog.metafor.kr/163
3. https://beststar-1.tistory.com/15
4. https://twinparadox.tistory.com/623