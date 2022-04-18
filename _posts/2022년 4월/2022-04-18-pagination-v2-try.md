---
title: "[Github][Minimal-mistakes][jekyll-paginate-v2] jekyll-paginate-v2로 여러 페이지에 paginate 적용시키기 - 추천 X"
excerpt: "jekyll-paginate-v2로 각 category/tag별 페이지에 paginate를 적용시키려 했으나, github blog에 지원하지 않아 실패하였다. 따라서 이 방법은 추천하지 않으며, 내가 겪은 경험을 서술하는 글이다."
date: 2022-04-18
last_modified_at: 2022-04-18
categories:
  - blog
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
  - pagination
---

## 1. jekyll-paginate-v2

결론부터 말하면, **Github Blog인 경우 jekyll-paginate-v2 적용을 추천하지 않는다.** 그 이유는 아래에 적어놓았다. 

나는 이틀동안 헤매다가 local에서 겨우겨우 원하는 모양으로 성공시키긴 했다. 그러나 나중에서야 이를 github blog에 적용시킬 수 없다는 사실을 알게 되었고, 원래 버전으로 다시 되돌릴 수밖에 없었다. 

따라서 이 글은 paginate-v2를 적용시키는 방법을 설명하는 글이 아니라, 내가 겪었던 일과 실패 과정을 서술해놓은 글이다.

> [Github: jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2){: target="_blank"}

해당 깃헙을 들어가보면 Readme 첫줄에 대놓고 이렇게 적혀있다. `Please note that this plugin is NOT supported by GitHub pages.` 왜 이걸 제대로 보지 않았는지 지금와서 생각하면 정말 어이가 없다. 이 말 그대로 jekyll-paginate-v2 plugin은 github page에서 지원하지 않기 때문에, 적용시킬 수 없다.

그 뒤에 그래도 적용시키고 싶다면 다음과 같은 방법을 사용하면 된다...라고 적혀있으나, 성공시킨 사례도 적을 뿐더러 구글에 검색해보면 과정이 꽤나 복잡하고 실패한 사례도 많다. 

정말 paginate-v2를 적용시키고 싶다면, 해당 plugin을 github blog에 적용시키는 작업을 성공하고 나서 본인의 블로그를 customize 하는 것을 추천한다. (난 그것도 모르고 이틀 동안 customize를 먼저 시도했고, plugin 적용시키기를 실패해서 의미가 없어졌다.)

단, `bundle exec jekyll serve`를 통해 만든 local server에서는 누구나 그냥 정상적으로 적용된다는 것에 주의해야 한다. 여기서 잘 된다고 github blog에 적용되는 것이 아니다. **반드시 local server가 아닌, git push를 하여 '(깃헙 닉네임)/github.io'에서 잘 적용되었는지 확인하여야 한다.**

## 2. 파일 수정

변화시킨 파일들의 내용은 아래에 정리하였다. 모두 기존 [Minimal-mistakes](https://github.com/mmistakes/minimal-mistakes){: target="_blank"}에서 가져온 기본 파일들을 변형시킨 것이다.

### A. Gemfile

```md
gem "jekyll-paginate-v2"
```

### B. _config.yml

```yml
plugins:
  # - jekyll-paginate [기존 plugin 주석처리]
  - jekyll-paginate-v2
```

```yml
pagination:
  enabled: true
  per_page: 6
  title: ':title'
  sort_field: 'date'
  sort_reverse: true
  permalink: /:num/
  trail:
    before: 2
    after: 2
```

옵션은 해당 plugin Github Readme에 적혀있는 설명을 참고하여 본인 마음대로 설정하면 된다.

### C. index.html

```html
---
layout: home
author_profile: true
pagination:
  enabled: true
---
```

### D. _includes/paginator.html

길어서 [Github Commit](https://github.com/BurningFalls/burningfalls.github.io/commit/0169ae6a5c91264c0a73f01a7a7b0aad0f1f59fd){: target="_blank"}으로 대체

원래 `paginator.html` 파일을 그대로 사용하면, `index.html`을 제외한 다른 곳에서 아래쪽 `페이지 이동 UI`가 제대로 작동하지 않아서 이를 수정하였다.

### E. _pages/categories/(category name).md

```md
# _pages/categories/category-algorithm.md
---
title: "ALGORITHM"
layout: home
permalink: /categories/algorithm/
pagination:
  enabled: true
  category: algorithm
---
```

### F. _pages/categories/(tag name).md

```md
# _pages/tags/tag-algorithm.md
---
title: "Algorithm"
layout: home
permalink: /tags/algorithm/
pagination:
  enabled: true
  tag: algorithm
---
```