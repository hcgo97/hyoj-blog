---
title: Redis CLI
slug: "/Redis-CLI"
date: 2022-03-21
tags:
  - Command
  - DevOps
---

### 서버 시작

```bash
redis-server
```

### 서버 확인

```bash
redis-cli ping
# 응답 결과: PONG
```

### 서버 정지

```bash
redis-cli shutdown
```

### 접속

```bash
redis-cli -p {포트번호}
```

### DB 변경

```bash
select {변경할 DB 번호}
```

### 패턴으로 키 조회

```bash
keys {패턴}
```

### 모든 키 삭제

```bash
flushall
```
