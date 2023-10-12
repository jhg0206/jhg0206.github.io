---
title: 스프링 프레임워크에서 @Bean과 @Autowired의 차이점
date: 2023-09-02 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - 프레임워크
  - Bean
  - Autowired
---
## @Bean이 무엇인가요?

`@Bean` 어노테이션은 스프링 컨테이너에서 관리되는 빈(Bean) 객체를 생성할 때 사용됩니다. 이 어노테이션을 사용하면 개발자가 직접 빈 객체의 생성 및 설정을 제어할 수 있습니다. 일반적으로 `@Configuration` 어노테이션이 붙은 클래스 안에서 `@Bean` 어노테이션을 사용합니다.

```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

이렇게 설정하면 `MyService` 클래스의 인스턴스가 스프링 컨테이너에 등록되며, 애플리케이션에서 이를 사용할 수 있습니다.

## @Autowired는 어떤 역할을 하나요?

`@Autowired` 어노테이션은 스프링 컨테이너에서 이미 생성된 빈(Bean)을 자동으로 주입하는 역할을 합니다. 이 어노테이션을 사용하면 개발자가 직접 빈을 찾아와 주입할 필요가 없습니다. 주로 변수, 생성자, 메소드에 사용됩니다.

```java
public class MyController {
    @Autowired
    private MyService myService;
}
```

여기서 `MyService` 빈은 자동으로 `MyController` 클래스의 `myService` 변수에 주입됩니다.

## 두 어노테이션의 주요 차이점

1. **생성 vs 주입**: `@Bean`은 빈 객체를 생성하고 설정하는 반면, `@Autowired`는 이미 생성된 빈을 주입합니다.
2. **설정 위치**: `@Bean`은 `@Configuration` 클래스 안에서 사용되며, `@Autowired`는 빈이 필요한 곳 어디에서나 사용할 수 있습니다.
3. **제어 가능성**: `@Bean`을 사용하면 빈의 생성과 설정을 더 세밀하게 제어할 수 있습니다.
4. **의존성 관리**: `@Autowired`를 사용하면 스프링이 자동으로 의존성을 관리해주기 때문에, 코드가 더 간결해집니다.

## 결론

`@Bean`과 `@Autowired`는 서로 다른 목적과 사용 사례를 가지고 있습니다. `@Bean`은 빈 객체를 생성하고 초기 설정을 제공하는 반면, `@Autowired`는 해당 빈을 필요로 하는 클래스에 자동으로 주입합니다. 이 두 어노테이션을 적절히 활용하면 스프링 기반의 애플리케이션 개발이 훨씬 효율적이고 간결해집니다.