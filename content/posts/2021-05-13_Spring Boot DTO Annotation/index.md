---
title: Spring Boot DTO Annotation
slug: "/Spring-Boot-DTO-Annotation"
date: 2021-05-13
tags:
  - Spring Boot
---

**1. Anotation 설정**

- @Entity
- @Table(name="table") : 설정되어있지 않으면 class명으로 table명 설정
- @Getter @Setter @EqualsAndHashCode : get/set 자동 생성, equals(), hashCode() 메소스 코드 생성
- @AllArgsConstructor : 모든 필드에 대한 값을 받는 생성자를 생성
- @Data : @Getter @Setter @EqualsAndHashCode @AllArgsConstructor 을 포함한 Lombok에서 제공하는 필드관련 모든 코드 생성

**2. 필드 설정**

- primary 필드 설정
    1. @Id , @GeneratedValue(strategy = GenerationType.AUTO) , @Column
    2. private Long seq
- @Column(nullable=false,length=50,columnDefinition="TEXT")
    1. 일반 필드 설정 시 Anotation
    2. nullable : default null설정 여부
    3. length : 필드 길이값
    4. columnDefinition : 데이터유형 설정 , TEXT,DATETIME
- DATE관련 설정
    1. import java.util.Date;
    2. @Column(nullable = false,columnDefinition = "DATETIME")
        
        private Date regDate;
        
    3. columnDefinition="TIMESTAMP DEFAULT CURRENT_TIMESTAMP" : insert시 현재 시간 적용

**3. @Temporal**

- 날짜타입(java.utilData, java.util.Calendar)를 매핑 시 사용
- @Temporal(TemporalType.DATE) / private Date date; // 날짜 2015-01-01
- @Temporal(TemporalType.TIME) / private Date time; // 시간 11:11:11
- @Temporal(TemporalType.TIMESTAMP) / private Date timestamp; // 날짜와 시간 2015-01-01 11:11:11
