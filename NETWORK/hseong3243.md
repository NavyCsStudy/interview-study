<details>
  <summary>1. cors에 대해 설명해주세요.</summary>

교차 출처 리소스 공유는 애플리케이션을 통합하기 위해 서로 다른 출처 간 요청을 허용하기 위한 메커니즘입니다.
</details>
<details>
  <summary>1-1. cors가 필요한 이유는 무엇인가요?</summary>

모든 브라우저는 보안 상의 이유로 동일 출처 정책(SOP)을 구현하고 있으며 이로 인해 CORS라는 별도의 메커니즘을 이용해 다른 출처의 요청을 허용해주어야 합니다.
</details>
<details>
  <summary>1-2. cors가 작동하는 과정에 대해 알고 있나요?</summary>

cors는 HTTP 헤더를 사용하여 출처가 다르더라도 응답을 주고받을 수 있도록 서버에서 리소스 호출이 허용된 출처(Origin)을 명시합니다. 브라우저는 OPTIONS 메서드로 프리플라이트(preflight) 요청을 통해 요청이 시작된 출처, 사용할 메서드, 헤더를 보냅니다. 프리플라이트 응답을 통해 허용하는 출처, 메서드, 헤더, 크리덴셜 포함 여부를 확인하고 실제 요청을 수행합니다.
</details>
<details>
  <summary>1-3. xss에 대해 설명해주세요.</summary>

사이트 간 스크립팅(Cross Site Scription, XSS)는 웹 애플리케이션에서 사용자 입력값에 대한 필터링이 제대로 이루어지지 않을 경우 공격자가 악의적인 스크립트를 삽입하여 희생자 측에서 동작하도록 하는 공격입니다. 

이를 이용해 공격자는 개인정보, 쿠키 탈취, 웹 페이지 변조 등의 공격을 수행할 수 있습니다.
</details>
<details>
  <summary>1-3. csrf에 대해 설명해주세요.</summary>

사이트 간 요청 위조(Cross Site Request Forgery, CSRF)는 악의적인 공격자가 XSS와 같은 방법을 이용하여 사용자의 권한을 탈취하고 해당 권한으로 서버에 요청을 보내는 공격입니다.

서버에서 사용자의 권한을 확인하는 고정된 값(예. 쿠키)이 존재한다면 이를 탈취해서 개인정보 수정과 같은 임의의 행동을 실행하도록 만드는 것입니다.
</details>

---

<details>
  <summary>2. HTTP 상태 코드 종류를 설명해주세요.</summary>

#### 1xx(Informational)
요청이 수신되어 처리중을 뜻합니다.

#### 2xx(Successful)
요청이 정상 처리되었음을 뜻합니다.

#### 3xx(Redirection)
요청을 완료하기 위해 추가 행동이 필요함을 뜻합니다.
웹 브라우저는 응답 결과에 Location 헤더가 있으면 해당 위치로 자동 이동(리다이렉트)합니다.

##### 영구 리다이렉션
리소스의 URI가 영구적으로 이동했음을 뜻합니다.
- 301 Moved Permanently
  - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있습니다.
- 308 Permanent Redirect
  - 리다이렉트시 요청 메서드와 본문이 유지됩니다.

##### 일시 리다이렉션
리소스의 URI가 일시적으로 변경됨을 뜻합니다. 일시적 리다이렉션을 통해 동일한 프로세스의 중복 처리를 방지할 수 있습니다.
- 302 FOUND
  - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있습니다.
- 303 See Other
  - 리다이렉트시 요청 메서드가 GET으로 변경됩니다.
- 307 Temporary Redirect
  - 리다이렉트시 요청 메서드와 본문이 유지됩니다.

##### 캐시 리다이렉션
- 304 Not Modified
  - 캐시를 목적으로 사용합니다.
  - 클라이언트에게 리소스가 수정되지 않았음을 알려줍니다. 클라이언트는 로컬에 저장된 캐시를 재사용합니다.
  - 응답에 메시지 바디를 포함하면 안됩니다.

#### 4xx(Client Error)
클라이언트 측의 오류, 잘못된 문법 등의 이유로 서버가 요청을 수행할 수 없음을 뜻합니다.
- 400 Bad Request
  - 클라이언트의 잘못된 요청으로 서버가 요청을 처라힐 수 없음을 뜻합니다.
- 401 Unauthorized
  - 클라이언트가 해당 리소스에 대한 인증(Authentication)이 필요함을 뜻합니다.
- 403 Forbidden
  - 서버가 요청을 이해했지만 승인을 거부함을 뜻합니다.
  - 인증 자격 증명은 있지만, 접근 권한(Authorization)이 불충분한 경우입니다.
- 404 Not Found
  - 요청 리소스가 서버에 없음을 뜻합니다.

#### 5xx(Server Error)
서버 오류, 서버가 정상 요청을 처리하지 못함을 뜻합니다.
- 500 Internal Server Error
  - 서버 내부 문제로 오류가 발생했음을 뜻합니다.
- 503 Service Unavailable
  - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음을 뜻합니다.

</details>
<details>
  <summary>2-1. HTTP 메서드에 대해 알고 있는 것들을 설명해주세요.</summary>

#### GET
리소스 조회에 사용합니다. 쿼리 스트링을 통해 데이터를 전달합니다.

#### POST
요청 데이터 처리에 사용합니다. 메시지 바디를 통해 서버로 데이터를 전달합니다. 주로 신규 리소스 등록, 프로세스 처리에 사용합니다.

#### PUT
리소스가 없으면 생성하고 있으면 대체합니다. POST와 달리 클라이언트가 리소스를 식별한다는 특징이 있습니다.

#### PATCH
리소스의 일부를 변경합니다.

#### DELETE
리소스를 삭제합니다.

</details>
<details>
  <summary>2-2. HTTP 메서드의 속성에 대해 알고 있는게 있나요?</summary>

#### 안전(Safe)
호출해도 리소스를 변경하지 않는다는 속성입니다. 해당 리소스의 변경 여부에만 집중하고 로그와 같은 부차적인 부분은 고려하지 않습니다.
안전한 메서드에는 GET, OPTIONS와 같은 메서드가 포함됩니다.

#### 멱동(Idempotent)
몇 번을 호출하든 결과가 동일하다는 속성입니다. 외부 요인으로 중간에 리소스가 변경되는 것은 고려하지 않습니다.
멱등한 메서드에는 GET, PUT, DELETE가 포함됩니다.

#### 캐시 가능(Cacheable)
응답 결과 리소스를 캐시해도 되는가에 관한 속성입니다.
캐시 가능한 메서드에는 GET, POST이 포함되나 실제로는 GET 정도만 사용합니다.

</details>
<details>
  <summary>2-3. HTTP에 대해서 설명해주세요.</summary>

HTTP는 웹상에서 정보를 주고받기 위한 프로토콜입니다. 서버는 80번 포트를 사용하고 클라이언트는 임시 포트 번호를 사용합니다.

#### HTTP 특징
- 클라이언트-서버 프로토콜
  - 클라이언트는 서버에 요청을 보내고 응답을 대기합니다.
- 무상태 프로토콜
  - 서버는 클라이언트의 상태를 보관하지 않습니다.
- 비연결성
  - 클라이언트와 서버 사이의 연결은 요청-응답이 종료되면 끊어집니다.
  - 서버 자원을 효율적으로 사용할 수 있습니다.
</details>
<details>
  <summary>2-4. REST에 대해 설명해주세요.</summary>

REST는 자원을 이름으로 구분하여 자원의 상태를 주고받는 것을 의미합니다. REST는 HTTP URI를 통해 자원을 명시하고 Method를 통해 자원에 대한 행위를 결정합니다.
state transfer
</details>

---

<details>
  <summary>3. TCP와 UDP의 차이에 대해 설명해주세요.</summary>

#### TCP
TCP는 연결형, 신뢰성 전송 프로토콜입니다. 3 way handshake를 통해 통신 전에 두 호스트의 전송 계층 사이 논리적 연결을 수립합니다. 오류제어, 흐름제어, 혼잡제어를 통해 신뢰성 있는 서비스를 제공합니다.

#### UDP
UDP는 비연결형, 비신뢰성 프로토콜입니다. 별도의 세션 수립 과정을 거치지 않으며 오류제어, 흐름제어, 혼잡제어를 제공하지 않습니다. 단순하고 빠르다는 장점이 있습니다.

</details>
<details>
  <summary>3-1. 오류제어, 흐름제어, 혼잡제어에 대해 설명해주세요.</summary>

#### 흐름제어(Flow Control)

흐름제어란 상대방이 받을 수 있을 만큼만 데이터를 효율적으로 전송하는 것을 말하며 슬라이딩 윈도우(Sliding window) 방식을 사용합니다. 슬라이딩 윈도우는 상대방이 수신 가능한 크기(Window size) 내에서 데이터를 연속해서 전송하능 방식입니다.

#### 오류제어(Error Control)

오류제어란 데이터의 오류나 누락(missing)없이 안전한 전송을 보장해주는 것을 말합니다. 오류 또는 누락 발생 시 재전송을 수행하여 이를 보장합니다.

오류의 판단 기준은 송신측에서 계산한 체크섬(checksum)을 수신측에서 검증하여 오류 여부를 판단합니다.

누락은 네트워크 장애에 의한 데이터 손실, TTL 초과, 데이터 오류 등에 의한 폐기, 네트워크 혼잡에 의한 지연등의 상황입니다.

재전송 방법에는 선택적 재전송(Selective Repeat ARQ), 누락된 부분부터 다시 재전송(Go-Back-N ARQ) 등이 있습니다.

#### 혼잡제어(Congestion Control)

혼잡제어란 네트워크의 혼잡정도에 따라 송신자가 데이터 전송량을 제어하는 것을 말합니다.

혼잡정도의 판단 기준은 데이터 손실 발생 유무로 판단합니다. 전송한 데이터에 누락이 발생하면 네트워크가 혼잡한 상태로 판단하여 존송량을 조절합니다.

</details>
<details>
  <summary>3-1. SSL/TLS에 대해서 설명해주세요.</summary>

클라이언트-서버 환경에서 TCP 기반의 애플리케이션에 대한 종단간 보안서비스를 제공하기 위한 전송계층 보안 프로토콜입니다.

#### 보안 서비스
- 대칭키 암호화 알고리즘을 이용한 **기밀성**을 제공합니다.
- 공개키 인증서를 이용한 서버/클라이언트 간 **상호 인증**을 수행합니다.
- 메시지 인증 코드(MAC: Message Authentication Code)를 통해 송수신 메시지의 위, 변조 여부를 확인할 수 있는 무결성을 제공합니다.

#### 핸드셰이크
클라이언트와 서버 상호간에 사용할 보안 파라미터를 협상하기 위한 프로토콜입니다.

1. Client Hello: 클라이언트는 서버에 사용 가능한 Cipher Suite 목록, SSL 버전, 세션 ID, 압축 방법, 초기 난수 등을 전달합니다.
2. Server Hello: 사용할 SSL/TLS 버전, cipher suite, 압축 방식, 난수, 세션 ID 등을 클라이언트에게 전달합니다.
3. Certificate: 서버가 자신의 SSL 인증서를 클라이언트에게 전달합니다.
4. Server Key Exchange / ServerHello Done: SSL 인증서 내부에 서버의 공개키가 없는 경우 Server Key Exchange를 통해 공개키를 클라이언트에게 전달합니다. 클라이언트는 공개키를 이용해 SSL 인증서를 복호화하여 서버를 인증합니다.
5. Client Key Exchange: 클라이언트는 대칭키를 생성하고 서버의 공개키를 이용해 암호화한 뒤 서버에 전달합니다. 암호 알고리즘의 종류에 따라 대칭키 대신 대칭키를 생성하기 위한 재료를 교환할 수도 있습니다.
6. ChangeCipherSpec / Finished: 클라이언트, 서버 모두 필요한 정보를 교환한 뒤 통신 준비가 되었음을 알립니다.

</details>
<details>
  <summary>3-2. DNS의 작동 방식에 대해서 설명해주세요.</summary>

클라이언트가 DNS 서버에 주소를 조회합니다. 만약 해당 DNS 서버에 주소가 등록되어 있지 않으면 차례대로 상위 DNS 서버에 조회하는 과정을 반복합니다.
</details>
<details>
  <summary>3-3. 브라우저에 google.com을 입력했을 때 어떤 동작이 일어나나요?.</summary>

1. 브라우저는 DNS를 통해 서버의 IP 주소를 찾습니다.
2. 브라우저는 HTTP 메시지를 생성하고 Socket 라이브러리를 통해 프로토콜 스택에 건네줍니다.
3. 서버와 TCP 연결을 수립하고 TCP/IP 패킷을 생성하고 데이터를 전송합니다.
4. 서버는 TCP/IP 패킷을 해석하고 HTTP 요청 메시지에 따라 작업을 처리합니다.
5. 작업의 결과를 토대로 HTTP 응답 메시지를 만들고 TCP/IP 패킷으로 만들어 클라이언트에게 반환합니다.
6. 클라이언트는 응답 메시지에 따라 브라우저를 렌더링합니다.
</details>

---

<details>
  <summary>4. 쿠키와 세션의 차이에 대해 설명해주세요.</summary>

쿠키는 클라이언트측에 키-값 쌍으로 저장되는 데이터입니다.   
세션은 서버측에 저장되는 데이터로 서버에서 관리되기 때문에 쿠키보다 안전합니다. 그러나 서버의 자원을 사용하고 분산 환경에서 추가적인 관리가 필요합니다. 

쿠키 만료 시간, 접근 허용하는 경로와 도메인, 보안 정보를 설정할 수 있습니다.
- Secure
  - https인 경우에만 쿠키 전송을 허용합니다.
- HttpOnly
  - 스크립트를 통한 쿠키 접근을 허용하지 않습니다.
  - HTTP 전송에서만 사용가능합니다.
- SameSite
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키를 전송합니다.
</details>
<details>
  <summary>4-1. 쿠키는 요청, 응답에서 어떻게 사용되나요?</summary>

- 요청

  서버에서 클라이언트로 응답시 Set-Cookie 속성을 이용하여 클라이언트에 쿠키를 만듭니다.
 
- 응답

  클라이언트 측에서는 별다른 조작 없이 request header의 Cookie 속성에 담아 서버로 쿠키를 전송합니다.
</details>
<details>
  <summary>4-2. 세션은 요청, 응답에서 어떻게 사용되나요?</summary>

- 요청
  
  서버에서 클라이언트로 응답시 Set-Cookie 속성을 이용하여 session ID를 가지고 있는 쿠키를 만듭니다.

- 응답

  클라이언트 측에서는 쿠키와 동일하게 request header의 Cookie 속성에 session ID 쿠키를 서버로 전송합니다. 서버는 해당 세션 쿠키를 이용하여 session ID에 해당하는 정보를 참조하여 사용자에게 필요한 응답을 만듭니다.
</details>

---

<details>
  <summary>5. OSI 모델과 TCP/IP 프로토콜 그룹에 대해 설명해주세요.</summary>

#### OSI 모델
OSI 모델은 네트워크 통신을 표준화한 모델로 통신 시스템을 7단계로 규정하고 있습니다.
- 응용(HTTP, SMTP, FTP, SSH, ...)
- 표현
- 세션(SSL, TLS, ...)
- 전송(TCP, UDP, ...)
- 네트워크(IP, ICMP, ARP, RARP, ...)
- 데이터 링크(이더넷, ...)
- 물리

#### TCP/IP 프로토콜 그룹
TCP/IP 프로토콜 그룹은 현재의 인터넷에서 사용하는 프로토콜의 그룹으로 이 중 TCP와 IP가 가장 많이 쓰여 TCP/IP 프로토콜 그룹으로 불립니다. OSI 모델과는 달리 4계층 혹은 5계층으로 규정하고 있습니다.
- 응용(DNS, TLS/SSL, HTTP, FTP, SNMP, SSH, ...)
- 전송(TCP, UDP, ...)
- 인터넷(IP)
- 네트워크 액세스(혹은 데이터 링크, 물리)(APR, RARP, 이더넷, ...)
</details>
<details>
  <summary>5-1. IP 주소는 어떻게 구성되어 있나요?</summary>

IPv4는 32비트의 디지털 데이터로 네트워크 번호와 호스트 번호로 구성되어 있습니다. 서브넷 마스크로 네트워크 번호와 호스트 번호의 경계를 결정하며 1인 부분이 네트워크 번호, 0인 부분이 호스트 번호입니다.

#### 10.10.10.0/24 인 경우 몇 개의 주소 공간을 사용할 수 있나요?
호스트 번호가 모두 0인 서브넷 주소와 모두 1인 브로드캐스트를 제외하고 2^8-2개의 주소 공간을 사용할 수 있습니다.

#### 서브넷은 무엇인가요?
서브넷(subnetwork)은 네트워크 내부의 네트워크입니다. 

#### CIDR이 무엇인가요?
CIDR는 IP주소를 할당하는 방법입니다. 과거에는 클래스 기반의 IP 주소 할당 방식을 사용하였지만 조직에 할당되는 서브넷이 필요 이상의 크기로 할당되어 IPv4 주소가 소진되는 것을 방지하기 위해 가변 길이 서브넷 마스킹을 사용하는 CIDR이 등장하게 되었습니다.
</details>

---

<details>
  <summary>6. 웹 서버와 웹 애플리케이션 서버의 차이에 대해 설명해주세요.</summary>

#### 웹 서버
웹 서버는 클라이언트의 요청에 따라 정적 콘텐츠를 제공하거나 동적인 컨텐츠의 제공을 위해서 WAS에게 요청하는 서버입니다.

#### 웹 애플리케이션 서버
웹 애플리케이션 서버는 클라이언트의 요청에 따라 비즈니스 로직을 처리하고 동적인 컨텐츠를 웹서버로 전송합니다.
</details>
<details>
  <summary>6-1. nginx와 apache</summary>

nginx와 apache는 웹 서버 소프트웨어로 웹 애플리케이션, API 등을 호스팅하는데 사용됩니다.
nginx는 이벤트 기반 모델을 통해 apache의 프로세스 기반 모델보다 적은 리소스로도 많은 트래픽을 효율적으로 처리할 수 있습니다.
</details>
<details>
  <summary>6-2. 로드밸런서에 대해 설명해주세요.</summary>

로드 밸런서는 서버에 가해지는 부하를 분산해주는 장치를 말합니다. 클라이언트와 서버 풀 사이에 위치하여 트래픽이 증가하는 경우 스케일 아웃을 통해 서버를 증설하고 로드 밸런서는 여러 대의 서버로 트래픽을 균등하게 분산합니다.

#### 알고리즘
- 라운드 로빈(RR)
  - 요청이 들어온 순서대로 서버에 돌아가면서 배정하는 방식입니다.
- 가중 라운드 로빈(Weighted RR)
  - 각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배분합니다.
- 최소 연결 방식(Least Connection Method)
  - 요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분합니다.

#### L4와 L7
- L4
  - L4 로드밸런서는 포트와 IP를 바탕으로 로드 밸런싱을 수행합니다.
  - 데이터를 들여다보지 않고 패킷 레벨에서 로드 밸런싱을 수행해 빠르고 효율성이 높습니다.
- L7
  - TCP/UDP뿐만 아니라 HTTP의 URI등의 정보를 이용해 로드 밸런싱을 수행합니다.
  - 상위 계층에서 부하르 분산하기 때문에 섬세한 라우팅이 가능하지만 패킷 내용을 복호화 해야하기 때문에 추가적인 비용이 들어갑니다.
</details>

---

<details>
  <summary>7. 3-way-handshake에 대해 설명해주세요.</summary>

3-way-handshake는 통신을 위해 연결을 수립하기 위한 과정입니다. 

1. 클라이언트는 서버에게 SYN 패킷을 보냅니다.
2. 서버는 클라이언트에 ACK과 SYN 플래그가 설정된 패킷을 보냅니다.
3. 클라이언트는 서버에게 ACK 패킷을 보냅니다.

#### 연결 종료는 어떻게 이루어지나요?

연결 종료는 4-way-handshake라는 과정을 통해 이루어집니다. 

1. 클라이언트는 서버에게 FIN 플래그를 보냅니다.
2. 서버가 FIN을 받으면 클라이언트에게 ACK을 보냅니다.
3. 서버가 모든 데이터를 보냈으면 클라이언트에게 FIN을 보냅니다.
4. 클라이언트가 FIN을 받으면 서버에게 ACK을 보냅니다. 이 때, 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 바로 연결을 종료하지 않고 기다립니다.(Time Wait)
</details>

---

<details>
<summary>8. REST란 무엇인가요?</summary>

웹 서비스를 설계하고 구현하기 위한 소프트웨어 아키텍처 원칙입니다. URI를 통해 리소스를 명시하고 HTTP 메서드를 활용해 행위를 결정합니다. 또한, 각 요청은 독립적으로 이루어져 요청을 처리하기 위한 모든 정보가 포함되어 있어야 합니다.

</details>
