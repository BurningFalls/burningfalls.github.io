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

## 1. 특정 카테고리 페이지 생성

나는 이 파일을 `page`로 정의해서 `_pages` 폴더 안에 넣어 관리하고 있다. 무슨 종류로 지정하든 크게 상관은 없지만, `_config.yml`의 default 설정으로 미루어보아 `page`가 제일 적절하다. 본인 마음대로 커스터마이징하면 된다.

> 아래 코드블럭에서 `%` 관련 문법을 사용할 경우, 블로그에 코드가 제대로 나타나지 않는 현상이 발생하였다. 다른 특수 문법과 겹치기 때문인 것 같은데 해결 방법을 모르겠다. 따라서 `%` 앞에 `\`을 하나씩 붙여서 작성하였다. 원래 코드에는 `%` 앞에 `\`가 전부 없다.

```md
---
title: "(적당한 제목)"
layout: archive
permalink: (적당한 링크)
---

{\% assign posts = site.categories.(카테고리명) \%}
{\% for post in posts \%} {\% include archive-single.html type=page.entries_layout \%} {\% endfor \%}
```

**(적당한 제목)**에는 이 페이지의 적당한 제목을 아무거나 쓰면 된다.

**(적당한 링크)**에는 이 페이지의 링크를 적당히 설정해준다. 단, 링크이므로 띄어쓰기나 특정 특수문자들을 사용하면 오류가 날 수 있다. (대표적으로 `-`는 사용 가능, 한글도 복사시 깨지므로 비추천)

**(카테고리명)**에는 반드시 본인 블로그 posts에서 생성한 정확한 카테고리 명칭이 들어가야 한다.

> [내가 만들어서 사용하고 있는 예시](https://github.com/BurningFalls/burningfalls.github.io/blob/master/_pages/categories/category-algorithm.md?plain=1){: target="_blank"}

이렇게 만들면, (본인 블로그)/(설정한 permalink)로 들어갔을 때, (카테고리명)의 category를 갖는 글들만 해당 페이지에 표시되는 것을 볼 수 있다.

tag별로 페이지를 구분할 때도 이와 똑같은 방식으로 하면 된다. 다만, 위 코드의 `site.categories`를 `site.tags`로 바꿔주면 된다.

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



