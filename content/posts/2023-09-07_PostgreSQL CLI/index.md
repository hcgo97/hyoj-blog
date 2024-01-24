---
title: PostgreSQL CLI
slug: "/PostgreSQL-CLI"
date: 2023-09-07
tags:
  - Database
  - Command
---

## 기본 명령어

### PostgreSQL 접속
```bash
psql -U {username} -d {database name} -h {host} -p {port}
```

### PostgreSQL 종료
```bash
\q
```

### DB 목록 조회
```bash
\list
```
or
```bash
\l
```

### DB 목록 상세조회
```bash
\list+
```
or
```bash
\l+
```

### 다른 DB로 접속
```bash
\connect {database name}
```
or
```bash
\c {database name}
```

### 테이블 목록 조회
```bash
\d
```

### 테이블 상세조회
```bash
\dt {table name}
```

### 시스템 테이블 목록 조회
```bash
\dS
```

### 뷰 목록 조회
```bash
\dv
```

### 시퀀스 목록 조회
```bash
\ds
```

### 롤 목록 조회
```bash
\du
```

### 스키마 목록 조회
```bash
\dn
```

<hr></hr>

## 백업 및 복원 명령어

### 전체 백업
```bash
pg_dump > {백업파일명}
```

### DB만 백업
```bash
pg_dump {database name} > {백업파일명}
```

### 외부에서 DB만 백업
```bash
psql -U {username} {database name} > {백업파일명}
```

### DB만 복원
```bash
psql {database name} < {백업파일명}
```
