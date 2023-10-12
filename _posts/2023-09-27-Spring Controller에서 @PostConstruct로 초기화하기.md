---
title: Spring Controller에서 @PostConstruct로 초기화하기
date: 2023-09-27 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringController
  - PostConstruct
---
## 왜 `init()` 메서드가 필요할까?

Spring Framework에서 컨트롤러(Controller)를 사용할 때 종종 초기 설정이 필요하다. 예를 들어, 데이터베이스에서 몇몇 데이터를 미리 가져와야 하는 경우, 이러한 초기화 작업을 위해 `init()` 메서드를 사용하곤 했다. `init()` 메서드는 서블릿 초기화 메서드에서 영감을 받아 사용되었으며, 주로 XML 기반의 Spring 설정에서 사용되었다.

## 어노테이션 기반에서는 어떻게?

XML 설정을 사용하지 않고 어노테이션 기반으로 Spring을 사용하려면 어떻게 초기화할까? 이런 경우에는 `@PostConstruct` 어노테이션을 사용한다. 이 어노테이션은 클래스가 인스턴스화되고 모든 의존성이 주입된 후에 실행되는 메서드에 붙인다.

```java
import javax.annotation.PostConstruct;

@Controller
public class MyController {
    @PostConstruct
    public void init() {
        // 초기화 코드
    }
}
```

## `@PostConstruct`와 `init()` 메서드의 차이

`@PostConstruct`는 Java EE 표준이므로 Spring 외의 다른 프레임워크에서도 사용할 수 있다. 반면에 `init()` 메서드는 Spring에서만 특별한 의미를 가진다. 또한, `@PostConstruct`를 사용하면 별도의 설정 없이도 메서드가 자동으로 호출되기 때문에 코드가 더 간결해진다.

## 주의사항

1. `@PostConstruct` 어노테이션이 붙은 메서드는 반환 타입이 `void`이어야 하며, 매개변수가 없어야 한다.
2. 한 클래스에 `@PostConstruct` 어노테이션이 붙은 메서드는 하나만 있어야 한다.
3. `@PostConstruct`는 스프링 빈이 완전히 생성되고 나서 실행되므로 의존성 주입이 완료된 후 사용해야 한다.

## 결론

어노테이션 기반의 Spring에서 초기화 작업을 할 때는 `@PostConstruct`를 사용하면 간단하고 효율적이다. 이를 통해 초기 설정을 쉽게 처리할 수 있으므로 개발 시간을 단축할 수 있다.