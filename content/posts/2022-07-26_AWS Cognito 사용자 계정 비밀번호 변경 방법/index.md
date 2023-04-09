---
title: AWS Cognito 사용자 계정 비밀번호 변경 방법
slug: "/AWS-Cognito-사용자-계정-비밀번호-변경-방법"
date: 2022-07-26
tags:
  - DevOps
  - AWS
---

- Cognito 사용자 계정의 비밀번호를 변경하고 싶은 경우 아래 CLI 사용하여 변경 가능
- 계정의 상태가 ‘RESET_REQUIRED’ 일때, ‘CONFIRMED’ 로 변경하기 위해서도 해당 방법 사용

```bash
aws cognito-idp admin-set-user-password \
  --user-pool-id <user-pool-id> \
  --username <username> \
  --password <password> \
  --permanent
```

## 사용자 풀 ID 확인 방법

1. Amazone Cognito 접속
2. User Pool 선택
3. 대시보드에서 User Pool ID 확인

> 참고: [https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/admin-set-user-password.html](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/admin-set-user-password.html)
