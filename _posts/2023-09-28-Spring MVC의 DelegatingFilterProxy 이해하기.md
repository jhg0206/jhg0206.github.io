---
title: Spring MVC의 DelegatingFilterProxy 이해하기
date: 2023-09-28 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - DelegatingFilterProxy
---
## 무엇이 DelegatingFilterProxy인가?

DelegatingFilterProxy는 Spring Framework에서 제공하는 클래스로, 서블릿 필터의 역할을 하는 구성 요소입니다. 필터는 웹 애플리케이션에서 클라이언트와 서버 사이에 위치해 특정 작업을 수행합니다. DelegatingFilterProxy는 이러한 필터의 실행을 Spring의 애플리케이션 컨텍스트에 있는 다른 빈에 위임하는 역할을 합니다.

## DelegatingFilterProxy가 필요한 이유

1. **통합성**: Spring이 관리하는 빈과 서블릿 필터를 쉽게 통합할 수 있습니다. 
2. **재사용성**: Spring 컨텍스트 내에서 정의한 빈을 여러 필터에서 재사용할 수 있습니다.
3. **설정 용이성**: XML이나 Java 설정을 통해 빈을 쉽게 구성할 수 있습니다.
4. **테스트 용이성**: Spring이 관리하는 빈이므로, 테스트하기 쉽습니다.

## 작동 원리

DelegatingFilterProxy는 실제로 서블릿 필터의 구현을 담당하지 않습니다. 대신, 이 클래스는 Spring 애플리케이션 컨텍스트에서 특정 빈을 찾아 그 빈에게 필터링 작업을 위임합니다. 이 때문에, 실제 필터 로직은 Spring 빈으로 관리되므로 위에서 언급한 여러 이점이 있습니다.

## 예시: Spring Security와의 연동

Spring Security는 보안 관련 여러 기능을 제공하는데, 이를 위해 여러 가지 필터를 사용합니다. 예를 들어, `UsernamePasswordAuthenticationFilter`라는 빈이 로그인 인증을 처리할 수 있습니다. DelegatingFilterProxy를 사용하면 이러한 Spring Security의 필터를 쉽게 통합할 수 있습니다.

## 코드에서의 활용

일반적으로 `web.xml` 파일이나 Java 설정 클래스에서 DelegatingFilterProxy를 정의합니다. 예를 들어, `web.xml`에서는 다음과 같이 설정할 수 있습니다.

```xml
<filter>
    <filter-name>myFilter</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
</filter>
```

이 경우, `myFilter`라는 이름의 Spring 빈이 실제 필터링 로직을 처리하게 됩니다.

## 정리

DelegatingFilterProxy는 필터 로직을 Spring이 관리하는 빈에 위임하여, 통합성, 재사용성, 설정 용이성 등의 이점을 제공합니다. 이를 통해 웹 애플리케이션의 유지보수가 편리해지며, 다양한 Spring 라이브러리와의 통합이 수월해집니다.