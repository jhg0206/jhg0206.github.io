---
title: RestTemplate에서 HTTP GET 요청 시 헤더 설정하기
date: 2023-08-28 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
  - HTTP
  - GET요청
---
## 개요
Spring Framework에서 `RestTemplate`을 사용하여 HTTP GET 요청을 보낼 때, 헤더를 설정하는 방법을 자세하게 설명합니다.

## RestTemplate이란 무엇인가?
`RestTemplate`은 Spring Framework에서 제공하는 클래스로, 웹 서비스에 HTTP 요청을 보내고 응답을 받는 역할을 합니다. 이 클래스를 사용하면 웹 API와 쉽게 통신할 수 있습니다.

## 헤더를 포함한 HTTP GET 요청 보내기

헤더를 추가하여 HTTP GET 요청을 보내려면, `HttpHeaders` 객체를 사용해야 합니다. `HttpHeaders` 객체에 헤더 정보를 입력한 후, 이를 `HttpEntity` 객체에 적용하면 됩니다. 

### 예시 코드

```java
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.web.client.RestTemplate;

public class Application {
    public static void main(String[] args) {
        RestTemplate restTemplate = new RestTemplate();
        
        HttpHeaders headers = new HttpHeaders();
        headers.set("Authorization", "Bearer your_token_here");
        
        HttpEntity<String> entity = new HttpEntity<>("parameters", headers);
        
        String result = restTemplate.exchange(
            "http://example.com/api/resource", 
            HttpMethod.GET, 
            entity, 
            String.class
        ).getBody();
        
        System.out.println(result);
    }
}
```

위의 코드는 `Authorization` 헤더에 토큰 값을 설정하여 HTTP GET 요청을 보냅니다.

## 주의사항
헤더의 정보가 민감한 경우, 이를 안전하게 관리하는 방법을 고려해야 합니다. 예를 들어, 헤더에 포함된 토큰은 외부에 노출되지 않도록 주의해야 합니다.

## 정리
`RestTemplate`을 사용하여 헤더를 포함한 HTTP GET 요청을 보내는 것은 꽤 간단합니다. `HttpHeaders` 객체를 이용하여 필요한 헤더를 설정한 뒤, `HttpEntity` 객체에 적용하면 되는 것입니다. 이를 통해 웹 서비스와 효율적으로 통신할 수 있습니다.