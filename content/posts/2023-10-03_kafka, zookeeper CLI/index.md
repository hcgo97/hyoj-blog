---
title: kafka & zookeeper cli
slug: "/kafka-and-zookeeper-cli"
date: 2023-10-03
tags:
  - Kafka
  - Command
  - DevOps
---

### 토픽 생성

```bash
kafka-topics.sh --create --topic {topic name} --bootstrap-server {kafka host:port} --replication-factor 1 --partitions 1
```

### 토픽 목록 조회

```bash
kafka-topics.sh --list --bootstrap-server {kafka host:port}
```

### 토픽 정보 조회

```bash
kafka-topics.sh --bootstrap-server {kafka host:port} --topic {topic name} --describe
```

### 특정 토픽으로 메시지 발행

```bash
kafka-console-producer.sh --broker-list {kafka host:port} --topic {topic name}
```

### 특정 토픽으로 발행된 메시지 pulling

- `--from-beginning` : 해당 토픽의 맨 처음 메시지부터 확인 가능

```bash
kafka-console-consumer.sh --bootstrap-server {kafka host:port} --topic {topic name}
```

### zookeeper CLI 접속

- 주키퍼 설치 디렉토리 내부 `/bin` 폴더로 이동하여 다음 커맨드 입력

```bash
zkCli.sh start
```

### znode 생성하기

```bash
create {생성할 znode 경로}
```

```bash
create /kafka_local
```