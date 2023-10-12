---
title: Spring의 WebMvcConfigurerAdapter가 Deprecated된 이유와 대체 방안
date: 2023-08-29 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - WebMvcConfigurerAdapter
  - Deprecated
---
## WebMvcConfigurerAdapter가 Deprecated된 배경

`WebMvcConfigurerAdapter` 클래스는 이전에 Spring MVC의 설정을 쉽게 도와주는 목적으로 사용되었습니다. 하지만, 이 클래스가 `Deprecated`라는 표시를 받게 된 이유는 Spring 5.0 버전 이상에서 더 효율적이고 유연한 설정을 지원하기 위해서입니다. `Deprecated`란 개발자가 더 이상 이용하면 안 되는 기능이나 클래스를 의미합니다. 대신 `WebMvcConfigurer` 인터페이스를 직접 구현하면 동일한 설정을 적용할 수 있습니다.

## WebMvcConfigurer를 사용하는 방법

`WebMvcConfigurer` 인터페이스를 사용하려면 다음과 같이 구현하면 됩니다. 이는 `WebMvcConfigurerAdapter`를 사용하는 것보다 더 나은 접근법입니다.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
  // 설정 코드
}
```

## 주의할 사항

`WebMvcConfigurerAdapter`를 그대로 사용하는 것은 권장되지 않지만, 이미 프로젝트에 적용되어 있다면 큰 문제는 아닙니다. 단지, 미래에 업데이트가 되거나 유지 보수를 할 때 문제가 생길 수 있으므로 변경을 권장합니다.

## 정리

Spring 5.0 이상에서는 `WebMvcConfigurerAdapter` 대신 `WebMvcConfigurer` 인터페이스를 구현하여 사용하는 것이 좋습니다. 이 변경은 더 효율적이고 유연한 코드 작성을 가능하게 하므로, 가능한 빨리 적용해 보는 것이 좋습니다.