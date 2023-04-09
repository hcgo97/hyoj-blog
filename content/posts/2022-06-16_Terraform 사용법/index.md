---
title: Terraform 사용법
slug: "/Terraform-사용법"
date: 2022-06-16
tags:
  - DevOps
---

## 로그인

1. terraform login
2. token 받아서 붙여넣기
3. terraform plan 명령어로 terraform 이 동작되는지 확인
    1. plan 동작 오류나면 .lock 파일이 없기 때문
        1. .lock 파일이 없을때는 terraform init 명령어로 클라우드와 동기화 시켜야함
        2. provider 버전이 달라졌을 수 있기 때문에 .lock파일은 새로만들어질때마다 해시가 변경 됨

## import 방법

### import 해야하는 경우

- aws 에는 있는 resource 가 테라폼 코드로는 없을 때
- aws 에 있는 resource 를 테라폼 코드로도 가져와서 동기화할 때 사용
- 테라폼 코드로 새로운 resource 를 만드는 경우에는 import 하면 안됨

### 특정 resource import 명령어 찾기

1. terraform registry 접속 ([https://registry.terraform.io](https://registry.terraform.io/)/)
2. browse all 선택
3. 설정 찾는 클라우드 선택
4. documentation 선택
5. 찾는 resource 검색
6. 해당 resource 페이지 가장 밑에 import 명령어가 있는데, 이걸 터미널에 복사/붙여넣기

### import 순서

1. 테라폼 레지스트리에서 import 할 리소스 검색해서 import 명령어 가져옴
2. import할 resource 작성 - 테라폼 레지스트리의 example을 보면됨
3. import 명령어에 resource 정보 삽입

### 기존 설정을 최대한 유지하면서 import 하고 싶을때

1. 기존 설정된 리소스 중 하나를 잠깐 삭제한 후 terraform plan 명령어 실행
2. 그러면 기존 설정을 삭제한다고 나오는데 그 부분을 복사
3. 복사한 부분을 IDE 에 붙여넣은 후 필요없는 부분 삭제
    1. 마이너스(-)
    2. 화살표 null(→ null)

### import 한 resource 를 삭제하고 싶을 때

```bash
# terraform state rm 리소스.리소스 이름
terraform state rm aws_s3_bucket.example_bucket
```

### import 말고 data 쓰는 경우

- data 를 쓰면 arn 을 string으로 바로 가져올수있기 때문에
- 거의 안바뀌는 값들 (subnet , security group …)

## 적용할 때

1. terraform plan 으로 변경점 확인
2. terraform apply → 하고 **yes** 명령어까지 쳐야 적용됨 **(yes 치기 전에 조심 또 조심!!!!)**
3. resource(특히 로드밸런서) 삭제 시 해당 resource에 연결되어 있는 resource 들을 먼저 연결해제 해야함

### 리소스 껍데기만 만들고 import → plan 햇는데 replace 라고 뜰때

1. 기존 설정된걸 덮어씌운다는 말이기 때문에 적용하면 큰일남
2. 만들었던 리소스 껍데기를 지우고 다시 plan
3. 그러면 삭제된다고 뜨는데 그걸 복사해서 필요없는 부분(마이너스(-), → null) 삭제하면됨

## Azure 참고

### 애저의 경우 구독 키(subscript key) 가 다르면 환경을 인식못함

- 구독 키 하나당 하나의 환경으로 인식을 함
- 그러므로 구독 키 별로 폴더를 따로 만들어서 관리

### 애저 구독키 변경

```bash
az account set --subscription "subscription_name"
```

### 애저 database 생성 시 주의할 점

create_mode = DEFAULT 가 기본값인데, 이렇게 되면 관리자 계정이랑 암호를 무조건 설정해줘야함
