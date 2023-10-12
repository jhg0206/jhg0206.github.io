---
title: Spring에서 현재 ApplicationContext 얻기
date: 2023-09-05 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ApplicationContext
---
## ApplicationContext란 무엇인가?

ApplicationContext는 Spring 프레임워크에서 매우 중요한 역할을 합니다. 이것은 Spring 컨테이너의 고급 설정 인터페이스입니다. 간단히 말하면, ApplicationContext는 빈(Bean)이라고 하는 객체를 생성, 구성, 제공하는 역할을 합니다. 빈(Bean)은 Spring에서 관리하는 객체를 의미합니다.

## 왜 ApplicationContext를 얻어야 하는가?

여러 빈들이 서로 상호작용을 할 때, 특정 위치에서 ApplicationContext를 접근해야 하는 경우가 종종 있습니다. 예를 들어, 동적으로 빈을 조회하거나 이벤트를 발행할 때 이를 사용할 수 있습니다. 

## 방법 1: `ApplicationContextAware` 인터페이스 구현하기

`ApplicationContextAware` 인터페이스를 구현하여 현재 ApplicationContext를 얻을 수 있습니다.

```java
public class MyBean implements ApplicationContextAware {
    private static ApplicationContext context;

    @Override
    public void setApplicationContext(ApplicationContext context) throws BeansException {
        MyBean.context = context;
    }

    public static ApplicationContext getApplicationContext() {
        return context;
    }
}
```

## 방법 2: `@Autowired` 사용하기

`@Autowired` 애노테이션을 사용하여 ApplicationContext를 주입받을 수 있습니다.

```java
public class MyOtherBean {
    @Autowired
    private ApplicationContext context;
}
```

## 방법 3: `ApplicationListener<ContextRefreshedEvent>` 이벤트 사용하기

Spring에서 제공하는 `ContextRefreshedEvent` 이벤트를 사용하여 ApplicationContext를 얻을 수 있습니다.

```java
public class MyEventListener implements ApplicationListener<ContextRefreshedEvent> {
    private ApplicationContext context;

    @Override
    public void onApplicationEvent(ContextRefreshedEvent event) {
        context = event.getApplicationContext();
    }
}
```

## 주의사항

어떤 방법을 사용하든, ApplicationContext는 빈의 생명주기에 민감하게 반응합니다. 따라서 이를 적절하게 관리하는 것이 중요합니다.

## 결론

Spring에서 ApplicationContext를 얻는 방법에는 여러 가지가 있습니다. 당신의 프로젝트 상황과 요구에 따라 적절한 방법을 선택하면 됩니다. 이러한 방법들은 각각의 상황과 요구에 따라 유용하게 사용될 수 있습니다.