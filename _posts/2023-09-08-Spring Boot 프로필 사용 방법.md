---
title: Spring Boot 프로필 사용 방법
date: 2023-09-08 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 프로필이란 무엇인가?

프로필이란 어플리케이션의 설정을 환경에 따라 구분할 수 있는 방법입니다. 예를 들어, 개발 환경에서는 데이터베이스 연결을 다르게 하고, 실제 운영 환경에서는 다른 설정을 적용할 수 있습니다.

## Spring Boot에서 프로필 설정하기

Spring Boot에서 프로필을 설정하는 가장 간단한 방법은 `application.properties` 파일 내에서 `spring.profiles.active`를 설정하는 것입니다. 이렇게 설정하면 Spring Boot는 해당 프로필을 활성화합니다.

```java
spring.profiles.active=dev
```

또는 프로그램 실행 시에 JVM 옵션으로도 설정할 수 있습니다.

```bash
java -jar myapp.jar --spring.profiles.active=prod
```

## @Profile 어노테이션 사용하기

Spring에서는 클래스나 빈에 `@Profile` 어노테이션을 사용하여 특정 프로필에서만 활성화되도록 할 수 있습니다.

```java
@Configuration
@Profile("dev")
public class DevConfig {
    // 여기에 개발 환경에서만 적용될 빈 설정
}
```

## 여러 프로필을 동시에 활성화하기

여러 개의 프로필을 동시에 활성화하고 싶다면 쉼표로 구분해서 나열할 수 있습니다.

```java
spring.profiles.active=dev,oauth
```

## 프로필별로 다른 설정 파일 사용하기

`application-dev.properties`와 `application-prod.properties` 같은 방식으로 프로필별로 설정 파일을 분리할 수 있습니다. 그럼 해당 프로필이 활성화될 때 자동으로 해당 설정 파일이 적용됩니다.

## 주의 사항

`spring.profiles.include` 속성을 사용하면 하나의 프로필이 다른 프로필을 포함할 수 있습니다. 하지만 이 기능은 주의해서 사용해야 하며, 각 프로필의 설정이 충돌하지 않도록 관리해야 합니다.

이렇게 Spring Boot에서는 다양한 방법으로 프로필을 관리하고 설정을 적용할 수 있습니다. 환경에 따른 유연한 설정이 가능하므로 개발과 배포가 더 효율적으로 이루어집니다.