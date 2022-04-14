---
title: "[Github Blog][Minimal-Mistakes][Google Search Console] Github blog를 Google 검색 엔진에 노출시키기"
excerpt: "Github Blog(theme: minimal-mistakes)를 Google 검색 엔진에 노출시키기 위해 Google search console에 내 블로그를 등록한다."
date: 2022-04-07
last_modified_at: 2022-04-14
categories:
  - essay
tags:
  - blog-making
  - github-blog
  - minimal-mistakes
  - goolge-search-console
  - google-seo
---

> 이 블로그는 [Minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/){: target="_blank"} 테마가 적용되어 이를 기반으로 서술되었음을 밝힌다.

> Minimal-misakes 테마의 경우, Naver 등록은 간단히 해결되는 문제가 아님을 확인하였다. 아예 불가능한건지 아니면 다른 어려운 방법이 있는 건지는 모르겠지만, 나는 일단 등록하기를 포기했다. 

> 아직까지 Sitemap 등록을 성공시키지 못해서 계속 기다리는 중이다.

## 1. sitemap, RSS feed, robots.txt 생성

[Minimal-mistakes Github](https://github.com/mmistakes/minimal-mistakes){: target="_blank"}에서 그대로 가져온 경우(2022/04/12 기준), `_config.yml` 파일의 plugins에 아래 코드와 같이 `jekyll-sitemap` `jekyll-feed`가 이미 적혀있기 때문에 `sitemap.xml`, `feed.xml`, `robots.txt`를 따로 추가하지 않아도 자동으로 생성된다. 실제로 주소를 입력해서 확인해볼 수 있다.

```yml
# Plugins (previously gems:)
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jekyll-include-cache

# mimic GitHub Pages with --safe
whitelist:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jekyll-include-cache
```

다른 블로그를 참고해보니 `Gemfile`에도 이를 아래와 같이 적어야한다고 서술되어있다.

```
gem "jekyll-paginate"
gem "jekyll-sitemap"
gem "jekyll-gist"
gem "jekyll-feed"
gem "jekyll-include-cache"
```

그런데 내 경우, `Gemfile`에 위와 같이 작성하지 않아도 아래와 같이 url을 입력해서 확인해보니 사이트를 정상적으로 확인할 수 있었다. 그래서 뭐가뭔지 모르겠지만, 일단 혹시 몰라서 `Gemfile`에 내용을 추가하였다. (추측상으로는 설치한 다른 gem에 이미 이 내용이 포함되어 있는 것 같다.)

```
(블로그 주소)/sitemap.xml
```

![sitemap.xml](https://user-images.githubusercontent.com/30232837/162904009-37a5458a-1d77-4c65-b60f-79e923fe5e08.png "sitemap.xml"){: width="100%" height="100%"}{: .align-center}

```
(블로그 주소)/feed.xml
```

![feed.xml](https://user-images.githubusercontent.com/30232837/162904823-a42b894c-7422-46dd-8ef1-681833ebcb55.png "feed.xml"){: width="100%" height="100%"}{: .align-center}

```
(블로그 주소)/robots.txt
```

![robots.txt](https://user-images.githubusercontent.com/30232837/162904962-8d47494c-6dcf-4fc4-be34-8e58674ea9cd.png "robots.txt"){: width="100%" height="100%"}{: .align-center}

## 2. Google Search Console에 등록하기

$1.$ [Google Search Console](https://search.google.com/u/1/search-console/welcome){: target="_blank"}에 접속한다.
$2.$ 오른쪽의 `URL 접두어` 칸에 본인의 블로그 URL을 입력한다.
$3.$ `계속`을 누른다.

![google-search-console](https://user-images.githubusercontent.com/30232837/163291239-888c7965-c1ca-4986-ac57-e0290c01af15.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

$4.$ html 파일을 다운받고 블로그의 `/root` 경로에 집어넣은 뒤, Github에 push한다.

$5.$ 아래 두 번째 사진처럼 ✔ 표시로 바뀌어 Github Push가 확인되면, `확인` 버튼을 누른다.

![google-search-console](https://user-images.githubusercontent.com/30232837/163291619-a3951e70-5aad-4c75-978e-5b00f4a174fd.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

![google-search-console](https://user-images.githubusercontent.com/30232837/163293864-929c71cc-dcfd-4657-b754-4894f50e78d6.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

$6.$ 소유권이 확인되었음을 확인할 수 있다. `속성으로 이동`을 눌러서 본인 페이지 분석 창을 확인할 수 있다.

![google-search-console](https://user-images.githubusercontent.com/30232837/163292526-a99b98cc-28ea-47e6-83eb-6dffb8274ed5.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

---

사실 `Minimal-mistakes` 테마를 사용하는 경우, `_config.yml` 파일에 이미 블로그를 간편하게 등록할 수 있도록 조치가 취해져 있다.

html 파일 다운로드 방법을 사용하지 않고 밑으로 스크롤을 내려보면, txt 레코드를 본인 블로그에 복사하라고 되어있다.

`_config.yml` 파일을 확인해보면, 다음과 같은 코드를 볼 수 있다. 여기에 저 txt 레코드를 붙여넣으면 된다.

```yml
# SEO Related
google_site_verification :
```

![google-search-console](https://user-images.githubusercontent.com/30232837/163293267-8c8e01e5-08f1-42c2-8fdc-7ccfe14412b7.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

이 방법이 있음에도 불구하고 html 파일 등록을 먼저 소개한 이유는 그냥 구글에서 추천하는 권장 방법이기 때문이다. 본인이 편한대로 하면 될 것 같다. 나는 두 가지 방법을 서로 다른 구글 계정에 각각 해보았고, 현재 두 계정 모두에 블로그 분석이 등록되어 있다. 

## 3. Sitemap 등록하기

1. 왼쪽 메뉴의 `Sitemaps`에 들어간다.
2. `새 사이트맵 추가`에 `sitemap.xml`을 입력하고 `제출`을 누른다.

![google-search-console](https://user-images.githubusercontent.com/30232837/163293038-d8868386-8b44-475b-85fe-5ab16ef402c4.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

3. 사이트맵이 제출되었음을 확인할 수 있다.

![google-search-console](https://user-images.githubusercontent.com/30232837/163293110-c74688d6-445f-41b8-9c0f-4f9efee8e5e8.png "google-search-console"){: width="100%" height="100%"}{: .align-center}

---

여기서부터가 문제인데, 나는 Sitemap의 `가져올 수 없음` 상태가 한 달 동안 해결되지 않고 있다. 검색을 통해 여러 방법을 시도해보았으나, 어떤 방법으로도 문제가 해결되지 않았다. url 검사에도 전부 문제가 없으면 기다리는 것밖에는 방법이 없다고 해서, 어쩔 수 없이 계속 기다리는 중이다.

메뉴의 `URL 검사`를 통해 각 페이지마다 일일이 색인을 생성하는 방법도 있다. 그래서 문제가 해결될 기미가 보이지 않는다면, 어쩔 수 없이 귀찮더라도 모든 페이지의 색인을 일일이 등록하려고 한다. (위에서 블로그 등록 방법을 두 가지 모두 해본 이유도, 혹시나 Sitemap 등록에 영향을 줄 수도 있어 해본 실험이다.)










