---
title: "[Github blog][Minimal-mistakes] Minimal-mistakes 테마 Github blog 만들기 3"
excerpt: "minimal-mistakes 테마를 사용하여 github blog를 만드는 과정을 서술하였다."
date: 2022-03-15
last_modified_at: 2022-04-05
categories:
  - blog
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
---

> [Minimal Mistakes - Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/){: target="_blank"}

해당 링크의 테마 가이드를 토대로 만들었으나, 내가 생각하는 중요도에 맞추어서 순서를 바꾸었기 때문에, 위에서부터 아래로 순서대로 쭉 가지 않고 중간중간 건너뛰고 돌아가는 방식으로 설명되어 있다. 

> 이 글은 내가 블로그를 만들면서 그 당시 겪은 일을 그대로 서술한 것이다. 그래서 초반 부 글에는 잘못된 내용까지 고쳐지지 않은 채로 서술되어 있다. 뒤에서 해당 내용을 조금씩 고쳐가긴 하지만, 만약에 깃헙 블로그를 만들고 싶어서 이 글을 읽으면서 따라한다면 조금 헤맬 수도 있다.

> [이전 글: Minimal-mistakes 테마 Github blog 만들기 1](https://burningfalls.github.io/blog/blog-making-1/)

> [이전 글: Minimal-mistakes 테마 Github blog 만들기 2](https://burningfalls.github.io/blog/blog-making-2/)

## _pages 폴더 복구

`_config.yml` 파일 수정을 마무리하고 실제 글을 올려볼 차례가 되었다. 로컬 환경에서 이것저것 시도해보다가 원래 Github에 있던 `_pages` 폴더에 생각보다 필요한 파일(tag-archive, year-archive 등등)이 많다는 것을 깨닫게 되어, 다시 전부 다운받고 폴더 파일을 전부 옮겼다.

![error](https://user-images.githubusercontent.com/30232837/161659585-1fa7a4d0-4f6e-4888-886f-edd57f5a85de.png "error"){: width="80%" height="80%"}{: .align-center}

`about.md`에서 오류가 나길래 직접 `minimal-mistakes` 사이트에 들어가서 `/about` 링크를 들어가 보았다. 살펴본 결과, 내 블로그에는 필요 없는 내용이어서 그냥 파일 자체를 삭제하여 오류를 해결하였다.

## Category 설정

큰 틀은 다음과 같이 정해보았다. (특별함을 주기 위해 일부러 첫 글자 ABCDE를 맞춰서 설정해보았다.)

1. Algorithm - baekjoon, programmers, etc
2. Blog - blog CRUD(Create, Read, Update, Delete)
3. Contest - contest review (baekjoon, etc)
4. Deep learning - deep learning study
5. Essay - diary

각각의 글을 `post` 형식으로 작성하고, `category`를 다음 다섯 개 중 하나로 설정하여 그룹화할 예정이다. 원래는 `collection`으로 묶어서 `docs`에 저장하려 했다. 그런데 나중에 `pages`폴더에 `page-archive`, `tag-archive`, `year-archive` 등 파트별로 묶어주는 기본 설정이 되어있음을 깨달았다. 그래서 `post` 형식으로 작성하기로 했다.

