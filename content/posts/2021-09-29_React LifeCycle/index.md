---
title: React LifeCycle
slug: "/React-LifeCycle"
date: 2021-09-29
tags:
  - Frontend
---

### constructor

- 초기설정 (컴포넌트가 새로 만들어질때마다 이 함수가 호출됨)

### componentDidMount

- 컴포넌트가 화면에 나타날때 호출됨

### componentDidUpdate

- render() 호출 후 호출됨, 파라미터로 prevProps prevState 조회 가능

### componentWillUnmount

- 등록했던 이벤트 제거, setTimeount 제거
