---
title: Spring CRUDRepository에서 대소문자 구분 없는 쿼리 사용하기
date: 2023-09-20 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - CRUDRepository
---
## 문제 상황

Spring Data JPA를 사용할 때, `CRUDRepository` 인터페이스를 이용해 쿼리를 작성합니다. 그런데 문제는 이 쿼리들이 대소문자를 구분한다는 것입니다. 여기서는 어떻게 대소문자 구분 없이 쿼리를 할 수 있는지 알아보겠습니다.

## 대소문자 무시하는 쿼리 작성법

### 사용되는 어노테이션: `@Query`

JPA에서 제공하는 `@Query` 어노테이션을 사용하면 SQL 또는 JPQL(Java Persistence Query Language) 쿼리를 직접 작성할 수 있습니다. 이때, `LOWER` 함수를 사용하면 대소문자를 무시할 수 있습니다.

```java
@Query("SELECT u FROM User u WHERE LOWER(u.username) = LOWER(:username)")
List<User> findByUsernameCaseInsensitive(@Param("username") String username);
```

### 사용되는 메소드: `IgnoreCase`

Spring Data JPA에서는 `IgnoreCase`라는 키워드를 사용해서 대소문자 구분 없이 쿼리를 할 수 있습니다.

```java
List<User> findByUsernameIgnoreCase(String username);
```

## 장점과 단점

### 장점

1. **간결성**: `IgnoreCase`를 사용하면 코드가 더 간결해집니다.
2. **표준화**: JPQL을 사용하면, 다양한 데이터베이스에 쿼리를 쉽게 적용할 수 있습니다.

### 단점

1. **성능 이슈**: `LOWER` 함수를 사용하면 쿼리의 성능이 떨어질 수 있습니다.
2. **데이터베이스 종속성**: `@Query`를 사용하면 데이터베이스에 따라 동작이 달라질 수 있습니다.

## 결론

대소문자 구분 없이 쿼리를 하려면 `@Query` 어노테이션을 사용하거나 `IgnoreCase` 키워드를 사용할 수 있습니다. 각 방법은 장단점이 있으니, 상황에 맞게 선택하면 됩니다.