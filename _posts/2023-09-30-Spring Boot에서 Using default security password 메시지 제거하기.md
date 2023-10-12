---
title: Spring Boot에서 Using default security password 메시지 제거하기
date: 2023-09-30 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황

Spring Boot를 사용하면서 콘솔에 나타나는 "Using default security password"라는 메시지가 거슬린다면, 이 글은 여러분을 위한 것입니다. 이 메시지는 Spring Boot의 보안 기능이 기본 설정으로 동작하고 있다는 것을 알려주는데, 여러분이 사용자 정의 보안 설정을 원할 경우 이 메시지를 제거할 필요가 있습니다.

## 해결 방법 1: `application.properties` 파일 수정

가장 간단한 방법 중 하나는 `application.properties` 파일에 몇 가지 설정을 추가하는 것입니다.

```properties
spring.security.user.name=사용자이름
spring.security.user.password=비밀번호
```

여기서 `사용자이름`과 `비밀번호`는 원하는 값을 입력하면 됩니다. 이렇게 하면 기본 보안 설정을 덮어쓰게 되어, "Using default security password" 메시지가 더 이상 나타나지 않습니다.

## 해결 방법 2: `SecurityConfig` 클래스 생성

보다 고급 설정을 원한다면, `SecurityConfig`라는 이름의 새로운 클래스를 생성하고 `WebSecurityConfigurerAdapter`를 상속 받을 수 있습니다.

```java
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

public class SecurityConfig extends WebSecurityConfigurerAdapter {
    // 구현 내용
}
```

이 클래스에서 여러분은 원하는 대로 보안 설정을 구현할 수 있습니다. 이 방법을 사용하면, Spring Boot가 기본 보안 설정 대신 이 클래스의 설정을 사용하게 됩니다.

## 주의 사항

두 가지 방법 중 어느 것을 선택하든, 반드시 애플리케이션의 보안을 신중하게 고려해야 합니다. 보안은 중요한 이슈이므로, 무턱대고 기본 설정을 무시하는 것은 위험할 수 있습니다.

## 정리

Spring Boot에서 "Using default security password" 메시지를 제거하는 방법은 크게 두 가지입니다. `application.properties` 파일을 수정하거나, 새로운 `SecurityConfig` 클래스를 생성하여 보안 설정을 사용자 정의할 수 있습니다. 선택한 방법에 따라, 보안 설정을 세심하게 관리하는 것이 중요합니다.