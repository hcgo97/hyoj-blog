---
title: CIDR 계산법
slug: "/CIDR-계산법"
date: 2021-09-14
tags:
  - DevOps
---

### /32

- 해당 아이피만 허용 (255.255.255.255)

### /16

- 172.31.**0.0** ~ 172.31.**255.255**
- **255*255개**
- **아이피 2번째까지 바뀌어도 됨** (255.255.0.0)

### /24

- 172.31.0**.0** ~ 172.31.0**.255**
- **255개만**
- **아이피 3번째까지 바뀌어도 됨** (255.255.255.0)

### /48

- ipv6

> 참고 사이트
> 
> [https://account.arin.net/public/cidrCalculator](https://account.arin.net/public/cidrCalculator)
> 
> [https://ko.wikipedia.org/wiki/사이더_(네트워킹)](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%EB%8D%94_(%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%82%B9))

