<details>
  <summary>1. 데이터 분산 방법에는 무엇이 있을까요?</summary>
  대표적으로 복제(replication)와 샤딩(sharding)이 있습니다.
  <li>복제(replication) <ul>
    <li> 같은 데이터를 복사해 여러 노드에 분산하는 방법</li>
    <li> 크게 master-slave와 peer-to-peer 두 가지 방법이 있다.</li></ul></li>
  <li> 샤딩(sharding) <ul>
    <li> 특정 기준에 따라 데이터를 나눠서 각 노드에 저장하는 방법</li></ul></li>
</details>
<details>
  <summary>1-1. Replication 장단점</summary>
  장점:
  <li> 가용성 증가<ul>
    <li> Master DB가 죽을 경우, Slave 서버를 Master로 승격시켜 서비스를 복구할 수 있음</li></ul></li>
  <li> 부하 분산 가능(스케일 아웃)<ul>
    <li> Master DB에서는 WRITE(CUD), Slave DB에서는 Read(SELECT) 작업을 처리하게하여 부하 분산 가능</li></ul></li>
  <li> 데이터 보호<ul>
    <li> 복제 과정을 중단하고 Slave에서 백업 서비스를 가동할 수 있음</li></ul></li>
단점:
  <li>노드들 간의 데이터 동기화가 보장되지 않아 일관성 있는 데이터를 얻지 못할 수 있음</li>
  <li>노드가 다운되면 복구 및 대처가 까다로움</li>
</details>
<details>
  <summary>1-2. Replication의 기법 중 하나에 대해 설명해주세요</summary>
  Master/Slave<br>
  2대 이상의 DBMS를 Master와 Slave로 나눠서 데이터를 저장하는 방식을 말합니다. <br>
  또한 Master DBMS와 Slave DBMS는 각자 다른 역할을 수행하는데, Master DBMS는 주로 CUD 작업을 처리하며 웹서버로 부터 데이터 CREATE, UPDATE, DELETE 요청이 들어오면 바이너리 로그를 생성하여 Slave 서버로 전달합니다. <br>
  Slave DBMS는 주로 READ 작업을 처리하며 Master DBMS로부터 전달받은 바이로그를 데이터로 반영합니다.
</details>

---

<details>
  <summary>2. 샤딩이 무엇인지 설명해주세요</summary>
  샤딩은 대규모 데이터베이스를 작은 단위로 분할하여 저장하는 수평적 확장 방식입니다. 예를 들어, 하나의 테이블에 너무 많은 레코드가 저장되어 있을 때 레코드를 두 개의 테이블에 절반씩 나누어서 저장할 수 있는데 이런 경우가 샤딩이라고 볼 수 있습니다.
</details>
<details>
  <summary>2-1. 샤딩의 장단점</summary>
  장점으로는 스케일 아웃이 가능하고, 스캔 범위를 줄여서 쿼리 반응 속도를 빠르게 할 수 있습니다. 또한 장애가 샤드 단위로 일어납니다.<br>
  하지만 단점으로는 프로그래밍 복잡도가 증가하고, 데이터가 한쪽에 몰릴 경우 샤딩이 무의미해질 수 있습니다.
</details>
<details>
  <summary>2-2. 샤딩의 종류 중 하나에 대해 설명해주세요.</summary>
  모듈러 샤딩
    <li> PK를 모듈러 연산한 결과로 DB를 라우팅하는 방식</li>
    <li> 레인지 샤딩에 비해 데이터가 균일하게 분산된다.</li>
    <li> DB를 추가 증설하는 과정에서 이미 적재된 데이터의 재정렬이 필요하다.</li>
    <li> 데이터가 일정 수준에서 예상되는 데이터 성격을 가진 곳에 적용할 때 어울린다.</li><ul>
        <li> 데이터가 늘어남에 따라 샤딩을 추가적으로 해야하는 상황이 자주 생기면 큰 부하가 발생하기 때문이다.</li></ul>
</details>
<details>
  <summary>2-3. 샤딩 고려할 점</summary>
  유명인사(celebrity) 문제<br>
  핫스팟 키(hotspot key) 문제라고도 부른다. 특정 샤드에 질의가 집중되어 서버에 과부하가 걸리는 문제<br>
  페이스북 같은 서비스에서 유명 인사 유저가 모두 한 샤드에 집중적으로 저장되어 있다면 해당 샤드만 큰 과부하가 걸리게 됨.<br>
  이 문제를 해결하기 위해 유명인사 각각에 샤드 하나씩을 할당해야 할 수도 있고, 더 잘게 샤드를 쪼개야할수도 있음.
</details>

---

<details>
  <summary>3. NoSQL에 대해 설명해주세요</summary>
  비관계형 데이터베이스로 대량의 분산된 비정형 데이터를 저장하고 조회하는데 특화된 데이터베이스입니다.<br>
  주로 빅데이터, 분산 시스템 환경에서 대용량의 데이터를 처리하는데 적합합니다.
</details>
<details>
  <summary>3-1. NoSQL 장단점</summary>
  장점
<li> RDBMS에 비해 저렴한 비용으로 분산처리와 병렬 처리 가능</li>
<li> 비정형 데이터 구조 설계로 설계 비용이 감소</li>
<li> 빅데이터 처리에 효과적</li>
<li> 가변적인 구조로 데이터 저장 가능</li>
<li> 데이터 모델의 유연한 변화 가능</li>
단점
<li> 데이터 업데이트 중 장애 발생시 데이터 손실 발생 가능</li>
<li> 많은 인덱스를 사용하려면 충분한 메모리가 필요<ul>
    <li> 인덱스 구조가 메모리에 저장</li></ul></li>
<li> 데이터 일관성이 항상 보장되지 않음</li>
</details>
<details>
  <summary>3-2. RDBMS와 NoSQL은 어느 경우에 적합한가요?</summary>
  <li> RDBMS:<ul>
    <li> 데이터 구조가 명확하고, 변경 될 여지가 없으며 스키마가 중요한 경우에 사용하는 것이 좋다.</li>
    <li> 중복된 데이터가 없어(데이터 무결성) 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템에 적합하다.</li></ul></li>
<li> NoSQL:<ul>
    <li> 정확한 데이터 구조를 알 수 없고 데이터가 변경/확장 될 수 있는 경우 사용하는 것이 좋다.</li>
    <li> NoSQL은 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 시 모든 컬렉션에서 수정해야 하기 때문에 Update가 많이 이루어지지 않는 시스템에 좋다.</li>
    <li> scale-out이 가능하다는 장점을 활용해 막대한 데이터를 저장해야 해서 DB를 Scale-out 해야 되는 시스템에 적합하다.</li></ul></li>
</details>

---

<details>
  <summary>4. Redis가 무엇인지 설명해주세요</summary>
  Key-Value 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 NoSQL 입니다. 데이터베이스, 캐시, 메세지 브로커로 사용되며 인메모리 데이터 구조를 가진 저장소입니다.
</details>
<details>
  <summary>4-1. Redis의 특징</summary>
    <li> 영속성을 지원하는 인 메모리 데이터 저장소</li>
<li> 다양한 자료 구조를 지원함 → String, List, Set, Sorted Set, Hash, …</li>
<li> 싱글 스레드 방식으로 인해 연산을 원자적으로 수행이 가능함 → Thread Safe</li>
<li> 읽기 성능 증대를 위한 서버 측 리플리케이션을 지원</li>
<li> 쓰기 성능 증대를 위한 클라이언트 측 샤딩 지원</li>
<li> 다양한 서비스에서 사용되며 검증된 기술</li>
</details>
<details>
  <summary>4-2. Redis는 왜 속도가 빠른가?</summary>
    Key-Value 방식이므로 쿼리를 날리지 않고 결과를 얻을 수 있다.
</details>
<details>
  <summary>4-3. Redis는 어떻게 영속성을 보장하는가?</summary>
    RDB 또는 AOF 방식을 통해 영속성을 보장한다.
<li> RDB(Snapshotting) 방식: 순간적으로 메모리에 있는 내용 전체를 디스크에 옮겨 담는 방식</li>
<li> AOF(Append On File) 방식: Redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태</li>
</details>

---

<details>
  <summary>5. Redis(캐시) 사용할 때 주의해야 할 점</summary>
  <li> 데이터 정합성 문제<ul>
    <li> 하나의 데이터를 캐시와 데이터베이스 두 곳에서 관리하기 때문에 저장된 값이 불일치하는 문제가 발생할 수 있다.</li>
    <li> 따라서 적절한 캐시 읽기 전략(Read Cache Strategy)과 캐시 쓰기 전략(Write Cache Strategy)을 통해, 캐시와 DB간의 데이터 불일치 문제를 극복하면서도 빠른 성능을 잃지 않게 하기 위해 고심히 연구를 할 필요가 있다.</li></ul></li>
<li> 서버에 장애가 발생했을 경우 그에 대한 운영 플랜이 꼭 필요합니다. 인메모리 데이터 저장소의 특성상, 서버에 장애가 발생했을 경우 데이터 유실이 발생할 수 있기 때문입니다.</li>
<li> 인메모리이기 때문에 용량이 작아 메모리 관리가 중요합니다.</li>
<li> 싱글 스레드의 특성상, 한 번에 하나의 명령만 처리할 수 있습니다. 처리하는데 시간이 오래 걸리는 요청, 명령은 피해야 합니다.</li>
</details>
<details>
  <summary>5-1. 캐시 읽기 전략과 쓰기 전략 중 하나씩 설명해주세요</summary>
  Look Aside (읽기 전략)
<li> 데이터를 찾을 때 캐시에 저장된 데이터가 있는지 우선적으로 확인하는 전략 ⇒ 만일 캐시에 데이터가 없으면 DB에서 조회함</li>
<li> 반복적인 읽기가 많은 호출에 적합</li>
<li> 캐시와 DB가 분리되어 가용되기 때문에<ul>
    <li> 원하는 데이터만 별도로 구성하여 캐시에 저장</li>
    <li> 캐시 장애 대비 구성이 되어 있음<ul>
        <li> 만일 redis가 다운 되더라도 DB에서 데이터를 가져올수 있어 서비스 자체는 문제가 없음</li></ul></li>
    <li> Cache Store와 Data Store(DB)간 정합성 유지 문제가 발생할 수 있음</li>
    <li> 초기 조회 시 무조건 Data Store를 호출해야 하므로 단건 호출 빈도가 높은 서비스에 적합하지 않다. 👉 대신 반복적으로 동일 쿼리를 수행하는 서비스에 적합한 아키텍처<ul>
        <li> 이런 경우 DB에서 캐시로 데이터를 미리 넣어주는 Cache Warming 작업을 하기도 한다.</li></ul></li></ul></li>
<li> 대신에 캐시에 붙어있던 connection이 많았다면, redis가 다운된 순간 순간적으로 DB로 몰려서 부하 발생</li>
<br>
Write Around (쓰기 전략)

<li> 모든 데이터는 DB에 저장 (캐시를 갱신하지 않음)</li>
<li> Cache miss가 발생하는 경우에만 DB와 캐시에도 데이터를 저장</li>
<li> 따라서 캐시와 DB 내의 데이터가 다를 수 있음 (데이터 불일치)</li>
</details>

---
