---
title: 정규식 패턴 정리
slug: "/정규식-패턴-정리"
date: 2023-01-17
tags:
  - 정보
---

> 출처: https://mkil.tistory.com/205

- 정규식 테스트 사이트: https://regexr.com/

## 사용 방법

```javascript
RegExp.test(string);

// 예시
var match = /sample/.test("sample text");
console.log(match); // true or false
```

## 정규식 패턴
- `^The`
  - `The` 로 시작하는 문자열
- `of despair$`
  - `of despair` 로 끝나는 문자열
- `^abc$`
  - `abc` 로 시작하고 `abc`로 끝나는 문자열
  - `abc` 만 있는 문자열도 해당됨
- `ab*`
  - `a` 뒤에 `b` 가 0개 이상인 문자열
  - `a`, `ab`, `abb`, `abbb`, `abbbb` 등
- `ab+`
  - `a` 뒤에 `b` 가 최소 1개 이상인 문자열
  - `ab`, `abbb` 등
- `ab?`
  - `a` 뒤에 `b` 가 0개 또는 1개인 문자열
  - `a` 또는 `ab`
- `ab{2}`
  - `a` 뒤에 `b` 가 2개인 문자열
  - `abb`
- `ab{2,}`
  - `a` 뒤에 `b` 가 최소 2개 이상인 문자열
  - `abb`, `abbb` 등
- `ab{3,5}`
  - `a` 뒤에 `b` 가 3개 이상 5개 이하인 문자열
  - `abbb`, `abbbb`, `abbbbb`

## 예시 패턴
### 모든 공백 체크 정규식
```javascript
var regExp = /\s/g;
```

### 숫자만 체크 정규식
```javascript
var regExp = /^[0-9]*$/;
```

### 한글만 체크 정규식
```javascript
var regExp = /^[ㄱ-ㅎ|가-힣|a-z|A-Z|0-9|]*$/;
```

### 이메일 체크 정규식
```javascript
// 영문, 숫자, 특수문자
var regExp = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/i;
```

### 휴대폰 번호 정규식
```javascript
// 하이픈 없이
var regExp = /^\d{3}-\d{3,4}-\d{4}$/;
```

### 일반 전화번호 정규식
```javascript
// 02-123-1234, 02-1234-1234, 031-123-1234, 031-1234-1234
var regExp = /^\d{2,3}-\d{3,4}-\d{4}$/;
```

### 아이디나 비밀번호 정규식
```javascript
// 영문, 숫자 4~12자
var regExp = /^[a-zA-Z0-9]{4,12}$/;
```

### 휴대폰번호 체크 정규식
```javascript
// 010-1234-1234, 011-123-1234, 016-1234-1234, 017-123-1234, 018-1234-1234, 019-123-1234
var regExp = /^01(?:0|1|[6-9])-(?:\d{3}|\d{4})-\d{4}$/;
```

### a가 있는 문자열
```javascript
var regExp = /a/;
```

### a~z 사이의 모든 문자
```javascript
var regExp = /[a-z]/;
```

### a~z, A~Z, 0~9 사이의 모든 문자
```javascript
var regExp = /[a-zA-Z0-9]/;
```

### a~z 혹은 0~9 사이의 문자
```javascript
var regExp = /[a-z]|[0-9]/;
```

### a 혹은 b 혹은 c 인 문자
```javascript
var regExp = /[a|b|c]/;
```

### a~z 까지의 문자가 아닌 문자
```javascript
// ^ : 부정(not)
var regExp = /[^a-z]/;
```

### 문자의 처음이 a~z로 시작되는 문자
```javascript
var regExp = /^[a-z]/;
```

### 문자의 끝이 a~z로 끝나는 문자
```javascript
var regExp = /[a-z]$/;
```

### 태그(< >) 찾아 제거(태그 안 내용까지)
```javascript
var regExp = /<[^>]*>/g;
```

### 한글 제거
```javascript
var regExp = /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/g;
```

### 숫자만 통과
```javascript
var regExp = /^[0-9]*$/;
```

### 정수 및 소수점 포함 숫자들만 통과 (음수 포함)
```javascript
var regExp = /^[-+]?[0-9]*\.?[0-9]+$/;
```

### 정수 및 소수점 포함 숫자들만 통과 (음수 미포함, 소수점 2자리 까지)
```javascript
var regExp = /^[0-9]*\.?[0-9]{0,2}$/;
```

### 숫자 및 x, X, P, E 만 통과
```javascript
var regExp = /^[0-9xXpPeE]+$/;
```

### 특수문자 포함 체크
```javascript
var regExp = /[~!@#$%^&*()_+|<>?:{}]/;
```
