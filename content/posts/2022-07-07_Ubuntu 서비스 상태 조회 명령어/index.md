---
title: Ubuntu 서비스 상태 조회 명령어
slug: "/Ubuntu-서비스-상태-조회-명령어"
date: 2022-07-07
tags:
  - Ubuntu
  - Linux
  - Command
  - DevOps
---

### [ + ] : 실행 중인 서비스
### [ - ] : 중지된 서비스

### 모든 서비스 상태 조회
```bash
service --status-all
```

### 실행 중인 서비스만 조회
```bash
service --status-all | grep +
```

### 중지된 서비스만 조회
```bash
service --status-all | grep -
```
