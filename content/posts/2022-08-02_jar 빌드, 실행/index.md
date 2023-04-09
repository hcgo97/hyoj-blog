---
title: jar 빌드, 실행
slug: "/jar-빌드,-실행"
date: 2022-08-02
tags:
  - DevOps
  - Java
---

## bootJar

- Spring Boot은 Plugin을 통해 Gradle을 지원한다.

```
plugins {
	id 'org.springframework.boot' version '2.5.1'
}
```

- `bootJar`은 실행가능한 jar을 빌드하는 태스크로, 플러그인에 포함되어 있다.
- 실행가능한 jar를 만드는데 사용했던 `bootRepackage`가 Spring Boot 2.0에서 `bootJar`로 확장됐다.

## 설정

- `build.gradle`에서 `bootJar` 설정을 추가할 수 있다.
- `mainClass`을 지정해서 시작 포인트를 지정하거나, `archieveName` 등을 지정해서 jar 파일 이름을 지정할 수도 있다.

```
bootJar {
	mainClass = 'com.example.ExampleApplication'
}
```

## 빌드

프로젝트 루트 디렉토리에서 아래 명령어를 실행하면 `./build/libs` 디렉토리에 `jar` 실행파일이 생성된다.

```bash
$ ./gradlew bootJar

# clean: /build 폴더 다 지우고 빌드
$ ./gradlew clean bootJar
```

## 실행

직접 `jar` 파일이 있는 곳에서 `java -jar`으로 실행해도 되고, 루트 디렉토리에서 아래 명령어를 실행해도 된다.

```bash
$ ./gradlew bootRun

# clean: /build 폴더 다 지우고 실행
$ ./gradlew clean bootRun

# nohup: 터미널이 끊겨도 실행한 프로세스는 계속 동작하도록 하기
# & : 백그라운드에서 실행하기
$ nohup java -Dspring.profiles.active=dev -jar pupsload-0.0.1-SNAPSHOT.jar &
```
