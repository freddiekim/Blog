---

layout: post
title: "Adding comment"
categories: Archives
tags: [documentation,disqus]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2020-02-21
#### Title : adding comment

#### reference

1. [댓글기능 Disqus장착법](https://youtu.be/etvHFmVCvj8?list=PLm_Qt4aKpfKijgP0rDH7FSJOlS9IBGbT1) 
2. [jekyll Post 사용법](https://www.youtube.com/watch?v=Ff8_V6IIbw0&list=PLm_Qt4aKpfKijgP0rDH7FSJOlS9IBGbT1&index=20)

***
#### 댓글 기능 추가하기.

예전부터 추가해야하지 했었는데...\\
계속 하지 않고 있다가 댓글기능 넣어야지 했었는데 너무 쉽게 구현되었다.

내가 사용하는 template은 다 구현되어 있어서 \\
_config.yml파일을 아래처럼 자신의 id로 변경하면 된다.

참조2를 보면 jekyll 언어 사용법이 나와있는데 도움이 많이 된다.\\
이 사이트가 내가 만든것이 아니지만 한 번 보면 어떻게 동작하는지 이해하는데 도움이됨.

~~~
{% %}
~~~

~~~
disqus:              "freddiekim"
~~~

~~~
# jekyll서버 동작 시키기...
$ jekyll serve --watch --baseurl ''

# 웹에서 보기
localhost:4000/

# cache지우기
rm -r -f .jekyll-cache/

# 폴더 지우기
rm -rf blog/
~~~

layout.html 에 있는 댓글 추가 구문
~~~
{% if site.disqus %}
  {% include disqus.html %}
{% endif %}
~~~










