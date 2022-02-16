## 🌈 HTTP & HTTPS 

## HTTP(HyperText Transfer Protocol)

> 지난번 작성한 [HTTP](https://velog.io/@lck0827/TIL-031-HTTP) 글을 통해 HTTP에 대해 간략하게 정리한적이 있었다. 이번에는 좀 더 자세하게 공부하고, 보안이 강화된 HTTPS에 대해서도 알아보고자 한다. 

### HTTP 란?

- 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약(protocol)
  - 프로토콜(protocol)이란, 컴퓨터 내부 또는 컴퓨터 사이에서 데이터의 교환 방식을 정의하는 규칙 체계이다. 기기 간 통신은 교환 되는 데이터의 형식에 대해 상호 합의를 요구한다. 이런 형식을 정의하는 규칙의 집합
  
- 다시 말해, HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, **80번 포트**를 사용하고 있다. 따라서 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며, 클라이언트는 80번 포트로 요청을 보내게 된다.

### HTTP의 특징
**1.  Request / Response (요청 / 응답)**

- HTTP 통신의 핵심은 요청(request)과 응답(response)이다. 

- 브라우저에 URL을 입력하면 HTTP 표준에 따라 URL을 요청 메시지로 변환하고 TCP/IP를 사용하여 인터넷을 통해 요청(request)을 보낸다. 웹 서버는 요청을 수신하고 클라이언트가 요청한 웹 페이지를 반환(response)한다.
 
**2. Stateless**

- 각각의 HTTP 통신(요청/응답)은 독립적 이기 때문에 과거의 통신(요청/응답)에 대한 내용을 전혀 알지 못한다. 

- 따라서 매 통신마다 필요한 모든 정보를 담아서 요청을 보내야 한다. 

- 만일 여러번의 통신(요청/응답)의 진행과정에서 연속된 데이터 처리가 필요한 경우(ex. 온라인 쇼핑몰에서 로그인 후 장바구니 기능)를 위해 로그인 토큰 또는 브라우저의 쿠키, 세션, 로컬스토리지 같은 기술이 탄생하였다.

### HTTP Request 구조 
**1. Start line **
: HTTP Method, 타겟 url, HTTP version

**2. Headers **
```
Headers: {
	Host: 요청을 보내는 목표(타겟)의 주소. 즉, 요청을 보내는 웹사이트의 기본 주소가 된다
	(ex. www.google.com)
    	User-Agent: 요청을 보내는 클라이언트의 대한 정보 (ex. chrome, firefox, safari, explorer)
	Content-Type: 해당 요청이 보내는 메세지 body의 타입 (ex. application/json)
	Content-Length: body 내용의 길이
	Authorization: 회원의 인증/인가를 처리하기 위해 로그인 토큰을 Authroization 에 담는다
}
```

**3. Body**
: 해당 요청의 실제 내용이 담긴다. 주로 POST 메서드를 사용할 때 body에 내용이 담긴다. 

```
Body: {
	"name": "Chankyu"
	"email": "chankyu@gmail.com"
}
```

![](https://images.velog.io/images/lck0827/post/f2049bd4-97e0-4a71-86d0-7aba4ddc6345/image.png)

### HTTP Response 구조

**1. Status line**
: 응답의 상태 줄이다. 응답은 요청에 대한 처리상태를 클라이언트에게 알려주면서 내용을 시작한다. 응답의 Status Line 도 세 부분으로 구성된다.
>  1. HTTP Version: 요청의 HTTP버전과 동일
 2. Status Code: 응답 메세지의 상태 코드
 3. Status Text: 응답 메세지의 상태를 간략하게 설명해주는 텍스트

**2. Headers**
: 요청의 헤더와 동일하다. 응답의 추가 정보(메타 데이터)를 담고있는 부분이다. 다만, 응답에서만 사용되는 헤더의 정보들이 있다. (ex. 요청하는 브라우저의 정보가 담긴 User-Agent 대신, Server 헤더가 사용된다.)

**3. Body**
: 요청의 Body와 일반적으로 동일하다. 요청의 메소드에 따라 Body가 항상 존재하지 않듯이. 응답도 응답의 형태에 따라 데이터를 전송할 필요가 없는 경우엔 Body가 없을 수도 있다. 가장 많이 사용되는 Body 의 데이터 타입은 JSON(JavaScript Object Notation) 이다.


![](https://images.velog.io/images/lck0827/post/5c0852e9-38e7-4066-b14e-7c0d3b75b18f/image.png)



> 👉 HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. 
👉 HTTP는 암호화가 되지 않은 텍스트 데이터를 전송하는 프로토콜이였기 때문에, 누군가 네트워크에서 신호를 가로채면 내용이 노출되는 보안 이슈가 존재한다. 
👉 이러한 문제를 해결하기 위해 HTTPS가 등장하게 되었다.

---


## HTTPS(HyperText Transfer Protocol Secure)

### HTTPS 란?
- HyperText Transfer Protocol over Secure Socket Layer, HTTP over TLS, HTTP over SSL, HTTP Secure 등으로 불리는 HTTPS는 HTTP에 데이터 암호화가 추가된 프로토콜이다. 

-  HTTPS를 사용하면 서버와 클라이언트 사이의 모든 통신 내용이 암호화된다.

- HTTPS 프로토콜은 SSL이나 TLS 프로토콜을 통해 세션 데이터를 암호화한다. SSL은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와주고 서버 브라우저가 민감한 정보를 주고받을 때 이것이 도난당하는 것을 막아준다.  

- HTTPS는 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 공개키 암호화를 지원하고 있다.

### 공개키 & 개인키
- HTTPS는 공개키/개인키 암호화 방식을 이용해 데이터를 암호화한다.
  - 공개키: 모두에게 공개가능한 키
  - 개인키: 나만 가지고 알고 있어야 하는 키
 

- 공개키/개인키 암호화의 효과
  - 공개키 암호화: 공개키로 암호화를 하면 개인키로만 복호화할 수 있다. 
  -> 개인키는 나만 가지고 있으므로, 나만 볼 수 있다.
  - 개인키 암호화: 개인키로 암호화하면 공개키로만 복호화할 수 있다. 
  -> 공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있다.

### 대칭키 방식
- 양쪽 당사자가 공통 비밀 키를 공유하여 동일한 키로 암호화, 복호화가 가능하다. 

✔ **장점**
- 대칭키는 매번 랜덤으로 생성되어 누출되어도 다음에 사용할 때는 다른 키가 사용되기 때문에 안전하다.
- 공개키보다 통신 속도가 빠르다. 

✔ **단점**
- 암호화 통신을 하는 사용자끼리 같은 대칭키를 공유해야만 한다는 단점이 있다.
  - 대칭키를 전달하는 과정에서 해킹의 위험에 노출될 수 있다.
  - 대칭키는 데이터를 전송하는 쌍마다 필요하기 때문에, 통신을 총 n명이 한다면 nC2=n(n-1)/2 만큼의 대칭키 생성작업이 필요하다.
- 결론적으로, 키 관리가 힘들다. 

![](https://images.velog.io/images/lck0827/post/ec3741fe-af26-47eb-b74f-aa3ae24a30b8/image.png)


### 비대칭키 방식
- 공개키, 개인키 두개의 키를 한 쌍으로 각각 암호화/복호화에 사용한다. 
- 공개키로 암호화 한것은 개인키로 복호화 할 수 있고, 개인키로 암호화 한것은 공개키로 복호화 할 수 있다. 
- 공개키는 대칭키 방식보다 훨씬 안전하지만, 계산 과정이 복잡하고 연산 도중 컴퓨터의 자원을 많이 사용하기 때문에 현업에서는 공개키 방식과 대칭키 방식을 적절히 조합하여 사용한다. 

👉 이러한 SSL 방식을 적용하려면 인증서를 발급받아 서버에 적용시켜야 한다. 인증서는 사용자가 접속한 서버가 우리가 의도한 서버가 맞는지를 보장하는 역할을 한다. 인증서를 발급하는 기관을 CA(Certificate Authority)라고 부른다. 공인인증기관의 경우 웹 브라우저는 미리 CA 리스트와 함께 각 CA의 공개키를 알고 있다.

#### ✔ **동작 방식**
**1. 서버 - 인증 서명 요청서(CSR) 생성**
- 서버에서 개인키와 공개키를 쌍으로 생성한다. 
- 서버에서 인증 서명 요청서(CSR)을 만든다. 
  - SHA256과 같은 해쉬 알고리즘으로 해싱
  - 국가코드, 도시, 회사명, 이메일, 도메인 주소 등이 들어가며 서버의 공개키도 넣는다. 
  - CA에 전달한다. 

**2. CA - SSL 인증서 발급**
- CA는 서버로부터 받은 인증 서명 요청서(CSR)에 CA의 개인키를 통해 전자서명('암호화'라 표현하지 않고 '전자서명'이라고 표현)을 한 형태인 SSL 인증서를 발급한다. 

**3. 서버 - SSL 인증서 수령**
- 서버가 암호화된 SSL 인증서를 CA로부터 받는다.

![](https://images.velog.io/images/lck0827/post/858ae4f1-fe12-4f7e-abc0-f728c9e61e21/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.25.09.png)

**4. 클라이언트 - SSL Handshake의 첫 번째 단계 : Client Hello**
-  Client가 요청을 하게 되면, 가장 먼저 Server에 3-Way Handshake를 통해 연결을 시도한다.(TCP 연결을 위한 시도)

- 3-Way Handshake를 연결이 완료되면, 클라이언트(브라우저)가 Client Hello 단계를 수행

- HTTPS를 사용하는 것을 알게 된 클라이언트(브라우저)는 Client Hello 단계에서 밑의 정보를 보낸다.
  - 브라우저가 지원하는 암호화 방식 모음(Cipher Suites)
  - 브라우저가 순간적으로 생성한 임의의 난수(Random byte)
  - 만약 이전에 SSL 핸드 셰이크가 완료된 상태라면, 그때 생성된 세션 아이디(Session ID)
  - 브라우저가 사용하는 SSL 혹은 TLS 버전 정보 (SSL Protocol Version)

**5. 서버 - SSL HandShake의 두 번째 단계 : Server Hello
Client가 보내온 Client Hello 패킷을 받아, 밑의 정보를 Client에게 응답한다.**

- 브라우저가 지원하는 암호화 방식(Cipher Suite) 중에서 하나를 선택해서 Client로 전달

- Server가 자신의 SSL 인증서를 Client로 전달한다.
  - SSL 인증서 내부에 Server가 발행한 공개키가 포함 (개인키는 Server가 소유)
  - SSL 인증서는 CA(Certificate Authority, 인증 기관)의 개인키로 ‘서명‘되어 있고, Server가 CA로부터 미리 발급 받아놓은 상태.
  - SSL 인증 내부에 기록되어 있는 Server에 대한 정보(=원본 데이터)
  - 서버가 순간적으로 생성한 임의의 난수(숫자)

**6. 클라이언트 - SSL HandShake의 세 번째 단계 : Premaster Secret 생성**
-  브라우저는 서버의 SSL 인증서가 믿을만한지 확인.

- Client(브라우저)가 SSL 인증서(CA의_Private_key로 암호화(해싱된 Server에 대한 정보))를 CA의 Public Key로 디코딩해본다. 그러면 **Hash(Server에 대한 정보)**의 값을 얻을 수 있다. 그리고 **Server에 대한 정보**를 Hash화 해서 서로 일치하는 지 체크한다. 이를 통해 SSL 인증서가 위조 됐는 지 여부를 체크할 수 있다.
👉 브라우저 내부에 CA의 Public Key가 저장되어 있음.

- 브라우저는 자신이 생성한 난수와 서버의 난수를 사용하여 premaster secret을 만들어서 Server로 전송한다.

- Client(브라우저)에서, 서버로부터 받은 랜덤값과 Client(브라우저)에서 생성한 랜덤값을 Server의 Public Key로 암호화한다. 이 암호화한 값을 premaster secret이라고 하며, 이 값을 Server로 전달한다.

  -  **Server의 Publickey로암호화(Server 랜덤값 + Client 랜덤값) = premaster secret = 세션 키(session key)**
👉 여기서 말하는 세션은, ‘쿠키와 세션’에서 말하는 세션과는 다른 의미이다.
👉 세션 종료가 됐을 때 세션 키를 폐기한다고 되어 있는데, 여기서 말하는 세션은 한 번의 통신을 애기하는 것이 아니다. 사이트에 한 번 접속했을 때부터 종료했을 때까지를 하나의 세션으로 볼 수도 있는 것이다. 즉, 사이트에 한 번 접속한 이후부터 종료할 때까지 세션이 종료되면서 세션 키가 폐기되는 것은 아니라는 말이다.

**7. 서버/클라이언트 - SSL HandShake 종료 & HTTPS 통신 시작**
- 브라우저(Client)와 서버(Server)는 SSL handshake가 정상적으로 완료되었고, 이제는 웹상에서 데이터를 세션 키(session key)를 사용하여 암호화/복호화하며 HTTPS 프로토콜을 통해 주고받을 수 있다. - HTTPS 통신이 완료되는 시점에서 서로에게 공유된 세션 키(session key)를 폐기한다. 만약 세션(session)이 여전히 유지되고 있다면, 브라우저는 SSL handshake 요청이 아닌 세션 ID만 서버에게 알려주면 된다. 
- Client Hello 과정에서 보면 이전에 SSL Handshake가 완료되었을 때, 세션 아이디를 Server한테 보내는 것을 확인할 수 있다. 

- SSL 인증서 과정에는 대칭키 방식과 공개키 방식 두 개 모두 사용되었다. SSL Handshake 단계까지는 공개키 방식, 그 이후의 HTTPS 통신은 대칭키 방식을 사용하였다.

> 🙆‍♂️ **CA(Certificate Authority)란?**
> 
- certification authority (CA)는 공개키와 공개 DNS명(ex.www.example.com)의 연결을 보장하는 기관이다. 따라서 신뢰성이 엄격하게 공인된 기업들만 참여할 수 있다. 
- 자신만의 암호화 키로 웹사이트의 공개키를 암호학적으로 사인하는 데 사용함으로써 특정 공개키가 특정 사이트의 공개키라는 것을 보장한다. 이 서명은 계산적으로 위조할 가능성이 없다. 브라우저(그 외 클라이언트)는 잘 알려진 CS가 소유한 공개키를 보관하는 신뢰할 수 있는 anchor 저장소(trust anchor stores)를 유지하고 CS 서명을 암호학적으로 확인하는데 이 공개키를 사용한다.

> **🙆‍♂️ SSL(TLS)이란?**
HTTPS는 SSL(Secure Socket Layer)/TLS(Transport Layer Security) 전송 기술을 사용한다. TCP, UDP와 같은 일반적인 인터넷 통신에 안전한 계층(layer)을 추가하는 방식이다. 그리고 이 기술을 구현하기 위해 웹 서버에 설치하는 것이 SSL/TLS 인증서이다. TLS는 SSL의 개선 버전이며, 최신 인증서는 TLS를 사용하지만 편의적으로 SSL 인증서라고 불리운다.


#### HTTPS의 장단점
- HTTPS는 웹사이트의 무결성을 보호해준다. 웹 사이트와 사용자 브라우저 사이의 통신을 침입자가 건드리지 못하도록 한다. (침입자라함은, 악의가 있는 공격자는 물론이고, 합법이지만 통신에 침입하여 페이지에 광고를 삽입하는 경우도 해당한다.)
- 가벼운 웹 서핑이라면 HTTP도 상관없지만, 사용자의 정보를 웹 서버와 주고 받아야하는 경우라면 HTTP는 정보 유출의 위험성을 갖게 된다. HTTPS는 침입자가 웹사이트와 사용자 사이의 통신을 몰래 수신하는 것을 방지함으로써 보안을 강화해준다.
- getUserMedia()를 통한 사진 촬영이나 오디오 녹음, 프로그레시브 웹 앱과 같은 강력한 웹 플랫폼 신기능들은 실행하려면 사용자의 명시적인 권한 허락을 필요로 한다. 지오로케이션 API와 같은 오래된 API들도 실행할 때 권한이 필요하도록 업데이트되고 있는데, HTTPS는 이러한 새 기능과 업데이트된 API에 대한 권한 허락을 가능하게 한다.
- 네이버, 다음은 물론이고 구글 역시 검색 엔진 최적화(SEO: Search Engine Optimization) 관련 내용을 HTTPS 웹사이트에 대해서 적용하고 있다. 즉, 키워드 검색 시 상위 노출되는 기준 중 하나가 보안 요소이다.
- 모든 사이트에서 텍스트를 암호화해서 주고 받으면 과부하가 걸려 속도가 느려질 수 있다. 중요한 사이트는 HTTPS로 관리하고, 그렇지 않은 사이트는 HTTP를 사용한다.
- HTTPS를 지원한다고 해서 무조건 안전한 것은 아니다. 신뢰할 수 있는 CA 기업이 아니라 자체적으로 인증서를 발급할 수도 있고, 신뢰할 수 없는 CA 기업을 통해서 인증서를 발급받을 수도 있기 때문이다.




![](https://images.velog.io/images/lck0827/post/f4661271-0aa5-45fa-9d59-0f57cc6892bc/image.png)


---
📝 **Reference**
1. https://mangkyu.tistory.com/98
2. https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/HTTP%20%26%20HTTPS.md
3. https://rachel-kwak.github.io/2021/03/08/HTTPS.html
4. https://jaeseongdev.github.io/development/2021/07/02/HTTPS,SSL,TLS/