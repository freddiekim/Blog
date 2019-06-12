---

layout: post
title: "Markdown-Kramdown"
categories: Archives
tags: [documentation,Markdown]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2017-11-29
#### Title : Kramdown 문법

마크다운을 정리한 사이트는 많다.

아래 사이트를 참고 하자.

[Markdown 문법(syntax) (1)](https://shjchad78.tistory.com/3)

[Quick Reference](https://kramdown.gettalong.org/quickref.html) 

latex변환기 \\
latex문법이라고 하며 아래 주소에 변환해주는 사이트가 있다 이 사이트를 이용해서 블로그를 하면 될듯 싶다. \\
-- [hostmath](http://www.hostmath.com/) \\
-- [추천사이트모음](https://leejk.net/149)

markdown 문서에 graph 넣기 \\
-- [그래프 넣기](http://kkpattern.github.io/2015/05/15/Embed-Chart-in-Jekyll.html)

markdown text highlight \\
-- [하이라이트](https://support.discordapp.com/hc/ko/articles/210298617-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4-%ED%85%8D%EC%8A%A4%ED%8A%B8-101-%EC%B1%84%ED%8C%85-%EC%84%9C%EC%8B%9D-%EA%B5%B5%EA%B2%8C-%EA%B8%B0%EC%9A%B8%EC%9E%84%EA%BC%B4-%EB%B0%91%EC%A4%84-)
***

### 2017
처음 이 글자체를 썼을때 그냥 예제가 이거여서 썼는데 이유가 있었네 ㅡㅡ;; \\
이 글자체는 수식을 포함하고 있는 markdown글자체라고 한다. \\
고수들은 다른거 쓴는것 같지만 난 이걸로 만족하고 불편하면 다시 하자 \\

사용방법 : https://kramdown.gettalong.org/quickref.html

수식 시작 : `` $$ `` 으로 시작하고 `` $$ ``으로 끝남. \\
덩어리로 묶기 : { } 사용   \\
예약어 문자로 사용하기 : use two or more backticks

테이블 alignment definition
if there is a colon only before the dashes, the column is left aligned, \\
if there are colons before and after the dashes, the column is center aligned \\
and if there is only a colon after the dashes, the column is right aligned.

### 2019

내가 자주 사용하고 알고 있으면 유용한것 만 적어놓으려고 한다. 자세한것은 위 참고를 보자!.

#### 줄로 구분하기
***,--- 로 구분선을 만들 수 있다.\\
+++도 된다고는 하나 난 안되었다.\\
예시)

***

#### 코드 블럭 사용하기.
~~~ c , ~~~ ruby, ~~~ python 처럼 사용해도 되고 그냥 ~~~만 해도 된다.

`` ~~~ `` \\
code 내용  \\
`` ~~~ ``

식으로 작성하면된다. \\
예시)

~~~
printf("Hello world")
~~~

#### 수식 사용하기.

수식을 사용하기 위해서 아래 latex변환기 도움을 받아야한다.

[hostmath](http://www.hostmath.com/)

`` $$ `` \\
수식 붙여 넣기 \\
`` $$ ``

예시)

$$
\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$

#### 마크다운 문법 비활성화.
아래처럼 사용하면 마크다운 문법을 하이라이트 되면서 비활성화 시킬 수 있다.
~~~
`` 마크다운 ``
~~~

예시)
~~~
`` $$ ``
`` ~~~ ``
`` \\ ``
~~~

#### 줄 바꾸기.
줄 바꾸는것은 여러방법으로 적용되는것 같다.
`` <br> ``, `` \\ `` , enter 등등 그러나 난 \\
`` \\ `` 가 제일 편해서 이걸 사용하고 있다.

#### 링크 만들기.

링크 만드는 법은 굉장히 쉽다.
`` [링크 Title](주소) `` 식이다. 위에 링크도 같은 방식으로 걸려 있다.

#### 이미지 넣기.

`` ![의미 없음](이미지 상대 주소) ``

#### 글자 크기 조절.
해더 타입은 총 6개 지원하고 해더 옵션을 이용해서 글자 크기를 조절한다. \\
`` #, ##, ### ~~~,###### `` 많이 `` # `` 이 붙을 수록 글자 크기는 작아진다. \\

#### 그래프 넣기.
~~~
head.html에 아래 내용 추가하고
<script src="mermaid.full.min.js"></script>

markdown 문서에 아래 내용 추가하면 아래 처럼 보인다.
<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D; 
</div>
~~~
<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D; 
</div>

#### 글자 굵게하기.

~~~
**hightlight text**
~~~