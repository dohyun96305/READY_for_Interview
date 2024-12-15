
# Contents of Database
* [Database Key의 의미와 종류 - #1](#1)
  * [기본 키 수정 가능 여부 - #1-1](#1-1)
  * [MySQL에서 기본 키 없이도 테이블을 만들 수 있는 이유 - #1-2](#1-2)
  * [외래 키 NULL 값 가능 여부 - #1-3](#1-3)
  * [UNIQUE 키워드에 따른 쿼리 성능의 차이 - #1-4](#1-4)
  
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
---

## #1-2
### MySQL에서 기본 키 없이도 테이블을 만들 수 있는 이유

</br>

***REF***

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
---

## #1-4
### UNIQUE 키워드에 따른 쿼리 성능의 차이
  * UNIQUE 키워드가 설정된 칼럼은 해당 값들이 중복되지 않도록 보장됨
    * **UNIQUE Index**생성
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
--- 
