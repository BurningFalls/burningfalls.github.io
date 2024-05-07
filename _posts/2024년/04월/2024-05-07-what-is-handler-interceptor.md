---
title: "[Spring] Spring MVC의 핸들러 인터셉터(Handler Interceptor)란?"
excerpt: "Spring MVC의 핸들러 인터셉터(Handler Interceptor)란? 핸들러 인터셉터의 주요 메서드는? 핸들러 인터셉터 구현 예제는? 핸들러 인터셉터 등록 예제는?"
date: 2024-05-07
last_modified_at: 2024-05-07
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring MVC`의 `핸들러 인터셉터(Handler Interceptor)`란?

## 2. Answer

`핸들러 인터셉터(Handler Interceptor)`는 `Spring MVC`에서 매우 유용한 구성 요소로서, 컨트롤러(핸들러) 실행의 전과 후, 그리고 request 완료 후에 특정 로직을 수행할 수 있게 해준다. `HandlerInterceptor`는 `AOP(Aspect-Oriented Programming)`의 원칙을 웹 request 처리에 적용하여, 교차 관심사(cross-cutting concerns)를 효과적으로 관리할 수 있도록 돕는다.

## 3. Detail

### A. 핸들러 인터셉터의 주요 메서드

`HandlerInterceptor` 인터페이스는 주로 세 가지 메서드를 정의하며, 이를 구현하여 원하는 기능을 실행할 수 있다.

`preHandle(HttpServletRequest request, HttpServletResponse response, Object handler):`

* 컨트롤러 메서드가 실행되기 전에 호출된다.
* 이 메서드는 `boolean` 값을 반환하며, `true`를 반환하면 request 처리가 계속되고, `false`를 반환하면 request 처리가 중단된다.
* 인증 체크, 로깅, request 정보의 사전 처리 등에 사용할 수 있다.

`postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView):`

* 컨트롤러 메서드가 실행된 후, 그러나 뷰가 렌더링되기 전에 호출된다.
* Response 데이터를 수정하거나 추가 로직을 실행하는 데 사용할 수 있다.
* `ModelAndView` 객체를 조작하여 컨트롤러에서 생성된 모델 데이터를 변경하거나, 다른 뷰를 선택할 수 있다.

`afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex):`

* Request 처리의 전체 과정이 완료된 후에 호출된다(뷰 렌더링 포함).
*  예외 발생 유무에 관계없이 실행되며, 리소스 정리나 후처리 로직을 수행하는 데 사용된다.
* 로그 기록이나, 실행 시간 계산 등의 작업에 유용하다.

### B. 핸들러 인터셉터 구현 예제

```java
@Component
public class MyInterceptor implements HandlerInterceptor {
  @Override
  public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    System.out.println("Pre Handle method is Calling");
    return true;
  }

  @Override
  public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
    System.out.println("Post Handle method is Calling");
  }

  @Override
  public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    System.out.println("Request and Response is completed");
  }
}
```

### C. 핸들러 인터셉터 등록

핸들러 인터셉터를 사용하기 위해서는 `Spring MVC` 구성에 인터셉터를 등록해야 한다. 이는 보통 `Java Config`에서 `WebMvcConfigurer` 인터페이스를 구현하는 클래스를 통해 이루어진다.

```java
@Configuration
pbulic class WebMvcConfig implements WebMvcConfigurer {
  @Autowired
  MyInterceptor myInterceptor;

  @Override
  public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(myInterceptor);
  }
}
```

이렇게 설정함으로써, `MyInterceptor`는 `Spring MVC`의 request 처리 파이프라인에 통합되어, 지정된 시점에 자동으로 실행된다. 핸들러 인터셉터를 통해 애플리케이션의 모듈성을 향상시키고, 중복 코드를 줄이며, 관리가 쉬운 코드베이스를 유지할 수 있다.

## 4. Reference

None