---
title: Ubuntu 방화벽(UFW) 설정
slug: "/Ubuntu-방화벽(UFW)-설정"
date: 2023-03-24
tags:
  - Linux
  - Ubuntu
  - Command
  - DevOps
---

### UFW 활성화/비활성화

UFW는 기본 비활성화 상태이기에 이를 활성화 한다.

```bash
sudo ufw enable
```

### UFW 비활성화

```bash
sudo ufw disable
```

### UFW 상태 확인

```bash
sudo ufw status verbose
```

## UFW 기본 룰

- UFW에 설정되어 있는 기본 룰은 아래와 같다.
    - 들어오는 패킷에 대해서는 전부 거부(deny)
    - 나가는 패킷에 대해서는 전부 허가(allow)

### 기본 룰 확인

```bash
sudo ufw show raw
```

### 기본 정책 차단

```bash
sudo ufw default deny
```

### 기본 정책 허용

```bash
sudo ufw default allow
```

## UFW 허용과 차단

### UFW 허용

```bash
sudo ufw allow <port>/<optional: protocal>
```

### 예) SSH 포트 22번 허용(tcp/udp 22번 포트를 모두 허용)

```bash
sudo ufw allow 22
```

### tcp 22번 포트만을 허용 - SSH는 tcp 22번 포트만 허용하는게 정답

```bash
sudo ufw allow 22/tcp
```

### udp 22번 포트만을 허용

```bash
sudo ufw allow 22/udp
```

## UFW 거부

## 예) ssh 포트 22번 거부(tcp/udp 22번 포트를 모두 거부)

```bash
sudo ufw deny 22
```

### tcp 22번 포트만을 거부

```bash
sudo ufw deny 22/tcp
```

### udp 22번 포트만을 거부

```bash
sudo ufw deny 22/udp
```

## UFW 룰의 삭제

### ufw deny 22/tcp 설정이 되어있다고 가정

```bash
sudo ufw delete deny 22/tcp
```

## service 명을 이용한 설정

- /etc/services에 지정되어 있는 서비스명과 포트를 이용해 UFW를 설정할 수 있다.

### 서비스명 보기

```bash
less /etc/services
```

### 서비스명으로 허용

```bash
sudo ufw allow <service name>
```

### 예) SSH 서비스

```bash
sudo ufw allow ssh
sudo ufw deny ssh
```

### UFW 로그 기록

```bash
sudo ufw logging on
sudo ufw logging off
```

## Advanced Syntax

문법을 확장하여 목적지 주소와 포트, 프로토콜등을 지정할 수 있다.

## 특정한 IP 주소 허가/거부

### 특정한 IP주소 허용

```bash
sudo ufw allow from <ip address>
```

### 예) 192.168.0.100 주소 허용(IP 주소192.168.0.100 에서만 접속이 가능해진다)

```bash
sudo ufw allow from 192.168.0.100
```

### 네트워크 단위로 지정하여 같은 네트워크 상에 있는 컴퓨터들은 접속가능해진다.

```bash
sudo ufw allow from 192.168.0.0/24

```

### 특정 IP 주소와 일치하는 포트 허용

```bash
sudo ufw allow from <ip address> to <protocol> port <port number>
```

### 예) 192.168.0.100 주소와 포트, 프로토콜 허용

```
sudo ufw allow from 192.168.0.100 to any port 22
```

## 특정 IP 주소와 프로토콜, 포트 허용

```bash
sudo ufw allow from <ip address> to <protocol> port <port number> proto <protocol name>
```

### 예) 192.168.0.100 주소와 tcp 프로토콜 22번 포트 허용

```bash
sudo ufw allow from 192.168.0.100 to any port 22 proto tcp
```

- 위의 예제들에서 allow 대신 deny를 입력하면 거부가 된다.

## ping (icmp) 허용/거부

- UFW 기본설정은 ping 요청을 허용하도록 되어있다.

```bash
sudo vi /etc/ufw/before.rules

   # ok icmp codes
  -A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
  -A ufw-before-input -p icmp --icmp-type source-quench -j ACCEPT
  -A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
  -A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
  -A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT
```

- 위 코드들의 ACCEPT 부분을 모두 DROP으로 변경하거나 삭제하면 ping 요청을 거부하게 된다.

## ufw numbered rules

- UFW 룰들에 숫자를 붙여서 볼 수 있다. 이를 이용해 룰에 수정이나 삭제, 추가를 할 수 있다.

### ufw number 보기

```bash
sudo ufw status numbered
```

### ufw numbered 수정

```bash
sudo ufw delete 1
sudo ufw insert 1 allow from 192.168.0.100
```

## 추천 방화벽 정책

```bash
sudo ufw enable
sudo ufw allow from 192.168.0.3 to any port 22 proto tcp
sudo ufw allow 123/udp
sudo ufw allow 80/tcp
sudo ufw allow 3306/tcp
sudo ufw status
```
