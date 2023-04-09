---
title: Linux 유저, 유저 그룹 관련 명령어
slug: "/Linux-유저,-유저-그룹-관련-명령어"
date: 2023-02-23
tags:
  - Linux
  - Command
  - DevOps
---

# 사용자 관련

## 사용자 조회

- 모든 사용자 출력

```bash
# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
...
```

- root과 useradd 또는 adduser를 통해 생성한 사용자 계정 출력

```bash
# grep /bin/bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
jb:x:1000:1000:JB:/home/jb:/bin/bash
```

## 사용자 추가

### useradd

- jb 사용자 추가

```bash
useradd jb
```

- 사용자 홈 디렉토리도 같이 생성하고 싶다면 -d 옵션 사용

```bash
useradd jb -d /home/jbdir
```

- jb 사용자의 비밀번호 생성

```bash
passwd jb
```

### adduser

- adduser 명령어로 사용자를 추가 가능
- useradd와는 달리 사용자 홈 디렉토리를 자동으로 만들고, 비밀번호 설정 등도 한 번에 가능

## 사용자 수정

- jb 사용자의 uid를 1001로 변경

```bash
usermod -u 1001 jb
```

- jb 사용자의 홈 디렉토리를 /home/jb-home으로 변경
- /home/jb-home는 수동으로 생성해야 함

```bash
usermod -d /home/jb-home jb
```

- /home/jb-home을 생성하고, jb 사용자의 홈 디렉토리를 /home/jb-home으로 변경하고, 파일 등을 이동

```bash
usermod -m -d /home/jb-home jb
```

## 사용자 삭제

- jb 사용자를 삭제

```bash
userdel jb
```

- jb 사용자를 강제로 삭제

```bash
userdel -f jb
userdel --force jb
```

- jb 사용자와 함께 사용자 디렉토리, 사용자 메일함도 삭제

```bash
userdel -r jb
userdel --remove jb
```

## 기타

- jb 사용자가 속한 모든 그룹 출력

```bash
groups jb
```

# group

### 그룹 조회

- 그룹 목록은 /et/group 파일에 존재

```bash
cat /etc/group
```

- *`X:Y:Z`* 형식으로 출력됨
    - X - 그룹 이름
    - Y - 그룹 비밀번호
    - Z - 그룹 ID

## 그룹 추가

- groupadd 명령으로 그룹을 추가

```bash
[root@localhost ~]# groupadd group-1
[root@localhost ~]# tail -n 5 /etc/group
slocate:x:21:
rngd:x:974:
tcpdump:x:72:
vboxsf:x:973:
group-1:x:1000:
```

## 그룹 삭제

- groupdel 명령으로 그룹을 삭제

```bash
[root@localhost ~]# groupdel group-1
[root@localhost ~]# tail -n 5 /etc/group
avahi:x:70:
slocate:x:21:
rngd:x:974:
tcpdump:x:72:
vboxsf:x:973:
```

## 그룹 수정

### 그룹에 사용자 추가

- user-1을 group-1에 추가

```bash
[root@localhost ~]# gpasswd -a user-1 group-1
Adding user user-1 to group group-1
```

- user-1이 속한 그룹은 groups 명령으로 확인

```bash
[root@localhost ~]# groups user-1
user-1 : user-1 group-1
```

### 그룹에서 사용자 제거

- user-1을 group-1에서 제거

```bash
[root@localhost ~]# gpasswd -d user-1 group-1
Removing user user-1 from group group-1
[root@localhost ~]# groups user-1
user-1 : user-1
```

### 그룹 이름 변경

- group-1을 group-2로 변경

```bash
groupmod -n group-2 group-1
```
