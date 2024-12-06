---
title: "[Spring] TEST 전략 - 단위 테스트, 통합 테스트, Web MVC 테스트, 데이터 계층 테스트, 엔드투엔드 테스트"
excerpt: "Spring의 테스트 전략에는 어떤 것들이 있는가? 단위 테스트란? 통합 테스트란? Web MVC 테스트란? 데이터 계층 테스트란? 엔드투엔드 테스트란? Spring의 계층적 테스트 전략은? 외부 의존성을 가진 클래스의 단위 테스트 작성하는 방법은?"
date: 2024-12-05
last_modified_at: 2024-12-06
categories:
  - git
tags:
  - git
---

## A. Question

Spring Test 전략에는 어떤 것들이 있는가?

## B. Answer

### 1. 단위 테스트 (Unit Test)

* 목적: 클래스나 메서드와 같은 작은 단위의 기능을 독립적으로 검증
* 도구: Junit, Mockito, AssertJ
* 특징
  * Spring의 컨텍스트를 로드하지 않음
  * 외부 의존성을 모킹(Mock)하여 테스트
  * 빠르고 실행 비용이 적음
* 예시
  * `DiscountService`가 의존성이 없는 클래스인 경우
    ```java
    @Test
    void testCalculateDiscount() {
        DiscountService discountService = new DiscountService();
        assertEquals(50, discountService.calculate(500, 10));
    }
    ```
  * `DiscountService`가 외부 의존성을 가지고 있는 경우
    * `C. Detail - 외부 의존성을 가진 클래스의 단위 테스트 작성하는 방법` 에서 후술

### 2. 통합 테스트 (Integration Test)

* 목적: 애플리케이션의 여러 구성 요소가 올바르게 상호작용하는지 검증
* 도구: Spring TestContext Framework, `@SpringBootTest`
* 특징
  * Spring 컨텍스트를 로드하여 실제 빈(Bean)과 함께 테스트
  * 데이터베이스, 메시징 시스템 등 외부 리소스와의 통합 테스트 가능
  * 느릴 수 있지만, 중요한 부분
* 예시
    ```java
    @SpringBootTest
    @Transactional
    class UserServiceIntegrationTest {
        @Autowired
        private UserService userService;
        
        @Test
        void testCreateUser() {
            User user = userService.createUser("test", "test@example.com");
            assertNotNull(user.getId());
        }
    }
    ```

### 3. Web MVC 테스트 (Spring MVC Test)

* 목적: 컨트롤러 계층의 HTTP 요청/응답 처리를 테스트
* 도구: `@WebMvcTest`
* 특징
  * 컨트롤러 및 관련 빈(Bean)만 로드
  * MockMvc를 사용하여 요청과 응답을 검증
  * 빠르고 API 테스트에 적합
* 예시
    ```java
    @WebMvcTest(UserController.class)
    class UserControllerTest {
        @Autowired
        private MockMvc mockMvc;
        
        @Test
        void testGetUser() throws Exception {
            mockMvc.perform(get("/users/1"))
                    .andExpect(status().isOk())
                    .andExpect(jsonPath("$.name").value("John Doe"));
        }
    }
    ```

### 4. 데이터 계층 테스트 (Repository Test)

* 목적: 데이터베이스와의 상호작용이 올바른지 확인
* 도구: `@DataJpaTest`, H2와 같은 인메모리 데이터베이스
* 특징
  * Repository와 Entity 간의 매핑 및 쿼리 테스트
  * Spring 컨텍스트에서 필요한 부분만 로드
  * 실제 DB 대신 가벼운 인메모리 DB를 사용
* 예시
    ```java
    @DataJpaTest
    class UserRepositoryTest {
        @Autowired
        private UserRepository userRepository;
        
        @Test
        void testFindByEmail() {
            User user = userRepository.save(new User("test", "test@example.com"));
            User found = userRepository.findByEmail("test@example.com");
            assertEquals(user.getId(), found.getId());
        }
    }
    ```

### 5. 엔드투엔드 테스트 (End-to-End Test)

* 목적: 애플리케이션 전체 워크플로우를 검증
* 도구: Selenium, RestAssured, Testcontainers
* 특징
  * 모든 구성 요소와 외부 시스템을 포함
  * 실제 환경과 유사한 조건에서 테스트
  * 느리고 비용이 크지만, 실제 시나리오를 검증 가능
* 예시
```java
@SpringBootTest(webEnvironment = WebEnvironment.DEFINED_PORT)
class UserEndpointTest {
    @Test
    void testGetUserApi() {
        RestAssured.given()
                .get("http://localhost:8080/users/1")
                .then()
                .statusCode(200)
                .body("name", equalTo("John Doe"));
    }
}
```

### 6. 계층적 테스트 전략

* 테스트 전략을 계층적으로 적용하여 신뢰성과 성능을 극대화
  * 단위 테스트로 빠르고 작은 기능 검증
  * 통합 테스트로 주요 구성 요소의 상호작용 확인
  * E2E 테스트로 전체 사용자 시나리오를 점검

## C. Detail - 외부 의존성을 가진 클래스의 단위 테스트 작성하는 방법

**TaxService 인터페이스**

```java
public interface TaxService {
    int getTax(int price);
}
```

**DiscountService 클래스**

```java
class DiscountService {
    private final TaxService taxService;
    
    public DiscountService(TaxService taxService) {
        this.taxService = taxService;
    }
    
    public int calculate(int price, int discountPercentage) {
        int discount = (price * discountPercentage) / 100;
        return price - discount - taxService.getTax(price);
    }
}
```

### 1. Mocking (Mockito를 사용하는 방법)

```java
class DiscountServiceTest {
    
    @Test
    void testCalculateDiscountWithMock() {
        // Mock 객체 생성
        TaxService mockTaxService = mock(TaxService.class);
        
        // Mock의 동작 정의
        when(mockTaxService.getTax(anyInt())).thenReturn(10);
        
        // 테스트 대상 클래스 생성
        DiscountService discountService = new DiscountService(mockTaxService);
        
        // 테스트 실행 및 검증
        int result = discountService.calculate(500, 10);    // 500 - 50 - 10
        
        // Mock 메서드 호출 여부 검증
        verify(mockTaxService, times(1)).getTax(500);
    }
}
```

### 2. Stub (테스트 전용 객체 생성)

```java
class FakeTaxService implements TaxService {
    @Override
    public int getTax(int price) {
        return 10;  // 테스트용 고정값
    }
}

class DiscountServiceTest {
    
    @Test
    void testCalculateDiscountWithStub() {
        // Stub 객체 사용
        TaxService taxService = new FakeTaxService();
        DiscountService discountService = new DiscountService(taxService);
        
        // 테스트 실행 및 검증
        int result = discountService.calculate(500, 10);    // 500 - 50 - 10
        assertEquals(440, result);
    }
}
```

### 3. Spring의 @MockBean 사용

```java
import javax.annotation.processing.SupportedAnnotationTypes;

@SpringBootTest
class DiscountServiceTest {

    @MockBean
    private TaxService taxService;
  
    @Autowired
    private DiscountService discountService;

    @Test
    void testCalculateDiscountWithMockBean() {
        // MockBean 동작 정의
        when(taxService.getTax(anyInt())).thenReturn(10);
        
        // 테스트 실행 및 검증
        int result = discountService.calculate(500, 10);    // 500 - 50 - 10
        assertEquals(440, result);
    }
}
```

### 4. 외부 의존성을 가진 클래스의 단위 테스트 방법 비교

| **방법**                | **장점**                                                                 | **단점**                                                                                     | **적합한 상황**                                                          |
|-------------------------|--------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Mocking**             | - 간단하고 다양한 시나리오를 테스트 가능<br>- Mock의 동작을 유연하게 정의 가능  | - 외부 라이브러리(Mockito)에 의존<br>- 실제 객체의 동작과 다를 수 있어 현실감을 잃을 수 있음 | 외부 의존성을 완전히 격리해야 하고 다양한 시나리오를 테스트해야 할 때 |
| **Stub**                | - 특정 동작만 구현하여 간단하게 사용 가능<br>- 외부 라이브러리에 의존하지 않음  | - Stub 객체를 직접 생성해야 하므로 유지보수 비용 증가<br>- 동작이 복잡하면 코드가 길어질 수 있음 | 테스트 대상 의존성이 간단하고 고정된 값만 반환해도 충분한 경우        |
| **Spring의 `@MockBean`**| - Spring 컨텍스트에서 테스트 가능<br>- 의존성이 자동 주입되어 코드가 간결   | - Spring 컨텍스트를 로드하므로 실행 속도가 느림<br>- 간단한 단위 테스트에는 과도한 설정 | Spring 컨텍스트 내에서 테스트가 필요할 때, 통합에 가까운 단위 테스트를 할 때 |


## D. Reference

* [Spring - Testing](https://docs.spring.io/spring-framework/reference/testing.html)
