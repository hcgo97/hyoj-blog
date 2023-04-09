---
title: react + redux + saga 로 구성된 Frontend
slug: "/react-redux-saga-로-구성된-Frontend"
date: 2021-09-16
tags:
  - Frontend
---

## 개발 순서

1. **package.json:** 환경별 run 스크립트 작성
2. **env-config:** 환경별 API 엔드포인트 설정
3. **DataSource**: API URI 정의
4. **Route**: path, 연결될 컴포넌트 설정
5. **서브 컴포넌트**: 페이지에 필요한 부수적인 컴포넌트들을 추가 (헬프메시지, 목록박스 등등)
6. **컨테이너 요소 작성**
    1. **constants.js**
    2. **actions.js**
    3. **reducer.js**
    4. **selector.js**
    5. **services.js**
    6. **saga.js**
    7. **Loadable.js**
    8. **index.js**
7. **메인 컴포넌트**: 컨테이너 내부 index.js와 연결될 메인 컴포넌트 작성

### DataSource.js

- API URI 정의

### Route

- Web path 설정
- 어떤 컴포넌트에 연결될 것 인지
- 어떤 컴포넌트(layout)에 연결될 것 인지
    - 실질적으로는 컨테이너의 loadable이랑 연결됨
    - loadable이랑 연결되면 해당 컨테이너 내부의 index.js 로 연결되는데, index.js 는 페이지를 어떻게 표시할 것인지 정의되어있음
    - 이 index.js 는 컨테이너와 연결됨

## 컨테이너 패키지 요소

- constants + actions + reducer 한 묶음 → 상태 변화가 일어나는 변수를 정의하는 요소
- saga + selector + services 한 묶음 → 실질적으로 상태변화를 시키는 요소
- loadable + index 한 묶음 → 페이지를 어떻게 보여줄 것인지 정의

### constants.js

- 상태가 변경되는 모든 케이스들을 상수로 정의해놓은것 (변수 말고 케이스만)
- 밑의 url 같은거는 상수가 어떤 컴포넌트에서 쓰이는지 구분짓기 위한것임

### actions.js

- 상태 변화 함수 정의
- constants에서 정의한 케이스에 대해 어떤 매개변수를 사용해서 변화시킬건지 작성 (매개변수는 없어도됨)

### reducer.js

- 초기 상태변수(initialState)를 정의하고, 이 초기상태들이 contants의 케이스들을 만나면 어떻게 변화할 것인지 정의함
- 첫번째 매개변수(state)는 바꾸고싶은 객체, 두번째 매개변수(draft)는 바뀔 상태 값(상태를 변경하는 로직) 작성
- 작성후에 프로젝트 최상단 reducers.js 에서 key: reducer 형식으로 정의해야함

### selector.js

- reducer와 연결하여 상태변화할때 직접적으로 사용할 함수를 정의
- reducer key로 연결

### services.js

- API 와 어떻게 연결할지에 대한 비즈니스 로직 정의
- Alert, 예외처리시 메시지도 여기서 정의

### saga.js

- 연결된 API를 호출했을때 어떻게 동작할지 정의
- token 검증도 여기서함(API를 호출했을때의 동작이므로)
- services에서 정의해놓은 함수대로 동작함

### Loadable.js

- Route와 index.js를 서로 연결해줌

### index.js

- 메인 컴포넌트가 어떻게 보여질것인지 정의함
- **useInjectReducer, useInjectSaga**
    - key값으로, 어떤 reducer, saga 와 연결할지 설정
- index.js **메인함수에서 사용하는 변수들의 propType 설정**
- **mapStateToProps**
    - 변수의 상태변화에 필요한 selector 지정
- **mapDispatchToProps**
    - actions, reducer에서 지정한 함수대로 매개변수에 의해 어떤 케이스의 상태로 변화될건지 작성
- **export default compose(withConnect, memo)(LogList)**
    - **compose(withConnect, memo)**
        - 요소들을 합성하는 함수
        - compose로 withConnect랑 memo를 감싸서 memo 함수가 동작하도록 함
            - **memo**: withConnect의 요소들에서 바뀐게있는지 비교함, withConnect(props)의 상태가 바뀌지 않았다면 리렌더링 안하도록 하는 함수
    - export 되는 요소는 컴포넌트 내부 함수구조와 같음
