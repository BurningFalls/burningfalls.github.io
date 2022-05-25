---
title: "[Github Blog] Github blog를 Google 검색 엔진에 노출시키기"
excerpt: "Github Blog(theme: minimal-mistakes)를 Google 검색 엔진에 노출시키기 위해 Google search console에 내 블로그를 등록한다."
date: 2022-04-07
last_modified_at: 2022-05-25
categories:
  - blog
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

## 1. Google Search Console에 등록하기

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

이 방법이 있음에도 불구하고 html 파일 등록을 먼저 소개한 이유는 그냥 구글에서 추천하는 권장 방법이기 때문이다. 본인이 편한대로 하면 될 것 같다. 나는 두 가지 방법을 서로 다른 구글 계정에 각각 해보았고, 현재 블로그 분석은 후자의 방법이 적용되어 있다.

## 2-1. sitemap, robots.txt 자동 생성

[Minimal-mistakes Github](https://github.com/mmistakes/minimal-mistakes){: target="_blank"}에서 그대로 가져온 경우(2022/04/12 기준), `_config.yml` 파일의 plugins에 아래 코드와 같이 `jekyll-sitemap`가 이미 적혀있기 때문에 `sitemap.xml`를 따로 추가하지 않아도 자동으로 생성된다. 실제로 주소를 입력해서 확인해볼 수 있다. (robots.txt도 기본으로 있던데 그건 어느 부분에서 자동 생성되는지는 모르겠다. 네이버 등록을 위한 jekyll-feed도 있지만, 네이버 등록은 하다가 포기했다.)

```yml
# Plugins (previously gems:)
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jekyll-include-cache
```

```
(블로그 주소)/sitemap.xml
```

![sitemap.xml](https://user-images.githubusercontent.com/30232837/162904009-37a5458a-1d77-4c65-b60f-79e923fe5e08.png "sitemap.xml"){: width="100%" height="100%"}{: .align-center}

```
(블로그 주소)/robots.txt
```

![robots.txt](https://user-images.githubusercontent.com/30232837/162904962-8d47494c-6dcf-4fc4-be34-8e58674ea9cd.png "robots.txt"){: width="100%" height="100%"}{: .align-center}

## 2-2. sitemap, robots.txt 수동 생성

자동 생성이 있음에도 불구하고, 아래의 Sitemap 등록이 장시간 제대로 되지 않아서 그냥 직접 생성해보기로 하였다. **수동 생성은 본인 블로그 폴더 root 경로에 직접 두 파일을 생성해주면 된다.**

`jekyll-sitemap`으로 자동 생성된 Sitemap과의 중복을 피하기 위해 이름을 `my-sitemap.xml`로 지었다. 어차피 아래에서 Sitemap을 등록할때 url을 넘기므로, 본인이 원하는대로 이름을 지어도 상관 없다고 추측한다. **단, robots.txt에도 본인이 만든 Sitemap 주소로 내용을 바꾸어야 한다.**

Sitemap code는 다음을 복사 붙여넣기 하면 된다.

```xml
{% raw %}---{% endraw %}
{% raw %}layout: null{% endraw %}
{% raw %}---{% endraw %}

{% raw %}<?xml version="1.0" encoding="UTF-8"?>{% endraw %}
{% raw %}<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
                xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">{% endraw %}
{% raw %}    {% for post in site.posts %}{% endraw %}
{% raw %}    <url>{% endraw %}
{% raw %}        <loc>{{ site.url }}{{ post.url }}</loc>{% endraw %}
{% raw %}        {% if post.lastmod == null %}{% endraw %}
{% raw %}        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>{% endraw %}
{% raw %}        {% else %}{% endraw %}
{% raw %}        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>{% endraw %}
{% raw %}        {% endif %}{% endraw %}

{% raw %}        {% if post.sitemap.changefreq == null %}{% endraw %}
{% raw %}        <changefreq>weekly</changefreq>{% endraw %}
{% raw %}        {% else %}{% endraw %}
{% raw %}        <changefreq>{{ post.sitemap.changefreq }}</changefreq>{% endraw %}
{% raw %}        {% endif %}{% endraw %}

{% raw %}        {% if post.sitemap.priority == null %}{% endraw %}
{% raw %}        <priority>0.5</priority>{% endraw %}
{% raw %}        {% else %}{% endraw %}
{% raw %}        <priority>{{ post.sitemap.priority }}</priority>{% endraw %}
{% raw %}        {% endif %}{% endraw %}

{% raw %}    </url>{% endraw %}
{% raw %}    {% endfor %}{% endraw %}
{% raw %}</urlset>{% endraw %}
```

robots.txt는 다음과 같이 작성하였다. **이 파일은 Sitemap처럼 링크를 넘겨서 등록하는 작업이 없으므로, 이름을 바꾸어서는 안될 것 같다.**(이것도 어디까지나 추측이다.) 위에 적은대로 본인이 지은 새로운 Sitemap의 이름대로 code에 제대로 기입해주어야 한다.

```
User-agent: *
Allow: /

Sitemap: https://burningfalls.github.io/my-sitemap.xml
```

2-1에서 했던 것과 동일하게, 각각의 주소를 입력하여 파일이 제대로 생성되었는지 확인해볼 수 있다. 수동 생성한 robots.txt는 자동 생성된 파일과 이름이 동일함에도 불구하고, url 확인시 수동 생성한 파일의 내용으로 바뀐 것을 확인할 수 있었다. 아마 잘 오버라이딩된 것이 아닐까 추측한다.

```
(블로그 주소)/(본인이 지은 sitemap 이름).xml
```

![sitemap](https://user-images.githubusercontent.com/30232837/164980022-6d6958c1-00cb-41bd-9bbe-3c81f08ea24e.png "sitemap"){: width="100%" height="100%"}{: .align-center}

```
(블로그 주소)/robots.txt
```

![robots](https://user-images.githubusercontent.com/30232837/164980061-12406f7c-0bef-4339-8792-d3d29f528a1f.png "robots"){: width="100%" height="100%"}{: .align-center}


## 3. Sitemap 등록하기 (수동 생성 기준)

1. 왼쪽 메뉴의 `Sitemaps`에 들어간다.
2. `새 사이트맵 추가`에 `(본인이 지은 sitemap 이름).xml`을 입력하고 `제출`을 누른다.
3. 사이트맵이 제출되었음을 확인할 수 있다. (아래 사진은 자동 생성된 sitemap을 제출한 사진이다.)

![sitemap](https://user-images.githubusercontent.com/30232837/164980555-bc2c6cd9-2243-433b-9b6c-e30173a70347.png "sitemap"){: width="100%" height="100%"}{: .align-center}

## 4. 상황 분석

(2022.04.14)

여기서부터가 문제인데, 나는 Sitemap의 `가져올 수 없음` 상태가 한 달 동안 해결되지 않고 있다. 검색을 통해 여러 방법을 시도해보았으나, 어떤 방법으로도 문제가 해결되지 않았다. url 검사에도 전부 문제가 없으면 기다리는 것밖에는 방법이 없다고 해서, 어쩔 수 없이 계속 기다리는 중이다.

메뉴의 `URL 검사`를 통해 각 페이지마다 일일이 색인을 생성하는 방법도 있다. 그래서 문제가 해결될 기미가 보이지 않는다면, 어쩔 수 없이 귀찮더라도 모든 페이지의 색인을 일일이 등록하려고 한다. (위에서 블로그 등록 방법을 두 가지 모두 해본 이유도, 혹시나 Sitemap 등록에 영향을 줄 수도 있어 해본 실험이다.)

---

(2022.04.24)

4월 24일 현재, Google search console에 접속해보니, 4일 전부터 일부 페이지 색인이 자동으로 등록되어 구글 검색이 가능해졌음을 확인할 수 있다. (해당 url들에 직접 색인 요청을 하지 않은 상태였다.)

![create-index](https://user-images.githubusercontent.com/30232837/164980278-546c9ad2-4064-4893-a7e3-36ccb83e3019.png "create-index"){: width="100%" height="100%"}{: .align-center}

구글에 `site:(본인 블로그 주소)`를 검색하여 검색이 되는지 직접 확인해볼 수 있다.

![google-search](https://user-images.githubusercontent.com/30232837/164980437-fac89d45-9ebf-40a1-ae0a-24cdd53e2afc.png "google-search"){: width="100%" height="100%"}{: .align-center}

Sitemap을 성공적으로 인식했기 때문에 색인 요청이 잘 진행되고 있을 것이라 생각했다. 그런데 Sitemap 등록은 아래 사진과 같이 여전히 상태가 `가져올 수 없음`이다.

![sitemap](https://user-images.githubusercontent.com/30232837/164980555-bc2c6cd9-2243-433b-9b6c-e30173a70347.png "sitemap"){: width="100%" height="100%"}{: .align-center}

일단 색인 등록 상황을 좀더 지켜보기로 했다.

---

(2022.05.17)

![sitemap](https://user-images.githubusercontent.com/30232837/168701532-4786bdfb-5b4d-44c4-926d-279fec918407.png "sitemap"){: width="100%" height="100%"}{: .align-center}

1달 넘게 걸려 드디어 sitemap 등록 상태가 '성공'으로 변했다. 안그래도 페이지마다 일일이 색인을 생성해야하나 고민하고 있었는데, 2022/05/17 당일인 오늘 들어가보니 성공으로 되어있었다.

그런데 색인 생성 범위를 보니, 30개만 성공하고 134개가 제외되었음을 확인할 수 있었다. 유형을 확인해보니 **발견됨-현재 색인이 생성되지 않음**이었다.

![index](https://user-images.githubusercontent.com/30232837/168701909-4fd10add-8df6-409c-bee4-78617c46cbaf.png "index"){: width="100%" height="100%"}{: .align-center}

![image](https://user-images.githubusercontent.com/30232837/168702008-7cbf93f9-f505-4157-a33b-002917fd8f3d.png)

이에 대해 Search Console 고객센터에 조사해보니, **발견됨-현재 색인이 생성되지 않음** 상태는 다음과 같이 설명이 적혀있었다.

> **발견됨-현재 색인이 생성되지 않음**: Google에서 페이지를 발견했지만, 페이지가 아직 크롤링되지 않았습니다. 일반적으로 Google에서 URL을 크롤링하려고 했지만, 이로 인해 사이트가 과부하 상태가 될 수 있기 때문에 Google에서 크롤링 일정을 변경한 경우입니다. 그렇기 때문에 보고서에 마지막 크롤링 날짜가 비어 있는 것입니다.

아직 크롤링되지 않았다는 의미이기 때문에 좀더 기다려야 할 것 같다. 그런데, 마지막 크롤링 날짜는 등록되어 있어서 위의 문구와는 차이점이 있기도 해서 실패한 것인지 아직 안한 것인지 애매한 점이 있기는 하다.

제외되지 않은 페이지를 몇 개 골라서 URL 테스트를 해봤는데, 페이지 자체는 색인 생성 가능으로 문제가 없었다. 그냥 일일이 134개를 색인 요청할 수도 있으나, 그냥 좀더 기다려보기로 했다.