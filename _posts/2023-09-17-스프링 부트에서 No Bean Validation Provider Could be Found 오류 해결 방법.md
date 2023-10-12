---
title: 스프링 부트에서 No Bean Validation Provider Could be Found 오류 해결 방법
date: 2023-09-17 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot오류
---
## 오류 개요

스프링 부트(Spring Boot) 프로젝트를 진행하면서 "Unable to create a Configuration because no Bean Validation provider could be found" 이라는 오류 메시지가 나타나는 경우가 있습니다. 이 문제는 스프링 부트 애플리케이션에서 데이터 유효성 검사(bean validation)를 수행하기 위한 제공자(provider)를 찾을 수 없다는 것을 의미합니다.

## 원인 파악

이 오류는 주로 의존성 설정이 잘못되었거나 필요한 라이브러리가 누락되었을 때 발생합니다. 스프링 부트는 기본적으로 Hibernate Validator를 사용하여 데이터 유효성 검사를 수행합니다. 그런데 이 라이브러리가 프로젝트에 포함되어 있지 않으면, 위와 같은 오류 메시지가 출력됩니다.

## 해결 방법

### 의존성 확인

먼저 `pom.xml` 파일이나 `build.gradle` 파일에서 Hibernate Validator 라이브러리가 정확히 추가되었는지 확인합니다. Maven을 사용하는 경우 다음과 같은 의존성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

Gradle을 사용하는 경우에는 다음과 같이 추가합니다.

```groovy
dependencies {
    implementation 'org.hibernate.validator:hibernate-validator'
}
```

### 빌드와 재시작

의존성을 추가한 후 프로젝트를 다시 빌드하고 애플리케이션을 재시작합니다. 이 과정을 거치면 일반적으로 해당 오류는 해결됩니다.

### 코드 검토

의존성 문제가 아니라면, `@Valid` 어노테이션이나 다른 유효성 검사 관련 코드가 올바르게 작성되었는지 검토합니다. 잘못된 설정이나 코드 누락이 문제를 일으킬 수 있습니다.

## 정리

"No Bean Validation Provider Could be Found" 오류는 주로 의존성 누락이나 잘못된 설정 때문에 발생합니다. 해결 방법은 의존성을 확인하고 필요한 라이브러리를 추가하는 것입니다. 이러한 단계를 따르면 문제를 효과적으로 해결할 수 있습니다.