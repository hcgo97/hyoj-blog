---
title: HTTP Status Code 처리
slug: "/HTTP-Status-Code-처리"
date: 2021-05-13
tags:
  - 정보
---

### 400 Bad Request

- 클라이언트가 유효하지 않은 요청을 보낸 경우 (request body나 파라미터를 빼먹은 경우같이)

### 401 Unauthorized

- 해당 서버에 클라이언트 인증이 실패한 경우

### 403 Forbidden

- 클라이언트가 인증은 됐지만 요청한 자원에 대한 권한은 없는 경우 (예를 들어 로그인된 사용자가 관리자 페이지에 접근하는 경우)

### 404 Not Found

- 요청한 자원이 존재하지 않는 경우

### 412 Precondition Failed

- Request Header 필드 중 한 개 이상의 값이 잘못 된 경우

### 500 Internal Server Error

- 서버에서 발생된 일반적인 에러

### 503 Service Unavailable

- 요청된 서비스가 이용가능하지 않는 경우
