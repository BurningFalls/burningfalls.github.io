---
title: "[Github Blog][Minimal-mistakes] Github blog category/tag별 페이지 구분"
excerpt: "Github blog Minimal-mistakes 테마를 가져오면, 글에 category와 tag를 적용할 수 있다. 이는 전부가 하나의 페이지에서 #으로 이동하는 형태인데, 보기 쉽도록 각각의 분류당 한 페이지로 구분시킨다."
date: 2022-04-15
last_modified_at: 2022-04-18
categories:
  - blog
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
---

## 1. 특정 카테고리/태그 페이지 생성

![search-machine](https://user-images.githubusercontent.com/30232837/163798102-e79ba063-3bbe-44c4-b958-d6b5a0455733.png "search-machine"){: width="80%" height="80%"}{: .align-center}

나는 위의 사진과 같이 `_pages`에 각 Category별 페이지를 담아놓는 `categories` 폴더와 각 Tag별 페이지를 담아놓는 `tags` 폴더를 만들고, 그 안에 파일들을 정리해두었다.

```md
# _pages/categories/category-algorithm.md

---
title: "ALGORITHM"
layout: category
permalink: categories/algorithm
taxonomy: algorithm
---
```

다음과 같이 `layout: category`로 `taxonomy: algorithm` 코드를 넣은 파일을 생성하면, minimal-mistakes에 이미 있는 `_layouts/category.html`에서 `taxonomy` 값을 받아서 해당 category(algorithm) 값을 갖는 posts만 페이지에 띄워준다. 특정 tag 페이지를 생성할 때도 마찬가지이다.

```md
# _pages/tags/tag-boj-23000-23999.md

---
title: "BOJ 23000~23999"
layout: tag
permalink: tags/boj-23000-23999
taxonomy: boj-23000-23999
---
```

## 2. 링크 설정

이제 적당한 곳에 이 페이지를 들어갈 수 있도록 링크를 설정해주면 된다. main link로 걸어서 위쪽에 보이게 할 수도 있고, sidebar link로 걸어서 왼쪽 sidebar에 보이게 할 수도 있다.

```yml
main:
  - title: "(적당한 제목)"
    url: (위에서 설정한 permalink)
posts:
  - title: "(적당한 제목)"
    url: (위에서 설정한 permalink)
```

위의 `posts`는 밑의 `_config.yml`에서 `sidebar`로 설정되어 있다. 

```yml
defaults:
  # _posts
  - scope:
        path: ""
        type: posts
    values:
      sidebar:
        nav: "posts"
```

## 3. 완성

![github-blog](https://user-images.githubusercontent.com/30232837/163506247-56ad1149-97f4-4dbe-af06-4b5e507090d1.png "github-blog"){: width="100%" height="100%"}{: .align-center}

`Essay`를 누르니 `essay` category를 가진 글만 뜨는 별개의 페이지가 표시됨을 볼 수 있다.




