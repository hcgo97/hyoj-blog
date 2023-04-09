---
title: DB index 정리
slug: "/DB-index-정리"
date: 2021-09-29
tags:
  - Database
---

## 1. 인덱스를 검사하는 법

- 쿼리문 앞에 explain 붙이기
- **explain** select * from Table_Name where A='a' and B='b' order by C,D,E ;
- type 컬럼
    - ALL :  인덱스 타지 않음
    - 그외 : 인덱스 타는 중 → (system,const,eq_ref,range,index,ALL,fulltext)
- key 컬럼
    - 해당 쿼리문이 타고 있는 인덱스

### 2. 경우의 수가 작은 것은 인덱스를 타지 않는다

- 성별같이 경우의 수가 2개인 것은 인덱스 타지않음 (데이터가 아무리 많아도 안탐)
- 쿼리문의 결과값이 1/3미만일 경우에만 인덱스 탐
- ex) Table_Name 테이블에서 No 필드가 Primary Key, A 필드에 Index가 걸려있고, 데이타수가 30000개일 경우
    - select * from Table_Name where No\>0 and A\>0; // **인덱스 안탐.**
    - select * from Table_Name where No\>20000 and A\>0; // **Primary 인덱스를 탐.**
    - select * from Table_Name where No\>0 and A\>20000; // **A 인덱스를 탐.**

### 3. 여러개의 인덱스 동시에 태우려면 결합인덱스 사용 (검색조건 여러개인 경우)

- 결합인덱스는 세개의 필드를 정렬해서 하나의 인덱스를 생성
- CREATE INDEX GeoHistory_requestId_createdAt_serviceName_index
ON GeoHistory **(A,B,C)**;
- ALTER TABLE Table_Name ADD INDEX **(A,B,C)**;

### 4. order by 에서 사용하는 인덱스

- select * from Table_Name order by A; → 이 경우에 A인덱스를 탄다
- select * from Table_Name where B='b' order by A; → 이 경우에 B인덱스만 탄다.
- 이경우에 두개의 인덱스를 다 타게 하려면 결합인덱스로 (A,B)를 생성시키고, A의 조건을 where 문에 지정해야함
- ORDER BY 에서 인덱스가 적용 안되는 경우
    - `order by b, c`
        - 인덱스 첫번째 컬럼인 **a가 누락**되어 사용 불가
    - `order by a, c`
        - 인덱스에 포함된 **b 컬럼이 a, c 사이에 미포함**되어 사용 불가
    - `order by a, c, b`
        - 인덱스 컬럼과 order by 컬럼간 **순서 불일치**로 사용 불가
    - `order by a, b desc, c`
        - b 컬럼의 `desc` 로 인해서 사용 불가
    - `order by a, b, c, d`
        - 인덱스에 **존재하지 않는 컬럼** 으로 인해 사용 불가
- MySQL 8.0 이전 버전까지는 desc index 적용되지 않음
    - 단지 scan 방식만 선택가능함
    - 만들어진 index 블록을 앞에서부터 읽을지 / 뒤에서부터 읽을지

### 5. LIKE 에서 사용하는 인덱스

- where A like '%a%' → 인덱스를 타지 않음
- where A like 'a%' → 인덱스를 탐

### 6. join문에서의 인덱스

- SELECT A.x, B.y, C.z
FROM A, B, C
WHERE A.x = B.y
AND B.y = C.z;
- A,B,C 테이블에 각각 1000개의 데이터가 들어있다고 가정하면 1000 * 1000 * 1000 번이 되기 때문에 속도이슈 발생함
**→ 해결방안 :**
    - **(1)** B 테이블에 A 테이블의 데이터와 관련있는곳에 인덱스를 사용
    - **(2)** C 테이블에 B 테이블의 데이터와 관련있는곳에 인덱스를 사용
