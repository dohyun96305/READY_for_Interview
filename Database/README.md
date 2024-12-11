
# Contents of Database
* [Database Key의 의미와 종류](#1)
  
---

## #1 
### **Database Key** 
* 데이터베이스에서 각 행을 구분하는 유일한 식별자 
  * 테이블에서 하나 이상의 열로 구성
  * 해당 열 값은 유일하고 불변해야 함
  * 데이터 정합성 유지, 검색, 수정, 삭제 등 작업을 수행할 때 중요한 역할
    * 데이터 정합성 : 데이터가 올바르게, 일관성 있게 유지되는 것을 의미

<br>

**슈퍼 키 (Super Key)**
* '유일성'의 특성을 만족하는 속성 또는 속성들의 집합

<br>

**후보 키 (Candidate Key)**
* '유일성'과 '최소성'을 만족하는 속성 및 속성들의 집합
* 슈퍼 키 중 '최소성'을 만족하는 것이 후보 키

<br>
  
**기본 키 (Primary Key)**
* 테이블에서 특정 행을 고유하게 식별할 수 있는 하나의 속성 또는 속성의 집합
* 테이블의 모든 행을 고유하게 식별할 수 있는 유일한 식별자
* 테이블에서 반드시 하나만 존재
* 모든 행에 대해 유일하고 NULL 값을 포함하지 않아야 함
  
<br>

**대체 키 (Alternate Key)**
* 기본 키로 선택되지 못한 후보 키
  
<br>
 
**복합 키 (Composite Key)**
* 두 개 이상의 속성으로 구성된 키
* 데이터 중복을 방지하고 무결성을 유지

<br>

**외래 키 (Foreign Key)**
* 어떤 테이블에 소속된 속성 또는 속성 집합이 다른 테이블의 기본 키가 되는 키
* 테이블 간 관계를 표현하기 위해 필요

<br>

**유니크 키 (Unique Key)**
* 특정 속성 또는 속성의 집합에 대해 유일성을 강제하는 제약조건 
  * 해당 속성에 대해 중복된 값을 허용하지 않음
* 여러 개의 속성을 조합하여 지정, NULL 값을 포함할 수 있음.
* 테이블에서 중복된 값을 허용하지 않아야하는 경우 사용.

<br>

**REF**
- [[DB] 관계형 데이터베이스 키(key) 이해하기](https://adjh54.tistory.com/245)
- [[데이터베이스/DB] 4. 관계형 데이터베이스의 키(key)의 종류](https://ddecode.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4DB-4%EA%B4%80%EA%B3%84%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%9D%98-%ED%82%A4key%EC%9D%98-%EC%A2%85%EB%A5%98)
- [[데이터베이스] Key의 종류와 역할](https://velog.io/@yoonuk/DB-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%97%90%EC%84%9C-Key%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%EC%97%AD%ED%95%A0)

---