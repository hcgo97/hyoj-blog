---
title: Linux 라이브러리 의존성 확인
slug: "/Linux-라이브러리-의존성-확인"
date: 2023-01-16
tags:
  - Ubuntu
  - Linux
  - Command
  - DevOps
---

### ldd - 라이브러리 의존성 확인

```bash
# 이 명령어로 필요한 라이브러리 확인 후 /lib 내부로 필요한 라이브러리 옮기면됨
# /lib 혹은 /usr/local/lib
ldd [옵션] 파일명
```
