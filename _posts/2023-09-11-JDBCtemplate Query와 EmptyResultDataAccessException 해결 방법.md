---
title: JDBCtemplate Query와 EmptyResultDataAccessException 해결 방법
date: 2023-09-11 20:00:00 +0900
categories:
  - Spring
tags:
  - JavaScript시간
  - JDBCtemplate
---
## 문제 상황: EmptyResultDataAccessException 에러 발생

Java를 사용하여 데이터베이스와 연동할 때, Spring Framework의 `JdbcTemplate` 클래스를 사용하는 경우가 많습니다. 하지만 때로는 `EmptyResultDataAccessException` 이라는 에러를 마주칠 수 있습니다. 이 에러는 쿼리의 결과가 없을 때 발생하는데, 이를 어떻게 처리해야 할지에 대해 설명하겠습니다.

## 원인 파악

`EmptyResultDataAccessException` 에러는 데이터베이스 쿼리가 예상과 다르게 빈 결과를 반환했을 때 발생합니다. 예를 들어, 특정 ID로 데이터를 검색하려 했는데 해당 ID에 대한 데이터가 없다면 이 에러가 발생할 것입니다.

## 해결 방법 1: try-catch 사용

가장 기본적인 해결 방법은 `try-catch` 구문을 사용하여 예외를 처리하는 것입니다. `try` 블록 안에서 쿼리를 실행하고, `catch` 블록에서 `EmptyResultDataAccessException`을 잡아 처리할 수 있습니다.

```java
try {
    String result = jdbcTemplate.queryForObject("SQL 쿼리", String.class);
} catch (EmptyResultDataAccessException e) {
    // 예외 처리 로직
}
```

## 해결 방법 2: Optional 활용

Java 8 이상에서는 `Optional`을 사용하여 더 깔끔하게 코드를 작성할 수 있습니다. `Optional`은 값이 있을 수도, 없을 수도 있는 상황에 유용하며, `null`을 직접 다루는 것보다 안전합니다.

```java
Optional<String> result = Optional.ofNullable(jdbcTemplate.queryForObject("SQL 쿼리", String.class));
```

여기서 `Optional.ofNullable` 메서드는 쿼리의 결과가 `null`일 경우, `Optional.empty()`를 반환하게 됩니다. 따라서 이후 로직에서 `result.isPresent()`를 사용하여 값의 존재 여부를 확인할 수 있습니다.

## 결론

`EmptyResultDataAccessException` 에러는 쿼리 결과가 없을 때 발생하는 예외입니다. 이를 처리하기 위한 두 가지 방법, 즉 `try-catch` 구문과 `Optional`을 사용한 방법을 소개했습니다. 선택하는 방법은 상황과 개발 환경에 따라 다르겠지만, 두 방법 모두 안전한 코딩을 위한 유용한 방법입니다.