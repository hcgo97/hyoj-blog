---
title: API 설계 잘하는 법
slug: "/API-설계-잘하는-법"
date: 2021-06-18
tags:
  - 정보
---

- status code, method, header(userAgent, Authorization, Encoding(MIME)
- 멱등(Idenpotent) 뭔지 정의하기
- URI 리소스를 식별하는 지정자 (쿼리파라미터 뺀거)
- URL - 쿼리파라미터 포함하면 URL

### endpoint

- scheme(http://, https://) + host + port 합친주소

### prefix

- / \{버전이름\} / api /
- prefix 뒤의 URI에는 리소스(엔티티)만 들어와야함. (로그인같은 예외경우 제외)

### PathVariable 에서 엔티티를 식별할 때는 id(PK) 가 아닌 uuid 를 사용한다

- 개인정보 관련 같이 중요한 테이블에서 auto increment 로 만들어진 id 탈취되면 위험할 수도 있음
- uuid 를 사용하여 엔티티를 식별하도록 하는 것이 Best

### Resource

사람

- 유저

동물

- 펫

### table

- user
- pet

### class

User

- 변수명 users
    - (List\<User\> 타입이라서 리스트인걸 명확히 알 수 이ㅆ록)

Pet

- 변수명 pets

### API

- \<prefix\> / users /
- \<prefix\> / pets /

### 액션 - 메소드

- 조회(검색) - GET
    - \<prefix\> / users
- 이름에 k 들어가는사람 검색 - GET
    - \<prefix\> / users ? name=k
- 한명만 검색 - GET
    - \<prefix\> / users / \<uid\>
- 유저 추가 - POST
    - \<prefix\> /users
- 하나만 유저 수정 - PUT
    - \<prefix\> / users / \<uid\>
- 여러 유저 수정 - PUT
    - \<prefix\> / users
- 삭제 - DELETE
    - \<prefix\> / users / \<uid\>

### stauts code

- URI가 없거나, API가 없거나
    - 404
- 검색하고자하는 유저 데이터가 없을때
    - 200 을 주되, 유저정보가 없다는 메시지 출력
- 유저가 파라미터빠트렸을때
    - 400
- 서버 DB 나 등등 서버에서 오류났을때
    - 500
- 로드밸런서나 엔진엑스에서 에러가 났을때 (게이트웨이에서 에러가남)
    - 502 (Bad Gateway)

### basic auth

- 로그인같은 인증을 서버가 아닌 웹에서 처리하도록 한 인증방법
- Basic id:pass 형태
    - id:pass 는 base64 형태라서 걍 다 노출됨
