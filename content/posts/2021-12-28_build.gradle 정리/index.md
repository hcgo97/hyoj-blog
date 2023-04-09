---
title: build.gradle 정리
slug: "/build.gradle-정리"
date: 2021-12-28
tags:
  - Spring Boot
---

```groovy
// 빌드시 필요한 모든 과정을 플러그인 내부 task가 진행해준다.
plugins {
    id 'org.springframework.boot' version '2.2.0.RELEASE'
    id 'io.spring.dependency-management' version '1.0.8.RELEASE'
    id 'java'
//    id 'groovy'
}

group = 'io.lpin'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

configurations {
    compileOnly {
        extendsFrom annotationProcessor
    }
}

/**
 * 저장소 정보를 관리하는 프로퍼티
 * 해당 저장소에 지정된 라이브러리를 gradle 이 참조하여 가져올수있다.
 */
repositories {
    mavenCentral()
}

// ext는 gradle의 모든 task에서 사용할 수 있음
// 일종의 전역변수를 선언하는 블록
//ext['groovy.version'] = '2.4.9'

/**
 * 의존성에 관한 설정을 관리하는 프로퍼티
 * 여기에 필요한 라이브러리 등의 정보를 기술하면 그 라이브러리를 참조가능
 *
 *
 * implementation - 컴파일할때 접근가능
 * testImplementation - 테스트 컴파일할때 접근가능
 *
 * !! compile, testCompile 과 차이점
 * A라는 모듈을 수정한다고 했을때
 * compile - A 모듈을 직접 혹은 간접 의존하고 있는 모든 모듈들이 재빌드되어야함
 * implementation - A 모듈을 직접 의존하고 있는 모듈만 재빌드함
 * 그러므로 API의 노출이 최소화 되어 보안적인 면에서 더 좋다 (implementation > compile)
 *
 *
 * compileOnly - 컴파일시에만 사용
 * runtimeOnly - 런타임시에만 사용
 *
 *
 * 라이브러리 쓸때는 길게쓸수도 있고, 짧게쓸수도 있다.
 * compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'
 * compile 'org.hibernate:hibernate-core:3.6.7.Final'
 *
 *
 * classpath - 지정된 라이브러리를 클래스 경로에 추가할 수 있음
 */
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-aop'
    implementation 'org.springframework.boot:spring-boot-starter-test'

// spring batch
implementation 'org.springframework.boot:spring-boot-starter-batch'

    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

// Redis
implementation 'org.springframework.boot:spring-boot-starter-data-redis'
//embedded-redis
implementation group: 'it.ozimov', name: 'embedded-redis', version: '0.7.2'

// Model Mapper
implementation group: 'org.modelmapper', name: 'modelmapper', version: '2.3.5'

// https://mvnrepository.com/artifact/io.springfox/springfox-swagger2
implementation group: 'io.springfox', name: 'springfox-swagger2', version: '2.9.2'
// https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui
implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '2.9.2'
    implementation 'org.projectlombok:lombok:1.18.18'
    implementation 'org.projectlombok:lombok:1.18.18'

// https://mvnrepository.com/artifact/com.nimbusds/nimbus-jose-jwt
compile group: 'com.nimbusds', name: 'nimbus-jose-jwt', version: '8.2.1'

// https://mvnrepository.com/artifact/com.google.code.gson/gson
compile group: 'com.google.code.gson', name: 'gson', version: '2.8.5'

// aws kms sdk
implementation group: 'software.amazon.awssdk', name: 'cloudwatchlogs', version: '2.16.49'
    implementation group: 'com.amazonaws', name: 'aws-java-sdk', version: '1.11.106'
    implementation group: 'com.amazonaws', name: 'aws-encryption-sdk-java', version: '2.0.0'

// https://mvnrepository.com/artifact/org.spockframework/spock-core
testCompile group: 'org.spockframework', name: 'spock-core', version: '1.1-groovy-2.4'
// https://mvnrepository.com/artifact/org.spockframework/spock-spring
testCompile group: 'org.spockframework', name: 'spock-spring', version: '1.1-groovy-2.4'
    testCompile 'org.junit.jupiter:junit-jupiter:5.7.1'

    compileOnly 'org.projectlombok:lombok'
    runtimeOnly 'com.h2database:h2'
    implementation 'org.mariadb.jdbc:mariadb-java-client:2.6.1'
    annotationProcessor 'org.projectlombok:lombok'

    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }

    implementation("com.squareup.okhttp3:okhttp:4.8.0")

    compile 'commons-codec:commons-codec:1.14'
    compile group: 'org.bouncycastle', name: 'bcprov-jdk15on', version: '1.66'
    testCompile 'com.google.guava:guava:20.0'

    implementation 'org.mapstruct:mapstruct:1.4.1.Final'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.4.1.Final'

//Spring security
implementation 'org.springframework.boot:spring-boot-starter-security'
    implementation 'io.jsonwebtoken:jjwt:0.9.1'

// Newrelic Agent API
compile group: 'com.newrelic.agent.java', name: 'newrelic-api', version: '6.3.0'

// POI
compile group: 'org.apache.poi', name: 'poi', version: '3.17'//.xls
compile group: 'org.apache.poi', name: 'poi-ooxml', version: '3.17'//.xlsx

    // ShedLock
compile group: 'net.javacrumbs.shedlock', name: 'shedlock-spring', version: '2.5.0'
    compile group: 'net.javacrumbs.shedlock', name: 'shedlock-provider-redis-spring', version: '2.5.0'

}

test {
    useJUnitPlatform()
}
```
