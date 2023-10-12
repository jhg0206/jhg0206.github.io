---
title: Spring에서 HttpServletRequest를 Request-Scoped Bean에 주입하는 방법
date: 2023-09-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - HttpServletRequest
---
## 개요

이 글에서는 Java의 Spring 프레임워크를 사용할 때 `HttpServletRequest` 객체를 Request-Scoped Bean에 주입하는 방법에 대해 자세히 알아보겠습니다. `HttpServletRequest`는 HTTP 요청 정보를 담고 있는 객체입니다. Request-Scoped Bean은 HTTP 요청마다 새롭게 생성되는 빈입니다.

## `HttpServletRequest`와 Request-Scoped Bean이란?

### HttpServletRequest
`HttpServletRequest`는 Servlet API의 일부로, 클라이언트가 서버에 보내는 HTTP 요청의 세부 정보를 포함하고 있습니다. 이를 통해 요청 메서드, 헤더, 파라미터 등을 알 수 있습니다.

### Request-Scoped Bean
Spring에서 빈(Bean)은 객체를 의미합니다. Request-Scoped는 빈의 범위 중 하나로, HTTP 요청이 시작될 때 생성되고, 요청이 완료되면 소멸합니다.

## 주입 방법

### @Autowired 어노테이션 사용하기

가장 간단한 방법은 `@Autowired` 어노테이션을 사용하는 것입니다. 이 어노테이션은 Spring이 자동으로 해당 타입의 빈을 찾아 주입해주는 기능을 수행합니다.

```java
@Autowired
private HttpServletRequest request;
```

### 생성자를 통한 주입

생성자를 통해 주입을 할 수도 있습니다. 이 방법은 불변성을 유지하면서 의존성을 주입하는 데 유리합니다.

```java
private final HttpServletRequest request;

@Autowired
public YourClass(HttpServletRequest request) {
    this.request = request;
}
```

## 주의사항: Circular Dependency

`HttpServletRequest`를 주입받는 동안 순환 의존성(Circular Dependency) 문제가 발생할 수 있습니다. 순환 의존성이란 두 개 이상의 빈이 서로를 참조, 즉 의존하고 있는 상황을 의미합니다. 이런 문제를 피하기 위해 `@Lazy` 어노테이션을 사용할 수 있습니다.

```java
@Autowired
@Lazy
private HttpServletRequest request;
```

## 결론

Spring에서 `HttpServletRequest`를 Request-Scoped Bean에 주입하는 것은 `@Autowired` 어노테이션 또는 생성자를 통해 가능합니다. 주의해야 할 점은 순환 의존성 문제로, 이를 해결하기 위해 `@Lazy` 어노테이션을 사용할 수 있습니다. 이러한 방법들을 통해 HTTP 요청에 따라 동적으로 데이터를 처리할 수 있게 됩니다.