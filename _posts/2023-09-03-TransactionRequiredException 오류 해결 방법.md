---
title: TransactionRequiredException 오류 해결 방법
date: 2023-09-03 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring오류
---
## 오류 개요

Java에서 JPA(Java Persistence API)를 사용할 때 발생하는 `TransactionRequiredException`이라는 오류에 대해 이야기해보겠습니다. 이 오류는 데이터베이스와 상호 작용할 때 트랜잭션(Transaction)이 필요하다는 것을 알려주는 오류 메시지입니다.

## 원인 파악

`TransactionRequiredException` 오류는 주로 데이터베이스에 쓰기 작업(Update/Delete)을 할 때 트랜잭션을 시작하지 않았을 경우에 발생합니다. JPA에서는 데이터의 일관성을 위해 이러한 쓰기 작업을 트랜잭션 안에서 처리해야 합니다.

## 해결 방법 1: Annotation 사용

코드에서 `@Transactional` 이라는 어노테이션(Annotation)을 사용하여 해당 메서드가 트랜잭션을 필요로 한다는 것을 명시할 수 있습니다.

```java
import javax.transaction.Transactional;

@Transactional
public void updateData() {
    // 쓰기 작업
}
```

## 해결 방법 2: 프로그래밍 방식으로 트랜잭션 관리

어노테이션 외에도, 프로그래밍 방식으로 트랜잭션을 시작하고 커밋할 수 있습니다. `EntityManager`를 사용하여 트랜잭션을 수동으로 제어할 수 있습니다.

```java
EntityManager em = ...;
em.getTransaction().begin();
// 쓰기 작업
em.getTransaction().commit();
```

## 예방 조치

- 쓰기 작업을 할 때는 반드시 트랜잭션을 시작하세요.
- 트랜잭션을 명시적으로 커밋하거나 롤백하는 코드를 작성하세요.

## 결론

`TransactionRequiredException` 오류는 데이터베이스의 쓰기 작업을 트랜잭션 없이 수행하려고 할 때 발생합니다. 이를 해결하기 위해 `@Transactional` 어노테이션을 사용하거나, `EntityManager`를 통해 수동으로 트랜잭션을 관리할 수 있습니다. 이러한 방법을 통해 데이터의 일관성을 유지할 수 있습니다.