---
title: Spring Boot와 Spring Security 활용하여 CORS 설정하기
date: 2023-09-01 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - SpringSecurity
  - CORS
---
## CORS 란 무엇인가?

CORS(Cross-Origin Resource Sharing)는 웹 페이지가 다른 도메인에서 리소스를 요청할 수 있도록 하는 기술입니다. 예를 들어, 도메인 A의 웹 페이지가 도메인 B의 API를 호출하려면 도메인 B의 서버는 CORS 설정이 필요합니다.

## Spring Boot에서 CORS 설정하기

### Java Config 방식

Spring Boot에서는 `WebMvcConfigurer` 인터페이스를 구현하여 CORS 설정을 할 수 있습니다.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
            .allowedOrigins("http://localhost:8080");
    }
}
```

이 코드는 모든 경로(`/**`)에 대해 `http://localhost:8080`에서 오는 요청을 허용합니다.

### @CrossOrigin 어노테이션

특정 컨트롤러나 메소드에만 CORS 설정을 하고 싶다면, `@CrossOrigin` 어노테이션을 사용할 수 있습니다.

```java
@RestController
public class MyController {
    @CrossOrigin(origins = "http://localhost:8080")
    @GetMapping("/api/data")
    public Data getData() {
        // 코드 구현
    }
}
```

이 설정은 `/api/data` 경로에 대해 `http://localhost:8080`에서 오는 요청만 허용합니다.

## Spring Security와 CORS 설정하기

Spring Security를 사용하고 있다면, 별도로 CORS 설정을 해주어야 합니다. 이때 `HttpSecurity` 객체를 활용해야 합니다.

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.cors().and()
            // Spring Security 설정 코드
    }
}
```

여기서 `http.cors()` 메소드 호출이 CORS 설정을 활성화합니다.

### CORS 필터 사용

`CorsFilter`를 사용하면, 좀 더 세밀한 설정이 가능합니다. `UrlBasedCorsConfigurationSource` 객체를 생성하여 필터에 전달해야 합니다.

```java
@Bean
public CorsFilter corsFilter() {
    UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
    CorsConfiguration config = new CorsConfiguration();
    // CORS 설정 추가
    source.registerCorsConfiguration("/**", config);
    return new CorsFilter(source);
}
```

## 정리

Spring Boot와 Spring Security에서 CORS 설정을 하려면 Java Config 방식, 어노테이션, Spring Security 설정 등 다양한 방법이 있습니다. 이러한 설정을 통해 웹 애플리케이션의 보안성과 사용성을 높일 수 있습니다.