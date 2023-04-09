---
title: 백엔드 프로세스 A to Z
slug: "/백엔드-프로세스-A-to-Z"
date: 2022-11-12
tags:
  - 정보
---

> 출처: [https://velog.io/@city7310/백엔드가-이정도는-해줘야-함-커리큘럼-털어놓기](https://velog.io/@city7310/%EB%B0%B1%EC%97%94%EB%93%9C%EA%B0%80-%EC%9D%B4%EC%A0%95%EB%8F%84%EB%8A%94-%ED%95%B4%EC%A4%98%EC%95%BC-%ED%95%A8-%EC%BB%A4%EB%A6%AC%ED%81%98%EB%9F%BC-%ED%84%B8%EC%96%B4%EB%86%93%EA%B8%B0)

### 개요

컨텐츠의 시작을 알리는 이런저런 이야기를 했다.

### 버전 관리 시스템과 버전 관리 웹호스팅 서비스 결정

버전 관리 시스템과, 이러한 버전 관리 시스템을 사용하는 프로젝트를 지원하는 웹호스팅 서비스를 의사결정했다.

### 개발 프로세스 정립

이슈 관리, 작업 진행 방식, 작업의 제품 반영 과정과 같은 것들에 대한 규칙을 정리했다.

### API 설계 원칙과 직렬화 포맷 결정

API 설계 원칙과 직렬화 포맷을 결정했다.

### 사용자 인증 방식 결정

리소스가 특정 사용자에게 귀속되는 서비스라면 꼭 필요한 사용자 인증 방식을 결정했다.

### API 스펙 설계와 문서화 방식 결정

- API 스펙 설계를 위한 가이드라인을 일러두고, 실제로 API 스펙을 설계했다.
- 프론트엔드 팀에게 전해줄 문서를 작성해야 하므로, API 문서를 어떤 식으로 작성하고 관리할지 결정했다.

### 어플리케이션 기술스택 결정과 Hello World 서버 작성

어플리케이션 레벨의 기술스택을 결정하고 Hello World 서버를 작성했다.

### 의존성 관리 도구 결정

의존성 관리 도구를 결정했다.

### Compute Engine 결정과 Hello World 서버 배포

서버를 실행할 위치인 Compute Engine을 결정하고 Hello World 서버를 배포해 봤다.

### 데이터베이스 선정과 인스턴스 시작

서비스 운영을 위한 메인 데이터베이스를 결정하고, AWS 위에 해당 데이터베이스 엔진을 사용하는 인스턴스를 띄워 봤다.

### 배포 자동화

배포 자동화에 대한 의사결정을 하고, 실제로 배포 자동화를 구성해 봤다.

### 어플리케이션 레벨 의사결정

코드를 작성하는 데에 있어서 판단의 기반이 될 의사결정을 진행했다.

### 웹 어플리케이션 개발

웹 어플리케이션 개발에 있어서 몇 가지 '일러두기' 설명을 했다.

### 웹 어플리케이션 개발 과정 회고

웹 어플리케이션 개발 과정을 회고했다.

### 테스트에 대한 이야기와 의사결정

테스트에 대해 이야기하고, 테스트 프레임워크에 관해 의사결정했다.

### 테스트에 대한 고민

테스트를 작성하며 생길 수 있는 고민들을 미리 이야기해 봤다.

### RDS 인스턴스에 새로운 Security Group을 만들어 연결하기

Security Group이라는 것을 미리 알아두기 위해, 언젠가는 마땅히 했어야 할 Security Group 관련 설정을 진행해 봤다. RDS에서 돌아가고 있는 MySQL에 아무도 접근할 수 없게 만들었다.

### Local DB에 관한 작업

- 테스트 코드는 Production DB에 영향을 주지 않아야 하므로, 테스트 코드 실행 시 항상 로컬의 MySQL을 사용하도록 한다.
- 어떻게 하면 DB Host에 관해 개발자가 실수할 일이 없는 환경을 만들 수 있을지 고민해 본다.

### 테스트가 성공했을 때만 배포하게 하기

- CI에서 배포하기 전에 테스트를 수행하도록 만들고, 테스트가 성공했을 때만 배포하게 해 본다.
- 테스트 코드가 항상 로컬의 MySQL을 사용하도록 했으니, 테스트 실행 전에 MySQL을 로컬에 띄우도록 해 본다.

### unit test에 대한 고민

- API test를 통해 간접 테스트되는 함수들을 그대로 내버려두는 게 맞는 것인지
- 정말로 mock을 사용해 unit test를 작성하는 게 국룰인지
- integration test를 중점적으로 테스트를 작성했을 때의 장단점을 살펴보며 의사결정을 하고
- state verification, behavior verification과 함께 mock, stub, fake와 같은 test double에 대해 이야기

### 테스트할 수 없는 코드는 없다

- API 서버라고 API만 테스트할 이유가 없으니, 테스트를 바라보는 여러 관점에 대해 이야기
- testability, DRY한 코드를 작성하라고 그렇게나 강요하는 이유에 대해 이야기

### CI 워크플로우 다듬기

- PR이 올라가면 테스트를 수행하게 하기
- 테스트가 성공하지 못하면 merge가 불가능하게 두기(branch protection)
- 배포할 땐 테스트하지 않게 하기 : PR용과 merge용으로 CI Job을 별도로 구성 vs buildspec에서 if문을 써서 처리하기

### 저장소 다듬기

- 테스트 커버리지 시스템 연동하기
- 코드 퀄리티파이어 추가하기
- Black 적용하기

### 저장소 다듬기 2

- fork해서 작업하는 워크플로우 구성하기
- pull request에서 리뷰어의 approve가 없으면 merge할 수 없게 하기

### 스키마에 대한 고민

- hard delete와 soft delete
- created_at과 updated_at

### 스키마 관리에 대한 고민

- Liquibase
- 스키마 변경을 어떻게 기록할 수 있을까?

### 릴리즈 준비

- 배포된 어플리케이션의 API 호출해 보기 : DB 접근 권한 문제로 에러가 날 것. WAS용 security group을 생성하고 해당 security group을 DB inbound로 허용한 후, zappa_settings.json에 security group에 관련된 내용을 설정
- zappa certify로 도메인을 달기
- DDL에 관한 이야기 : SQLAlchemy에서 제공하는 테이블 생성 메소드를 사용할지, 별도의 DDL을 export해서 사용할지 등에 대해 의사결정

### 예민한 데이터를 Amazon SSM으로 관리하기

Amazon SSM의 Secrets Manager로 예민한 데이터를 관리하기 시작한다.

### 위험한 쿼리가 허용되지 않은 유저 만들기

개발자들이 개발 용도로 사용하는 유저는 DROP Table같은 위험한 쿼리를 하지 못하게 해야 한다. 권한이 잘 설정된 유저를 만들어 본다.

### 개발용 서버를 따로 두기

막 붙이면서 테스트할 수 있는 환경이 필요하다.

### CORS 적용하기

CORS를 적용한다.

### 프론트엔드 배포 돕기

- S3 upload, 이에 관한 CI 세팅
- cloudfront 세팅
- S3 bucket에 직접 접근하는 것에 대한 restricting

### 저장소 다듬기 3

- README.md에 빌드 상태, 테스트 커버리지, 코드 퀄리티, black에 대한 badge 달기
- Issue Template, Pull Request Template 추가하기
- CONTRIBUTING.md 추가하기

### 파일 업로드 다듬기

- 스토리지 서비스와 CDN을 사용하기

### IAM Role 잘 다루기

- Zappa가 자동으로 생성한 role 말고, 별도로 role을 생성해 달아주기

### Lambda 배포 시 생기는 다운타임 문제 해결하기

Lambda에 새로운 버전의 함수가 배포되면 cold start에 의해 다운타임이 생기곤 한다. alias를 이용해 이러한 문제를 해결하는 방법을 이야기한다.

### DB에 read 전용 replica 두기

master/slave나 primary/secondary같은 분류의 범주에 들어가는, read replication을 해 본다.

### DB Access하는 로직을 별도로 분리하기

WET한 코드를 줄이기 위해 로직을 분리하기 시작한다.

### Repository Pattern과 DI를 적용하기

분리한 비즈니스 로직을 repository화 하고, Dependency Injection 구조를 사용해 비즈니스 로직을 테스트하기 좋게 만든다. DAO, DTO, DO, marshal과 같은 개념을 살펴본다.

### JWT 로직을 개선하기

identity는 어떻게 생성해줘야 할 지, blacklisting은 어떻게 해야 할 지, refresh 정책은 어떻게 두어야 할 지 등을 결정한다.

### 로그 시스템과 사투하기

- New Relic같은 별도의 SaaS APM을 쓸 지, 로그를 CloudWatch에 남겨서 ElasticSearch로 넘길지, Elastic APM을 써볼지 등등에 대해 의사결정한다.
- CloudWatch도 써 보고, Elastic APM도 써 보고, New Relic도 써 보고, ELK Stack도 써 보고, TICK Stack도 써 본다.
- 이것저것 써보는 동안 Grafana같은 걸로 로그 시각화도 한 번씩 해 본다.
- StatsD같은 로그 집계 프록시를 로그 파이프라인 사이에 끼워넣어 본다.
- 결론적으로 우리에게 가장 쓸만한 솔루션은 무엇일지 검토한다.

### API Scenario Test를 작성하자

- Runscope를 통해 API 사용 시나리오를 작성하고, 일정 시간마다 실행되게 만들어 본다.

### Alert 연동하기

- alert를 잘 도와주는 툴을 찾아 scenario test가 실패했을 때 나한테 전화가 오게 만들어 본다.

### Alert의 범위를 넓히기

- 그동안 구성해 뒀던 로그 시스템들에 alert policy들을 만들어 본다.
- 이것도 슬랙이나 전화 등의 창구로 alert을 받아볼 수 있게 해 본다.

### Queue와 Worker

이메일 전송과 같은 것들을 위해 worker를 만들어서 HTTP blocking으로 생기는 레이턴시를 줄여 본다.

### 시스템을 정리해 보기

front-end tier, back-end tier, data tier, monitoring tier로 나누어 시스템의 현재 상태를 정리해 본다.

### ECS로 인프라 이동하기

- 지금 API 서버가 Lambda로 만족스럽게 운영할 수 있는 상태인지 검토한다.
- 그렇지 않다고 가정하고, ECS를 위해 Docker와 친해져 본다.
- ECS로 인프라를 이동해 본다.

### space-time tradeoff

in-memory caching을 이용해 API의 속도를 높여 본다.

### 테스트를 Docker Container에서 실행하기

MySQL과 같은 테스트를 위한 인프라도, 어플리케이션도 dockerize해서 잘 정의된 테스트 코드 실행 환경을 만들어 본다.

### Terraform 시작하기

Terraform으로 IaC를 시작해 본다.

### GitOps 시작하기

GitOps를 시작해 본다.
