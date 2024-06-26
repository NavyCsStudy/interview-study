<details>
  <summary>1. TCP와 UDP의 차이를 설명해주세요.</summary>
  TCP는 연결형 서비스로 3-way handshaking 과정을 통해 연결을 설정하기 때문에 높은 신뢰성을 보장하지만, 속도가 비교적 느리다는 단점이 있습니다.

UDP는 비연결형 서비스로 3-way handshaking을 사용하지 않기 때문에 신뢰성이 떨어지는 단점이 있지만, 데이터 수신 여부를 확인하지 않기 때문에 속도가 빠르다는 장점이 있습니다.

TCP는 신뢰성이 중요한 파일 교환과 같은 경우에 쓰이고 UDP는 실시간성이 중요한 스트리밍에 자주 사용됩니다.
</details>
<details>
  <summary>1-1. UDP는 항상 신뢰성을 보장하지 않나요?</summary>
  UDP도 신뢰성을 UDP 자체에서 보장하지 않는 것 뿐이지, 개발자가 직접 신뢰성을 보장하도록 할 수 있습니다. HTTP/3의 경우,  UDP 기반의 QUIC이라는 프로토콜을 사용합니다. UDP 자체는 신뢰성을 보장하지 않지만, 추가적인 정의를 통해 신뢰성을 보장받을 수 있습니다.
</details>
<details>
  <summary>1-2. TCP의 신뢰성을 보장하는 방법을 설명해보세요.</summary>
  1. 연결지향성 통신<br>
TCP는 3 way-handshaking을 통해 연결을 수립하고, 데이터 전송이 완료된 후에는 연결을 종료하는 과정을 거칩니다. 이 과정을 통해 양쪽 통신 당사자 간의 안정적인 연결을 보장하며, 데이터의 전송이 시작되기 전에 세션이 성공적으로 수립되었는지 확인합니다.<br>
2. 시퀀스 번호와 ACK<br>
각 TCP 패킷에는 시퀀스 번호가 부여되며, 이를 통해 수신자는 데이터 패킷의 순서를 정확히 파악하고 재조립할 수 있습니다. 수신자는 수신한 패킷의 시퀀스 번호에 해당하는 확인 응답(ACK)을 송신자에게 보내어, 해당 패킷이 성공적으로 도착했음을 알립니다. 송신자는 ACK를 받지 못한 패킷을 재전송함으로써 데이터 손실에 대응합니다.<br>
3. 재전송 <br>
TCP는 타임아웃이나 수신 확인 응답(ACK)의 누락을 감지할 경우, 해당 데이터 패킷을 자동으로 재전송합니다. 이를 통해 패킷 손실이 발생하더라도 데이터가 최종적으로 수신자에게 도달할 수 있도록 보장합니다.<br>
4. 흐름 제어, 혼잡 제어, 오류 제어
</details>
<details>
  <summary>1-3. 3 way-handshaking 얘기 해주셨는데, TCP 통신은 종료시에도 3 way-handshaking을 사용하나요?</summary>
  TCP는 3 way-handshaking 과정을 통해 연결을 설정하고, 4 way-handshaking 과정을 통해 연결을 해제합니다.
</details>
<details>
  <summary>1-4. 3 way-handshake와 4 way-handshake를 설명해주세요.</summary>
  3 way-handshake란 TCP 네트워크에서 통신 하는 장치가 서로 연결이 잘 되었는지 확인하는 방법입니다. 송신자와 수신자는 총 3번에 걸쳐 데이터를 주고 받으며 통신이 가능한 상태인지 확인합니다.

4 way-handshake란 TCP 네트워크에서 통신 하는 장치의 연결을 해제하는 방법입니다. 송신자와 수신자는 총 4번에 걸쳐 데이터를 주고 받으며 연결을 끊습니다.
</details>

---

<details>
  <summary>2. HTTP Method와 각각이 사용되는 경우에 대해서 설명해주세요.</summary>
  HTTP 메소드는 클라이언트가 서버에게 사용자 요청의 목적을 알리는 '수단'입니다.

- GET: 데이터 조회
- POST: 요청 데이터 처리 (보통 데이터 등록)
- PUT: 데이터 변경 (해당 데이터가 없으면 생성)
- PATCH: 일부 데이터만 변경
- DELETE: 데이터 삭제
</details>
<details>
  <summary>2-1. GET과 POST의 차이에 대해 설명해주세요.</summary>
  GET은 데이터를 조회하기 위해 사용되는 방식으로 데이터를 헤더에 추가하여 전송하는 방식입니다. URL에 데이터가 노출되기 때문에 보안적으로 중요한 데이터를 포함해서는 안됩니다.

POST는 데이터를 추가 또는 수정하기 위해 사용되는 방식으로 데이터를 바디에 추가하여 전송하는 방식입니다. 완전히 안전하다는 것은 아니지만 URL에 데이터가 노출되지 않아 GET보다는 안전합니다.
</details>
<details>
  <summary>2-2. HTTP 통신에서의 멱등성이란?</summary>
  동일한 요청이 여러번 수행되어도 동일한 응답값을 줄 수 있는 것을 멱등성이라고 합니다
</details>
<details>
  <summary>2-3. 멱등성이 지켜지는 HTTP Method는?</summary>

  ![image](https://github.com/team-winey/Winey-Server/assets/88873302/eb47b1ae-7ff6-4fdd-b193-87812942d9c5)
</details>

---

<details>
  <summary>3. 세션 기반 인증과 토큰 기반 인증의 차이에 대해 얘기해주세요.</summary>
  세션 기반 인증은 클라이언트로부터 요청을 받으면 클라이언트의 상태 정보를 저장하므로 Stateful한 구조를 가지고,

토큰 기반 인증은 상태 정보를 서버에 저장하지 않으므로 Stateless한 구조를 가집니다.
</details>
<details>
  <summary>3-1. 그렇다면 Stateful한 세션 기반의 인증 방식을 사용하게 된다면 어떠한 단점이 있을까요?</summary>
  1. 서버에 세션을 저장하기 때문에 사용자가 증가하면 서버에 과부하를 줄 수 있어 확장성이 낮습니다.<br>
2. 해커가 훔친 쿠키를 이용해 요청을 보내면 서버는 올바른 사용자가 보낸 요청인지 알 수 없습니다. (세션 하이재킹 공격)
</details>
<details>
  <summary>3-2. 그렇다면 세션 기반 인증과 토큰 기반 인증은 각각 어느 경우에 적합한가요?</summary>
  단일 도메인이라면 세션 기반 인증을 사용하고, 아니라면 토큰 기반 인증을 사용하는 것이 적합하다고 생각합니다.

왜? - 세션을 관리할 때 사용되는 쿠키는 단일 도메인 및 서브 도메인에서만 작동하도록 설계되어 있기 때문에 여러 도메인에서 관리하는 것은 어렵습니다. (CORS 문제)
</details>
<details>
  <summary>3-3. 세션기반 인증 동작 방식</summary>
  사용자가 로그인을 하면, 해당 인증 정보를 서버의 세션 저장소에 저장하고, 사용자에게는 저장된 세션 정보의 식별자인 Session ID를 발급한다. 발급된 Session ID는 브라우저에 쿠키 형태로 저장되지만, 실제 인증 정보는 서버에 저장되어 있다.

브라우저는 인증 절차를 마친 이후의 요청마다 HTTP Cookie 헤더에 Session ID 를 함께 서버로 전송한다. 서버는 요청을 전달받고, Session ID에 해당하는 세션 정보가 세션 저장소에 존재한다면 해당 사용자를 인증된 사용자로 판단한다.
</details>
<details>
  <summary>3-4. 토큰기반 인증 동작 방식</summary>
  토큰 기반 인증은 인증 정보가 토큰의 형태로 브라우저의 로컬 스토리지(혹은 쿠키)에 저장된다. 

사용자가 가지고 있는 토큰을 HTTP 의 Authorization 헤더에 실어 보낸다. 이 헤더를 수신한 서버는 토큰이 위변조 되었거나, 만료 시각이 지나지 않은지 확인한 이후 토큰에 담겨있는 사용자 인증 정보를 확인해 사용자를 인가한다.
</details>

---

<details>
  <summary>4. DNS가 무엇인가요?</summary>
  DNS란 숫자로 된 인터넷 프로토콜 주소 대신 인터넷 도메인 이름을 통해 웹사이트에 접속 할 수 있게 해주는 시스템입니다.
</details>
<details>
  <summary>4-1. 도메인 이름으로 실제 IP를 어떻게 찾을 수 있는지 흐름을 설명해 주세요.</summary>
  1. 웹 브라우저에 `www.naver.com`을 입력<br>
2. 웹 브라우저는 이전에 방문한적 있는지 찾음 (캐싱)<br>
3. ISP에서 DNS서버에 쿼리를 보냄<br>
4. DNS서버에게 IP 주소를 응답 받음<br>
5. ISP는 해당 IP 주소를 캐싱<br>
6. 웹 브라우저에게 응답
</details>

---

<details>
  <summary>5. www.naver.com에 접속할 때 생기는 과정에 대해 설명해주세요.</summary>
  1. 사용자가 브라우저에 URL([www.naver.com](http://www.naver.com/))을 입력<br>
2. DNS 서버에 도메인 네임으로 서버의 진짜 주소를 찾음<br>
3. IP 주소로 웹 서버에 TCP 3 handshake로 연결 수립<br>
4. 클라이언트는 웹 서버로 HTTP 요청 메시지를 보냄<br>
5. 웹 서버는 HTTP 응답 메시지를 보냄<br>
6. 도착한 HTTP 응답 메세지는 웹 페이지 데이터로 변환되고, 웹 브라우저에 의해 출력
</details>

---

<details>
  <summary>6. HTTPS가 무엇인지</summary>
  HTTPS란 SSL/TLS 프로토콜을 거침으로써 정보를 암호화해 전송하는 방식이다.
</details>
<details>
  <summary>6-1. HTTP와는 어떻게 다른가요?</summary>
  기존의 HTTP 같은 경우는 SSL 프로토콜을 거치지 않고 데이터를 암호화하지 않고 전송하기 때문에 데이터 노출의 위험이 있습니다.
</details>
<details>
  <summary>6-2. HTTPS의 동작 과정에 대해 아는대로 설명해주세요.</summary>
  1. 클라이언트가 서버에 연결 요청을 한다. 메세지에는 TLS 버전, 암호화 알고리즘, 랜덤 문자열이 포함되어 있다.<br>
2. 요청을 받은 서버는 다시 클라이언트에 메세지를 보낸다. 메세지에는 서버의 SSL 인증서, 선택한 암호화 알고리즘, 서버에서 생성한 랜덤 문자열이 포함되어 있다.<br>
3. 메세지를 받은 클라이언트는 자신이 갖고 있는 인증기관의 공개키로 서버의 인증서를 해독한다. 여기서 서버의 정보와 서버의 공개키를 얻게 된다.<br>
4. 예비 마스터 암호 - 클라이언트는 랜덤 문자열을 공개 키로 암호화한 premater secret 키를 서버로 전송한다.<br>
5. 서버가 premaster secret 키를 자신의 비밀키를 통해 복호화한다. <br>
6. 세션 키 생성 - 클라이언트와 서버는 클라이언트가 생성한 무작위 키, 서버가 생성한 무작위 키, premaster secret 키를 통해 세션 키를 생성한다. 양쪽은 같은 키가 생성되어야 한다.<br>
7. 클라이언트 완료 전송 - 클라이언트는 세션 키로 암호화된 완료 메세지를 전송한다.<br>
8. 서버 완료 전송 - 서버도 세션 키로 암호화된 완료 메세지를 전송한다.<br>
9. 핸드셰이크 완료 - 핸드셰이크가 완료되고, 세션 키를 이용해 통신을 진행한다.
</details>

---

<details>
  <summary>7. HTTP의 특징에 대해 말해주세요.</summary>
  1. 클라이언트 - 서버 구조: 클라이언트가 서버에 요청을 보내면, 서버가 요청에 대한 응답을 보내는 클라이언트-서버 구조로 이루어져 있다.<br>
2. 무상태 프로토콜(Stateless): 서버가 클라이언트의 상태를 보존하지 않는다. 따라서 응답과 요청이 독립적이다.<br>
3. 비연결성:  HTTP에서는 실제로 요청을 주고받을 때만 연결을 유지하고 응답을 주고 나면 TCP/IP 연결을 끊는다.<ul>
    1. HTTP 1.0 버전에서는 비연결성이었으나 한계를 느끼고 이후부터는 연결성을 추가하였다.</ul>
</details>
<details>
  <summary>7-1. HTTP 비상태성으로 인한 문제점이 있나요?</summary>
  서버가 직전의 상태를 기억하지 못하므로, 로그인 등을 통해 사용자가 인증을 했더라도 다음 요청에서는 그 상태를 기억하지 못한다.
</details>
<details>
  <summary>7-2. HTTP의 비상태성을 해결하기 위한 방법</summary>
  세션 또는 토큰을 사용하여 문제를 해결한다.

- 세션기반 인가: 사용자의 인증 정보가 서버의 세션 저장소에 저장되는 방식이다.
    - 사용자의 인증 정보를 서버의 세션 저장소에 저장하고, 사용자에게는 Session ID를 발급한다. 발급된 Session ID는 브라우저에 쿠키 형태로 저장된다.
    - 브라우저는 인증 절차를 마친 이후의 요청마다 HTTP Cookie 헤더에 Session ID 를 함께 서버로 전송한다. 서버는 요청을 전달받고, Session ID에 해당하는 세션 정보가 세션 저장소에 존재한다면 해당 사용자를 인증된 사용자로 판단한다.
- 토큰기반 인가: 인증 정보를 클라이언트가 직접 들고 있는 방식이다.
    - 사용자의 인증 정보를 바탕으로 토큰을 생성하여 반환한다. 토큰은 브라우저의 로컬 스토리지 혹은 쿠키에 저장된다.
    - 토큰 기반 인증에서는 사용자가 가지고 있는 토큰을 HTTP 의 Authorization 헤더에 실어 보낸다. 이 헤더를 수신한 서버는 토큰이 위변조 되었거나, 만료 시각이 지나지 않은지 확인한 이후 토큰에 담겨있는 사용자 인증 정보를 확인해 사용자를 인가한다.
</details>
<details>
  <summary>7-3. HTTP 버전별 설명</summary>
  <li> HTTP 1.0<ul>
    <li> 연결성: keep-alive를 통해 여러 HTTP 요청을 하나의 TCP 연결을 통해 처리할 수 있게 되었다.</li>
    <li> pipelining: 여러개의 HTTP 요청을 하나의 TCP 연결을 통해 순서대로 보내되, 각각의 응답을 기다리지 않고, 바로 다음 요청을 보낼 수 있게 되었다.</li>
    <li> HOL(head of line) blocking: 여러 개의 데이터 패킷이 순서대로 처리되어야 할 때 첫번째 패킷이 지연되거나 처리되지 않아 그 뒤에 있는 패킷들도 대기 상태에 놓이게 되는 현상이 생기게 되었다.</li></ul></li>
<li> HTTP 2.0<ul>
    <li> 헤더 압축: HPACK 알고리즘을 사용해 헤더 정보를 압축 ⇒ 헤더의 크기가 줄어들고 전체적인 성능 향상</li>
    <li> HOL 블로킹 해결, 리소스 우선순위: 각 스트림에 우선순위를 지정할 수 있고, 하나의 스트림이 블로킹 되더라도 다른 스트림에는 영향을 미치지 않게 되었다.</li>
    <li> 서버 푸시: HTTP 1.1 에서는 클라이언트의 명시적인 요청이 있을 때만 리소스를 전송할 수 있는 반면 HTTP 2에서 서버는 클라이언트의 요청에 미리 대응해 필요한 리소스를 "푸시" 할 수 있다. 이로 인해 라운드 트립 시간을 줄일 수 있다.</li>
    <li> 프로토콜 방식: 텍스트 기반의 프로토콜에서 HTTP2는 바이너리 기반의 프로토콜이 되었다.</li></ul></li>
<li> HTTP 3.0<ul>
    <li> QUIC (Quick UDP Internet Connections) 프로토콜 사용: UDP를 안정성 있게 사용하게 해주는 프로토콜<ul>
        <li> TCP 대비 더 나은 동시성, 더 빠른 연결 설정, O-RTT 재연결</li></ul></li></ul></li>
</details>

---

<details>
  <summary>8. 쿠키, 세션 차이점</summary>
  관리의 측면에서 차이가 있다. 쿠키 같은 경우에는 해당 데이터를 브라우저에 저장하고 있다가 요청할 때 서버에 보내는 방식이라면, 세션의 경우 실제 데이터는 서버에서 관리하고 있고 브라우저에는 해당 세션 데이터를 식별할 수 있는 session id를 쿠키 형태로 저장하고 있어 요청할 때 session id를 보낸다.
</details>
<details>
  <summary>8-1. JWT 사용했을 때 문제점</summary>
  <li> 쿠키/세션과 다르게 토큰의 길이가 길어, 인증 요청이 많아질수록 네트워크 부하가 심해진다.</li>
<li> Payload 자체는 암호화가 되지 않아 중요한 정보는 담을 수 없다. 그래서 토큰을 탈취당한다면 대처가 매우 어렵다.</li>
</details>
<details>
  <summary>8-2. 어떻게 해결할 수 있는지</summary>
  Access Token과 Refresh Token을 함께 사용한다. 

- Access Token: 유효 기간을 짧게 설정한다.
- Refresh Token: 유효 기간은 길게 설정한다.
- 사용자는 Access Token과 Refresh Token을 둘 다 서버에 전송하여 전자로 인증하고 만료됐을 시, 새로운 Access Token을 발급받는다.

즉, 짧은 시간동안 사용할 수 있도록 하고 주기적으로 재발급을 하도록 하는 것이다. 이렇게 하면 앞에서 말했듯 토큰이 유출되어도 피해를 최소화할 수 있다. ⇒ 유효시간이 짧기 때문에 탈취하더라도 사용하지 못함
</details>
<details>
  <summary>8-3. 만약에 Refresh Token을 탈취당한다면?</summary>
  <li>데이터베이스에 각 사용자에 1 대 1로 맵핑되는 Access Token과, Refresh Token 쌍을 저장한다.</li>
<li> 정상적인 사용자는 기존의 Access Token으로 접근하며 서버측에서는 데이터베이스에 저장된 Access Token과 비교하여 검증한다.</li>
<li> 공격자는 탈취한 Refresh Token으로 새로 Access Token을 생성한다. 그리고 서버측에 전송하면 서버는 데이터베이스에 저장된 Access Token과 공격자에게 받은 Access Token이 다른 것을 확인한다.</li>
<li> 만약 데이터베이스에 저장된 토큰이 아직 만료되지 않은 경우, 즉 굳이 Access Token을 새로 생성할 이유가 없는 경우 서버는 Refresh Token이 탈취당했다고 가정하고 두 토큰을 모두 만료시킨다.</li>
<li> 이 경우 정상적인 사용자는 자신의 토큰도 만료됐으니 다시 로그인해야 한다. 하지만 공격자의 토큰 역시 만료됐기 때문에 공격자는 정상적인 사용자의 리소스에 접근할 수 없다.</li>
</details>

---

<details>
  <summary>9. GET과 POST의 차이점에 대해 설명해주세요.</summary>
  <li> 목적: GET은 주로 정보를 요청할 때, POST는 주로 정보를 생성/업데이트 요청하기 위해 사용한다.</li>
<li> 요청에 body 유무: GET은 URL 파라미터에 데이터를 담아 보내기 때문에 HTTP 메세지에 body가 없다. POST는 body에 데이터를 담아보낸다.</li>
<li> 캐시: GET 요청은 캐시되고, POST 요청은 캐시되지 않는다.</li>
</details>

---
