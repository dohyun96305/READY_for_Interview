# #Contents_of_Database
* [Database Key의 의미와 종류 - #1](#1)
  * [기본 키 수정 가능 여부 - #1-1](#1-1)
  * [MySQL에서 기본 키 없이도 테이블을 만들 수 있는 이유 - #1-2](#1-2)
  * [외래 키 NULL 값 가능 여부 - #1-3](#1-3)
  * [UNIQUE 키워드에 따른 쿼리 성능의 차이 - #1-4](#1-4)
* [Database Index Scan 방식의 종류 - #2](#2)
* [정규화의 의미 - #3](#3)
* [B-tree, B+tree - #4](#4)
* [DB Locking - #5](#5)
  * [Optimistic Lock / Pessimistic Lock - #5-1](#5-1)
*  [Transaction, ACID 원칙 - #6](#6)
   * [트랜잭션 격리 수준 (Isolation Level) - #6-1](#6-1)

---

## #1 
### **Database Key** 
* 데이터베이스에서 각 행을 구분하는 유일한 식별자 
  
  * 테이블에서 하나 이상의 열로 구성

  * 해당 열 값은 유일하고 불변해야 함

  * 데이터 정합성 유지, 검색, 수정, 삭제 등 작업을 수행할 때 중요한 역할

    * 데이터 정합성 : 데이터가 올바르게, 일관성 있게 유지되는 것을 의미

1. **슈퍼 키 (Super Key)**
   * '유일성'의 특성을 만족하는 속성 또는 속성들의 집합

2. **후보 키 (Candidate Key)**
   * '유일성'과 '최소성'을 만족하는 속성 및 속성들의 집합

   * 슈퍼 키 중 '최소성'을 만족하는 것이 후보 키

3. **기본 키 (Primary Key)**
   * 테이블에서 특정 행을 고유하게 식별할 수 있는 하나의 속성 또는 속성의 집합

   * 테이블의 모든 행을 고유하게 식별할 수 있는 유일한 식별자

   * 테이블에서 반드시 하나만 존재

   * 모든 행에 대해 유일하고 NULL 값을 포함하지 않아야 함
     
4. **대체 키 (Alternate Key)**
   * 기본 키로 선택되지 못한 후보 키
  
5. **복합 키 (Composite Key)**
   * 두 개 이상의 속성으로 구성된 키

   * 데이터 중복을 방지하고 무결성을 유지

6. **외래 키 (Foreign Key)**
   * 어떤 테이블에 소속된 속성 또는 속성 집합이 다른 테이블의 기본 키가 되는 키

   * 테이블 간 관계를 표현하기 위해 필요 

7. **유니크 키 (Unique Key)**
   * 특정 속성 또는 속성의 집합에 대해 유일성을 강제하는 제약조건 

   * 해당 속성에 대해 중복된 값을 허용하지 않음

   * 여러 개의 속성을 조합하여 지정, NULL 값을 포함할 수 있음

   * 테이블에서 중복된 값을 허용하지 않아야하는 경우 사용

<br>

***REF***
- [[DB] 관계형 데이터베이스 키(key) 이해하기](https://adjh54.tistory.com/245)
- [[데이터베이스/DB] 4. 관계형 데이터베이스의 키(key)의 종류](https://ddecode.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4DB-4%EA%B4%80%EA%B3%84%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%9D%98-%ED%82%A4key%EC%9D%98-%EC%A2%85%EB%A5%98)
- [[데이터베이스] Key의 종류와 역할](https://velog.io/@yoonuk/DB-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%97%90%EC%84%9C-Key%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%EC%97%AD%ED%95%A0)

</br>

[BACK TO HEAD](#Contents_of_Database)

--- 

## #1-1
### 기본 키 수정 가능 여부 => 조건에 따라 가능은 함
  1. 수정하고자 하는 값을 가진 기본 키가 없는 경우
  
  2. 다른 테이블에서 기본 키를 참조하는 외래 키가 없는 경우
  
  3.  수정하고자 하는 값이 NULL이 아닌 경우

### 기본 키 수정을 권장하지 않는 이유 
  1. 다른 테이블에서 외래 키를 통해 기본 키를 참조하는 경우 

      * 기본 키 수정할 경우 참조하는 외래 키 또한 전부 수정해야 함 => '성능 저하'
    
      * 일부 RDBMS는 'CASCADE UPDATE' 를 지원하지 않음
  
  2. 참조하는 외래 키가 Index 처리가 된 경우

      * 기본 키 수정할 경우 외래 키의 Index 구조에 대해 삭제 및 삽입 등 작업 발생 => '성능 저하' 

  3. Organization Index 테이블 혹은 Clustered 기본 키를 사용하는 RDBMS 경우 
  
       * 기본 키 값에 따라 데이터를 물리적으로 정렬한 상태 
     
         * 기본 키 수정에 따른 정렬 상태 유지를 위한 물리적인 삭제 및 삽입 등 작업 발생 => '성능 저하' 
  
          ```
          Organization Index 테이블
            * 기본 키에 대한 Index 구조를 통해 데이터를 저장하는 Table 구조 
          Clustered 기본 키
            * 기본 키 제약 조건이 지정된 속성에 대해 자동으로 생성된 index
          ```
  4. 외부 시스템 (어플리케이션 캐시, 다른 DB) 와의 참조가 되어있는 경우
   
       * 기본 키 수정에 따른 외부 시스템과의 참조 관계가 깨질 수 있음 

<br>

***REF***
- [stackoverflow](https://stackoverflow.com/questions/3838414/can-we-update-primary-key-values-of-a-table)
- [[DB] PK는 수정이 가능할까?](https://m42-orion.tistory.com/174)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #1-2
### MySQL에서 기본 키 없이도 테이블을 만들 수 있는 이유

</br>

***REF***

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #1-3
### 외래 키 NULL 값 가능 여부 => 가능 
  * 참조 무결성 제약 조건 
    * 외래 키 값은 NULL이거나 참조하는 기본 키 값과 동일해야 한다.
    * 각 테이블은 참조할 수 없는 외래 키 값을 가질 수 없다.
  
  <br>

  1. 테이블을 생성할 떄 외래 키의 값을 알 수 없는 경우 => NULL 값 
   
  2. 참조하는 테이블의 특정 데이터가 삭제되거나 기본 키의 값이 변경 될 경우
      * ON DELETE SET NULL 설정을 통해 외래 키 NULL 값 변경, 참조 무결성 유지 

<br>

***REF***
- [[데이터베이스]외래키(FK)는 NULL값을 허용할까?](https://hxerimione.tistory.com/33)
- [외래 키 (Foreign Key)](https://ruhaharu1107.tistory.com/24)
- [MySQL ON delte, cascade, set null에 대해](https://swkn.tistory.com/89ㄴ)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #1-4
### UNIQUE 키워드에 따른 쿼리 성능의 차이
  * UNIQUE 키워드가 설정된 칼럼은 해당 값들이 중복되지 않도록 보장됨
    * UNIQUE Index 생성
    * Index => Read가 빠르지만 CREATE, UPDATE, DELETE가 느림 

  * 일반적인 Index와 UNIQUE Index는 구조적인 차이가 없어 성능 상 차이가 거의 없음 
    * 테이블 내 중복되는 데이터의 개수에 따른 성능 차이 발생
  
  * **UNIQUE Index VS Index**
    * 중복되는 데이터가 없기 때문에 검색 속도가 빠를 수 잇음
    * 중복 여부를 확인하기 위해 쓰기 속도가 느림
      * 중복된 값을 체크할 때 읽기 잠금을 사용
      * 쓰기를 할 때 쓰기 잠금을 사용
      * **데드락 발생 가능성 증가**
    * 많은 데이터가 입력된 이후 UNIQUE Index 지정간 Index 구성에 많은 시간이 걸림 => 성능 저하
  *  불필요한 Index 설정은 DB 메모리의 남용으로 인한 성능 저하가 발생할 수 있음

<br>

***REF***
- [Unique 제약조건과 조회시 성능상의 이점](https://velog.io/@jurlring/Unique-%EC%A0%9C%EC%95%BD%EC%A1%B0%EA%B1%B4%EA%B3%BC-%EC%A1%B0%ED%9A%8C%EC%8B%9C-%EC%84%B1%EB%8A%A5%EC%83%81%EC%9D%98-%EC%9D%B4%EC%A0%90)
- [[MySQL] 인덱스(Index)란?](https://s-y-130.tistory.com/107)

</br>

[BACK TO HEAD](#Contents_of_Database)

--- 

## #2
### Database Index Scan 방식의 종류
* **Full Table Scan**
  * Index를 사용하지 않고 테이블의 모든 행을 검색하는 방식
  * WHERE 조건문을 기준으로 활용할 Index가 없는 경우 
  * 전체 데이터 대비 대량의 데이터가 필요한 경우 (20~25%)

</br>

* **Index Full Scan**
  * Index의 모든 값을 순차적으로 읽어오는 방식 
    * Index로 구성된 컬럼만 요구하는 쿼리일 경우 사용
* **Index Range Scan**
  * Index 내 특정 범위의 값을 검색할 때 사용하는 방식
    * 조건절에 비교연산자와 같은 범위 조건이 포함될 때 사용
* **Index Unique Scan**
  * Primary Key 혹은 Unique Index를 사용해 특정 행을 검색할 때 사용하는 방식
    * 조건문에서의 '=' 조건으로 검색할 때 사용
    * 유일한 Index가 적용된 컬럼에 대해 특정 값을 조회할 때 사용
* **Index Skip Scan**
  * 선행 데이터가 없는 경우 후행 데이터를 이용해서 검색하는 방식 ( GROUP BY, MIN(), MAX() 등 사용 )
    * 조건에 맞는 블록만 탐색하는 방식으로 조건에 맞지 않는 경우 Skip 진행
* **Index Merge Scan**
  * 테이블 내 Index들을 통합해서 검색하는 방식 
    * 조건문에서의 'OR' 조건으로 검색할 때 사용

</br>

***REF***
- [mysql index scan 정리](https://velog.io/@greentea/mysql-index-scan-%EC%A0%95%EB%A6%AC)
- [MySql 오브젝트 스캔 유형](https://hssm93.tistory.com/entry/%EC%9A%A9%EC%96%B4-mysql-%EC%98%A4%EB%B8%8C%EC%A0%9D%ED%8A%B8-%EC%8A%A4%EC%BA%94-%EC%9C%A0%ED%98%95)
- [MSSQL 인덱스(INDEX) 스캔 원리 및 방법](https://aurumguide.tistory.com/72) 
- [MySQL 인텍스 스킵 스캔 (Index Skip Scan)](https://mentha2.tistory.com/289)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #3
### 정규화의 의미 
* 관계형 데이터베이스 설계에서 데이터 중복을 줄이고 데이터 무결성을 개선하기 위해 데이터를 정규형에 맞도록 구조화하는 프로세스
* 이상 현상이 있는 릴레이션을 분해해 이상 현상을 없애는 과정 
  * 이상 현상 
    * 데이터간 중복이 있어 데이터 변경 (삽입, 삭제, 수정)간 발생하는 오류 
      * 삽입 이상 : 데이터 삽입 간 불필요한 데이터까지 삽입
      * 삭제 이상 : 데이터 삭제 간 유용한 데이터 삭제
      * 갱신 이상 : 중복된 데이터 중 일부만 수정되어 데이터 불일치 발생 
  
  * 함수 종속성 
    * 어떤 속성 A의 값을 알면 다른 속성 B의 값이 유일하게 정해지는 관계 
    * A -> B로 표기, A는 B의 결정자 (Determinant)
      * A는 B를 결정한다. (Determine)
      * B는 A에 종속한다. (Dependent)

* **정규화의 장점**
  * 데이터베이스 변경 시 이상 현상 (Anomaly)을 제거할 수 있다.
  * 정규화된 데이터베이스 구조에서 새로운 데이터 형의 추가로 인한 확장 시 용이하다.
  * 데이터베이스와 연동된 응용 프로그램에 최소한의 영향을 끼친다.

* **정규화의 단점**
  * 릴레이션의 분해로 릴레이션 간의 JOIN 연산이 많아진다.
  * 질의에 대한 응답시간이 느려질 수 있다.

</br> 

### **정규형 (Normal Form)**
  * **제 1 정규형** 
    * "각 컬럼이 원자 값 (더이상 분리되지 않는 값)으로만 구성되어야 한다."
      * 각 컬럼이 하나만의 속성만을 가져야 한다.
      * 하나의 칼럼은 같은 종류나 속성 (Type)을 가져야 한다.
      * 각 칼럼은 유일한 (Unique) 이름을 가져야 한다.
      * 칼럼의 순서가 상관없어야 한다.
  
  * **제 2 정규형**
    * 제 1 정규형을 만족
    * "모든 칼럼이 부분적 종속 (Partial Dependency)가 없어야 한다." => 모든 칼럼이 완전 함수 종속을 만족해야 한다.
      * 기본키의 부분집합이 결정자가 되어선 안된다.
  
  * **제 3 정규형**
    * 제 2 정규형을 만족
    * "기본키를 제외한 속성들 간 이행 종속성 (Transitive Dependency)가 없어야 한다."
      * 이행 종속성 : A -> B, B -> C일 때 A -> C가 성립되면 이행 종속 관계
  
  * **BCNF (Boyce-Codd Normal Form)**
    * 제 3 정규형을 만족
    * "모든 결정자가 후보키 집합에 속해야 한다."
      * 후보키 집합에 없는 칼럼이 결정자가 되어서는 안된다.
  
</br>

***REF***
- [데이터베이스 정규화](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)
- [이상(Anomaly)과 정규화(Normalization)](https://bactoria.tistory.com/entry/%EC%9D%B4%EC%83%81Anomaly%EA%B3%BC-%EC%A0%95%EA%B7%9C%ED%99%94Normalization)
- [[DB] 정규화란? (Normalization), 정규화 예시](https://code-lab1.com/%EC%A0%95%EA%B7%9C%ED%99%94/)
- [[DB] 이상현상(Anomaly), 함수 종속성(Functional Dependency)란?](https://code-lab1.com/%ec%9d%b4%ec%83%81%ed%98%84%ec%83%81/)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #4
### B-Tree, B+Tree 

### **이진 탐색 트리 (Binary Search Tree)**
  * 자식을 두개 가질 수 있는 노드들로 구성되는 트리 형태의 자료구조 
    * 각 노드의 값은 유일하며 중복된 값은 허용되지 않음
    * 각 노드의 왼쪽 서브 트리에는 자신보다 작은 값들이 배치 
    * 각 노드의 오른쪽 서브 트리에는 자신보다 큰 값들이 배치 
  
  * **순회 방법** 
    * **전위 순회 (Preorder Traversal)**
      * 루트 노드를 먼저 방문한 후, 왼쪽 서브트리 방문 이후 오른쪽 서브트리를 방문
    * **중위 순회 (Inorder Traversal)**
      * 왼쪽 서브트리를 먼저 방문한 후, 루트 노드 방문 이후 오른쪽 서브트리를 방문
    * **후위 순회 (Postorder Traversal)**
      * 왼쪽 서브트리, 오른쪽 서브트리를 방문한 후, 루트 노드 방문 
  
</br>

* **루트 노드 (Root Node)** : 가장 상단의 노드
* **브랜치 노드 (Branch Node)** : 중간 노드 
* **리프 노드 (Leaf Node)** : 가장 아래의 노드 

</br>

### B-Tree
  * 이진 탐색 트리를 발전시킨 자료구조 
  * 2개 이상의 자식 노드를 가질 수 있는 자료구조 
    * 부모 노드에 저장된 값이 N개 일 때 자식 노드는 최대 N+1개의 노드를 가질 수 있음
      * Ex) 부모 노드 : $X_1, X_2, \ldots$ 에 대해 
        * 자식 노드 :  $X_1$보다 작은 노드, $X_1$ 초과 $X_2$ 미만 노드, $\ldots$ , $X_n$ 보다 큰 노드 
  * 관계형 DB Index에서 자주 사용되는 자료구조 

</br>

### B+Tree
  * B-Tree 구조에서 검색 성능을 발전시킨 자료구조 
  * 리프 노드간 '연결성'이 추가된 자료 구조 
  * 범위 검색에 유용하다는 특징을 가짐  
    * Ex) A 이상 B 이하의 범위를 찾아야하는 상황
      * B-Tree
        * 최상위 노드 => A 값 노드 위치 => 최상위 노드 => B 값 노드 위치 
      * B+Tree
        * 최상위 노드 => A 값 노드 위치 => B 값 노드 위치 

</br>

### B-Tree vs B+Tree
  * B-Tree 
    * '균일성' : 어떤 값에 대해서 같은 시간에 결과를 얻을 수 있음 
    * 브랜치 노드 및 리프 노드에 주소값 및 데이터가 저장되기 떄문에 메모리 효율성이 낮음
  * B+Tree
    * 리프 노드에만 데이터가 저장되기 때문에 메모리 효율이 상대적으로  좋음
    * 리프 노드에 '연결성'을 나타내는 데이터가 추가적으로 관리되어야 함 
      * => 데이터 생성 및 수정 삭제가 일어날 때 성능이 비효율적임.
  
</br>

***REF***
- [[Algorithm] 이진 탐색 트리 (Binary Search Tree, BST) + 전위 중위 후위 순회](https://kangworld.tistory.com/51)
- [[MySQL] Index의 구조 : B-Tree, B+Tree](https://velog.io/@juhyeon1114/MySQL-Index%EC%9D%98-%EA%B5%AC%EC%A1%B0-B-Tree-BTree)
- [이진탐색트리(Binary Search Tree)의 핵심](https://jh2021.tistory.com/34)
- [[MySQL] B-tree, B+tree란? (인덱스와 연관지어서)](https://zorba91.tistory.com/293)
- [[DB] 인덱스에서 B+Tree를 사용하는 이유](https://munak.tistory.com/182)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #5
### **DB Locking**
  * 병행 트랜잭션이 가능한 환경에서 변경중인 Record를 다른 Transaction들이 접근하지 못하도록 막음 

  * '데이터베이스 동시성' 및 '데이터 일관성' 보장
    * 병행 트랜잭션 : 동시에 실행되고 있는 둘 이상의 트랜잭션

</br>

### **병행 트랜잭션의 동시성 문제** 
  * **갱신 분실 (Lost Update)**
    * 두 트랜잭션이 병렬로 같은 데이터를 읽고 갱신하는 과정에서 한 트랜잭션이 다른 트랜잭션의 갱신 값을 덮어쓰는 문제
  
  * **모순적 읽기 (Inconsistent Read)**
    * 두 트랜잭션이 병렬로 같은 데이터를 읽고 갱신하는 과정에서 데이터 불일치가 발생하는 문제
  
  * **Dirty Read**
    * 격리성 수준이 Read Uncommitted 이하인 환경에서 발생가능한 문제
    * 한 트랜잭션이 다른 트랜잭션으로부터 커밋되지 않은 값을 읽어 발생하는 문제
  
  * **Non-Repeatable Read**
    * 같은 데이터를 한 트랜잭션 내에서 읽었음에도 둘의 값이 다른 문제
  
  * **Phantom Read**
    * 같은 조건에 대한 검색을 한 트랜잭션 내에서 읽었음에도 다시 읽을 때 이전에 존재하던 값이 없어지거나, 새로운 값이 추가로 검색되는 문제
  
  * **연쇄적 롤백 (Cascading Rollback)**
    * 한 트랜잭션이 갱신한 데이터를 다른 트랜잭션이 갱신한 뒤 상황
    * 앞선 트랜잭션을 롤백하려 할 때  이후 실행했던 트랜잭션도 롤백해야 하나 이미 해당 트랜잭션은 완료되어 롤백이 불가능한 문제

</br>

### **LOCK 설정 범위** 
  * **데이터베이스**
    * 전체 데이터베이스를 기준 Lock
    * 1개의 세션만이 DB 데이터에 접근이 가능 

  * **파일**
    * 데이터베이스 파일을 기준 Lock 
      * 파일 : 테이블, Row 등과 같은 실제 데이터가 Write 되는 물리적인 저장소
    * 잘 사용되지 않음

  * **테이블**
    * 데이터베이스 테이블을 기준 Lock 
    * 테이블의 모든 행을 업데이트 하는 등 전체 테이블에 영향을 주는 변경을 수행할 때 유용
    * DDL (CREATE, ALTER, DROP) 구문과 함께 사용 => 'DDL Lock'

  * **페이지와 블록**
    * 파일의 일부인 페이지, 블록을 기준 Lock
    * 잘 사용되지 않음

  * **컬럼 (Column)**
    * 테이블 컬럼을 기준 Lock
    * Lock 설정 및 해제의 리소스가 많이 들어 잘 사용되지 않음

  * **행 (Row)**
    * 1개의 행을 기준 Lock
    * DML (SELECT, INSERT, UPDATE, DELETE)에 대한 Lock으로서 가장 일반적으로 사용되는 Lock

</br> 

### **Lock 종류** 
  * **공유 락 (Shared Lock, S)**
    * 데이터를 변경하지 않는 읽기 명령에 주어지는 Lock
    * 읽기 명령은 데이터 일관성에 영향을 주지 않기 때문에 동시 접근이 가능함

  * **베타 락 (Exclusive Lock, X)**
    * 데이터에 변경을 가하는 쓰기 명령에 주어지는 Lock
    * 다른 세션이 해당 자원에 접근 (SELECT, INSERT 등)을 막음 
    * 트랜잭션동안 유지됨

  * **업데이트 락 (Update Lock)**
    * 데이터를 수정하기 위해 베타 락을 걸기 전, 데드 락을 방지하기 위해 사용하는 Lock
    * 일반적으로 UPDATE 쿼리의 필터 (WHERE)가 실행되는 과정에서 적용
    * 컨버젼 데드락이 발생할 떄 이를 막기 위해 SELECT 쿼리에서도 적용될 수 있음

  * **내재 락 (Intent Lock)**
    * 사용자가 요청한 범위에 대한 락을 사용할 수 있는지 여부를 빠르게 파악하기 위해 사용하는 Lock 
    * 공유 락과 베타 락 앞에 I 기호를 붙인 IS, IX, SIX 등 있음

</br>

***REF***
- [[Database] 데이터베이스 락(Lock)의 종류와 역할](https://velog.io/@koo8624/Database-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EB%9D%BDLock%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%EC%97%AD%ED%95%A0)
- [[DB] DB Locking 알아보기](https://cloudsoswift.github.io/post/develop/database/db-locking/)
- [DB Lock 기초](https://shuu.tistory.com/88)
- [IT 위키 - 데이터베이스 병행제어](https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EB%B3%91%ED%96%89%EC%A0%9C%EC%96%B4#Cascade_Rollback)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #5-1
### Optimistic Lock / Pessimistic Lock

### 낙관적 Lock (Optimistic Lock)
  * 충돌이 거의 발생하지 않을 것이라고 가정, 충돌이 발생한 경우에 대비하는 방법
  * DB의 특징을 이용하는 것이 아닌 Application Level에서 처리

### 비관적 Lock (Pessimistic Lock)
  * 충돌이 발생할 확률이 높다고 가정, 트랜잭션 시작 전 공유 락 또는 베타 락을 미리 걸고 시작하는 방법
  * 데이터 수정 시 바로 트랜잭션의 충돌 여부를 확인할 수 있음

</br>

### Optimistic Lock vs Pessimistic Lock
  * Optimistic Lock
    * Lock으로 인한 대기시간이 없이 동시 처리량이 높음
    * Lock이 없어 deadlock 같은 상황 또한 발생하지 않음
    * Transaction이 실패하는 경우 retry 매커니즘 등 구현 어려움이 있음
  
  * Pessimistic Lock
    * 데이터 자체의 접근이 차단 => 무결성 향상, 구현이 쉬움
    * 데이터 Lock 되는 시간이 길어질수록 전체적인 처리량이 저하되며 deadlock 상태에 빠질 수 있음

</br>

***REF***
- [[JPA] 낙관적 락(Optimistic Lock)과 비관적 락(Pessimistic Lock)에 대해](https://mozzi-devlog.tistory.com/37)
- [[DB] 낙관적 락 (Optimistic Lock), 비관적 락 (Pessimistic Lock)](https://donkim0122.tistory.com/119)
- [비관적 락 (Pessismistic Lock) vs 낙관적 락 (Optimistic Lock)](https://jipang9-greedy-pot.tistory.com/161)
- [[DB] Optimistic Locking vs Pessimistic Locking](https://breakcoding.tistory.com/403)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #6
### Transaction, ACID 원칙 

### 트랜잭션 (Transaction)
  * 'DB 상태를 변환시키는 하나의 논리적 기능'을 수행하기 위한 작업의 단위 혹은 일련의 연산 

  * 트랜잭션의 연산 
    * **COMMIT** 
      * 트랜잭션이 성공적으로 수행되었음을 선언하는 연산
  
    * **ROLLBACK** 
      * 트랜잭션 수행이 실패했음을 선언하고 작업을 취소하는 연산

### ACID 원칙 (트랜잭션의 4가지 특성)
  * **원자성 (Atomicity)**
    * 트랜잭션의 연산은 DB에 전부 반영되거나 전부 반영되지 않아야한다 (All or Nothing)
    * 트랜잭션 내 모든 명령은 모두 완벽히 수행한 후 DB에 반영되어야함
    * 어느 하나의 명령이라도 오류가 발생하면 트랜잭션 전부가 취소되어야 함

  * **일관성 (Consistency)**
    * 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.
    * 트랜잭션이 성공적으로 종료되면 언제나 '데이터 무결성'을 보장
    * 고정요소에 대해 트랜잭션 수행 전과 수행 완료 후의 상태가 같아야함

  * **독립성 (Isolation)**
    * 하나의 트랜잭션이 실행하고 있는 도중, 다른 트랜잭션이 간섭할 수 없음
    * 수행중인 트랜잭션이 완전히 완료되기 전까지 다른 트랜잭션에서 수행 결과를 참조할 수 없음

  * **영속성 (Durability)**
    * 성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나도 영구적으로 반영되어야함.

</br>

***REF***
- [[DB] 트랜잭션 (Transaction) with 4가지 특성](https://jindevelopetravel0919.tistory.com/48)
- [[Database] 트랜잭션 정리](https://velog.io/@shasha/Database-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%A0%95%EB%A6%AC)

</br>

[BACK TO HEAD](#Contents_of_Database)

---

## #6-1
### 트랜잭션 격리 수준 (Isolation Level)

  * 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 독립되어야 하는가에 대한 수준 
  * 트랜잭션의 ACID 원칙 중 독립성 (Isolation)에 대한 수준
  * 'DB 내 트랜잭션의 처리 속도'와 '데이터 정확성'에 대한 Trade-Off

### 트랜잭션 격리 수준 4단계
  * **Read Uncommitted**
    * 한 트랜잭션의 내용이 COMMIT 혹은 ROLLBACK 연산과 상관없이 다른 트랜잭션에서 조회가 가능한 수준
    * SELECT문을 실행하는 동안 Shared Lock이 걸리지 않음 
  
  * **Read Committed**
    * 한 트랜잭션의 내용이 COMMIT되어야만 다른 트랜잭션에서 조회가 가능한 수준 
    * SELECT문을 실행할 때, Shared Lock이 걸림
    * SELECT문 조회시 실제 테이블 값이 아닌 Undo 영역의 백업된 레코드 값을 읽어옴 
    * 대부분의 RDMS에서 기본적으로 사용하는 수준 
   
  * **Repeatable Read**
    * 한 트랜잭션이 시작되기 전 COMMIT된 내용에 대해서만 조회가 가능한 수준 
    * 한 트랜잭션이 완료될 때까지 SELECT문이 사용하는 모든 데이터에 Shared Lock이 걸림 
    * 트랜잭션의 실행시간이 길어질수록 계속 멀티 버전을 관리해야함 
    * MySQL InnoDB 스토리지 엔진 기본 격리수준 

  * **Serializable** 
    * 가장 단순하면서 엄격한 격리 수준, 성능적으로 동시 처리 성능이 가장 낮음
    * 트랜잭션들이 동시에 일어나지 않고 순자적으로 진행

</br>

### 트랜잭션 상호작용에 따른 문제점 
  * **Dirty Read**
    * 아직 COMMIT 되지 않은 트랜잭션의 데이터를 읽음
    * Read Uncommitted 수준에서 발생 

  * **Non_repeatable Read**
    * 한 트랜잭션 내 같은 행에 대해 2번 이상 조회했을 때, 결과가 다른 상황
      * 데이터의 수정 (UPDATE 쿼리)가 발생한 경우 
    * Read Uncommitted, Read Committed 수준에서 발생

  * **Phantom Read**
    * 한 트랜잭션에서 같은 쿼리로 2번 이상 조회했을 때, 결과가 다른 상황
      * 데이터의 삽입/삭제 (INSERT/DELETE 쿼리)가 발생한 경우
    * Serializable 제외 모든 격리 수준에서 발생
    * MySQL InnoDB에서는 발생하지 않음 
      * => next key lock (record lock + gap lock) 사용 

</br>

***REF***
- [[DB] 트랜잭션 격리수준 (Isolation Level) 에 쉽게 이해하기](https://tlatmsrud.tistory.com/118)
- [Isolation Level이란?](https://akasai.space/db/about_isolation/)
- [트랜잭션 격리 수준과 격리 수준에 따른 문제점](https://leeeeeyeon-dev.tistory.com/121)
- [[MySQL] 트랜잭션의 격리 수준(Isolation Level)에 대해 쉽고 완벽하게 이해하기
](https://mangkyu.tistory.com/299)

</br>

[BACK TO HEAD](#Contents_of_Database)

---
