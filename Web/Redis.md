## 🌈 Redis (Remote Dictionary Server)

## Redis 란?
- 메모리 기반의 key-value 구조의 데이터 관리 시스템이다. 
- 모든 데이터를 메모리에 저장하고 조회하기 때문에 빠른 Read, Write 속도를 보장하는 NoSQL이다. 
- Redis는 Memcached와 비슷한 캐시 시스템으로서 동일한 기능을 제공하면서 영속성, 다양한 데이터 구조와 같은 부가적인 기능을 지원한다.
- Redis는 모든 데이터를 메모리에 저장하고 조회하는 인메모리 데이터베이스이다. 
- 다른 인메모리 디비들과의 가장 큰 차이점은 레디스의 다양한 자료구조이다.

![](https://images.velog.io/images/lck0827/post/6e942b97-17a1-43c3-af10-672552a7fc06/image.png)

### Redis의 기능
- In-Memory 캐싱
- Pub/Sub 메세지 큐
- 세션 스토어

### Redis가 지원하는 데이터 형식
- Redis는 위에서 언급하였듯이 다양한 자료구조(Collection)를 지원한다. 
✔ **String **
: 가장 일반적인 형태, key-value로 저장하는 형태이다.
✔ **Set**
: 중복된 데이터를 담지 않기 위해 사용하는 자료구조이다. 중복된 데이터를 여러번 저장하면 최종 한번만 저장된다.
✔ **Sorted Set**
: Sets와 유사하고 비반복 String collection, Score 순서를 보장해주는 Collection
✔ **Hash**
: String field와 String Values 사이의 맵, 객체를 나타내는데 사용 가능한 형태이다.
✔ **List**
: Array 형식의 데이터 구조이다. 리스트를 사용하면 처음과 끝에 데이터를 넣고 빼는건 속도가 빠르지만 중간에 데이터를 삽입, 삭제 하는건 어려움이 있다.

### Redis의 특징
- 메모리 기반이기 때문에 휘발성이 있고, 전원이 꺼지면 모든 데이터가 사라짐
- 파일에 메모리 상의 데이터를 저장(DISK)해두고 redis 서버의 실행 시 다시 파일에서 데이터를 읽어와 메모리상에 올린다
- 데이터를 DISK에 저장하는 방식에는 두 가지가 있다.
  - RDB(Snapshotting) 방식
    - 순간적으로 메모리에 있는 내용의 전체를 DISK에 옮겨 담는 방식
  - AOF(Append On File) 방식
    - Redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태
- 데이터 크기가 메모리에 제한 되므로 메모리 크기 이상의 데이터 저장을 위해 redis cluster를 추가해야 한다. 

![](https://images.velog.io/images/lck0827/post/f5d00cb2-69f9-4ee0-86fc-a16bd0bc898f/image.png)
  
### Redis의 장점
- 리스트, 배열과 같은 데이터를 처리하는데 유용하다
  --> value 값으로 다양한 데이터 형식을 지원하기 때문이다.

- 리스트형 데이터의 입력과 삭제가 Mysql보다 10배정도 빠르다.
- 메모리를 활용하지만 영속적인 데이터 보존이 가능하다(Persistence)
  - 명령어로 명시적 삭제, expires를 설정하지 않으면 데이터가 삭제되지 않음
  - 스냅샷 기능을 제공해 메모리 내용을 *.rdb 파일로 저장하여 해당 시점으로 복구할 수 있다.
  - AOF : Redis의 모든 Wirte/Update 연산을 log 파일에 기록 후 서버 재시작 시 순차적으로 재실행, 데이터 복구
  
- 1개의 싱글 쓰레드로 수행되기 때문에, 서버 하나에 여러개의 Redis Server를 띄울 수 있다.(Master-Slave 구조)
  - master-slave 간의 복제는 non-blocking

### Redis의 단점
- In-memory 방식이기 때문에 장애 발생 시 데이터 유실이 발생한다.
- 영속적인 데이터 보존을 위해 스냅샷과 AOF 기능을 통한 복구 방식을 주의해서 작성해야 데이터 유실에 대비할 수 있다.


### Redis vs Memcached

|분류|Redis|Memcached|
|---|-----|---------|
|처리속도|데이터가 디스크와 메모리에 저장되는데 Memcached와 성능 차이가 없음, 빠름|데이터가 메모리에만 저장, 빠름
|데이터 저장 방식|데이터가 디스크에도 저장이 되기 때문에 데이터 복구 가능|데이터가 메모리에만 저장되기 때문에 장애 발생시 데이터 유실
|만료일 지정 방식|만료일을 지정하면 만료된 데이터는 캐시처럼 사라짐|동일
|메모리 재사용|메모리를 재사용하지 않음, 명시적으로만 데이터 제거 가능|저장소 메모리를 재사용, 만료전에 더 이상 데이터를 넣을 메모리가 없으면 LRU 알고리즘에 따라 데이터 삭제
|데이터 타입|다양한 데이터 타입 지원|문자열만 지원


---

### 📝 Reference
1. https://devlog-wjdrbs96.tistory.com/374
2. https://genesis8.tistory.com/189
3. https://n1tjrgns.tistory.com/282
4. https://blog.naver.com/waws01/60196621306