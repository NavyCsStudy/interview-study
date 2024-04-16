<details>
<summary>1-1. 데이터베이스란 무엇인가요?</summary>
<div markdown="1">

한 조직의 여러 응용 시스템들이 공용하기 위해 통합, 저장한 운영 데이터의 집합을 데이터베이스라 합니다.

#### 공용 데이터
- 한 조직의 여러 응용 시스템들이 공동으로 소유, 유지, 이용하는 데이터
#### 통합 데이터
- 최소한의 중복
- 통제된 중복
#### 저장 데이터
- 컴퓨터가 실시간으로 접근 가능한 매체에 저장된 데이터
#### 운영 데이터
- 한 조직의 고유 기능을 수행하기 위해 필요한 데이터

</div>
</details>

<details>
<summary>1-2. 데이터베이스의 특성에 대해 설명해주세요.</summary>
<div markdown="1">

데이터베이스의 특성으로는 실시간 접근성, 지속적인 변환, 동시 공용, 내용에 의한 참조가 있습니다.
### 실시간 접근성(real-time accessibilities)
실시간 접근성은 질의에 대한 실시간 처리 및 응답 가능해야 한다는 특성입니다.
### 지속적인 변화(continuous evolution)
지속적인 변화는 삽입(insert), 갱신(update), 삭제(delete)를 통한 동적으로 데이터가 변함을 뜻합니다.
### 동시 공용(concurrent sharing)
동시 공용은 서로 다른 목적을 가진 여러 사용자가 동시에 사용할 수 있어야 함을 뜻합니다.
### 내용에 의한 참조(content reference)
내용에 의한 참조는 데이터의 위치(location)나 주소(address)가 아닌 내용(content)에 의한 참조를 수행함을 뜻합니다.

</div>
</details>

<details>
<summary>1-3. 데이터베이스와 파일 시스템은 어떤 차이가 있나요?</summary>
<div markdown="1">

파일 시스템은 각각의 응용 프로그램이 논리적 파일 구조를 정의하고 직접 물리적 파일로 구현하는 시스템을 말합니다. 응용 프로그램은 물리적 데이터 구조에 대한 접근 방법을 구현하기 때문에 개발자는 응용 프로그램 뿐만 아니라 데이터까지 모두 관리해야합니다. 이로 인해 발생하는 문제점은 데이터의 종속성, 중복성이 있습니다.

#### 데이터 종속성
- 데이터의 구성 방법이나 접근 방법 변경 시 응용 프로그램도 함께 변경해야 한다.
#### 데이터 중복성
- 한 시스템 내에 같은 내용의 데이터가 여러 파일에 중복 저장되어 관리된다.

</div>
</details>
<br/>

<details>
<summary>2-1. 관계형 데이터베이스란 무엇인고 장단점에는 어떤 것이 있나요?</summary>
<div markdown="1">

데이터베이스를 시간에 따라 내용이 변할 수 있는 테이블형태로 표현한 테이블들의 집합을 관계형 데이터베이스라 합니다. 관계형 데이터베이스의 스키마는 릴레이션 스키마(테이블)과 무결성 제약조건으로 이루어져 있습니다.
### 장점
- ACID 특성을 제공하여 데이터 일관성과 무결성을 보잡합니다.
- SQL을 통한 쉬운 관리 및 검색이 가능합니다.
### 단점
- 수평적 확장이 어려워 데이터 처리량에서 한계가 존재합니다. 
- 스키마를 변경하는 것이 어렵습니다. 
- 비정형 데이터나 복잡한 계층 구조를 다루는 데 적절하지 않습니다.

</div>
</details>

<details>
<summary>2-2. RDB의 무결성 제약조건에는 어떤 것들이 있나요?</summary>
<div markdown="1">

무결성 제약조건에는 개체 무결성과 참조 무결성이 있습니다.
### 개체 무결성(entity integrity)
개체 무결성은 키 값은 언제 어느 때고 null 값을 가질 수 없는 제약조건을 말합니다.
### 참조 무결성(referential integrity)
참조 무결성은 외래 키 값은 반드시 피참조 릴레이션의 기본키 값이거나 null이어야한다는 제약조건을 말합니다.

이러한 무결성 제약조건은 데이터베이스 상태가 항상 만족시켜야 되는 제약조건입니다.

#### 데이터베이스 상태(database state)
- 어느 한 시점에 데이터베이스에 저장되어 있는 모든 데이터 값

</div>
</details>
<br/>

<details>
<summary>3-1. SQL이란 무엇인가요?</summary>
<div markdown="1">

SQL은 RDBMS의 데이터를 관리하기 위해 설계한 특수 목적의 프로그래밍 언어입니다. SQL 문법의 종류는 DDL, DML, DCL세 가지로 분류됩니다.
### DDL(Data Define Language, 데이터 정의어)
DDL은 스키마, 테이블, 인덱스 등의 관계형 데이터베이스의 구조를 정의하기 위한 언어입니다. DDL의 주요 유형은 `CREATE`, `DROP`, `ALTER`, `TRUNCATE`가 있습니다.
### DML(Data Manipulation Language, 데이터 조작어)
DML은 데이터베이스 사용자 또는 응용 프로그램이 질의어를 통하여 저장된 데이터에 대해 검색, 등록, 삭제, 갱신을 하는데 사용하는 언어입니다. DML의 주요 유형은 `SELETE`, `INSERT`, `UPDATE`, `DELETE`가 있습니다.
### DCL(Data Control Language, 데이터 제어어)
DCL은 데이터에 대한 액세스를 제어하기 위한 언어입니다. `GRANT`, `REVOKE`, `COMMIT`, `ROLLBACK`이 있습니다. 이중 트랜잭션 제어를 위한 `COMMIT`과 `ROLLBACK`을 따로 빼서 TCL(Transaction Control Language)라고도 합니다.

</div>
</details>

<details>
<summary>3-2. SELETE 쿼리의 처리 순서에 대해 말해주세요.</summary>
<div markdown="1">

FROM -> WHERE -> GROUP BY -> DISTINCT -> HAVING -> SELECT -> ORDER BY -> LIMIT
### FROM
FROM 절은 조회할 테이블을 지정하고 JOIN을 실행하여 하나의 가상 테이블로 결합합니다.
### WHERE
WHERE 절에서 조건에 맞는 데이터를 필터링합니다.
### GROUP BY
GROUP BY 절에서 특정 컬럼의 값으로 레코드를 그룹화합니다.
### HAVING
HAVING 절에서 그룹화된 결과에 대해 필터링합니다.
### SELECT
SELECT 절에서 원하는 컬럼을 선택합니다.
### ORDER BY
ORDER BY절에서 행의 순서를 어떻게 보여줄지 정렬합니다.
### LIMIT
LIMIT 절에서 쿼리 결과 중 지정된 순서에 위치한 레코드만 가져오도록 선택합니다.

</div>
</details>
<br/>

<details>
<summary>4-1. 기본 키(primary key)에 대해서 설명해주세요.</summary>
<div markdown="1">

기본키는 후보키 중에서 선택한 하나의 키로서 각 튜플을 유일하게 구분하기 위해 선택된 컬럼 또는 컬럼의 집합입니다. 각 튜플에 대한 기본 키 값은 항상 유효한 값이어야 하기 때문에 null 이 허용될 수 없습니다.

#### 키(key)
- 각 튜플(tuple, row)을 유일하게 식별할 수 있는 애트리뷰트(attribute, column)의 집합

</div>
</details>

<details>
<summary>4-2. 후보키(candidate key)란 무엇인가요?</summary>
<div markdown="1">

후보키는 테이블의 컬럼들 중에서 유일성과 최소성을 만족하는 컬럼 집합입니다. 
### 유일성(uniqueness)
유일성이란 각 튜플에 대해 컬럼 집합의 값이 유일하다는 것을 말합니다.
### 최소성(minimality)
최소성이란 컬럼 집합이 각 튜플을 유일하게 식별하는데 필요한 컬럼만 포함된 것을 말합니다.

#### 슈퍼 키(super key)
- 유일성은 만족하지막 최소성은 만족하지 않는 애트리뷰트의 집합
#### 대체 키(alternate key)
- 후보 키 중에서 기본 키를 제외한 나머지 후보 키

</div>
</details>

<details>
<summary>4-3. 외래 키(foreign key)란 무엇인가요?</summary>
<div markdown="1">

테이블 R의 컬럼 집합 FK가 테이블 S의 기본키일 때 컬럼 집합 FK는 테이블 R의 외래 키입니다. 외래 키의 값은 테이블 S에 존재하는 값이거나 null 이어야하는 참조 무결성을 만족해야 합니다.

</div>
</details>
<br/>

<details>
<summary>5-1. MySQL의 아키텍처에 관해 설명해주세요.</summary>
<div markdown="1">

MySQL은 MySQL 엔진과 스토리지 엔진으로 구성되어 있습니다. 
### MySQL 엔진
MySQL 엔진은 클라이언트의 접속 및 쿼리 요청을 처리하는 커넥션 핸들러와 SQL 파서, 전처리기, 옵티마이저를 포함합니다.
### 스토리지 엔진
스토리지 엔진은 MySQL 엔진이 처리한 실제 데이터를 디스크 스토리지에 저장하거나 읽어오는 부분을 담당합니다. 

</div>
</details>

<details>
<summary>5-2. 옵티마이저에 대해 아는대로 말해주세요.</summary>
<div markdown="1">

옵티마이저는 쿼리를 최적으로 실행하기 위해 각 테이블의 데이터가 어떤 분포로 저장되어 있는지 통계 정보를 참조하여 최적의 실행 계획을 수립하는 기능을 담당합니다.

</div>
</details>

---

<details>
  <summary>6. SQL 인젝션에 대해 설명해주세요.</summary>

DB와 연동된 애플리케이션에서 입력된 데이터에 대한 유효성 검증을 하지 않을 경우, 악의적인 공격자는 입력 폼 등에 SQL을 삽입하여 DB로부터 정보를 열람하거나 조작할 수 있는 공격입니다.

### 예시
```sql
select * from users weher username='admin' adn password='' or '1'='1'
```
</details>
<details>
  <summary>6-1. SQL 인젝션을 막기위해서는 어떻게 해야하나요?</summary>

### Prepared Statement(선처리 질의문)
SQL 쿼리문을 선처리하여 이후 입력된느 변수 값이 항상 문자열 변수로만 다루어지도록 하는 방법입니다.
</details>

---

<details>
  <summary>7. SQL 인젝션에 대해 설명해주세요.</summary>

DB와 연동된 애플리케이션에서 입력된 데이터에 대한 유효성 검증을 하지 않을 경우, 악의적인 공격자는 입력 폼 등에 SQL을 삽입하여 DB로부터 정보를 열람하거나 조작할 수 있는 공격입니다.

### 예시
```sql
select * from users weher username='admin' adn password='' or '1'='1'
```
</details>

## 참고

Real MySQL

대학 강의 자료

https://dev-coco.tistory.com/158

https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4

https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/main/Database
