---
title: k6 활용한 부하 테스트
slug: "/k6-활용한-부하-테스트"
date: 2023-04-04
tags:
  - DevOps
---

### 스크립트 작성

```javascript
// script.js
import http from 'k6/http';
import { sleep } from 'k6';

export default function () {
	// 1. https://test.k6.io enpoint 로 GET 요청 보냄
  http.get('https://test.k6.io');

	// 2. 1초 동안 대기
  sleep(1);
}

// 테스트 도중 VU 증가/감소 시키기
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '30s', target: 20 }, // 30초 동안 20명으로 테스트
    { duration: '1m30s', target: 10 }, // 1분 30초 동안 10명으로 테스트
    { duration: '20s', target: 0 }, // 20초 동안 0명으로 테스트
  ],
};

export default function () {
	// 1. https://httpbin.test.k6.io enpoint 로 GET 요청 보냄
  const res = http.get('https://httpbin.test.k6.io');

	// 2. 응답 status code 가 200 인지 확인
  check(res, { 'status was 200': (r) => r.status == 200 });

	// 3. 1초 동안 대기
  sleep(1);
}
```

### 실행

```shell
# 1명, 1번 실행
k6 run script.js

# 10명, 30초 동안 실행
# --vus: virtual users(가상 사용자 수)
# --duration: 실행할 시간
k6 run --vus 10 --duration 30s script.js
```
