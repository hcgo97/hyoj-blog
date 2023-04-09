---
title: newman cli
slug: "/newman-cli"
date: 2022-07-22
tags:
  - DevOps
  - Command
---

### 포스트맨 컬렉션 테스트 실행

```bash
# -e: 환경변수 설정, --environment
newman run postman_collection.json -e postman_environment.json
```

### 테스트 실행 & 결과를 html 파일로 저장

```bash
# -r: --reporter
newman run postman_collection.json -e postman_environment.json -r htmlextra
```

### 결과 html 을 특정 디렉토리로 내보내기

```bash
# 폴더없어도 자동으로 만들어짐
newman run postman_collection.json -e postman_environment.json -r htmlextra --reporter-htmlextra-export ./newdir/new_report.html
```
