---
title: Spring Boot에서 CRUDRepository의 findBy 메서드와 Multiple In 연산자 사용하기
date: 2023-10-09 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - CRUDRepository
  - findBy
  - MultipleIn
---
## 문제 상황

CRUDRepository에서 `findBy` 메서드를 사용할 때, 여러개의 `In` 연산자를 함께 사용하고 싶다면 어떻게 해야할까요? 이 문제에 대한 해결책을 알아봅시다.

## `In` 연산자란?

`In` 연산자는 SQL 쿼리에서 주로 사용되는 연산자입니다. 이 연산자를 사용하면 특정 컬럼의 값이 주어진 값들 중 하나와 일치하는지 확인할 수 있습니다.

예를 들어, SQL 쿼리에서 `SELECT * FROM table WHERE column IN (value1, value2, value3)`과 같이 사용됩니다.

## Multiple In 연산자 사용하기

Spring Data JPA와 CRUDRepository를 사용할 때, `findBy` 메서드에 `In` 연산자를 여러 개 사용하고 싶다면 메서드 시그니처를 아래와 같이 작성할 수 있습니다.

```java
List<Entity> findByColumn1InAndColumn2In(List<Type1> column1Values, List<Type2> column2Values);
```

이렇게 하면 `Column1`과 `Column2` 모두에서 여러 값을 동시에 검색할 수 있습니다.

## 예제 코드

```java
public interface MyRepository extends CrudRepository<MyEntity, Long> {
    List<MyEntity> findByAgeInAndNameIn(List<Integer> ages, List<String> names);
}
```

이 코드에서 `MyRepository` 인터페이스는 `CrudRepository`를 확장합니다. `findByAgeInAndNameIn` 메서드는 `age`와 `name` 컬럼에 대해 `In` 연산자를 사용하여 값을 찾습니다.

## 주의할 점

이 방법은 간단하고 유용하지만, 매우 큰 데이터 세트에서는 성능 문제가 발생할 수 있습니다. 따라서, 대용량 데이터에서는 쿼리 최적화를 고려해야합니다.

## 에러 케이스

잘못된 메서드 시그니처를 사용하면 `InvalidDerivedQueryException`이 발생할 수 있습니다. 따라서 메서드 시그니처를 정확하게 작성하는 것이 중요합니다.

## 요약

CRUDRepository에서 `findBy` 메서드를 통해 Multiple `In` 연산자를 사용하려면, 메서드 시그니처를 정확하게 작성해야 합니다. 이렇게 하면 두 개 이상의 컬럼에서 여러 값들을 동시에 검색할 수 있습니다.