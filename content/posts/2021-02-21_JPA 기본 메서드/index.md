---
title: JPA 기본 메서드
slug: "/JPA-기본-메서드"
date: 2021-02-21
tags:
  - Spring Boot
---

**save()**    레코드 insert,update

**findOne()** primary key로 레코드 한건 찾기

**findAll()** 전체 레코드 불러오기, 정렬(sort), 페이징(pageable) 가능

**count()**   레코드 갯수

**delete()**  레코드 삭제

**findBy~**   쿼리를 요청하는 메서드임을 알림(where)

**countBy~**  쿼리 결과 레코드 수를 요청하는 메서드임을 알림

**And** - and검색

```
findByEmailAndUserId(String email, String userid)
```

**Or** - or검색

```
findByEmailOrUserId(String email, String userid)
```

**Between** - between검색

```
findByCreatedAtBetween(Date fromDate, Date toDate)
```

**LessThan** - 작은항목검색 \<

```
findByAgeLessThan(int age)
```

**GreaterThanEqual** - 크거나같은항목 \>=

```
findByAgeGreaterThanEqual(int age)
```

**Like** - like검색

```
findByNameLike(String name)
```

**IsNull** - null값인항목검색

```
findByJobIsNull()
```

**In** - 여러값중에 하나인 항목검색

```
findByJobIn(List<String> jobs)
```

**OrderBy** - 검색결과를 정렬하여 전달

```
findByEmailOrderByNameAsc(String email)
```

**@Query 어노테이션 사용해서 JPQL 사용가능**

- 무조건 String 타입(type check 불가능)
- native = true 옵션 사용으로 SQL 과 동일하게 사용가능

```
@Query("select m from Member m where m.username = ?1")
Member findByUsername(String username, Pageable pageable);
```
