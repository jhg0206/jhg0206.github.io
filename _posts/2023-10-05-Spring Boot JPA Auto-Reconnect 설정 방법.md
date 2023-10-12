---
title: Spring Boot JPA Auto-Reconnect 설정 방법
date: 2023-10-05 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - JPA
  - Auto-Reconnect
---
## 개요

Spring Boot와 JPA(Java Persistence API)를 사용할 때 데이터베이스 연결이 끊어졌을 경우 자동으로 재연결하는 설정에 대해 알아보겠습니다. 여기에서는 `autoReconnect` 옵션을 이용하는 방법을 중심으로 설명하겠습니다.

## `autoReconnect`이란?

`autoReconnect`은 MySQL 데이터베이스에 사용되는 JDBC URL의 옵션 중 하나입니다. 이 옵션은 데이터베이스 연결이 끊어졌을 때 자동으로 다시 연결하도록 지시합니다.

## 설정 방법

### `application.properties` 파일 수정

Spring Boot 프로젝트의 `src/main/resources` 디렉토리에 있는 `application.properties` 파일을 열어서 다음과 같이 작성합니다.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/your_database?autoReconnect=true
```

여기에서 `your_database`는 사용하고 있는 데이터베이스의 이름을 넣어주세요.

### `@Configuration` 클래스에서 설정

Java 설정 파일에서도 `autoReconnect`을 설정할 수 있습니다. `@Configuration` 어노테이션이 붙은 클래스에서 `DataSource` 빈을 생성할 때 옵션을 추가하면 됩니다.

```java
@Bean
public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();
    dataSource.setUrl("jdbc:mysql://localhost:3306/your_database?autoReconnect=true");
    return dataSource;
}
```

## 주의사항

- `autoReconnect` 옵션은 MySQL용입니다. 다른 데이터베이스에서는 지원하지 않을 수 있습니다.
- 연결이 끊어진 상태에서 쿼리를 실행하면 `CommunicationsException` 이라는 에러가 발생할 수 있습니다. 이 경우 추가적인 예외 처리가 필요합니다.

## 결론

Spring Boot와 JPA를 사용할 때 `autoReconnect` 설정은 데이터베이스 연결의 안정성을 높여줍니다. 하지만, 이 설정만으로는 모든 문제를 해결할 수 없으므로 다양한 예외 상황에 대한 대응이 필요합니다. 이를 통해 더욱 견고한 애플리케이션을 구축할 수 있습니다.