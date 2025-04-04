---
title: "[Spring] 테스트 데이터를 효율적으로 관리하기 위한 Fixture 개선 전략"
excerpt: "중복을 줄이고, 가시성을 높이며, 테스트의 목적에 충실한 Fixture 설계 방법에 대해 다룹니다."
date: 2025-04-04
last_modified_at: 2025-04-04
categories:
  - java
tags:
  - spring-study
---

## 1. 문제 상황 개요

테스트 코드에서 도메인 객체 생성을 반복적으로 수행하다 보면, 중복된 코드가 많아지고 테스트의 의도가 흐려질 수 있다. 특히 테스트마다 요구되는 필드가 다를 경우, 생성 메서드를 오버로딩하거나 추가적인 설정이 필요해진다.

```java
public class CategoryFixture {
    private static final String THUMBNAIL_URL = "https://example.com/categories/geumohrm.jpg";
    private static final String TITLE = "title";
    private static final String DESCRIPTION = "친구들과 함께한 여름 휴가 추억";

    public static Category create() {
        return Category.builder()
                .thumbnailUrl(THUMBNAIL_URL)
                .title(TITLE)
                .description(DESCRIPTION)
                .build();
    }

    public static Category create(LocalDate startAt, LocalDate endAt) {
        return Category.builder()
                .thumbnailUrl(THUMBNAIL_URL)
                .title(TITLE)
                .description(DESCRIPTION)
                .startAt(startAt)
                .endAt(endAt)
                .build();
    }

    public static Category create(String title, LocalDate startAt, LocalDate endAt) {
        return Category.builder()
                .thumbnailUrl(THUMBNAIL_URL)
                .title(title)
                .description(DESCRIPTION)
                .startAt(startAt)
                .endAt(endAt)
                .build();
    }
}
```

이 방식은 단순하지만 유연하지 않고, 테스트 목적에 따라 매번 Fixture를 수정해야 하며, 가시성도 낮다.

## 2. 기존 Fixture 설계의 한계점

* 오버로딩 메서드가 많아짐에 따라 **중복 코드 증가**
* 테스트마다 필요한 필드가 다를 경우, **Fixture 클래스 자체를 수정해야 하는 불편함**
* 어떤 값이 설정되었는지 한눈에 보이지 않아 **가시성 부족**
* `Repository.save()`와 같은 저장 로직이 섞이면서 **테스트의 목적이 흐려짐**

## 3. 개선 방향 및 설계 원칙

Fixture 개선의 목표는 다음과 같다.

* **확장성과 유연성 향상** - 필드가 바뀌어도 Fixture 코드를 수정할 필요 없음
* **가시성 증가** - 어떤 값이 설정되었는지 테스트 코드에서 명확히 드러남
* **의미의 분리** - 도메인 생성과 저장을 명확히 구분
* **중복 최소화** - 불필요한 오버로딩 제거 및 중복 로직 제거

이를 위해 **빌더 패턴을 활용한 Fixture 설계**를 도입한다.

## 4. 개선된 Fixture 구조

```java
public class CategoryFixtures {
    public static CategoryBuilder defaultCategory() {
        return new CategoryBuilder()
                .withThumbnailUrl("https://example.com/categoryThumbnail.jpg")
                .withTitle("categoryTitle")
                .withDescription("categoryDescription")
                .withTerm(LocalDate.of(2024, 1, 1), LocalDate.of(2024, 12, 31));
    }
  
    public static class CategoryBuilder {
        private Long id;
        private String thumbnailUrl;
        private String title;
        private String description;
        private Term term;
    
        public CategoryBuilder withId(Long id) { 
            this.id = id; 
            return this; 
        }
        public CategoryBuilder withThumbnailUrl(String thumbnailUrl) { 
            this.thumbnailUrl = thumbnailUrl; 
            return this; 
        }
        public CategoryBuilder withTitle(String title) { 
            this.title = title; 
            return this; 
        }
        public CategoryBuilder withDescription(String description) { 
            this.description = description; 
            return this; 
        }
        public CategoryBuilder withTerm(LocalDate startAt, LocalDate endAt) { 
            this.term = new Term(startAt, endAt); 
            return this; 
        }
        public Category build() {
          return new Category(id, thumbnailUrl, title, description, term.getStartAt(), term.getEndAt());
        }
        public Category buildWithMember(Member member) {
            Category category = build();
            category.addCategoryMember(member);
            return category;
        }
        public Category buildAndSave(CategoryRepository repository) {
            Category category = build();
            return repository.save(category);
        }
        public Category buildAndSaveWithMember(Member member, CategoryRepository repository) {
            Category category = buildWithMember(member);
            return repository.save(category);
        }
    }
}
```

## 5. 개선 전후 테스트 코드 비교

### A: 중복 제거 - 오버로딩 메서드 제거

> 개선 목적: 생성자나 팩토리 메서드의 오버로딩 없이 다양한 케이스를 커버하도록 구성

✨ 개선 전

```java
@DisplayName("카테고리가 기간을 가지고 있으면 참을 반환한다.")
@Test
void hasTerm() {
    // given
    Category category = CategoryFixture.create(
            LocalDate.of(2024, 1, 1),
            LocalDate.of(2024, 12, 31)
    );

    // when
    boolean result = category.hasTerm();

    // then
    assertThat(result).isTrue();
}
```

✅ 개선 후

```java
@DisplayName("카테고리가 기간을 가지고 있으면 참을 반환한다.")
@Test
void hasTerm() {
    // given
    Category category = CategoryFixtures.defaultCategory()
            .withTerm(LocalDate.of(2024, 1, 1),
                      LocalDate.of(2024, 12, 31))
            .build();

    // when
    boolean result = category.hasTerm();

    // then
    assertThat(result).isTrue();
}
```

> `create()` 메서드를 계속 오버로딩하지 않고, 필요한 필드만 덮어써서 유연하고 재사용 가능한 구조 확보

### B: 가시성 증가 - 테스트 목적이 명확하게 드러남

> 개선 목적: 어떤 데이터가 테스트에 중요한지를 테스트 코드에서 바로 확인할 수 있도록 함

✨ 개선 전

```java
@DisplayName("기간이 있는 카테고리 목록만 조회된다.")
@Test
void readAllCategoriesWithTerm() {
    // given
    Member member = memberRepository.save(MemberFixture.create());
    Category categoryFixture = CategoryFixture.createWithMember("first", member);
    Category category = categoryRepository.save(categoryFixture);

    Category categoryFixture2 = CategoryFixture.createWithMember(
            LocalDate.now(),
            LocalDate.now().plusDays(3),
            member
    );
    Category category2 = categoryRepository.save(categoryFixture2);

    List<Category> categories = new ArrayList<>();
    categories.add(category);
    categories.add(category2);

    // when
    List<Category> result = CategoryFilter.TERM.apply(categories);

    // then
    assertAll(
            () -> assertThat(result).hasSize(1),
            () -> assertThat(result.get(0).getTitle()).isEqualTo(category2.getTitle())
    );
}
```

✅ 개선 후

```java
@DisplayName("기간이 있는 카테고리 목록만 조회된다.")
@Test
void readAllCategoriesWithTerm() {
    // given
    Member member = MemberFixtures.defaultMember().buildAndSave(memberRepository);

    Category category1 = CategoryFixtures.defaultCategory()
            .withTitle("first")
            .withTerm(null, null)
            .buildAndSaveWithMember(member, categoryRepository);

    Category category2 = CategoryFixtures.defaultCategory()
            .withTitle("second")
            .withTerm(LocalDate.now(), LocalDate.now().plusDays(3))
            .buildAndSaveWithMember(member, categoryRepository);

    List<Category> categories = List.of(category1, category2);

    // when
    List<Category> result = CategoryFilter.TERM.apply(categories);

    // then
    assertAll(
            () -> assertThat(result).hasSize(1),
            () -> assertThat(result.get(0).getTitle()).isEqualTo(category2.getTitle())
    );
}
```

> 어떤 필드가 의도적으로 null인지, 유효한 기간이지 등 테스트 목적이 뚜렷하게 드러남

### C: 추상화 강화 - 저장 로직 등 구현 세부사항 감춤

> 개선 목적: 테스트 데이터의 목적은 "무슨 데이터를 준비했는가"이지 "어떻게 저장했는가"가 아님. 이를 감춰서 테스트 본연의 목적에 집중

✨ 개선 전

```java
@DisplayName("본인 것이 아닌 카테고리에 스타카토를 생성하려고 하면 예외가 발생한다.")
@Test
void cannotCreateStaccatoIfNotOwner() {
    // given
    Member member = memberRepository.save(MemberFixture.create());
    Member otherMember = memberRepository.save(MemberFixture.create());

    Category category = CategoryFixture.create(
            LocalDate.now(),
            LocalDate.now().plusDays(1)
    );
    category.addCategoryMember(member);
    categoryRepository.save(category);

    StaccatoRequest staccatoRequest = StaccatoRequestFixture.create(category.getId());

    // when & then
    assertThatThrownBy(() -> staccatoService.createStaccato(staccatoRequest, otherMember))
            .isInstanceOf(ForbiddenException.class)
            .hasMessage("요청하신 작업을 처리할 권한이 없습니다.");
}
```

✅ 개선 후

```java
@DisplayName("본인 것이 아닌 카테고리에 스타카토를 생성하려고 하면 예외가 발생한다.")
@Test
void cannotCreateStaccatoIfNotOwner() {
    // given
    Member member = MemberFixtures.defaultMember().buildAndSave(memberRepository);
    Member otherMember = MemberFixtures.defaultMember().buildAndSave(memberRepository);

    Category category = CategoryFixtures.defaultCategory()
            .buildAndSaveWithMember(member, categoryRepository);

    StaccatoRequest staccatoRequest = StaccatoRequestFixtures.defaultStaccatoRequest()
            .withCategoryId(category.getId())
            .build();

    // when & then
    assertThatThrownBy(() -> staccatoService.createStaccato(staccatoRequest, otherMember))
            .isInstanceOf(ForbiddenException.class)
            .hasMessage("요청하신 작업을 처리할 권한이 없습니다.");
}
```

> 저장, 관계 설정 등 '덜 중요한 세부사항'을 감추고 핵심 의미만 표현 -> 테스트 코드가 깔끔하고 목적 지향적

### D: 확장성 및 재사용성 증가 - DTO, 도메인 모두 동일한 방식 적용 가능

> 개선 목적: 도메인뿐 아니라 Request DTO 같은 계층도 동일한 방식으로 관리하면 전체 테스트 구조가 일관성ㅇ르 갖고 관리가 쉬워짐

✨ 개선 전

```java
static Stream<Arguments> invalidCategoryRequestProvider() {
    return Stream.of(
            Arguments.of(new CategoryRequest(
                    "https://example.com/categories/geumohrm.jpg",
                    null,
                    "친구들과 함께한 여름 휴가 카테고리",
                    LocalDate.of(2023, 7, 1),
                    LocalDate.of(2023, 7, 10)
            ), "카테고리 제목을 입력해주세요."),
            Arguments.of(new CategoryRequest(
                    "https://example.com/categories/geumohrm.jpg",
                    "가".repeat(31),
                    "친구들과 함께한 여름 휴가 카테고리",
                    LocalDate.of(2023, 7, 1),
                    LocalDate.of(2023, 7, 10)
            ), "제목은 공백 포함 30자 이하로 설정해주세요.")
    );
}
```

✅ 개선 후

```java
static Stream<Arguments> invalidCategoryRequestProvider() {
    return Stream.of(
            Arguments.of(CategoryRequestFixtures.defaultCategoryRequest()
                    .withCategoryTitle(null)
                    .build(), "카테고리 제목을 입력해주세요."),
            Arguments.of(CategoryRequestFixtures.defaultCategoryRequest()
                    .withCategoryTitle("가".repeat(31))
                    .build(), "제목은 공백 포함 30자 이하로 설정해주세요.")
    );
}
```

> default 값을 재사용하고, 변경이 필요한 필드만 `.withXXX()` 메서드로 설정 -> 중복도 줄고 실수도 줄어듦
  
## 6. 정리 및 기대 효과

Fixture 개선을 통해 얻은 이점

* **확장성 향상**: 필드가 바뀌어도 기존 코드를 수정할 필요 없이 `withXXX()` 메서드로 덮어쓰기 가능
* **가시성 증가**: 어떤 필드를 변경했는지 테스트 코드 상에서 명확히 드러남
* **중복 제거**: 오버로딩 메서드 제거, 공통 데이터 설정 분리
* **추상화 증가**: 저장과 같은 비즈니스 로직을 감추고 테스트 목적에 집중 가능
* **테스트의 명확성 향상**: 테스트가 의도한 의미를 코드만 보고도 이해할 수 있음

## 7. 실제 적용 사례 (Github)

이 문서에서 다룬 Fixture 개선 전략은 실제 프로젝트에 적용되었습니다. 전체 코드 구조와 패턴이 궁금하다면 아래 링크를 참고하세요.

👉 [프로젝트 Github PR 링크](https://github.com/woowacourse-teams/2024-staccato/pull/712)
