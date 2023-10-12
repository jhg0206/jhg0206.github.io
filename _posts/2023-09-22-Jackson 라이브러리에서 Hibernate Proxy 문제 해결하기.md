---
title: Jackson 라이브러리에서 Hibernate Proxy 문제 해결하기
date: 2023-09-22 20:00:00 +0900
categories:
  - Spring
tags:
  - Jackson
  - HibernateProxy
---
## 문제 상황: No Serializer Found for Class 오류

프로젝트에서 Hibernate와 Jackson을 함께 사용할 때, 다음과 같은 에러 메시지를 자주 볼 수 있습니다: `No Serializer Found for Class org.hibernate.proxy.pojo.bytebuddy.ByteBuddyInterceptor`. 이 에러는 Hibernate가 데이터베이스에서 객체를 불러올 때 사용하는 프록시 객체가 Jackson에 의해 직렬화(Serialization)되지 못해서 발생합니다.

## 원인 파악: Hibernate 프록시와 직렬화

Hibernate는 성능 향상을 위해 프록시 객체를 사용합니다. 이 프록시 객체는 실제 객체를 대신해서 데이터베이스에서 데이터를 불러옵니다. Jackson은 이 프록시 객체를 어떻게 처리해야 할지 모르기 때문에 에러가 발생하는 것입니다.

## 해결 방안 1: `@JsonIgnoreProperties` 어노테이션 사용

첫 번째 해결 방법은 `@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})` 어노테이션을 사용하는 것입니다. 이 어노테이션을 모델 클래스에 추가하면 Jackson은 프록시 객체의 특정 프로퍼티를 무시하게 됩니다.

```java
@Entity
@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})
public class MyEntity {
    // ...
}
```

## 해결 방안 2: `@JsonIdentityInfo` 어노테이션 활용

두 번째 방법은 `@JsonIdentityInfo` 어노테이션을 사용하는 것입니다. 이 어노테이션은 순환 참조(circular reference) 문제를 해결하는 데도 도움이 되며, Jackson이 객체를 유니크한 식별자로 관리하도록 해줍니다.

```java
@Entity
@JsonIdentityInfo(
  generator = ObjectIdGenerators.PropertyGenerator.class, 
  property = "id")
public class MyEntity {
    // ...
}
```

## 해결 방안 3: Custom Serializer 구현

마지막 방법은 직접 커스텀 Serializer를 구현하는 것입니다. 이 방법은 복잡하지만, 프록시 객체를 정확히 원하는 형태로 직렬화할 수 있습니다.

```java
public class MyEntitySerializer extends JsonSerializer<MyEntity> {
    @Override
    public void serialize(MyEntity value, JsonGenerator gen, SerializerProvider serializers) throws IOException {
        // 커스텀 로직
    }
}
```

이 세 가지 방법 중에 하나를 선택해서 사용하면 `No Serializer Found for Class org.hibernate.proxy.pojo.bytebuddy.ByteBuddyInterceptor` 에러를 해결할 수 있습니다. 해결 방안을 적용한 후에는 반드시 코드를 재컴파일하고 프로젝트를 다시 실행해야 합니다.