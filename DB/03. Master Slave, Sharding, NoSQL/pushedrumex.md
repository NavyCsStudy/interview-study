<details>
  <summary>1. CAP 이론에 대해서 알고계신다면 설명해주세요.</summary>
일관성, 가용성, 파티션 감내라는 세가지 요구 사항을 동시에 만족하는 분산 시스템을 설계하는 것은 불가능하다라는 이론입니다.
일관성은 분산 시스템에 접속하는 모든 클라이언트는 어떤 노드에 접속하든 언제나 같은 데이터를 보게 되어야한다는 것이고, 
가용성은 분산 시스템에서 접속하는 클라이언트는 일부 노드에 장애가 발생해도 항상 응답을 받을 수 있어야한다다는 것이고,
파티션 감내는 분산 시스템에서 두 노드 간에 통신 장애가 발생해도 시스템은 계속 동작해야한다는 것입니다.

</details>
<details>
  <summary>1-1. Replication 을 사용하여 가용성을 어떻게 향상시킬 수 있나요? </summary>
  master 서버에 장애가 발생할 경우 slave 중 하나를 master 로 승격시켜 가용성을 향상시킬 수 있습니다.
</details>
<details>
  <summary>1-2. master 서버에 장애가 생겨 slave 중 하나를 master 로 승격시킬 경우 어떤 문제가 있으며 어떻게 해결할 수 있을까요?</summary>
  slave 의 내용이 최신화되지 않은 상태일 가능성이 있습니다. 이 경우 복구 스크립트를 통해 로그를 보며 데이터를 최신화할 수 있습니다.
</details>

---

<details>
  <summary>2. db 서버를 scale out 할 수 있는 방법에 대해 알고계신게 있나요?</summary>
    replication, sharding, clustering 가 있습니다.
</details>
<details>
  <summary>2-1. replication 과 clustering 의 공통점과 차이점에 대해 설명해주세요.</summary>
  replication 과 clustering 모두 여러대의 db 서버를 복제하여 모든 db 를 동일한 값으로 동기화합니다.
replication 은 master-slave 로 구성되며 master 에는 쓰기작업하고 slave 로 동기화를 하여, slave 에는 읽기작업을 수행합니다.
clustering 은 여러대의 db 서버를 하나의 db 서버로 인식하고, 쓰기작업과 읽기작업을 모든 db 서버에 분산하여 수행합니다.
</details>
<details>
  <summary>2-2. sharding 이란 무엇인지 설명해주세요.</summary>
  sharding 은 데이터베이스를 샤드라는 작은 단위로 분할하는 기술입니다. 모든 샤드는 같은 스키마를 쓰지만 샤드에 보관하는 데이터 사이에는 중복이 없습니다.
</details>

---

<details>
  <summary>3. 캐시란 무엇이며 어떤 데이터를 캐시하는게 적절하다고 생각하시나요?</summary>
  데이터의 원래 소스보다 더 빠르고 효율적으로 액세스할 수 있는 임시 데이터 저장소입니다. 같은 데이터를 반복적으로 액세스하는 작업이 많고 자주 갱신되지 않는 데이터를 캐싱하는게 적절하다고 생각합니다.
</details>
<details>
  <summary>3-1. 캐시의 읽기 전략 중 알고계신게 있다면 설명해주세요.</summary>
  캐시의 읽기 전략에는 Look Aside, Read Through 가 있습니다.
Look Aside 는 캐시에 데이터가 존재하면 해당 데이터를 응답하고, 캐시에 존재하지 않는다면 db 에서 데이터를 가져와서 캐시에 저장합니다.
Read Through 는 캐시에 데이터가 존재하면 해당 데이터를 응답하고, 캐시에 존재하지 않는다면 캐시 서버에서 db 에 데이터를 조회하여 자체 업데이트 후 캐시에 데이터를 가져옵니다.
</details>
<details>
  <summary>3-2. 캐시의 쓰기 전략 중 알고계신게 있다면 설명해주세요.</summary>
  캐시의 쓰기 전략에는 Write Back, Write Aroung, Write Through 가 있습니다.
Write Back 은 캐시에 데이터를 모아 일정 주기 배치 작업을 통해 db에 반영합니다.
Write Aroung 은 db에만 데이터를 저장하고 cache miss 가 발생했을 때만 캐시에 db에 있는 데이터를 가져옵니다.
Write Through 는 캐시에 데이터를 저장하고 캐시에서 db에 데이터를 저장합니다.
</details>

---

<details>
  <summary>4. Redis 가 무엇인가요?</summary>
  key-value 구조의 in-memory 데이터 저장소입니다.
</details>
<details>
  <summary>4-1. Redis 의 자료구조에 대해서 알고계신게 있다면 설명해주세요.</summary>

- Strings: 가장 기본적인 데이터 타입으로, set 커멘드를 통해 데이터를 저장
- Bitmaps: 비트 단위의 데이터 타입으로 비트 단위의 연산 가능
- Lists: 데이터를 순서대로 저장(큐로 사용하기 적절)
- Hashes: 하나의 키 안에 여러개의 field 와 value 쌍으로 데이터를 저장
- Sets: 중복되지 않는 문자열의 집합
- Sorted Sets: 중복되지 않는 값을 저장하되, 모든 값을 score 기준을 정렬됨(score 가 같은 경우 사전 순으로 정렬)

</details>
<details>
  <summary>4-2. Redis 의 데이터를 영구적으로 저장하는 방법에 대해 아신다면 설명해주세요.</summary>
  AOF 와 RDB 두가지 방법이 있습니다. 
AOF 는 데이터를 변경하는 커멘드가 들어오면 커멘트를 모두 저장합니다.
RDB 는 저장 당시에 메모리에 존재하는 데이터 그대로를 파일로 저장합니다.
</details>

---

<details>
  <summary>5. NoSQL 과 RDB 의 차이가 무엇인가요?</summary>
RDB 는 정해진 스키마에 따라 데이터가 테이블에 저장됩니다. 데이터는 연관관계를 통해 여러 테이블에 분산되며 join 연산을 통해 연관된 데이터를 가져옵니다.
NoSQL 은 정해진 스키마 없이 데이터를 저장합니다. 데이터를 키-값, 그래프, 문 등으로 저장합니다. 
</details>
<details>
  <summary>5-1. RDB 가 NoSQL 에 비해 수평적 확장이 어려운 이유가 무엇인가요?</summary>
RBD 는 NoSQL 과는 달리 테이블 간의 복잡한 연관관계나 제약 조건이 존재하기 때문에 수평적 확장이 어렵습니다. 물론 샤딩과 같은 방법으로 수평적 확장이 가능하지만 NoSQL 에 비해 복잡한 메카니즘이 필요합니다.
</details>
<details>
  <summary>5-2. RDB 와 NoSQL 각각 어떤 경우에 사용하는게 적절하다고 생각하니사요?</summary>
  데이터의 제약 조건이 존재해야하거나 엄격한 스키마 구조가 필요하다면 RDB 를 사용하는게 적절하고, 비정형 데이터를 다루거나 낮은 응답 지연시간이 요구되는 경우 NoSQL 을 사용하는게 적절하다고 생각합니다.
</details>

---
