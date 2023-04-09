---
title: mobx 로그가 proxy 로 보일 때 해결 방법
slug: "/mobx-로그가-proxy-로-보일-때-해결-방법"
date: 2021-09-29
tags:
  - Frontend
---

로그 대상 파일의 import 문에 mobx 의 toJS 를 추가하면 해결됨

```javascript
import {toJS} from 'mobx';
```
