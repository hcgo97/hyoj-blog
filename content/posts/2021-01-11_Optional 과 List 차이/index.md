---
title: Optional 과 List 차이
slug: "/Optional-과-List-차이"
date: 2021-01-11
tags:
  - Spring Boot
---

### Optional\<T\>

- **단일 엔티티** 조회시 사용
- 조회하려는 값이 존재할수도, 존재하지도 않을수도있어서 null에 의한 오류를 최소화하기 위해 사용
- **ifPresent()** : 특정결과 반환x
    
    Optional 값이 존재할경우에만 결과값 리턴(null일경우 리턴x)
    
    함수형 인자
    
- **isPresent()** : 특정결과 반환x
    
    Optional 값이 null인지 확인가능
    
    if-else문 안쓰고 null값 검사 가능
    

### List\<\>

- **리스트**를 받을경우에 사용
- 리스트결과값 없을때 null이 아니라 Empty List가 나옴
