---

layout: post
title: "How to insert chart in markdown"
categories: Archives
tags: [documentation,Install]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2019-06-05
#### Title : markdown 문서에 차트 넣기

지금 당장 필요하지 않지만 궁금해서 찾아 봤고 있었고 정리한다.

참고 사이트 \\
-- [Embed Mermaid Charts in Jekyll without Plugin](http://kkpattern.github.io/2015/05/15/Embed-Chart-in-Jekyll.html)

실제 설치 branch version \\
-- [ImanimalXI-graph_editor_page](https://github.com/knsv/mermaid/tree/ImanimalXI-graph_editor_page)

mermaidjs 공식 github \\
-- [mermaidjs](https://mermaidjs.github.io/)

***
0.2.0 최신버전 여러 버전을 해봤는데 위 버전이 제일 안정적이 었다. 나한테는 그래서 난 위 버전을 clone후 사용했다.

0) clone 으로 다운 받는다. 
~~~
git clone -b ImanimalXI-graph_editor_page --single-branch https://github.com/knsv/mermaid.git
~~~

1) dist에 있는 파일을 js 폴더를 만든 후 옮긴다. 
~~~
cp -r ../mermaid/dist/ ./js/
~~~

2) head.html에 아래 내용을 추가한다. 
~~~
<script src="mermaid.full.min.js"></script>
~~~

3) markdown 문서에 아래 처럼 작성한다. 
~~~
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
