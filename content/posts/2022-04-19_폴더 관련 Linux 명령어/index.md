---
title: 폴더 관련 Linux 명령어
slug: "/폴더-관련-Linux-명령어"
date: 2022-04-19
tags:
  - Linux
  - Command
  - DevOps
---

### **압축하고 비번걸기**

```bash
zip -er {압축파일경로/압축파일.zip} {압축할파일}
```

### **gz 압축 풀기**

```bash
gzip -d {압축 파일명}.gz

# gzip 설치
apt-get install gzip
```

### **검색한 라인 밑에 입력한 라인 수 만큼 더 출력함**

```bash
A {출력할 라인 수}
```

### **파일 시스템의 사용 가능 공간 표시**

```bash
# h: 메가바이트(M) 단위로 출력
# .(점) : 현재 디렉토리가 소속된 파일시스템만 출력
df -h .
```

### **폴더별 용량확인**

```bash
# d 1: 디렉토리 depth 1 까지만 출력
# h: 메가바이트(M) 단위로 출력 (human read)
du -d 1 -h
```

### 1. 로컬에서 원격으로 (Local→Remote)

```bash
scp [전송할 파일 경로] [유저명]@[IP주소]:[받을 경로]

# ex) 로컬의 /home/example.txt 파일을 원격지의 /home/test 디렉토리로 전송
scp /home/example.txt dhj@141.211.xx.xxx:/home/test
```

### 2. 원격에서 로컬로 (Remote→Local)

```bash
scp [유저명]@[IP주소]:[전송할 파일 경로] [받을 경로]

# ex) 원격지의 /home/test.txt 파일을 로컬의 /home/example 디렉토리로 전송
scp dhj@141.211.xx.xxx:/home/test.txt /home/example
```

### 3. 원격에서 원격으로 (Remote→Remote)

```bash
scp [유저명]@[IP주소]:[전송할 파일 경로] [유저명]@[IP주소]:[받을 경로]

# ex) A 원격지의 /home/test.txt 파일을 B 원격지의 /home/example 디렉토리로 전송
scp dhj@141.211.xx.xxx:/home/test.txt gildong@141.223.xx.xxx:/home/example
```

---

### 옵션 (options)

```bash
# r: 폴더를 복사할 때 사용(전송 대상을 폴더로 지정). 모든 폴더들을 재귀적으로 복사함.
# P: ssh 포트 지정
# i: identity file을 지정해서 사용(identity file 경로를 지정)
scp -i ~/.ssh/dhj-server-private ~/example.txt dhj@141.223.xx.xxx:/home/test
```

```bash
# v: 상세내용을 보면서 디버깅 할 때 사용(verbose 모드)
# p: 전송 시 파일 수정 시간과 권한을 유지
scp -P 22 dhj@141.223.xx.xxx:/home/dhj/example.txt /home/test
```

---

## 복수의 파일 전송

### 1. 로컬에서 원격으로 (Local→Remote)

```bash
scp [옵션] [파일명1] [파일명2] [유저명]@[IP주소]:[받을 경로]
```

### 2. 원격에서 로컬로 (Remote→Local)

```bash
# 1번의 경우와 다르게 원격지에서 보낼 파일들의 경로를 " "을 이용해 묶어준다.
scp [옵션] [유저명]@[IP주소]:"[파일명1] [파일명2]" [받을 경로]
```

### 3. 원격에서 원격으로 (Remote→Remote)

```bash
# 마찬가지로 원격지에서 보낼 파일들의 경로를 " "을 이용해 묶어준다.
scp [옵션] [유저명]@[IP주소]:"[파일명1] [파일명2]" [유저명]@[IP주소]:[받을 경로]
```
