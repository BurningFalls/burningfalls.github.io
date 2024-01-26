---
title: "[Markdown] Markdown codeblock Liquid {% %} 사용 가능하게 하기"
excerpt: Github blog markdown codeblock에서 liquid의 일부 문법이 의도대로 표출되지 않는 현상이 발생하는데, 이를 'raw' tag를 사용하여 해결한다.
date: 2022-04-25
last_modified_at: 2022-04-25
categories:
  - blog
tags:
  - markdown
  - github-blog
  - liquid
---

## 1. 문제점

Github blog에서 markdown을 사용하여 post 내용을 작성할때, codeblock에 `{% raw %}{% ... %}{% endraw %}` code를 보여주려고 이를 그대로 타이핑하게 된다. 

![non-raw](https://user-images.githubusercontent.com/30232837/164982049-16b91749-102f-45d1-ba40-01be77bcc22f.png "non-raw"){: width="100%" height="100%"}{: .align-center}

그러나, 이대로 하게 되면 이 코드가 실행된 결과를 보여주어, 블로그에 본인의 의도와 다른 내용이 표출되게 된다. 아래는 위 그대로 작성한 결과이다. 아무 코드도 보여지지 않는 것을 확인할 수 있다.

```
{% assign cattotal = 0 %}
{% for category in site.categories %}
  {% if category[0] == nav.category  %}
    {% assign cattotal = cattotal | plus: category[1].size %}
  {% endif %}
{% endfor %}
```

## 2. 해결 방법

`{% raw %}{% %}{% endraw %}`를 사용하는 경우, 아래 사진과 같이 raw tag를 사용하여 코드를 감싸주면 된다.

![raw](https://user-images.githubusercontent.com/30232837/164982209-259a924e-ea6a-4dff-acb4-985ff5915c0b.png "raw"){: width="100%" height="100%"}{: .align-center}

아래는 위 그대로 작성한 결과이다. 원래 의도대로 잘 표출되는 것을 볼 수 있다.

```
{% raw %}{% assign cattotal = 0 %}{% endraw %}
{% raw %}{% for category in site.categories %}{% endraw %}
{% raw %}  {% if category[0] == nav.category  %}{% endraw %}
{% raw %}    {% assign cattotal = cattotal | plus: category[1].size %}{% endraw %}
{% raw %}  {% endif %}{% endraw %}
{% raw %}{% endfor %}{% endraw %}
```

추가로 `{% raw %}{{ ... }}{% endraw %}`를 표출하려는 경우에도 위와 같은 방법이 필요하다고 한다. 안전하게 codeblock에서 `{ }`를 사용하는 모든 경우에 raw tag를 감싸는 것이 괜찮은 방법이라고 생각한다.