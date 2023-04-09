---
title: JavaScript 변수 선언 3가지 방법
slug: "/JavaScript-변수-선언-3가지-방법"
date: 2022-07-22
tags:
  - Frontend
---

## 유효 범위 보는법

1. 개발자 도구 - Sources 탭
2. 중단점 설정
3. 로드
4. 오른쪽 하단 Scope 창에서 확인 가능

### 1. var (function scope)

```javascript
var i; // 선언, "undefined" 로 초기화됨
var sum = 0; // 선언 및 초기화

var i, sum; // 여러개 함께 선언 가능

var i=0, sum=10, message="Hello"; // 선언과 초기화 동시에 하기

name = "javascript~"; // 선언되지 않은 변수는 전역 변수가 됨
```

- 초기값은 undefined
- function scope (함수 유효범위)
    - 그 함수 전체에 걸쳐 유효함
    - 변수가 선언되기도 전에 유효하다는 뜻
- 함수 안에 있는 모든 var 변수를 함수 맨 꼭대기로 끌어올린것처럼 동작함 (hoisting 됨)

```javascript
var scope = "global";

function example() {
		console.log(scope); // "global"이 아닌 "undefiend" 로 출력됨

		var scope = "local";
		console.log(scope); // "local" 출력
}

// => 실제로 실행되는 코드
function example() {
		var scope; // 끌어올림(hoisting) 된다. (대신 정의만 끌어올려진다)
		console.log(scope); // "undefined" 출력

		scope = "local"; // 초기화는 끌어올려지지 않는다.
		console.log(scope); // "local" 출력
}
```

### 2. let (block scope)

```javascript
let i; // 선언, "undefined" 로 초기화됨
let sum = 0; // 선언 및 초기화

let i, sum; // 여러개 함께 선언 가능

let i=0, sum=10, message="Hello"; // 선언과 초기화 동시에 하기
```

- 초기값은 undefined
- block scope (블록 유효범위)
    - 선언된 블록, 구분 또는 표현식 내부에서만 유효함
    - var 와 다른점
        - var: 블록 범위를 무시하고 전역 변수나 함수 지역 변수로 선언됨
        - let: 블록 범위에서만 유효
- hoisting 되지 않는다.
    - 선언되기 전에 참조할경우 ReferenceError 발생함

### 3. const (block scope)

- 상수 - 재할당 불가, 재선언 불가
- 선언과 동시에 반드시 초기화 필요
- 범위는 let과 같음 (블록 유효범위)
- 함수 선언만 hoisting 됨, 함수 표현식은 x

```javascript
/* 함수 선언 */

foo(); // "bar"

function foo() {
		console.log('bar');
}

/* 함수 표현식 */

foo(); // TypeError: foo is not a function

var foo = function() {
		console.log('bar');
};
```
