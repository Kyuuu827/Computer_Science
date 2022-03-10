## 🌈 Blocking/Non-blocking & Synchronous & Asynchronous

> 🧐 **이전에 자바스크립트, Node.js를 공부했을때도 그렇고 비동기 개념은 매우 중요하게 다뤄진다. 비동기에 대한 개념은 이제 어느정도 확실하게 알고있지만 Blocking과 Synchronous, Non-blocking과 Asynchronous의 개념이 혼동되는 경우가 많아 정리해 보고자 한다. **

---

## Blocking vs Non-blocking
- Blocking과 Non-blocking은 **'제어권'**의 관점에서 접근하는 방식이다. 

- Blocking이라는 것은 한국어로 '막혀 있다' 라는 뜻으로, 호출된 함수가 제어권을 넘겨주지 않아 호출한 함수측에서는 다른 작업을 수행할 수 없어 제어권이 돌아오기를 기다리는 것을 말한다. 

- 반대로 Non-Blocking은, 제어권이 넘겨 지지 않으므로, 대상의 작업 처리 여부와 상관이 없이 호출한 함수 측에서 제어권을 가지고 다음 작업들을 수행할 수 있다.

- 다시말해 Non-Blocking 으로 작동한다는 것은, 제어권은 호출한 함수 측에서 계속해서 가지고 있기 때문에, 만약에 다른 함수가 실행된다면 그 함수에 대한 결과값을 받을 수 있는 상황인지 체크하는 과정이 필요한 것이다. 


## Synchronous vs Asynchronous
- Synchronous, Asynchronous는 '시간'의 관점에서 접근해야 한다.

- 호출된 함수와 호출한 함수 두 함수 관점에서 바라보면, Synchronous 는 두 함수의 시작과 종료 시간에 대해 맞춰져야한다는 뜻이다. 스택에서 함수 하나가 빠져 나가고, 다음 함수가 실행이 되고, 이런 느낌으로 시간이 지켜지면서 순차적으로 일어날 수 있는 것을 의미한다. 실제로 한국어로 동기화 또한 그런 맥락에서 들어맞는다고 볼 수 있다. 

- Asynchronous는 두 함수의 시작과 종료 시간이 완전히 맞춰지지가 않는다는 뜻이다. 호출한 함수는 호출된 함수의 결과를 기다리지만, 제어권이 어떻게 될지는 관심이 없다. 비동기적으로 다른 함수가 실행이 된다는 데에 의미가 있고 호출된 함수의 결과값을 받게 되는데 다른 비동기 함수로 부터 받은 결과값에 대해 모든 순서가 완전히 보장이 될 순 없다는 의미이다. Ajax 가 대표적인 그 예시이다.

---

## Blocking/Non-blocking & Synchronous/Asynchronous

- 위에서 각각의 개념들을 살펴보았듯이, Blocking이라고 반드시 Sync가 되는 것이 아니다. 그리고 Non-blocking이라고 반드시 Async인 것도 아니다. 
- 즉 Blocking/Non-blocking과 Sync/Async는 별개의 개념이다. 

![](https://images.velog.io/images/lck0827/post/fba374d9-957e-4f1e-b035-dfbc48974155/image.png)
출처: [homoefficio님 블로그](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)

- 몇 가지 모델을 살펴 보도록 하자.


### Non-blocking + Synchronous

![](https://images.velog.io/images/lck0827/post/54ec115b-a016-431c-a687-2c532f77a745/image.png)

- **제어권을 호출된 함수에게 넘겨주지 않는다 (Non-blocking)**

- **But, 결과값의 순서는 보장된다 (Synchronous)
**

- 제어권을 호출된 함수에게 넘겨주지 않기 때문에 (Non-blocking), 프로그램 측에서는 호출한 함수가 끝나기를 기다리면서 다른 작업들을 수행할 수가 있는 것이 핵심이다. 
하지만 Synchronous의 특성 때문에, 시간을 맞춰주기 위해 매 시간 호출된 함수가 끝났는지 테스팅하는 요청이 필요하다.

### Blocking + Asynchronous
![](https://images.velog.io/images/lck0827/post/db0e53b8-2a18-4791-9c6b-e08af60d6ef6/image.png)

- **제어권을 호출된 함수에게 넘겨주게 된다 (Blocking)**

- **But, 결과값의 순서는 보장되지 않으며 결과를 바탕으로 이루어진다 (Asynchronous)**

- 호출한 함수는 제어권을 호출된 함수에게 넘겨주어 다른 작업들을 할 수 없게 된다. 호출된 함수에 대한 결과값의 응답을 받은 후, 제어권 또한 넘겨받게 되어 다른 작업들이 실행된다. 그리고 Asynchronous의 특성을 가진다. 사실 이런 케이스는 비효율적이기 때문에 거의 사용되지 않는다. 환경이 다른 두 프로그램을 혼합에서 사용하면서 겪게 되는 희귀한 경우 (ex. Node.js와 MySQL을 함께 사용하는 경우)에 사용되어진다고 한다.

---

### 📝 Reference
1. http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/
2. https://programming119.tistory.com/238
3. https://jh-7.tistory.com/25