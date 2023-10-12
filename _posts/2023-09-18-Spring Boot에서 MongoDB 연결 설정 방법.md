---
title: Spring Boot에서 MongoDB 연결 설정 방법
date: 2023-09-18 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - MongoDB
---
## 들어가기 전에: Spring Boot와 MongoDB란 무엇인가?

Spring Boot는 Java로 웹 애플리케이션을 쉽고 빠르게 개발할 수 있도록 도와주는 프레임워크입니다. MongoDB는 NoSQL 데이터베이스 중 하나로, JSON과 유사한 형식의 문서를 저장합니다. 이 두 기술을 함께 사용하면 데이터를 효율적으로 관리할 수 있습니다.

## MongoDB 연결 설정의 중요성

MongoDB와 연결을 설정하는 것은 애플리케이션의 성능과 안정성에 큰 영향을 미칩니다. 잘못 설정하면 `MongoSocketException` 같은 에러가 발생할 수 있어, 올바른 설정이 중요합니다.

## `application.properties` 파일에서 설정하기

Spring Boot에서는 `application.properties` 파일을 사용하여 MongoDB와의 연결을 설정할 수 있습니다. 이 파일은 프로젝트의 `src/main/resources` 폴더 내에 위치해야 합니다.

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/your-database
```

여기서 `localhost:27017`은 MongoDB가 실행되고 있는 주소와 포트 번호입니다. `your-database`는 연결할 데이터베이스의 이름입니다.

## Java 코드에서 설정하기

`MongoClient` 객체를 사용하여 Java 코드 내에서 MongoDB에 연결할 수도 있습니다.

```java
@Bean
public MongoClient mongoClient() {
    return MongoClients.create("mongodb://localhost:27017/your-database");
}
```

`@Bean` 어노테이션은 Spring Boot가 시작할 때 `MongoClient` 객체를 생성하도록 지시합니다.

## 추가 설정 옵션

설정 파일이나 코드에서 다양한 옵션을 추가할 수 있습니다. 예를 들어, 아래와 같이 타임아웃 시간을 설정할 수 있습니다.

```properties
spring.data.mongodb.serverSelectionTimeout=3000
```

## 정리

Spring Boot와 MongoDB를 함께 사용하려면 `application.properties` 파일이나 Java 코드 내에서 연결을 설정해야 합니다. 올바른 설정을 통해 애플리케이션의 성능과 안정성을 높일 수 있습니다.