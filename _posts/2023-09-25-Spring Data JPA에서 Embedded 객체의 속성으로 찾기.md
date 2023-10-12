---
title: Spring Data JPA에서 Embedded 객체의 속성으로 찾기
date: 2023-09-25 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringDataJPA
  - Embedded객체
---
## 문제 설명: `InvalidDataAccessApiUsageException` 오류

Spring Data JPA에서 Embedded 객체의 속성을 사용하여 데이터를 검색하려고 할 때, 종종 `InvalidDataAccessApiUsageException` 이라는 오류가 발생합니다. 이 문제를 어떻게 해결할 수 있는지에 대한 해결책을 제공합니다.

## 잘못된 쿼리 메서드 문제

`InvalidDataAccessApiUsageException` 오류가 발생하는 주된 원인은 잘못 구성된 쿼리 메서드 때문입니다. 예를 들어, `Address`라는 Embedded 객체가 있고, 그 안에 `city`라는 필드가 있는 경우, `findByAddress_City(String city)`와 같은 형식으로 메서드를 작성해야 합니다.

## 해결 방법: 올바른 메서드 시그니처 사용

1. **Repository 인터페이스에 메서드 추가**: `Address` 객체의 `city` 속성으로 검색하려면, 다음과 같이 Repository 인터페이스에 메서드를 추가하세요.
    ```java
    List<User> findByAddress_City(String city);
    ```

2. **NamedQuery 사용**: `@NamedQuery` 어노테이션을 사용하여 JPQL 쿼리를 명시적으로 작성할 수도 있습니다.
    ```java
    @NamedQuery(name = "findUserByCity", query = "SELECT u FROM User u WHERE u.address.city = :city")
    ```

3. **@Query 어노테이션 사용**: 복잡한 쿼리의 경우, `@Query` 어노테이션을 사용하여 쿼리를 직접 작성합니다.
    ```java
    @Query("SELECT u FROM User u WHERE u.address.city = ?1")
    List<User> findUsersByCity(String city);
    ```

## 주의 사항: Embedded 객체와 필드 이름

Embedded 객체와 그 객체의 필드 이름을 정확하게 지정하는 것이 중요합니다. 대소문자를 정확하게 맞추고, 필드 이름이 두 단어 이상으로 이루어진 경우에는 카멜 케이스(Camel Case)를 사용해야 합니다.

## 정리

Spring Data JPA에서 Embedded 객체의 속성으로 데이터를 찾을 때 주의해야 할 사항은 메서드의 올바른 시그니처와 필드 이름의 정확한 사용입니다. 이를 통해 `InvalidDataAccessApiUsageException` 오류를 피할 수 있습니다.