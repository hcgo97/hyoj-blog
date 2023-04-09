---
title: 프로세스 관련 Linux 명령어
slug: "/프로세스-관련-Linux-명령어"
date: 2021-05-13
tags:
  - Command
  - Linux
  - DevOps
---

### 특정 포트 상태 조회

```bash
lsof -i tcp:{조회할 포트}
```

### 특정 포트 죽이기

```bash
kill $(lsof -t -i:{죽일 포트})
```

### 현재 리스닝하고있는 것들 보여줌 (LIST = 리스닝)

```bash
# -a: all, tcp + udp + sockets 까지 다알려줌
# -n: Local Address 를 IP 주소 형식으로 보여줌
# -p: 프로세스까지 같이알려줌

netstat -anp | grep LIST
```

### 제목행을 포함해서 포트+프로세스 다 보여줌

```bash
# -t: tcp 포함
# -u: udp 포함
# -l: localhost(0.0.0.0) 포함

netstat -tulpn
```

### 프로세스 id 로 프로세스 죽이기

```bash
kill -9 <pid>
```

### 특정 포트를 사용하는 프로세스 죽이기

```bash
# -k: kill

fuser -k {죽일 포트}/tcp
```

### 실행중인 프로세스 중에서 특정 문자열 드간거 보여줌

```bash
# -e: all process
# -f: full-format, 명령줄을 포함한 전체 형식
# -ef: 명령줄을 포함한 전체형식의 모든 프로세스

ps -ef | grep {문자열1} | grep {문자열2}
```
