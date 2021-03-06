## 🌈 쿠키(cookie), 세션(session) 그리고 캐쉬(cache)란?

## 쿠키(cookie)란?
- 사용자의 브라우저에 저장되는 서버에서 받은 데이터 파일이며, 통신할 때 HTTP 헤더에 포함되는 텍스트 데이터 파일

- 해당 사용자의 컴퓨터를 사용한다면 누구나 쿠키에 입력된 값을 쉽게 확인 가능

- 쿠키는 변수(이름 : 값)를 텍스트 파일로 저장한 파일

### 쿠키의 특징
- 정보의 유효기간을 지정할 수 있다.
 -> 유효기간 미지정 시 메모리에 기록되어 웹 브라우저 종료 시 소멸되고, 지정 시 하드디스크에 저장 됨
 
- 쿠키 값은 UTF-8로 인코딩 / 디코딩 해서 사용한다.

- 로그인 정보 같이 유저가 굳이 다시 서버에 다시 요청하기에는 비효율적인 정보를 로컬에 저장해둠으로서 생산성을 높이는 것이 목적이다.

- 사용 예시 : 자동 로그인 , 오늘 그만보기 팝업창 등

![](https://images.velog.io/images/lck0827/post/a9e6ad4d-912d-4dba-ba31-ae6f1d52e653/image.png)


### 쿠키의 장점
- 쿠키를 사용하면 속도가 빠르다. 서버에 정보 요청 없이 바로 꺼내올 수 있기 때문이다. 
- 서버에 요청 빈도가 줄어들어 서버 부하가 낮다. 

### 쿠키의 단점
- 다른 사람이 해당 컴퓨터를 사용하거나 해킹하여 접속한다면 하드 디스크에서 쿠키를 열어보기 쉽다. 따라서 보안성이 낮다.
- 클라이언트는 총 300개의 쿠키를 저장할 수 있고, 하나의 도메인 당 20개의 쿠키만 가질 수 있다. 20개가 넘어가면 오래된 쿠키부터 자동 삭제 된다. 
- 쿠키 하나당 4KB 까지 저장 가능하다. 

---

## 세션(session)이란?
- 웹 서버 내 웹 컨테이너에 클라이언트의 상태 또는 값을 저장해 둔 것
- 주로 중요한 데이터를 저장할 때 사용하며 브라우저를 종료할 때까지 유지 된다. 

### 세션의 구성 요소
: **세션 ID, 세션 생성 시간, 세션의 최근 접근 시간**

👉 웹 서버에서 클라이언트를 구분하기 위해 세션 ID를 생성
👉 세션을 만들면서 별도로 웹 브라우저에 세션 ID 값이 담긴 쿠키를 만들어 저장한다. 그리고 웹 서버에 요청할 때 이 쿠키도 같이 보내서 웹 서버가 세션 ID를 비교하여 세션 값을 꺼내 읽어올 수 있게 된다. 

### 세션 동작 방식
1) 클라이언트가 서버에 접속 시, 세션 ID를 발급한다.
2) 서버에서는 클라이언트로 발급해준 세션 ID를 쿠키를 이용해서 저장
3) 클라이언트는 다시 페이지에 접속할 때, 쿠키에 저장된 세션 ID를 서버에 전달
4) 서버는 Request Header에 쿠키 정보(세션 ID)로 클라이언트를 판별


### 세션의 특징
- 웹 컨테이너는 하나의 웹 브라우저마다 한 세션을 생성한다.
- 브라우저가 닫히거나 서버 내에서 세션 삭제시 사라지며, 유효 기간 설정이 가능하다. 
--> 세션에 유효기간 설정이 되어있지 않다면, 나중에 세션 객체가 웹 컨테이너에 쌓이게 되서 메모리가 부족해질 수 있다.
- 주로 로그인 정보 유지(유효 기간 별도 지정)에 사용된다. 
- 쿠키보다 보안성이 높으나 쿠키보다 느리다. 

---

## 캐시(cache)란?
- 사용자의 브라우저에 저장되는 서버에서 받은 데이터를 저장한 파일이다. 
- 이미지(jpg,png 등), css/js, 배너 등 변경사항이 크지 않고 재사용될 것 같거나 용량이 큰 리소스를 임시로 저장하여 렌더링 속도를 높인다.
- 캐시를 사용하지 않는다면 웹 페이지의 출력 속도가 느려지고 웹 서버의 부하가 커지게 된다. 

> **✔ 캐시 히트 (Cache Hit)**
\- CPU가 참조하려는 메모리가 캐시에 존재하고 있는경우
> 
✔ **캐시 미스 (Cache Miss)**
\- 캐시 히트와 반대로, 메모리에 캐시가 존재하지 않는경우


---
📝 **Reference**
1. https://maivve.tistory.com/180
2. https://ryusae.tistory.com/7