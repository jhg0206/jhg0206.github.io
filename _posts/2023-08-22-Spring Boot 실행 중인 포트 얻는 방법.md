---
title: Spring Boot 실행 중인 포트 얻는 방법
date: 2023-08-22 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## Spring Boot 이란?

Spring Boot는 Java로 개발된 웹 애플리케이션을 빠르고 쉽게 실행할 수 있는 프레임워크입니다. 이 프레임워크를 사용하면 복잡한 설정 없이도 손쉽게 웹 서버를 구동할 수 있습니다. 이제 이 훌륭한 도구를 이용하면서 실행 중인 포트 번호를 어떻게 알 수 있는지 알아보겠습니다.

## 실행 중인 포트 얻는 첫번째 방법: `ApplicationListener`

`ApplicationListener`는 Spring Boot에서 제공하는 인터페이스로, 애플리케이션의 여러 사건들에 대한 처리를 담당합니다. `WebServerInitializedEvent`라는 이벤트를 이용하면 현재 실행 중인 웹 서버의 포트를 알아낼 수 있습니다.

```java
import org.springframework.boot.web.context.WebServerInitializedEvent;
import org.springframework.context.ApplicationListener;

public class PortListener implements ApplicationListener<WebServerInitializedEvent> {
    private int port;
  
    @Override
    public void onApplicationEvent(WebServerInitializedEvent event) {
        this.port = event.getWebServer().getPort();
    }
  
    public int getPort() {
        return port;
    }
}
```

이 코드를 프로젝트에 추가하면, 웹 서버가 초기화되면서 포트 정보를 가져올 수 있습니다.

## 실행 중인 포트 얻는 두번째 방법: `Environment API`

Spring Framework에서는 `Environment` API를 제공합니다. 이 API를 사용하면 실행 중인 애플리케이션의 환경 정보를 알 수 있습니다.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;

public class PortService {
    @Autowired
    private Environment environment;
  
    public int getPort() {
        return Integer.parseInt(environment.getProperty("local.server.port"));
    }
}
```

`Environment` 객체를 주입받아(`Autowired`), `getProperty` 메서드를 사용하면 `local.server.port` 정보를 얻을 수 있습니다.

## 정리

Spring Boot에서는 주로 두 가지 방법으로 실행 중인 포트를 알아낼 수 있습니다. 첫번째는 `ApplicationListener`를 이용하는 것이고, 두번째는 `Environment API`를 활용하는 것입니다. 두 방법 모두 간단하고 효율적이므로, 본인의 프로젝트에 맞게 선택해서 사용하면 됩니다.