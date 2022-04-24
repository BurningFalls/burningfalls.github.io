---
title: "[Github Blog][Minimal-mistakes] Github blog sidebar에 tag별 post 개수 표기"
excerpt: "Github blog sidebar에 category/tag 별로 글 개수가 자동으로 세어져 표기되도록 파일을 커스터마이징한다."
date: 2022-04-14
last_modified_at: 2022-04-24
categories:
  - blog
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
---

> 이 블로그는 [Minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/){: target="_blank"} 테마가 적용되어 이를 기반으로 서술되었음을 밝힌다.

목표는 다음과 같다.

![github-blog](https://user-images.githubusercontent.com/30232837/163345353-4903466e-11fa-4e15-a6fe-5b188e2178ad.png "github-blog"){: width="100%" height="100%"}{: .align-center}

변경해야할 파일은 총 두 개이다.
```
_includes/nav_list
```
```
_data/navigation.yml
```

## 1. navigation 준비

본인이 커스텀한 sidebar 코드를 기반으로 바꾸면 된다.

예시를 들기 위해 내 블로그의 [_data/navigation.yml](https://github.com/BurningFalls/burningfalls.github.io/blob/master/_data/navigation.yml){: target="_blank"} 수정 전 파일을 축약해서 가져왔다.

```yml
# sidebar
  posts:
  - title: Algorithm
    url: /categories/algorithm
    children:
      - title: "boj 23000~23999"
        url: /tags/boj-23000-23999
      - title: "boj 24000~24999"
        url: /tags/boj-24000-24999
  - title: Blog
    url: categories/blog
    children:
      - title: "blog making"
        url: /tags/blog-making
      - title: "markdown"
        url: /tags/markdown
```

## 2. nav_list 준비

minimal-mistakes를 그대로 fork하거나 download 했을 경우, [Minimal-mistakes github](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/nav_list){: target="_blank"}에서 기본 파일을 볼 수 있다. 이를 기반으로 잡고 변경한다.

## 3. nav_list 변경

해당 코드의 정확한 위치는 [최종 변경 파일](https://github.com/BurningFalls/burningfalls.github.io/blob/master/_includes/nav_list){: target="_blank"}을 보는 것을 추천한다.

### A1. 전체 글 수 세기

```
{% raw %}{% assign sum = site.posts | size %}{% endraw %}
```

### A2. 전체 글 수 표시

```html
<span style="font-size: 14pt"><b>TOTAL ({{sum}})</b></span>
```

### B1. 카테고리별 글 수 세기

```
{% raw %}{% assign cattotal = 0 %}{% endraw %}
{% raw %}{% for category in site.categories %}{% endraw %}
{% raw %}  {% if category[0] == nav.category  %}{% endraw %}
{% raw %}    {% assign cattotal = cattotal | plus: category[1].size %}{% endraw %}
{% raw %}  {% endif %}{% endraw %}
{% raw %}{% endfor %}{% endraw %}
```

### B2. 카테고리별 글 수 표시

```html
<a href="{{ nav.url | relative_url }}"><span class="nav__sub-title">{{ nav.title }} ({{cattotal}})</span></a>
```

단순 표기 방법은 위와 같다. 나는 `POSTS BY CATEGORY`나 `VERSION`과 같이 글 수가 표시되지 않기를 원하는 category가 있기 때문에, 글 수가 $0$개이면 `cattotal`을 표시하지 않도록 코딩하였다. 따라서 들어가서 보이는 파일의 내용은 조금 다르다.

### C1. 태그별 글 수 세기

```
{% raw %}{% assign tagtotal = 0 %}{% endraw %}
{% raw %}{% for tag in site.tags %}{% endraw %}
{% raw %}  {% if tag[0] == child.tag  %}{% endraw %}
{% raw %}    {% assign tagtotal = tagtotal | plus: tag[1].size %}{% endraw %}
{% raw %}  {% endif %}{% endraw %}
{% raw %}{% endfor %}{% endraw %}
```

### C2. 태그별 글 수 표시

```html
<li><a href="{{ child.url | relative_url }}"{% if child.url == page.url %} class="active"{% endif %}>{{ child.title }} ({{tagtotal}})</a></li>
```

## 4. navigation 변경

위의 `태그별 글 수 세기` 코드에서 볼 수 있듯이

```
{% raw %}{% assign tagtotal = 0 %}{% endraw %}
{% raw %}{% for tag in site.tags %}{% endraw %}
{% raw %}  {% if tag[0] == child.tag  %}{% endraw %}
{% raw %}    {% assign tagtotal = tagtotal | plus: tag[1].size %}{% endraw %}
{% raw %}  {% endif %}{% endraw %}
{% raw %}{% endfor %}{% endraw %}
```

세 번째 줄에서 `child.tag` 변수가 필요하다. 따라서 `navigation` 파일의 각각의 tag에 아래와 같이 `tag` 변수와 그 값을 만들어주어야 한다.

단, site의 tag들이 `child.title`과 완벽하게 일치한다면, 따로 `tag` 변수를 만들 필요 없이 `child.title`로 접근하면 된다. 

```yml
# sidebar
  posts:
  - title: Algorithm
    url: /categories/algorithm
    children:
      - title: "boj 23000~23999"
        tag: boj-23000-23999    # 추가
        url: /tags/boj-23000-23999
      - title: "boj 24000~24999"
        tag: boj-24000-24999    # 추가
        url: /tags/boj-24000-24999
  - title: Blog
    url: categories/blog
    children:
      - title: "blog making"
        tag: blog-making        # 추가
        url: /tags/blog-making
      - title: "markdown"
        tag: markdown           # 추가
        url: /tags/markdown
```

category를 다루는 방식도 이와 마찬가지로 접근하면 된다. 

## 5. 완성본

### 1. _includes/nav_list

> [_includes/nav_list](https://github.com/BurningFalls/burningfalls.github.io/blob/master/_includes/nav_list){: target="_blank"}

### 2. _data/navigation.yml

> [_data/navigation.yml](https://github.com/BurningFalls/burningfalls.github.io/blob/master/_data/navigation.yml){: target="_blank"}
