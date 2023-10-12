---
title: Spring Boot application.properties 값 적용하여 문제 해결
date: 2023-09-29 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황

Spring Boot에서 `application.properties` 파일을 사용해 설정 값을 정의할 수 있습니다. 하지만 이 값이 예상대로 적용되지 않는 경우가 있습니다. 이러한 문제를 겪는 개발자들은 `Value Not Populating`이라는 에러 메시지와 함께 고민하게 됩니다. 

## 해결 방법 1: 애노테이션 사용 확인

Spring Boot에서는 `@Value` 애노테이션을 사용하여 `application.properties`의 설정 값을 자바 클래스에 주입합니다. 예를 들어, `application.properties`에 `server.port=8080`이라고 정의했다면, 자바 클래스에서는 다음과 같이 사용할 수 있습니다.

```java
@Value("${server.port}")
private int port;
```

이 과정에서 문제가 발생한다면, 먼저 `@Value` 애노테이션이 올바르게 사용되었는지 확인해야 합니다. 특히 중괄호 `{}`나 변수명에 오타가 없는지 주의해야 합니다.

## 해결 방법 2: 프로퍼티 파일 위치 확인

`application.properties` 파일이 올바른 디렉토리에 위치하고 있는지 확인해야 합니다. 일반적으로 이 파일은 `src/main/resources` 디렉토리에 있어야 합니다. 파일 위치가 틀리면 Spring Boot가 해당 설정 값을 읽어오지 못하므로, 올바른 위치에 파일을 배치하세요.

## 해결 방법 3: 스펠링과 문법 확인

`application.properties` 파일 내의 설정 값이 올바른지, 스펠링이나 문법에 문제가 없는지 확인해야 합니다. 예를 들어, `server.port = 8080` 대신 `server.port: 8080`을 사용할 수도 있으니, 이 부분도 주의가 필요합니다.

## 해결 방법 4: 로깅으로 문제 파악

Spring Boot는 로깅을 통해 다양한 시스템 정보를 제공합니다. 만약 `@Value` 애노테이션을 사용했는데도 값이 주입되지 않는다면, 로깅을 활용해 문제를 파악할 수 있습니다. 로깅은 시스템의 내부 상황을 파악하는 데 유용하므로, 로그 메시지를 꼼꼼히 확인해보세요.

## 정리

Spring Boot에서 `application.properties`의 설정 값이 정상적으로 적용되지 않을 때는 위와 같은 여러 방법으로 문제를 해결할 수 있습니다. 애노테이션 사용 방법, 파일 위치, 스펠링과 문법, 그리고 로깅을 통한 문제 파악을 체크해보면, 대부분의 문제를 해결할 수 있을 것입니다.