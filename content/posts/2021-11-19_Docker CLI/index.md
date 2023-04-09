---
title: Docker CLI
slug: "/Docker-CLI"
date: 2021-11-19
tags:
  - Command
  - DevOps
---

### 이미지파일 빌드
- 이미지 빌드할때 소스파일과 Dockerfile 은 같은 폴더에 있어야함

```bash
# -t : tag 사용
docker image build -t image_name:tag
```

### 이미지파일 리모트 푸쉬용으로 빌드

```bash
docker image build -t remote_id/image_name:tag
```

### 도커 리모트 이미지 파일 검색

```bash
docker search 옵션 검색어
```

### 이미지 다운로드

```bash
docker pull 옵션 image_name:tag
```

### 컨테이너 실행

```bash
# 포트포워딩: 9000포트를 열고 9000요청으로 들어오면 8080으로 보낸다 (컨테이너 외부:컨테이너 내부)
# -d: 백그라운드 모드
# -e: 컨테이너 내부에서 사용할 환경변수 설정
# --name: 컨테이너 이름
# -v: volumnes 설정 (마운트 호스트DIR:컨테이너DIR)
docker container run -t -p 9000:8080 이미지이름:태그
```

### docker-compose.yml 로 실행하기

```bash
# -f: compose 파일 지정
# -t: 멀티컨테이너 이름 지정
docker -f docker-compose.yml -t 멀티컨테이너이름 up
```

### docker compose up / down / run 차이점

- down → 컨테이너 아예 삭제, db, redis, api 다 삭제함
- run → up(컨테이너 띄우기)한 다음에 실행함
- IDE 우측상단 중지버튼 → api만 중지, 나머지 db, redis 다 켜져있음

### 실행되고 있는 컨테이너 내부에 접속하기

```bash
# -it: interactive terminal 모드
docker exec -it local-mysql bash
```

### docker 로 띄운 mysql 에 접속하기

```bash
mysql -u root -p -h 127.0.0.1
```

### 연관 관계 아예 없는 사용하지 않는 이미지 삭제

```bash
docker image rm $(docker image ls -a --filter "dangling=true" -q)
docker compose -f docker-compose.local.yml exec redis /bin/sh
```

### status = exited 인 컨테이너만 삭제

```bash
docker container rm $(docker container ls -a --filter "status=exited" -q)
```

### 현재 실행중인 컨테이너 옵션 확인

```bash
runlike -p 컨테이너 명
runlike -p local-mysql
```

### 도커 컨테이너 → 로컬로 파일 복사

```bash
# tmp_container 컨테이너 내부의 /root/data/test.md 파일을 로컬의 ~/data 로 복사하기
docker cp tmp_container:/root/data/test.md ~/data/
```

### 로컬 → 도커 컨테이너로 파일 복사

```bash
# 로컬의 ~/data/test.md 파일을 tmp_container 컨테이너 내부의 /root/data/ 로 복사하기
docker cp ~/data/test.md tmp_container:/root/data/
```
