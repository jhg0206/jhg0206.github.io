---
title: Spring Boot에서 application.yml로부터 Map 주입하기
date: 2023-09-10 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 개요

Spring Boot에서 `application.yml` 파일을 사용하면 애플리케이션의 설정 정보를 관리할 수 있습니다. 이 글에서는 `application.yml` 파일에서 Map 구조를 어떻게 Java 클래스에 주입하는지에 대해 자세히 설명하겠습니다.

## application.yml 파일 설정

먼저 `application.yml` 파일에서 설정 정보를 Map 형태로 정의해야 합니다. 예를 들어, 학생 이름과 성적을 매핑하고 싶다면 다음과 같이 작성할 수 있습니다.

```yml
students:
  Alice: 90
  Bob: 85
  Carol: 92
```

## Java 클래스에 Map 주입하기

### `@ConfigurationProperties` 사용

Spring Boot에서는 `@ConfigurationProperties` 어노테이션을 사용하여 외부 설정을 Java 클래스에 주입할 수 있습니다. 이 어노테이션을 사용하면 위에서 정의한 Map을 Java 클래스에 쉽게 연결할 수 있습니다.

```java
import java.util.Map;
import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties(prefix = "students")
public class StudentConfig {
    private Map<String, Integer> scores;

    // Getter와 Setter
}
```

### `@Value` 어노테이션 사용

`@Value` 어노테이션을 사용하는 또 다른 방법도 있습니다. 이 방법은 다음과 같습니다.

```java
import java.util.Map;
import org.springframework.beans.factory.annotation.Value;

public class StudentConfig {
    @Value("#{${students}}")
    private Map<String, Integer> scores;

    // Getter와 Setter
}
```

## 주의할 점

`@ConfigurationProperties`와 `@Value` 중 어떤 것을 사용할지 선택할 때, `@ConfigurationProperties`는 타입 안전성(Type Safety)을 제공하기 때문에 추천됩니다. 타입 안전성이란, 데이터의 타입이 예상대로 동작하는 것을 말합니다.

## 에러 해결

만약 이 과정에서 `NullPointerException`이나 다른 에러가 발생한다면, 주입되지 않은 Map 변수를 사용하려고 했을 가능성이 있습니다. 이 경우에는 설정 파일과 Java 코드의 매핑이 제대로 이루어졌는지 확인해보아야 합니다.

## 요약

Spring Boot에서 `application.yml` 파일의 Map 정보를 Java 클래스에 주입하는 것은 `@ConfigurationProperties` 또는 `@Value` 어노테이션을 사용하여 간단히 할 수 있습니다. 이러한 기능을 활용하면 애플리케이션의 설정을 더 효율적으로 관리할 수 있습니다.