---
title: DB Slow Query 조회, 튜닝 방법
slug: "/DB-Slow-Query-조회,-튜닝-방법"
date: 2021-07-21
tags:
  - Database
---

## Slow Query 원인

- select 하면 해당 테이블에 rock 이 걸림 -\> 검색하는 도중에 DB가 변경되면 안되기 때문이다.
- 기본적으로 PK 에는 index가 설정된다. 그래서 where 조건으로 PK 를 검색하면 빠르다.
- 하지만 where 구문으로 날짜(Date) 를 검색한다고 가정하면 모든 날짜들을 직접 비교하여 가져오므로 시간이 오래걸린다..
- 이때 Date 에 index 를 추가해주면 select 시 시간 단축이 가능

## 튜닝 방법

1. index 걸기
2. query 자체 변경
3. join 을 많이 사용하지 않기(select 시 join이 걸려있는 테이블 모두 rock 걸림)

## Index 단점

- Insert, Update, Delete 등 데이터를 변경해야 할때는 느림. 데이터가 변경될 경우에는 변경 후 정렬 작업을 다시 해야하기 때문임
- index 가 생성된 대상은 따로 정렬된 테이블이 생성되기 때문에, 해당 데이터만큼 용량이 증가하게 됨
