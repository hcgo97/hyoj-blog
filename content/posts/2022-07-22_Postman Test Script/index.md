---
title: Postman Test Script
slug: "/Postman-Test-Script"
date: 2022-07-22
tags:
  - DevOps
---

### responseBody 파라미터 equals test

```javascript
// responseBody json 파싱하기
const jsonData = pm.response.json()

// pm.test(테스트이름, 테스트코드)
pm.test("responseData is true", () => {

		// pm.expect(실제값).to.eql(기대값)
		pm.expect(jsonData.data.responseData).to.eql(true);
})

// not null check
pm.expect(jsonData.data.responseData).to.not.eql(null);
```

### status 테스트

```javascript
const status = pm.response.status // "OK"

// pm.test(테스트이름, 테스트코드)
pm.test("Status code is 200", () => {

		// pm.response.to.have.status(상태코드)
		pm.response.to.have.status(200);
})
```

### 다음으로 호출할 API 지정하기

```javascript
// postman.setNextRequest(API 이름)
// API 이름 지정할때 디렉터리 구조는 상관없음
// 만일 API 이름이 중복이라면 테스트 시 실패함

// 잘못 셋팅할경우 무한루프 걸릴수 있기 때문에 매우 조심!!!!!
postman.setNextRequest("로그 검색");
```

### 현재 API를 마지막 호출로 지정

```javascript
// API 이름 지정 시 null 로 지정하면 다음 API 호출하지 않음
postman.setNextRequest(null);
```
