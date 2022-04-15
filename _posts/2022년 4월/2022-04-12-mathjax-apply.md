---
title: "[Github blog][Minimal-mistakes][Mathjax] Github blog에 수식 적용시키기"
excerpt: "minimal-mistakes 테마 Github blog에 mathjax로 markdown 수식 사용을 가능하게 한다."
date: 2022-04-12
last_modified_at: 2022-04-12
categories:
  - blog
tags:
  - markdown
  - github-blog
  - minimal-mistakes
  - mathjax
---

> 이 블로그는 [Minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/){: target="_blank"} 테마가 적용되어 이를 기반으로 서술되었음을 밝힌다.

> `minimal-mistakes` 테마를 사용하면 [jekyll-spaceship](https://github.com/jeffreytse/jekyll-spaceship#additions-for-unlimited-github-pages){: target="_blank"}을 사용할 수 없어서, plugin으로 mathjax를 자동으로 적용시킬 수 없다.

## 1. config 파일 markdown 체크

`_config.yml` 파일에 다음과 같이 적혀있는지 확인한다. (2022/04/12 기준으로 [github](https://github.com/mmistakes/minimal-mistakes){: target="_blank"}에서 그대로 다운받아 사용하는 경우, 해당 내용이 이미 기재되어 있다.)

```yml
markdown: kramdown
```

## 2. _includes/scripts.html 파일 변경

`_includes/scripts.html` 파일의 원래 코드 밑에 다음 코드를 추가한다.

```html
<script type="text/javascript" async
	src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML">
</script>

<script type="text/x-mathjax-config">
   MathJax.Hub.Config({
     extensions: ["tex2jax.js"],
     jax: ["input/TeX", "output/HTML-CSS"],
     tex2jax: {
       inlineMath: [ ['$','$'], ["\\(","\\)"] ],
       displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
       processEscapes: true
     },
     "HTML-CSS": { availableFonts: ["TeX"] }
   });
</script>
```

> [참고 블로그](https://www.janmeppe.com/blog/How-to-add-mathjax-to-minimal-mistakes/){: target="_blank"}

## 3. 수식 사용

### 1. 일반적인 사용

양 옆에 `$` 기호로 수식을 묶는 방식으로 사용함

```
$L = \sqrt{a^2 + (b+R)^2}$
```

> $L = \sqrt{a^2 + (b+R)^2}$

```
$dp[n][k] = dp[n-1][k-1] + dp[n-1][k]$
```

> $dp[n][k] = dp[n-1][k-1] + dp[n-1][k]$

### 2. 띄어쓰기 및 줄바꿈

`$(내용)$`에서 spacebar로 공백을 만들어도 띄어쓰기가 되지 않는다. `\,`를 사용해서 한 칸 띄거나, `\;`를 사용해서 두 칸 띌 수 있다.

`$(내용)$`에서 enter로 줄바꿈을 해도 줄바꿈이 되지 않는다. `\\`를 사용해서 줄을 바꿀 수 있다.

```
$$
(LogLife)\\(Log\,Life)\\(Log\;Life)
$$
```

> $$
(LogLife)\\(Log\,Life)\\(Log\;Life)
$$

### 3. 자주 쓰는 기호

**곱하기: `\times`**

**분수: `\frac`**

```
$\frac{(2^k-1)\times (2^k-2)}{6}$
```

> $\frac{(2^k-1)\times (2^k-2)}{6}$

---

**부등호: `\lt`, `\leq`**

```
$3\lt P\leq min(100, N-3)$
```
> $3\lt P\leq min(100, N-3)$

---

**화살표: `\rightarrow`**

```
$10$초 버튼 누르기 $\rightarrow i = i + 1$
```

> $10$초 버튼 누르기 $\rightarrow i = i + 1$

---

**물결: `\sim`**

```
$a_1\times(a_2\sim a_N$까지의 합$)+a_2\times(a_3\sim a_N$까지의 합$)$
```
> $a_1\times(a_2\sim a_N$까지의 합$)+a_2\times(a_3\sim a_N$까지의 합$)$

---

**절댓값: `\vert`**

```
$max(0, P-( \vert a-c \vert + \vert b-d \vert ))$
```
$max(0, P-( \vert a-c \vert + \vert b-d \vert ))$

---

**시그마: `\sum`**

```
$\displaystyle\sum_{k=x}^{y}{(a+2k)}$
```

>$\displaystyle\sum_{k=x}^{y}{(a+2k)}$

---

**표**

```

||재료1의 세균 수|비교|재료2의 세균 수|
|:---:|:---:|:---:|:---:|
|2일|10|<|20|
|3일|10|<|20|
|4일|20|=|20|
|5일|30|>|20|
|6일|40|=|40|
|7일|50|<|60|
```

||재료1의 세균 수|비교|재료2의 세균 수|
|:---:|:---:|:---:|:---:|
|2일|10|<|20|
|3일|10|<|20|
|4일|20|=|20|
|5일|30|>|20|
|6일|40|=|40|
|7일|50|<|60|






