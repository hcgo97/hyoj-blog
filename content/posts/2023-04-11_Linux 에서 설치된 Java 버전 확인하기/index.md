---
title: Linux 에서 설치된 Java 버전 확인하기
slug: "/Linux-에서-설치된-Java-버전-확인하기"
date: 2023-04-11
tags:
  - DevOps
  - Linux
  - Command
  - Java
---

```bash
$ /usr/libexec/java_home -V

# 결과
Matching Java Virtual Machines (3):
    17.0.6 (arm64) "Azul Systems, Inc." - "Zulu 17.40.19" /Library/Java/JavaVirtualMachines/zulu-17.jdk/Contents/Home
    17.0.6 (arm64) "Homebrew" - "OpenJDK 17.0.6" /opt/homebrew/Cellar/openjdk@17/17.0.6/libexec/openjdk.jdk/Contents/Home
    11.0.16.1 (arm64) "Azul Systems, Inc." - "Zulu 11.58.23" /Library/Java/JavaVirtualMachines/zulu-11.jdk/Contents/Home
/Library/Java/JavaVirtualMachines/zulu-17.jdk/Contents/Home
```
