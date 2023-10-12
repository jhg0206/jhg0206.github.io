---
title: Title
date: 2023-09-21 20:00:00 +0900
categories:
  - Spring
tags:
  - JSON
  - Java
---
## 에러 상황 소개

프로그래밍에서는 자주 에러를 마주칩니다. 특히 자바와 JSON을 다룰 때, "No String Argument Constructor"라는 에러가 자주 발생할 수 있습니다. 이 문서에서는 이 에러가 왜 발생하는지, 그리고 어떻게 해결할 수 있는지에 대해 설명합니다.

## 에러 원인 분석

"No String Argument Constructor" 에러는 대체로 자바 객체를 JSON 형태로 변환하거나, 그 반대의 과정에서 발생합니다. 자바에서는 객체를 생성할 때 생성자(Constructor)라는 것을 사용합니다. 이 생성자는 객체가 어떤 초기 값을 가질지 설정해줍니다.

자바 객체를 JSON으로 변환하려면 해당 객체의 클래스에 빈 생성자(파라미터가 없는 생성자)가 있어야 합니다. 만약 빈 생성자가 없다면, JSON 라이브러리는 어떻게 객체를 생성해야 할지 모르기 때문에 에러가 발생합니다.

## 해결 방안

### 빈 생성자 추가하기

가장 간단한 해결 방법은 빈 생성자를 클래스에 추가하는 것입니다. 이렇게 하면 JSON 라이브러리가 객체를 쉽게 생성할 수 있습니다.

```java
public class MyClass {
    private String name;
    
    public MyClass() {
        // 빈 생성자
    }
    
    public MyClass(String name) {
        this.name = name;
    }
}
```

### @JsonCreator 어노테이션 사용하기

빈 생성자를 추가할 수 없는 상황이라면, `@JsonCreator` 어노테이션을 사용할 수 있습니다. 이 어노테이션은 JSON 라이브러리에게 어떤 생성자를 사용해야 하는지 알려줍니다.

```java
public class MyClass {
    private String name;
    
    @JsonCreator
    public MyClass(@JsonProperty("name") String name) {
        this.name = name;
    }
}
```

이러한 방법을 통해 "No String Argument Constructor" 에러를 해결할 수 있습니다. 효과적인 코드 작성을 위해 이러한 에러와 해결 방법을 잘 이해하는 것이 중요합니다.