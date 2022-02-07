---

layout: post
title: "GOF Design Pattern-decorator"
categories: Archives
tags: [documentation,GOF]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: true
---

#### Time : 2020-03-13
#### Title : decorator pattern

#### reference

1. [명월 일지-decorator](https://nowonbun.tistory.com/446?category=838281) 
2. [head first - decorator](http://wiki.gurubee.net/pages/viewpage.action?pageId=1507398)

***

아래 내용들은 위 reference를 참고해서 수정해서 사용했습니다. \\

#### decorator pattern 이란?

데코레이터 패턴은 간단하게 생각하면 interface - abstract - class 식으로 만들자의 패턴임. \\

#### decorator pattern 단점.
데코레이터 패턴을 이용해 디자인을 하다 보면 잡다한 클래스들이 많아 질 수 있다. \\
겹겹이 애워싼 객체의 정체를 알기가 힘들다.


#### decorator pattern 의미.
다른 패턴들은 이런 형태로 코딩하면 어떤 효과를 볼 수 있다 혹은 가독성이 증가한다이지만 \\
데코레이터 패턴은 제 생각에 OOP는 이렇게 만들어야 한다는 규약에 가깝습니다. \\
최근에는 클래스가 어떠한 것도 상속을 받지 않으면 무언가 잘 못 만드는 느낌마저 생깁니다. \\
그렇기 때문에 가장 중요한 패턴이라고도 생각되네요.\\
데코레이터 패턴으로 공통 함수 등을 정리하기 쉽기 때문에 가독성이 좋습니다.


