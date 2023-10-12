---
title: Shiro와 Spring Security 비교
date: 2023-08-30 20:00:00 +0900
categories:
  - Spring
tags:
  - Shiro
  - SpringSecurity
---
## Shiro는 무엇인가요??

Shiro는 Apache Software Foundation에서 개발한 보안 프레임워크입니다. 인증(Authentication), 권한 부여(Authorization), 세션 관리(Session Management) 등을 쉽게 처리할 수 있습니다.

## 무엇은 Spring Security?

Spring Security는 Spring Framework의 일부로, 엔터프라이즈 애플리케이션 보안을 위한 풍부한 기능을 제공합니다. 인증, 권한 부여, 공격 방어 등 다양한 보안 기능이 포함되어 있습니다.

## 주요 차이점

### 설정의 유연성
Shiro는 설정이 상대적으로 단순하고 유연합니다. 반면에 Spring Security는 많은 설정 옵션을 제공하기 때문에 복잡할 수 있습니다.

### 커뮤니티와 지원
Spring Security는 더 큰 커뮤니티와 더 많은 문서를 가지고 있습니다. 이는 문제 해결에 있어 더 많은 자원을 제공한다는 뜻입니다.

### 세션 관리
Shiro에서는 세션 관리가 더 강화되어 있습니다. 즉, 사용자가 여러 디바이스에서 동시에 로그인할 수 있도록 관리가 가능합니다.

### 통합성
Spring Security는 Spring Framework와의 통합이 잘 되어 있습니다. 따라서 Spring을 이미 사용하고 있다면 Spring Security가 더 나을 수 있습니다.

### 성능
두 프레임워크 모두 성능이 우수하며, 성능 차이는 미미하다고 볼 수 있습니다.

## 어떤 것을 선택할까?

Shiro와 Spring Security 모두 유용한 보안 기능을 제공합니다. 프로젝트의 요구사항, 사용하는 기술 스택, 그리고 팀의 능력에 따라 선택이 달라질 수 있습니다. 예를 들어, Spring Framework를 이미 사용하고 있다면 Spring Security가 더 적합할 수 있습니다. 반대로 더 단순하고 유연한 설정을 원한다면 Shiro가 좋을 수 있습니다.