---
title: "[Github Blog] Minimal-mistakes 테마 Github blog 만들기 2"
excerpt: "minimal-mistakes 테마를 사용하여 github blog를 만드는 과정을 서술하였다."
date: 2021-12-22
last_modified_at: 2022-05-25
categories:
  - blog
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
---

> [Minimal Mistakes - Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

해당 링크의 테마 가이드를 토대로 만들었으나, 내가 생각하는 중요도에 맞추어서 순서를 바꾸었기 때문에, 위에서부터 아래로 순서대로 쭉 가지 않고 중간중간 건너뛰고 돌아가는 방식으로 설명되어 있다. 

> 이 글은 내가 블로그를 만들면서 그 당시 겪은 일을 그대로 서술한 것이다. 그래서 초반 부 글에는 잘못된 내용까지 고쳐지지 않은 채로 서술되어 있다. 뒤에서 해당 내용을 조금씩 고쳐가긴 하지만, 만약에 깃헙 블로그를 만들고 싶어서 이 글을 읽으면서 따라한다면 조금 헤맬 수도 있다.

> [이전 글: Minimal-mistakes 테마 Github blog 만들기 1](https://burningfalls.github.io/blog/blog-making-1/)

## Migrating to Gem Version

테마를 이미 `bundle` 해서 [Migrating to Gem Version](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#migrating-to-gem-version){: target="_blank"}에 적힌 파일들을 지워버려도 되지만, 나중에 혹시 커스터마이징 할 수도 있을 것 같아 일단 남겨두었다.

## Update Gemfile

[Update Gemfile](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#update-gemfile)에 적힌 대로 Gemfile을 수정하였다. 이때, 앞에서 했던 Remote theme method 형식은 그대로 유지시키면서 수정하였다. Remote theme method 기준으로 정확히 어떻게 수정하면 되는지에 대한 자세한 설명이 없어서, 그냥 적힌 대로 수행했고 `bundle update`를 해서 성공시켰다.

## bundle exec jekyll serve

```
bundle exec jekyll serve
```

최종적으로 로컬에서 서버를 구동시키는 명령어이다.

이를 입력했더니 다음과 같은 `dependency error`가 떴다.

![error](https://user-images.githubusercontent.com/30232837/161528062-ce01d61f-b8d5-4020-97f7-4c513e8d1894.png "error"){: width="100%" height="100%"}{: .align-center}

이는 다음 명령어를 입력하여 해결하였다.

```
bundle add kramdown-parser-gfm
```

이번엔 또 이런 에러가 떴다. (실제 에러 메시지는 훨씬 길고, 핵심만 캡쳐하였다.)

![error](https://user-images.githubusercontent.com/30232837/161528261-bc3b967c-d919-45ff-8a9c-07010ea2a36d.png "error"){: width="100%" height="100%"}{: .align-center}

이는 다음 명령어를 입력하여 해결하였다.

```
bundle add webrick
```

이제 다시 서버를 구동시켰더니 정상적으로 로컬에서 작동함을 확인할 수 있었다.

![run-server](https://user-images.githubusercontent.com/30232837/161528393-c75fff1d-4faf-4eba-8b8c-af37e270ee2c.png "run-server"){: width="100%" height="100%"}{: .align-center}

Server address에 적힌 주소로 따라가면, 본인의 사이트를 볼 수 있다.

![myblog](https://user-images.githubusercontent.com/30232837/161528547-4ba371fa-5bc2-447c-99e2-d161db60766e.png "myblog"){: width="100%" height="100%"}{: .align-center}

> [다음 글: Minimal-mistakes 테마 Github blog 만들기 3](https://burningfalls.github.io/blog/blog-making-3/)