---

layout: post
title: "나이브 베이즈(Naive Bayes)분류"
categories: Archives
tags: [documentation,template]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: True
---

#### Time : 2022-10-13
#### Title : 나이브 베이즈(Naive Bayes)분류

#### reference

1. []() 
2. []()

***
#### regularization 

##### 나이브 베이즈 분류(1/2)

[![IMAGE ALT TEXT](https://youtu.be/hO9SVW6nnhM?list=PLVNY1HnUlO241gILgQloWAs0xrrkqQfKe/0.jpg)](https://www.youtube.com/watch?v=hO9SVW6nnhM "Video Title")


조건부 확률.<br>
<br>
서로 영향을 끼치지 않을때.<br>
P(A ∩ B) = P(A)*P(B)<br>
<br>
P(A|B) = P(A)<br>
<br>
P(B|A) = P(B)<br>
<br>
서로 영향을 주는 케이스<br>
<br>
p(A ∩ B) = P(A)*P(B | A)<br>
<br>
P(B|A) = P(A ∩ B) / P(B)<br>
<br>

##### 나이브 베이즈 분류(2/2)

[![IMAGE ALT TEXT](https://youtu.be/hO9SVW6nnhM?list=PLVNY1HnUlO241gILgQloWAs0xrrkqQfKe/0.jpg)](https://www.youtube.com/watch?v=hO9SVW6nnhM "Video Title")

<br>
스팸메일일 확률 3/10<br>
free라는 단어 포함 확률 : 4/10<br>
free라는 단어를 포함한 스펨 메일 : 2/3<br>
<br>
프리라는 단어가 있을때 스팸일 확률<br>
P(spam|free) =  P(free|spam)*P(spam) / P(free)<br>
             =  ((2/3) * (3/10)) / (4/10)<br>
<br>
독립적일 경우, 분자가 P(free|spam)*P(coupon|spam)*P(spam) <br>
독립적이지 않을 경우, 분자가 P(free|spam ∩ coupon)*P(coupon|spam)*P(spam)<br>
<br>
스팸(일 확률 P(spam) = 6/14<br>
프리 확률 : P(free) = 7/14<br>
스팸이 프리 포함 확률 : P(free|spam) = 4/6<br>
쿠폰 확률 P(coupon) = 5/14<br>
스팸이 쿠폰을 포함 확률 P(coupon|spam) = 3/6<br>
<br>
P(spam|free,coupon) = P(free|coupon ∩ spam)*P(coupon|spam)*P(spam) / p(free ∩ coupon) <br>
<br>
P(free ∩ coupon) = P(free|coupon)*P(coupon)<br>

강의 가 좋음.<br>