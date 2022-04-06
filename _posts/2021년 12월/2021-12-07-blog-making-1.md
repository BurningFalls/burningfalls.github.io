---
title: "[Github blog][Minimal-mistakes] Minimal-mistakes 테마 Github blog 만들기 1"
excerpt: "minimal-mistakes 테마를 사용하여 github blog를 만드는 과정을 서술하였다."
date: 2021-12-07
last_modified_at: 2022-04-04
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

## Remote theme method

Quick Start Guide 페이지 밑 쪽에 [Remote theme method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remote-theme-method){:target=".blank"}가 있는데, 여기서 Minimal Mistakes theme 링크를 누르면 minimal-mistakes를 바로 fork 가능하다. 그런데 fork 방식으로 하니 불편한 점이 많아서 그냥 다운로드해서 내 Github 저장소로 push했다.

## Remove the Unnecessary

[Remove the Unnecessary](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remove-the-unnecessary){:target=".blank"}에서 해당 파일들을 삭제하라고 한다. fork할 때 해당 파일들을 제외하고 fork하는 방법을 모르겠어서, 전체를 fork하고 local에 연결해서 파일을 삭제하고 다시 push했다. 그런데, fork가 아니라 위에서 언급했듯이 그냥 download 하면, local에서 삭제하고 깔끔하게 정리해서 Github에 push가 가능해진다.

![github](https://user-images.githubusercontent.com/30232837/161495252-3792ea8a-3b56-4e54-b9e7-cd777be4dc55.png "github"){: width="80%" height="80%"}{: .align-center}

![vscode](https://user-images.githubusercontent.com/30232837/161495463-68587b8b-a350-4360-b70d-fc8f2c62704b.png "vscode"){: width="80%" height="80%"}{: .align-center}

활동 툴은 Github 연동에 익숙하고 내가 느끼기에 Github과 가장 연동이 간편한 visual code(vscode)를 사용했다. `USERNAME`에 본인의 Github name을 집어넣어서 저장소 이름을 `USERNAME.github.io`로 하면 된다.

## Installing the theme

처음 블로그 만들기 시도 때 이미 [Installing the theme](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#installing-the-theme){:target=".blank"}에 적힌 Ruby나 jekyll을 설치한 후라서, 정확히 어느 타이밍에 이를 설치하고 적용시켜야 하는지 다시 확인하기 애매해졌다. 그래서 일단 사이트 글이 읽히는대로 따라서 가보기로 했다.

Jekyll에 cache를 적용시켜 사이트를 효율적으로 만들어준다고 적혀 있다. 이는 sidebar(왼쪽 메뉴)와 navigation(상단 메뉴)을 적용시키는 데 도움을 준다고 한다. 난 이 둘을 모두 사용할 것이므로, cache를 적용시키고 싶었는데 자세한 방법은 모르겠다.

## Gem-based method

[Gem-base method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#gem-based-method){:target=".blank"} 그대로 따라해보았다.

그런데 Github에 저장한 메일로 Github에서 `Page build warning`이 왔다. 

```
theme: "minimal-mistakes-jekyll"
```

이 부분에 문제가 생긴다는 내용이었다. 인터넷을 검색해보니 해당 줄은 지워버리고 remote theme를 사용하면 문제가 없다고 한다. 그래서 이 부분은 주석처리 해버리고, 다음에 나오는 remote theme method를 계속 해보기로 했다.

## Remote theme method

기존에 했던 방식을 모두 되돌리고 다시 [Remote theme method](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remote-theme-method){:target=".blank"}에 적힌 대로 했다. 

그런데 다음과 같은 에러가 발생했다.

![error](https://user-images.githubusercontent.com/30232837/161500137-250346ed-7419-4a88-af41-9dcaf386a52b.png "error"){: width="80%" height="80%"}{: .align-center}

이는 기존에 만들었던 Gemfile.lock과 충돌한다는 의미여서, 기존에 만든 Gemfile.lcok을 삭제하고 다시 `bundle`을 입력하였다. 그랬더니 error 없이 잘 수행되었다.

Minimal-mistakes의 버전도 뒤에 @를 붙여서 지정할 수 있는데, 일단 지정을 안한 채로 지나갔다. 여기까지 수행하고 `https://USERNAME.github.io`로 들어갔을 때 사이트가 잘 보여져야 하는데, 다행히도 성공적인 모습을 볼 수 있었다.

![myblog](https://user-images.githubusercontent.com/30232837/161500604-bbad2fef-11ca-4ce7-b06d-c2ab4e80fe29.png "myblog"){: width="80%" height="80%"}{: .align-center}

> [다음 글: Minimal-mistakes 테마 Github blog 만들기 2](https://burningfalls.github.io/blog/blog-making-2/)

