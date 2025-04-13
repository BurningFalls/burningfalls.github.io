---
title: "[Spring] Spring Boot + Thymeleaf로 이해하는 서버 사이드 렌더링(SSR) 구조"
excerpt: "이 글에서는 Spring Boot와 Thymeleaf를 활용한 서버 사이드 렌더링(SSR)의 구조와 동작 방식을 상세히 설명합니다. JSP와의 비교부터 CSR과의 차이, SSR 페이지의 캐싱 최적화를 위한 Redis와 CDN 연계 전략까지 실제 애플리케이션 아키텍처 설계에 필요한 개념들을 단계별로 정리했습니다."
date: 2025-04-12
last_modified_at: 2025-04-12
categories:
  - java
tags:
  - spring-study
---

## 1. 서버 사이드 렌더링이란?

**SSR(Server Side Rendering)**이란, 클라이언트(브라우저)로부터 요청이 들어오면 **서버에서 HTML을 완성해서 브라우저에 전달**하는 렌더링 방식이다.
즉, 서버가 **데이터 + 뷰(View 템플릿)**를 조합해 **완성된 HTML 문서**를 만들어 내보낸다.

**SSR 작동 흐름**

1. 클라이언트가 URL 요청
2. 서버가 해당 요청에 맞는 **데이터를 조회**
3. 서버에서 HTML 템플릿을 **데이터와 함께 렌더링**
4. 완성된 HTML이 클라이언트에게 전송됨
5. 브라우저는 이 HTML을 바로 표시함

## 2. Java 진영의 SSR: Spring + Thymeleaf / JSP

📄 JSP(Java Server Pages)

* 과거부터 사용된 전통적인 SSR 기술
* `.jsp` 파일에서 HTML 안에 **Java 코드를 직접 삽입**
* 컨트롤러에서 `Model` 데이터를 넣고 뷰로 전달 -> HTML로 렌더링됨

```java
// Spring Controller 예시
@GetMapping("/hello")
public String hello(Model model) {
    model.addAttribute("name", "홍길동");
    return "hello"; // /WEB-INF/views/hello.jsp
}
```

```html
<!-- hello.jsp -->
<html>
<body>
  안녕하세요, ${name} 님!
</body>
</html>
```

✅ 서버에서 HTML이 렌더링되므로, 클라이언트는 HTML만 받아 화면에 바로 표시할 수 있다.

📄 Thymeleaf

* JSP의 한계를 보완한 **현대적인 템플릿 엔진**
* HTML 문법을 유지하면서 속성 기반으로 데이터 바인딩
* Spring Boot와 통합성이 뛰어남

```java
@GetMapping("/welcome")
public String welcome(Model model) {
    model.addAttribute("user", "이순신");
    return "welcome"; // templates/welcome.html
}
```

```html
<!-- welcome.html -->
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>
  <h1 th:text="'환영합니다, ' + ${user} + '님!'"></h1>
</body>
</html>
```

* 컨트롤러에서 데이터를 모델에 담으면 **Thymeleaf가 서버에서 HTML로 변환하여 렌더링**
* 결국 사용자는 완성된 HTML을 받아 바로 볼 수 있음

## 3. CSR과의 차이점

| 항목             | SSR(Spring + Thymeleaf/JSP)                        | CSR(React, Vue 등 SPA)                                 |
|------------------|----------------------------------------------------|--------------------------------------------------------|
| HTML 생성 위치    | **서버에서 생성**                                   | **브라우저에서 JS가 HTML 생성**                         |
| 초기 렌더링 속도  | 빠름 (HTML 즉시 표시)                                | JS 번들 로딩 후 렌더링되어 초기 속도 느릴 수 있음         |
| SEO 친화성        | 우수 (HTML 완성본 제공)                             | 기본적으로 불리 (동적 렌더링 → 크롤링 어려움)             |
| 서버 부하         | 클라이언트 요청마다 HTML 렌더링 부담 존재            | 서버는 API만 제공 → 상대적으로 부하 적음                 |
| 상태 관리         | 서버에서 View만 그려주고 별도 상태 관리 없음         | 클라이언트에서 상태 직접 관리 (Redux, Vuex 등 사용)      |

## 4. 캐싱 계층(Redis, CDN)과의 연계

**SSR은 요청마다 서버가 HTML을 생성하기 때문에**, 트래픽이 몰릴 경우 **서버 렌더링 속도 자체가 병목(bottleneck)**이 될 수 있다. 이를 **캐싱 계층(Redis, CDN 등)**과 적절히 연계하면 서버 부담을 크게 줄이고 응답 속도를 개선할 수 있다.

### ✅ Redis를 통한 SSR 결과 캐싱 (서버 캐시)

💡 개념

* SSR의 결과물인 **렌더링된 HTML 문자열 자체를 Redis에 저장**
* 동일한 요청이 들어오면 **DB/API 호출 및 렌더링을 생략하고 Redis에서 즉시 응답**

💻 사용 예시 (Next.js, Spring 등 공통 전략)

```text
요청 → Redis에 캐시 여부 확인
→ 있으면 캐시된 HTML 응답
→ 없으면 SSR 수행 + Redis 저장 → 클라이언트 응답
```

📦 Redis 캐싱 키 설계 예

```text
cacheKey = "page:/products/123"
TTL = 60초 ~ 300초 (짧은 주기로 만료)
```

✅ 효과

* 데이터가 자주 바뀌지 않는 페이지 (예: 블로그, 마케팅 페이지)에 매우 효과적
* SSR 수행 횟수 ↓ → DB/API 접근 ↓ → 서버 부하 급감

### ✅ CDN 캐시 연계 (엣지 캐시)

💡 개념

* **AWS CloudFront** 등을 사용해 **SSR 결과를 캐싱**
* 특정 경로의 HTML을 **CDN 엣지 서버에서 직접 응답**

⚙️ 캐시 제어 방식

```text
Cache-Control: public, max-age=300, s-maxage=600
Vary: Cookie
```

* `s-maxage`: CDN에서의 캐시 수명
* `Vary: Cookie`: 로그인 여부나 A/B 테스트 값에 따라 캐시 분기

✅ 효과
* 사용자 위치에서 가까운 엣지 서버가 응답 -> **지연 시간 대폭 감소**
* 서버 요청 자체를 차단하므로 **서버 부하 '0'화 가능**

### ✅ Redis + CDN 조합 전략

* **Redis**: SSR 백엔드 결과물 캐시 (서버 안쪽)
* **CDN**: 클라이언트 응답 캐시 (서버 바깥쪽)

🧠 예시 흐름

```text
1. 사용자가 SSR 페이지 요청
2. CDN 캐시 HIT → CDN 응답 (끝)
3. CDN MISS → SSR 서버로 전달
4. SSR 서버가 Redis 확인
    - Redis HIT → 응답 전달 + CDN에 저장
    - Redis MISS → 렌더링 수행 → Redis 저장 → 응답 전달 + CDN 저장
```

## 5. Spring Boot + Thymeleaf 작동 구조

▶ 1단계: 클라이언트 요청

```text
GET /hello
```

▶ 2단계: Spring Controller 처리

```java
@Controller
public class HelloController {

    @GetMapping("/hello")
    public String hello(Model model) {
        model.addAttribute("name", "홍길동");
        return "hello"; // hello.html
    }
}
```

* `Model` 객체에 데이터를 담는다 -> View에 전달됨
* `return` "hello"는 템플릿 파일 이름 (확장자 생략)

▶ 3단계: ViewResolver가 템플릿 경로 찾음

Spring Boot에서 기본 설정:

```text
src/main/resources/templates/hello.html
```

* 자동으로 **ThymeleafViewResolver**가 적용되어 `.html` 템플릿을 렌더링 대상으로 판단

▶ 4단계: Thymeleaf가 HTML 템플릿 렌더링

```html
<!-- hello.html -->
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h1 th:text="'안녕하세요, ' + ${name} + '님!'">Placeholder</h1>
  </body>
</html>
```

* `${name}` -> 모델에 있는 "홍길동"으로 치환됨
* 완성된 HTML은 다음과 같다:

```html
<h1>안녕하세요, 홍길동님!</h1>
```

▶ 5단계: 브라우저에 완성된 HTML 응답

* 브라우저는 서버로부터 **이미 완성된 HTML**을 받아 렌더링 -> SSR 완료

> Spring Boot가 실행되면, 내부적으로 Tomcat(WAS)이 올라가고
> `DispatcherServlet`이 `/` 경로에 기본으로 매핑되어 모든 요청을 가로챈다.
> 즉, 브라우저 요청은 항상 DispatcherServlet부터 시작된다.
>
> 전체 요청 처리 흐름은 아래와 같다.
> ```text
> 클라이언트 요청
> ↓
> DispatcherServlet (서블릿)
> ↓
> HandlerMapping (어떤 컨트롤러가 처리할지 결정)
> ↓
> Controller (@Controller, @RestController)
> ↓
> HandlerAdapter (컨트롤러 실행)
> ↓
> ModelAndView 반환 (또는 ResponseBody 변환)
> ↓
> ViewResolver (뷰 파일 결정)
> ↓
> View 렌더링 (Thymeleaf, JSP 등)
> ↓
> HTTP 응답 반환
> ```

> 덧붙여 JSP 내부 동작 흐름은 다음과 같다.
> 1. 클라이언트가 `hello.jsp` 요청
> 2. WAS(Tomcat 등)가 `hello.jsp`를 `hello_jsp.java`라는 서블릿 코드로 변환
> 3. `hello_jsp.java`를 컴파일하여 `hello_jsp.class` 생성
> 4. 해당 클래스가 실행되며 HTML 응답 생성
> 5. 브라우저에 완성된 HTML 반환
