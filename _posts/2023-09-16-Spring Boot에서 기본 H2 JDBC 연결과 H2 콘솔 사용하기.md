---
title: Spring Boot에서 기본 H2 JDBC 연결과 H2 콘솔 사용하기
date: 2023-09-16 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - H2데이터베이스
---
## 문제 상황: H2 데이터베이스 연결

Spring Boot를 사용할 때, H2 데이터베이스에 연결하는 과정에서 몇 가지 문제가 발생할 수 있습니다. 특히, `spring.datasource.url` 설정 미스나 H2 콘솔 접근 문제는 많이 발생하는 이슈입니다.

## H2 데이터베이스란?

H2 데이터베이스는 자바로 작성된 오픈소스 관계형 데이터베이스입니다. 빠른 속도와 가볍다는 장점이 있으며, 임베디드 모드(내장형) 또는 서버 모드로 동작할 수 있습니다. 

## 설정: `application.properties` 파일

Spring Boot 프로젝트에서는 `application.properties` 파일에 데이터베이스 연결 정보를 작성합니다. H2 데이터베이스에 연결하기 위해서는 다음과 같은 설정이 필요합니다.

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
```

## H2 콘솔 활성화

개발 과정에서 H2 콘솔을 사용하면 데이터베이스 상태를 더 쉽게 확인할 수 있습니다. 콘솔을 활성화하기 위해서는 `application.properties` 파일에 다음 설정을 추가해야 합니다.

```properties
spring.h2.console.enabled=true
```

이 설정을 추가한 후에는 브라우저에서 `http://localhost:8080/h2-console`로 접속하여 H2 콘솔을 사용할 수 있습니다.

## 주의할 점: `DataIntegrityViolationException` 오류

데이터베이스 연결 시, `DataIntegrityViolationException`이라는 오류가 발생할 수 있습니다. 이 오류는 데이터 무결성을 위반한 경우에 발생합니다. 대체로 테이블 생성이나 데이터 입력 시에 유일성, 외래 키, 논리적 제약 조건 등이 올바르지 않을 때 발생하는 문제입니다.

## 결론

Spring Boot와 H2 데이터베이스를 연동하는 과정은 복잡하지 않습니다. `application.properties` 파일에 필요한 설정을 작성하고, H2 콘솔을 활성화하는 것만으로도 효율적인 개발이 가능합니다. 하지만 설정을 잘못 입력하거나 데이터 무결성을 위반하면 오류가 발생할 수 있으니 주의가 필요합니다.