---
title: MySQL 사용자 생성,수정,삭제
slug: "/MySQL-사용자-생성,수정,삭제"
date: 2022-12-14
tags:
  - Database
  - MySQL
---

```sql
use mysql;

# 유저 생성
select * from user;
create user 'user'@'%' identified by 'root1234';
create user 'readonly_user'@'%' identified by 'root1234';

# 권한 설정 (DB명.* to '유저명'@'%')
show grants for 'user'@'%';
show grants for 'readonly_user'@'%';
grant all privileges on mydb.* to 'user'@'%'; # 모든 권한 (grant all)
grant select on mydb.* to 'readonly_user'@'%'; # 읽기전용 유저 (grant select)
flush privileges;

# 권한 삭제
revoke all on mydb.* from 'user'@'%';

# 유저 삭제
drop user 'user'@'%';

# 접속 허용 host 확인
select host, user, authentication_string from user;

# 패스워드 변경
alter user 'user'@'%' identified with mysql_native_password by '12345678';

# 유저 rename
rename user 'user'@'%' to 'admin_user'@'%';
```
