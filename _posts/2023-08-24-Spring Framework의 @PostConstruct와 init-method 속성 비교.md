---
title: Spring Framework의 @PostConstruct와 init-method 속성 비교
date: 2023-08-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - 프레임워크
  - Postconstuct
  - init-method
---
## @PostConstruct 어노테이션
`@PostConstruct`는 자바에서 제공하는 어노테이션입니다. 이 어노테이션이 붙은 메서드는 객체가 생성된 후 자동으로 호출됩니다. 이 방식의 장점은 다음과 같습니다.

- 표준 자바 어노테이션입니다. Spring 외의 다른 자바 환경에서도 사용할 수 있습니다.
- 코드가 간결하고 명확합니다.

```java
import javax.annotation.PostConstruct;

public class MyBean {
    @PostConstruct
    public void init() {
        // 초기화 로직
    }
}
```

## init-method 속성
`init-method` 속성은 Spring XML 설정에서 사용합니다. 이 속성을 이용하면, 해당 메서드가 객체 초기화 후에 호출됩니다.

```xml
<bean id="myBean" class="com.example.MyBean" init-method="init"/>
```

이 방식의 장점은 다음과 같습니다.

- XML 설정에서 초기화 메서드를 명시적으로 설정할 수 있습니다.
- 여러 빈(Bean)에 동일한 초기화 메서드를 적용할 수 있습니다.

## 둘 중 어느 것을 사용해야 할까?
두 방식 모두 유용하지만 목적과 환경에 따라 선택이 달라집니다.

- `@PostConstruct`는 표준화된 방법이므로 다른 자바 환경에서도 활용할 수 있습니다.
- `init-method`는 XML 설정에서만 사용되므로, XML을 주로 사용하는 프로젝트에 더 적합합니다.

## 결론
`@PostConstruct`와 `init-method`는 모두 Spring에서 객체 초기화를 위한 방법입니다. 둘 중 어느 것이 더 나은지는 개발 환경과 필요에 따라 다릅니다. 선택의 기준은 프로젝트의 요구사항과 개발 팀의 선호도에 있습니다. 이 글을 통해 두 초기화 방법의 차이와 사용 케이스를 이해할 수 있기를 바랍니다.