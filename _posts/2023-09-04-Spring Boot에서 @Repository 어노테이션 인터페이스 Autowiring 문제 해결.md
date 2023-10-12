---
title: Spring Boot에서 @Repository 어노테이션 인터페이스 Autowiring 문제 해결
date: 2023-09-04 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - MongoRepository
  - Autowiring
---
## 문제 상황

Spring Boot 프로젝트에서는 보통 `@Autowired` 어노테이션을 사용하여 의존성을 주입합니다. 하지만 가끔 `@Repository` 어노테이션을 사용한 인터페이스와 관련해 의존성 주입 문제가 발생할 수 있습니다. 특히, `NoSuchBeanDefinitionException` 오류가 나타날 경우가 많습니다.

## 원인 파악

`NoSuchBeanDefinitionException` 이라는 오류 이름을 보면 Spring이 특정 빈(bean)을 찾을 수 없다는 것을 알 수 있습니다. 이 오류는 다음과 같은 상황에서 발생할 수 있습니다.

1. `@Repository` 어노테이션이 올바르게 설정되지 않았을 경우
2. 스캔 대상 패키지에 빈이 없을 경우
3. `@Autowired` 어노테이션이 올바르게 사용되지 않았을 경우

## 해결 방법

### @Repository 어노테이션 확인

먼저 `@Repository` 어노테이션이 올바르게 적용되어 있는지 확인해야 합니다. 이 어노테이션은 Spring 데이터 액세스 계층에만 사용되어야 하며, 구현 클래스가 없을 경우에도 인터페이스에 적용해야 합니다.

### 패키지 스캔 설정

빈을 찾을 수 없는 오류가 발생한 경우, 스프링 부트가 빈을 찾을 범위가 올바른지 확인해야 합니다. `@ComponentScan` 어노테이션을 사용하여 스캔할 패키지를 명시적으로 지정할 수 있습니다.

### @Autowired 사용법

마지막으로 `@Autowired` 어노테이션을 올바르게 사용했는지 확인합니다. 이 어노테이션은 생성자, 필드, 세터에 사용할 수 있습니다. 생성자 주입 방식이 권장됩니다.

## 결론

Spring Boot에서 `@Repository` 어노테이션 인터페이스와 `@Autowired`를 올바르게 사용하면 `NoSuchBeanDefinitionException` 같은 오류를 피할 수 있습니다. 오류 메시지를 잘 읽고 문제의 원인을 파악한 다음, 적절한 해결 방법을 적용해야 합니다.