---
title: "[Spring] Spring MVC의 DispatcherServlet이란?"
excerpt: "Spring MVC의 DispatcherServlet이란? DispatcherServlet의 구성 요소는? DispatcherServlet의 작동 원리는?"
date: 2024-05-07
last_modified_at: 2024-05-07
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring MVC`의 `DispatcherServlet`이란?

## 2. Answer

### A. 구성 요소 - HandlerMapping

`HandlerMapping`은 들어오는 요청 URL을 처리할 핸들러(컨트롤러 메서드)로 라우팅하는 역할을 한다. 요청의 URL 패턴이나 HTTP 메서드 타입 등의 정보를 기반으로 적절한 핸들러를 결정한다. 대표적인 구현체로는 `RequestMappingHandlerMapping`이 있으며, 이는 `@RequestMapping` annotation을 사용하여 request를 매핑한다.

### B. 구성 요소 - HandlerAdapter

`handlerAdapter`는 `DispatcherServlet`이 결정한 핸들러를 실행할 수 있게 돕는다. 이 구성 요소는 핸들러 메서드의 호출을 처리하고, 실행 결과를 `ModelAndView` 객체로 변환하여 반환한다. 이를 통해 다양한 유형의 핸들러를 지원하며, 핸들러의 반환 타입에 상관없이 일관된 방식으로 response를 처리할 수 있다.

### C. 구성 요소 - ViewResolver

`ViewResolver`는 `ModelAndView` 객체에 지정된 뷰 이름을 기반으로 실제 뷰 객체를 찾고 생성한다. 예를 들어, 뷰 이름이 "home"이면, 해당 이름을 갖는 뷰 템플릿 파일을 찾아 렌더링 과정을 진행한다. 일반적으로 JSP, Thymeleaf, FreeMarker 같은 다양한 뷰 기술을 지원한다.

### D. 구성 요소 - HandlerExceptionResolver

이 구성 요소는 요청 처리 중 발생하는 예외를 관리한다. `HandlerExceptionResolver`는 발생한 예외를 적절히 처리하고 사용자에게 보여줄 에러 페이지를 결정할 수 있다. 개발자는 `@ExceptionHandler` annotation을 사용하여 커스텀 예외 처리 로직을 구현할 수 있다.

### E. DispatcherServlet의 작동 원리

`DispatcherServlet`은 위의 구성 요소들을 활용하여 웹 request를 처리한다. Request가 들어오면 다음과 같은 순서로 작업을 진행한다.

1. Request 수신: 모든 HTTP request는 먼저 `DispatcherServlet`에 도달한다.
1. `Handler Mapping`: `DispatcherServlet`은 `HandlerMapping`을 사용하여 요청 URL과 매칭되는 적절한 핸들러를 찾는다.
1. `Handler Adapter` 호출: 선택된 핸들러를 실행하기 위해 `HandlerAdapter`를 호출한다.
1. 핸들러 실행 및 결과 반환: 핸들러는 비즈니스 로직을 수행하고 결과를 `ModelAndView`로 반환한다. 이 객체는 뷰 이름과 모델 데이터를 포함한다.
1. `View Resolver` 호출: `DispatcherServlet`은 `ViewResolver`를 사용하여 `ModelAndView`에서 지정된 뷰 이름에 해당하는 실제 뷰 객체를 찾는다. `ViewResolver`는 뷰 이름을 뷰 구현체(예: JSP 파일, Thymeleaf 템플릿)로 해석하고, 이를 렌더링할 준비를 한다.
1. 뷰 렌더링: `ViewResolver`에 의해 결정된 뷰 객체가 최종적으로 렌더링되며, 여기에 모델 데이터가 적용되어 사용자에게 보여질 최종 응답 페이지를 생성한다.
1. 예외 처리: 처리 중에 발생한 예외는 `HandlerExceptionResolver`를 통해 관리되며, 적절한 예외 처리 로직이 실행된다.

## 3. Detail

None

## 4. Reference

None