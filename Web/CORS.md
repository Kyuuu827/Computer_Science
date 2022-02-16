## 🌈 CORS(Cross-Origin Resource Sharing)


## CORS 란? 
- 교차 출처 리소스 공유(Cross-origin resource sharing, CORS)는 HTTP 헤더를 사용하여 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 
- 웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행한다.
- 출처의 정의를 알기 위해서는 우선 URI의 구조에 대해 알아야 한다. 

### 👉 URI(Uniform Resource Identifier)의 구조
- URI(Uniform Resource Identifier)는 인터넷에 있는 접근가능한 자원을 나타내는 유일한 주소를 일관되게 표현하는 형식을 일컫는다.
URI의 하위 개념으로는 URL과 URN이 있다.


![](https://images.velog.io/images/lck0827/post/682ced64-72f1-4b7e-b958-06af569a3c50/image.png)

- 프로토콜의 HTTP는 80번, HTTPS는 443번 포트를 사용하는데, 이 두 포트는 생략 가능하다.

### 👉 출처(Origin)란? 
- 출처(Origin)는 URL의 Protocol, Host, Port로 정의 된다. 두 객체의 Protocol, Host, Port가 일치할 경우 같은 출처라고 결론 내릴 수 있다. 

- 개발자 도구의 콘솔 창에`location.origin`를 실행하면 출처를 확인할 수 있다.
![](https://images.velog.io/images/lck0827/post/d59ef611-d2e6-4437-b484-faefde71e9ce/image.png)

## 동일 출처 정책(Same-Origin Policy, SOP)이란?
- 동일 출처 정책(Same-Origin Policy, SOP)은 어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 중요한 보안 방식이다. 
- 잠재적으로 해로울 수 있는 문서를 분리함으로써 공격받을 수 있는 경로를 줄여준다.
- 정리하자면, 동일 출처 정책은 웹 브라우저 보안을 위해 Protocol, Host, Port가 동일한 서버로만 ajax 요청을 주고 받을 수 있도록 한 정책이다.

### 👉 동일 출처 정책의 장점
동일 출처 정책을 지키면 외부 리소스를 가져오지 못해 불편하지만, 동일 출처 정책은 CSRF(Cross-Site Request Forgery)나 XSS(Cross-Site Scripting) 등의 보안 취약점을 노린 공격을 방어할 수 있다. 하지만 현실적으로는 외부 리소스를 참고하는 것은 필요하기 때문에 CORS 조항을 통해 외부 리소스를 가져올 수 있게 한다.

> 🌈 **외부 리소스를 사용하기 위한 SOP의 예외 조항이 CORS이다. 클라이언트의 요청이 있을 경우, 서버와 클라이언트가 정해진 헤더를 통해 서로 요청이나 응답에 반응할지 SOP 또는 CORS 정책에 따라 웹브라우저가 평가하고 결정한다. **


## CORS의 동작원리
- CORS의 동작의 기본적인 flow를 살펴보면 아래와 같다.
  1. 웹 클라이언트 어플리케이션이 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보내게 되는데, 이때 브라우저는 요청 헤더의 Origin이라는 필드에 요청을 보내는 출처(ex. Origin: https://velog.io)를 함께 명시한다.
  2. 서버가 해당 request에 대한 응답을 할 때, response header의 Access-Control-Allow-Origin 이라는 값에 “이 리소스 접근 허용된 출처”를 알려준다. 
  3. 브라우저는 자신이 보냈던 request의 Origin과 서버가 보내준 response의 Access-Control-Allow-Origin을 비교하여 response의 유효성을 결정한다. 

- CORS 동작은 위와같은 기본적인 flow로 흘러가지만, 이제 부터 소개할 Request 방식에 따라 flow는 변경된다.  

### 1. Simple Request
- Simple Request는 서버에게 바로 요청을 보내는 방법이다. 서버에 API를 요청하고, 서버는 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보낸다. 브라우저는 Access-Control-Allow-Origin 헤더를 확인해서 CORS 동작을 수행할지 판단한다.
- 아래 그림은 자바스크립트에서 API를 요청할 때 브라우저와 서버의 동작을 나타내는 그림이다. 

![](https://images.velog.io/images/lck0827/post/aa2f26a4-bf99-4509-8191-ca7f7377e1f4/image.png)

#### Simple Request의 조건
- Simple Request를 보낼 수 있으려면 몇 가지 조건이 성립되어야 한다. 
  - 요청 메서드(method)가 GET, HEAD, POST 중 하나여야 한다.
  - Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안된다.
  - Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나를 사용해야 한다.
  
 
> 😰 세 가지의 조건 중 첫 번째 조건은 쉬운 조건 이지만 두 번째, 세 번째 조건은 충족시키기 어려운 조건이다. 두 번째 조건은 사용자 인증에 사용되는 Authorization 헤더도 포함되지 않아 충족시키기 어려운 조건이며, 세 번째 조건은 많은 REST API들이 Content-Type으로 application/json을 사용하기 때문에 만족시키기 어려운 조건이다.

### 2. Preflight Request
- Preflight 요청은 서버에 예비 요청을 보내서 안전한지 판단한 후 본 요청을 보내는 방법이다. 따라서 요청을 한번에 보내지 않고 예비 요청, 본 요청으로 나누어 보낸다.
- 이 때 예비 요청을 Preflight Request라고 하며 HTTP method 중 `OPTION` method가 사용된다. 

![](https://images.velog.io/images/lck0827/post/d5ee19dc-02d8-45d1-b81f-201ecb1bfba9/image.png)

- `OPTIONS` method로 서버에 예비 요청을 먼저 보내면, 서버는 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보낸다. 브라우저는 단순 요청과 동일하게 Access-Control-Allow-Origin 헤더를 확인해서 CORS 동작을 수행할지 판단한다.
- 이 후 본 요청을 보내는 것이 안전하다고 판단이 되면 같은 엔드포인트로 본 요청을 보내게 되고 서버로 부터 받은 응답을 브라우저가 자바스크립트에게 넘겨준다. 


### 3. Credentialed Request
- Credentialed Request는 CORS의 기본 방식이라기 보단 다른 출처 간 통신의 보안을 좀 더 강화할때 사용하는 방법이다. 

- 기본적으로 브라우저가 제공하는 비동기 리소스 요청 API인 XMLHttpRequest 객체나 fetch API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다. 이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로 credentials 옵션이다.

👉 credentials 옵션에는 아래와 같은 3가지 값을 사용할 수 있다. 
>  same-origin (기본값) :	같은 출처 간 요청에만 인증 정보를 담을 수 있다
include :	모든 요청에 인증 정보를 담을 수 있다
omit :	모든 요청에 인증 정보를 담지 않는다

> **예시)**
```javascript
fetch('https://velog.io/@lck0827', {
  credentials: 'include', // Credentials 옵션 변경
});
```
👉 동일 출처 여부와 상관없이 무조건 요청에 인증 정보가 포함되도록 설정한 것이다.

- 위와 같은 옵션을 사용하여 리소스 요청에 인증 정보가 포함된다면, 브라우저는 다른 출처의 리소스를 요청할 때 단순히 Access-Control-Allow-Origin만 확인하는 것이 아니라 좀 더 까다로운 검사 조건을 추가하게 된다.

- 요청에 인증 정보가 담겨있는 상태에서 다른 출처의 리소스를 요청하게 되면 브라우저는 CORS 정책 위반 여부 검사시 아래의 두 가지 룰을 추가하게 된다.

> 1. Access-Control-Allow-Origin에는 *를 사용할 수 없으며, 명시적인 URL이어야한다.
2. 응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야한다.

---

## CORS 에러 해결 방법

### Access-Control-Allow-Origin 세팅하기
- CORS 에러 해결의 가장 대표적인 방법은, 서버에서 Access-Control-Allow-Origin 헤더에 알맞은 값을 세팅해주는 것이다.
- `*`로 설정해 주면 모든 출처의 요청을 허가하여 편하긴 하지만 보안적인 이슈가 발생할 수 있으므로 가급적이면 `Access_Control_Allow_Origin:https://velog.io/@lck0827` 와 같이 출처를 명시해 주는 것이 좋다. 

- 이 헤더는 Nginx나 Apache와 같은 서버 엔진의 설정에서 추가할 수도 있지만, 복잡하므로 소스 코드 내에서 응답 미들웨어 등을 사용하여 세팅하는 것이 편리하다.
- **Spring, Express, Django와 같이 대중적인 백엔드 프레임워크의 경우에는 모두 CORS 관련 설정을 위한 세팅이나 미들웨어 라이브러리를 제공하여 세팅하기가 용이하다. **

---

### Django - cross origin HTTP 요청 허가시키기
- django에서는 CORS를 해결하기위한 패키지를 제공하고 있다. 
`pip install django-cors-headers`

- 설치 후, settings.py의 INSTALLED_APP과 MIDDLEWARE에 아래 정보를 추가한다. 
```python
INSTALLED_APPS = [
...
	'corsheaders'
]

MIDDLEWARE = [
...
	'corsheaders.middleware.CorsMiddleware',

]
```
- setting.py의 하단에 아래의 코드를 추가한다.
```python
##CORS
CORS_ORIGIN_ALLOW_ALL=True 
# 모든 호스트를 허용시키기 위해 CORS_ORIGIN_ALLOW_ALL을 True로 지정
CORS_ALLOW_CREDENTIALS = True
# CORS_ALLOW_CREDENTIALS은 쿠키가 cross-site HTTP 요청에 포함될 수 있게하기 위한 설정이고 Default는 False임.

CORS_ALLOW_METHODS = (
    'DELETE',
    'GET',
    'OPTIONS',
    'PATCH',
    'POST',
    'PUT',
)

CORS_ALLOW_HEADERS = (
    'accept',
    'accept-encoding',
    'authorization',
    'content-type',
    'dnt',
    'origin',
    'user-agent',
    'x-csrftoken',
    'x-requested-with',
)

```

- 특정 호스트의 접근만 허용하기 위해서는 , `CORS_ORIGIN_ALLOW_ALL=True` 설정을 삭제하고 CORS_ORIGIN_WHITELIST를 추가한다. 

```python
##CORS
CORS_ORIGIN_WHITELIST = (
    "https://example.com",
    "https://sub.example.com",
    "http://localhost:8080",
    "http://127.0.0.1:9000"
)
CORS_ALLOW_CREDENTIALS = True

CORS_ALLOW_METHODS = (
    'DELETE',
    'GET',
    'OPTIONS',
    'PATCH',
    'POST',
    'PUT',
)

CORS_ALLOW_HEADERS = (
    'accept',
    'accept-encoding',
    'authorization',
    'content-type',
    'dnt',
    'origin',
    'user-agent',
    'x-csrftoken',
    'x-requested-with',
)

```

---

### Node.js Express - 미들웨어 CORS
- 미들웨어 cors를 사용하여 세팅해주는 방식이다. 

```javascript
npm i cors --save
```
```javascript
const express = require('express');
const cors = require('cors');
const app = express();
 
app.use(cors());
```
- 미들웨어 설치 후 App.js에 미들웨어를 추가하면 세팅 완료된다.

- 위와 같이 아무런 옵션없이 app.use(cors());로 설정한다면 모든 cross-origin 요청에 대해 응답을 해주게 된다.
만약 모든 요청에 응답하는 것이 아닌 보안상 특정 도메인 요청만 받아야 하는 경우 혹은 특정 요청에만 응답하는 경우에는 아래와 같이 옵션들을 다양하게 설정해 줄 수 있다.

** 1. 특정 도메인 접근 허용**
```javascript
const corsOptions = {
  origin: 'https://velog.io', // 접근 권한을 부여하는 도메인
  credentials: true, // 응답 헤더에 Access-Control-Allow-Credentials 추가
  optionsSuccessStatus: 200 // 응답 상태 200으로 설정 
};

app.use(cors(corsOptions));
```

** 2. 특정 요청 접근 허용**
```javascript
app.get('/products/:id', cors(), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for a Single Route'})
});
```
이외에도 특정 method 등을 옵션으로도 설정할 수도 있다.

---

### 프록시(Proxy) - 클라이언트 단 해결 방법
- 프록시 서버는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램을 가리킨다. 
- 주로 보안의 문제로 직접 통신하지 못하는 두 개의 컴퓨터 사이에서 서로 통신할 수 있도록 사용되기도 한다. 

![](https://images.velog.io/images/lck0827/post/cce58a23-e5e5-4ddb-a9a5-98a85f73cf82/image.png)

- 클라이언트 - 서버 중간에서 요청을 받아 Access-Control-Allow-Origin 헤더를 설정하여 서버에 요청하는 방법으로 해결할 수 있다.

---
📝 **Reference**
1. https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy
2. https://beomy.github.io/tech/browser/cors/
3. https://evan-moon.github.io/2020/05/21/about-cors/