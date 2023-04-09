---
title: Spring @Transaction
slug: "/Spring-@Transaction"
date: 2021-06-22
tags:
  - Spring Boot
---

- 메서드나 클래스에 @Transactional 어노테이션을 붙여서 해당 대상이 트랜잭션 처리가 필요한 것임을 명시
- 사용 시 메소드 실행 전에 트랜잭션 시작, 실행 후에 트랜잭션 커밋 or 롤백 처리함
- 클래스 레벨에서 사용 시 해당 클래스에 속한 모든 메소드가 트랜잭션 처리 대상이 됨
- default 로 UnCheckedException , Error 에 대해서 롤백 정책을 설정함
    - 따라서 @Transactional 에 아무 속성 안주면,
    @Transactional(rollbackFor = \{RuntimeException.class, Error.class\}) 로 인식됨
