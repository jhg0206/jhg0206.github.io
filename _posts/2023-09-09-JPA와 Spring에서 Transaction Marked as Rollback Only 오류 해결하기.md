---
title: JPA와 Spring에서 Transaction Marked as Rollback Only 오류 해결하기
date: 2023-09-09 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring오류
  - JPA
---
## 오류의 기본적인 이해

"Transaction Marked as Rollback Only"라는 문제는 Java Persistence API(JPA)와 Spring 프레임워크에서 트랜잭션이 롤백되어야 한다고 지시할 때 나타나는 오류입니다. 이 문제가 발생하면, 데이터베이스 트랜잭션은 완료될 수 없으며 롤백이라는 과정을 거쳐야 합니다. 롤백은 데이터베이스의 상태를 이전 상태로 되돌리는 것을 의미합니다.

## 원인 추적 방법

### 로깅 활성화하기

프로그램에서 이러한 오류가 발생한 원인을 찾으려면 로깅을 통해 상세한 정보를 얻을 수 있습니다. Spring 프레임워크에서는 `spring.jpa.show-sql=true` 설정을 사용하여 SQL 쿼리 로깅을 활성화할 수 있습니다.

### 예외 처리 검토

"Transaction Marked as Rollback Only" 오류는 대체로 예외 상황 때문에 발생합니다. 예외를 잘 처리하고 있는지 확인해야 합니다. 예외가 발생하면 해당 예외에 대한 처리 로직을 추가하거나 수정해야 할 수 있습니다.

### 트랜잭션 설정 검사

트랜잭션 설정이 제대로 되어 있는지 확인하십시오. `@Transactional` 애너테이션이 올바르게 사용되었는지, 트랜잭션의 격리 수준(Isolation Level)과 전파 옵션(Propagation Option)이 적절한지 검토해야 합니다.

## 해결 방안

### 롤백 방지

트랜잭션 내에서 예외가 발생하지 않도록 하는 것이 가장 좋은 해결책입니다. 이렇게 하려면 예외 처리를 통해 문제를 해결하거나, 문제가 되는 부분을 수정해야 합니다.

### 프로그래밍적 롤백 처리

`TransactionStatus` 객체를 사용하여 트랜잭션을 수동으로 롤백할 수 있습니다. 이렇게 하면 프로그램 내에서 더 세밀한 트랜잭션 제어가 가능합니다.

### 트랜잭션 설정 수정

`@Transactional` 애너테이션의 속성을 변경하여 트랜잭션의 동작을 제어할 수도 있습니다. 예를 들어, `readOnly=true` 설정을 통해 트랜잭션을 읽기 전용으로 설정할 수 있습니다.

이러한 방법들을 통해 "Transaction Marked as Rollback Only" 오류를 해결할 수 있습니다. 이 문제는 복잡한 원인에 기인할 수 있으므로, 여러 가지 방법을 시도해보는 것이 중요합니다.