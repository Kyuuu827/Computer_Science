## 🌈 REST API

## REST(Representational State Transer)란?
: **자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미**

- 소프트웨어 개발 아키텍처의 한 형식이며, REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.

- REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.

- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시

- HTTP Method(POST, GET, PUT, DELETE) 사용
- 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미한다.


### REST의 구성요소

- 자원 (Resource): URI
  - 모든 자원에 고유한 ID가 존재, 이 자원은 Server에 존재한다.
자원을 구별하는 ID는 ‘/users/signin’와 같은 HTTP URI 다.
Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
- 행위 (Verb): HTTP Method
  - HTTP 프로토콜의 Method(GET, POST, PUT, DELETE)를 사용한다.

- 표현 (Representation of Resource)
  - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
  - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있으며, JSON 또는 XML의 형식으로 데이터를 주고 받는 것이 일반적이다. 

### REST의 필요성
- 분산 시스템을 위함이다. 
거대한 애플리케이션을 모듈, 기능별로 분리하기 쉬워졌다. RESTful API를 서비스하기만 하면 어떤 다른 모듈 또는 애플리케이션들이라도 RESTful API를 통해 상호간에 통신을 할 수 있다. 

- WEB브라우저 외의 클라이언트를 위함이다(멀티 플랫폼).
최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.


### REST의 장단점
#### 😃 장점
- HTTP 프로토콜의 인프라 기반으로 설계되기 때문에 REST API 사용을 위한 별도의 인프라가 필요치 않다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

#### 😰 단점
- 정확한 표준 규약이 존재하지 않는다. 관리의 어려움과 좋은(공식화 된) API 디자인 가이드가 존재하지 않음을 의미하며, REST API는 많은 사람들이 하나씩 쌓아올리는 ‘정당화 된 약속들’ 로 구성되고 움직이게 된다.
- HTTP Method의 종류와 형태가 제한적이다.

---

## REST API(RESTful API) 란?
- REST API의 정의
  - REST API(RESTful API)란 REST 아키텍처의 제약 조건을 준수하는 애플리케이션 프로그래밍 인터페이스를 뜻한다.

  - 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.

### REST API의 특징
- 사내 시스템들도 REST 기반으로 시스템을 분산해 **확장성과 재사용성을 높여 유지보수 및 운용을 편리하게** 할 수 있다.

- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.

- REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.


### RESTful API의 목적
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니다. 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 목적이다.

### REST API 설계 규칙
1) 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

2) URI 마지막 문자로 슬래시(/)를 포함하지 않는다

3) 하이픈(-)은 URI가독성을 높이는데 사용

4) 밑줄(_)은 URI에 사용하지 않습니다.

5) URI 경로는 소문자가 적합합니다
대소문자에 따라 다른 리소스로 인식하게 되기 때문이다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하고 있다.

6) 파일 확장자는 URI에 포함시키지 않습니다.

7) 리소스 간에는 연관 관계가 있는 경우
	👉 _/리소스명/리소스 ID/관계가 있는 다른 리소스명_


---

### 📝 Reference
1. https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
2. https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80
3. https://www.redhat.com/ko/topics/api/what-is-a-rest-api