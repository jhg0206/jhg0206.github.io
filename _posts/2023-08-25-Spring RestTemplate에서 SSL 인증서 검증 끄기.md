---
title: Spring RestTemplate에서 SSL 인증서 검증 끄기
date: 2023-08-25 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
  - SSL인증서
---
## 문제 상황

개발자들이 Spring RestTemplate을 사용할 때, 로컬 환경이나 테스트 서버에서 SSL 인증서 검증을 끄고 싶은 상황이 발생할 수 있다. 이럴 때 어떻게 할 수 있는지 알아보자.

## SSL 인증서란 무엇인가?

SSL 인증서는 웹 서버와 사용자의 브라우저 사이의 정보를 암호화하여 보안을 유지하는 기술이다. 여기서 SSL은 'Secure Sockets Layer'의 약자로, 보안 소켓 계층을 의미한다. SSL 인증서는 특히 금융거래나 개인 정보를 다루는 웹 사이트에서 중요하다.

## `TrustSelfSignedStrategy` 활용

가장 간단한 방법은 `TrustSelfSignedStrategy` 클래스를 사용하는 것이다. 이 클래스는 Apache HttpClient 라이브러리에 포함되어 있다. 이 클래스를 활용하면 모든 SSL 인증서를 신뢰할 수 있다.

```java
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.springframework.http.client.HttpComponentsClientHttpRequestFactory;
import org.springframework.web.client.RestTemplate;

CloseableHttpClient httpClient
  = HttpClients.custom()
                .setSslcontext(sslContext)
                .setSSLHostnameVerifier(NoopHostnameVerifier.INSTANCE)
                .build();
HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory(httpClient);

RestTemplate restTemplate = new RestTemplate(factory);
```

## Java의 `TrustManager`를 커스터마이징

더 복잡한 설정을 원한다면, Java의 `TrustManager`를 커스터마이징할 수 있다. 이를 통해 특정 인증서만 허용하거나, 특정 조건에 따라 인증서를 거부할 수 있다.

```java
import javax.net.ssl.SSLContext;
import javax.net.ssl.TrustManager;
import javax.net.ssl.X509TrustManager;

public class TrustAllCertificates implements X509TrustManager {
  public void checkClientTrusted(java.security.cert.X509Certificate[] certs, String authType) {}
  public void checkServerTrusted(java.security.cert.X509Certificate[] certs, String authType) {}
  public java.security.cert.X509Certificate[] getAcceptedIssuers() { return null; }
}

SSLContext sslContext = SSLContext.getInstance("TLS");
sslContext.init(null, new TrustManager[] {new TrustAllCertificates()}, new java.security.SecureRandom());
```

## 주의사항: `NoopHostnameVerifier.INSTANCE`

위의 코드 예제에서 사용된 `NoopHostnameVerifier.INSTANCE`는 모든 호스트 이름을 신뢰한다는 것을 의미한다. 실제 상용 환경에서는 이러한 설정을 사용하지 않는 것이 좋다.

## 결론

Spring RestTemplate에서 SSL 인증서 검증을 끄는 방법은 여러 가지가 있다. 개발 환경이나 특수한 상황에서만 이러한 설정을 사용하고, 실제 상용 환경에서는 꼭 SSL 인증서 검증을 활성화 해야 한다.