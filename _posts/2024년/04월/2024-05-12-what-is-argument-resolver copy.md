---
title: "[Spring] Spring MVC의 ArgumentResolver란?"
excerpt: "Spring MVC의 ArgumentResolver란? ArgumentResolver의 주요 기능은? ArgumentResolver 구현 예제는? ArgumentResolver 등록 방법은?"
date: 2024-05-12
last_modified_at: 2024-05-12
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring MVC`의 `ArgumentResolver`란?

## 2. Answer

`ArgumentResolver`는 `Spring MVC`에서 컨트롤러 메서드의 파라미터를 동적으로 결정하고 처리하는 매커니즘을 제공한다. 이는 `Spring MVC`의 유연성을 크게 향상시키며, 개발자가 커스텀 파라미터 타입을 컨트롤러에 손쉽게 통합할 수 있도록 도와준다. `ArgumentResolver`는 컨트롤러 메서드 호출 전에 특정 조건에 따라 파라미터 값을 준비하고 제공하는 역할을 한다.

## 3. Detail

### A. ArgumentResolver의 주요 기능

`ArgumentResolver`는 컨트롤러 메서드의 파라미터에 대해 아래와 같은 처리를 할 수 있다.

* **사용자 정의 파라미터 타입 처리**: 개발자가 정의한 특정 클래스 타입의 파라미터를 처리하고자 할 때 사용한다.

* **HTTP request 정보의 추출 및 변환**: Request에서 특정 데이터를 추출하거나 변환하여 컨트롤러 메서드의 파라미터로 제공한다.

* **보안 및 검증 로직 통합**: 파라미터를 컨트롤러로 전달하기 전에 검증하거나 수정하는 로직을 적용할 수 있다.

### B. ArgumentResolver 구현 예제

```java
@Component
public class UserContextArgumentResolver implements HandlerMethodArgumentResolver {

  @Override
  public boolean supportsParameter(MethodParameter parameter) {
      return UserContext.class.isAssignableFrom(parameter.getParameterType());
  }

  @Override
  public Object resolveArgument(MethodParameter parameter, ModelAndViewContainer mavContainer, NativeWebRequest webRequest, WebDataBinderFactory binderFactory) throws Exception {
    HttpServletRequest request = (HttpServletRequest) webRequest.getNativeRequest();
    String userToken = request.getHeader("Authorization");
    // 토큰에서 사용자 정보 추출 로직
    return new UserContext(userToken);
  }
}

```

### C. ArgumentResolver 등록

`ArgumentResolver`를 시스템에 통합하려면 `Spring MVC` 설정에 등록해야 한다. 이는 `WebMvcConfigurer` 인터페이스를 구현하여 설정할 수 있다.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Autowired
    private UserContextArgumentResolver userContextArgumentResolver;

    @Override
    public void addArgumentResolvers(List<HandlerMethodArgumentResolver> resolvers) {
        resolvers.add(userContextArgumentResolver);
    }
}

```

이 설정을 통해 `UserContextArgumentResolver`가 `Spring MVC` 프레임워크의 request 처리 파이프라인에 통합되어, 지정된 파라미터에 대해 자동으로 실행된다.

## 4. Reference

None