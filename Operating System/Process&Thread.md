## 🌈 프로세스 & 스레드

## 프로세스란?
- 프로그램을 메모리 상에서 실행중인 작업
- 메모리에 올라와 CPU를 할당 받고 실행되고 있는 프로그램의 인스턴스(독립적인 개체)
- 운영체제로부터 시스템 자원을 할당받는 작업의 단위
- 프로그램은 정적인 개념, 프로세스는 동적인 개념이다

### 프로세스의 특징
- 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받는다.
- 프로세스마다 최소 1개의 스레드(메인스레드)를 소유하고 있다.
- 각 프로세스는 별도의 주소 공간에서 실행되며, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없다.
- 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC, inter-process communication)을 사용해야 한다.
  - ex) 파이프, 파일, 소켓 등을 이용한 통신 방법 이용


![](https://images.velog.io/images/lck0827/post/2fcf9f60-dc55-4f62-beb3-f1d3e29cb360/image.png)

✔ Code
- text 영역이라고도 불림
- 실행할 프로그램의 코드가 저장되는 영역
- CPU는 이 영역에 저장된 명령어를 하나씩 가져와 수행
- 프로그램이 시작되고 끝날때까지 메모리 영역에 유지

✔ Data
- 전역(global) 변수와 정적(static)변수가 저장되는 영역
- 프로그램 시작때 할당되고 종료될때 해제된다
- BSS와 GVAR영역을 통틀어 data영역이라 한다
  - BSS : 초기화가 되지 않은 데이터를 저장하기 위한 영역 (RAM에 저장)
  - GVAR : 초기화가 된 데이터를 저장하기 위한 영역 (ROM에 저장)
(초기화 된 데이터는 값을 저장해야하기에 비휘발성 메모리인 ROM에 저장)

✔ Stack
- 프로그램에 의해 사용되는 임시 데이터 영역
- 함수 호출시 생성되는 지역변수, 매개변수를 저장, 함수 종료시 해제
- 메모리 주소는 높은 곳에서 낮은 곳의 방향으로 할당

✔ Heap
- 프로그래머에 의해 할당되고 해제된다
- 메모리를 동적으로 할당하고 할 때 사용되는 메모리 영역 (ex. c언어를 예로 들면 malloc, calloc, ...)
- 스택과 반대로 메모리 주소가 낮은 곳에서 높은 곳의 방향으로 할당

---

## 스레드란?
- “프로세스 내에서 실행되는 여러 흐름의 단위”
- 프로세스의 특정한 수행 경로
- 프로세스가 할당받은 자원을 이용하는 실행의 단위

### 스레드의 특징
- 스레드는 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유한다.
  
- 스레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 같은 프로세스 내에 스레드끼리 공유하면서 실행된다.
- 같은 프로세스 안에 있는 여러 스레드들은 같은 힙 공간을 공유한다. 반면에 프로세스는 다른 프로세스의 메모리에 직접 접근할 수 없다.
- 각각의 스레드는 별도의 레지스터와 스택을 갖고 있지만, 힙 메모리는 서로 읽고 쓸 수 있다.
- 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.

> 📝 **프로세스는 자신만의 고유 공간과 자원을 할당받아 사용하는데 반해, 스레드는 다른 스레드와 공간, 자원을 공유하면서 사용하는 차이가 존재함
**

![](https://images.velog.io/images/lck0827/post/fe4c2813-348b-4624-a027-1a9e3a458be3/image.png)

---

## 멀티 프로세스
- 두개 이상 다수의 프로세서(CPU)가 협력적으로 하나 이상의 작업(Task)을 동시에 처리하는 것. (병렬처리)
- 각 프로세스 간 메모리 구분이 필요하거나 독립된 주소 공간을 가져야 할 경우 사용한다.

✔ **장점 ** 
   - 안전성 (메모리 침범 문제를 OS 차원에서 해결)
   - 여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않는다.

✔ **단점 **
- 각각 독립된 메모리 영역을 갖고 있어, 작업량 많을 수록 오버헤드 발생. Context Switching으로 인한 성능 저하
- 프로세스 사이의 어렵고 복잡한 통신 기법(IPC)
프로세스는 각각의 독립된 메모리 영역을 할당받았기 때문에 하나의 프로그램에 속하는 프로세스들 사이의 변수를 공유할 수 없다.

---

## 멀티 스레드
- 하나의 응용 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리하는 것
- 스레드들이 공유 메모리를 통해 다수의 작업을 동시에 처리하도록 해줌

✔ **장점 ** 
- 독립적인 프로세스에 비해 공유 메모리만큼의 시간, 자원 손실이 감소 전역 변수와 정적 변수에 대한 자료 공유 가능
- 시스템 자원 소모 감소
   - 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.
- 시스템 처리량 증가 (처리 비용 감소)
  - 스레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.
  - 스레드 사이의 작업량이 작아 Context Switching이 빠르다.
- 간단한 통신 방법으로 인한 프로그램 응답 시간 단축
  - 스레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 통신의 부담이 적다.

✔ **단점** 
- 안전성 문제. 하나의 스레드가 데이터 공간 망가뜨리면, 모든 스레드가 작동 불능 상태 (공유 메모리를 갖기 때문)
- 주의 깊은 설계가 필요하다.
- 디버깅이 까다롭다.
- 단일 프로세스 시스템의 경우 효과를 기대하기 어렵다.
- 다른 프로세스에서 스레드를 제어할 수 없다. (즉, 프로세스 밖에서 스레드 각각을 제어할 수 없다.)
- 멀티 스레드의 경우 자원 공유의 문제가 발생한다. (동기화 문제)
- 하나의 스레드에 문제가 발생하면 전체 프로세스가 영향을 받는다.

---

### 멀티 프로세스 대신 멀티 스레드를 사용하는 이유

- 자원의 효율성 증대
  - 멀티 프로세스로 실행되는 작업을 멀티 스레드로 실행할 경우, 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리 가능하다.
  -> 프로세스 간의 Context Switching시 단순히 CPU 레지스터 교체 뿐만 아니라 RAM과 CPU 사이의 캐쉬 메모리에 대한 데이터까지 초기화되므로 오버헤드가 크기 때문
  - 스레드는 프로세스 내의 메모리를 공유하기 때문에 독립적인 프로세스와 달리 스레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.
- 처리 비용 감소 및 응답 시간 단축
  - 프로세스 간의 통신(IPC)보다 스레드 간의 통신의 비용이 적으므로 작업들 간의 통신의 부담이 줄어든다.
  -> 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문
 - 프로세스 간의 전환 속도보다 스레드 간의 전환 속도가 빠르다.
   –> Context Switching시 스레드는 Stack 영역만 처리하기 때문


![](https://images.velog.io/images/lck0827/post/22601ed1-2e01-4bc2-a4ac-4cc4e470359d/image.png)

---

### 📝 Reference
1. https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html
2. https://velog.io/@raejoonee/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98-%EC%B0%A8%EC%9D%B4
3. byfuls.com/programming/read?id=61
4. https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Process%20vs%20Thread.md