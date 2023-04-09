---
title: 터미널에서 MySQL 접속
slug: "/터미널에서-MySQL-접속"
date: 2021-08-12
tags:
  - DevOps
---

### 접속하기

```bash
mysql -u username -p -h dbhost
```

### 외부에서 접속 시 ssh 터널링으로 **접속하기**

1. **특정 포트번호로 SSH 터널 생성**

```bash
# ex) 3307 포트로 SSH 터널링
ssh -i example.pem -f -N -L 3307:dbhost:3306 ubuntu@host
```

1. **생성된 터널로 mysql 접속**

```bash
# (local에서 터널을 생성했으므로 dbhost 는 127.0.0.1)
mysql -u root -p -h 127.0.0.1 -P 3307
```
