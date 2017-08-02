---

layout: post
title: "ML -CNN, activation function"
categories: archive
tags: [documentation,machine learning]
meta: ""
topic: "Distance metric"
image:
 feature:
 teaser:
 credit:
 creditlink:

---

머신러닝을 공부하려고하니 너무 방대하고 실제로 나의 업무에 어떻게 적용해야할지 모르겠다.
근본적인 원인은 난 로직를 C로 구현하는데 c로 어떻게 구현해야할 감이 안오는것이 문제였다.
책 : "처음만나는 머신러닝과 딥러닝" 아래 책이 나한테 약간의 해답을 준 책인것 같다.

책을 다 읽어본 결과 왜 CNN이 유명한지 알 수있었다.
vanishing gradient 현상을 없에기 위해서 
pooling layer를 집어 넣고 CNN을 사용한다고 설명하고있다.

그러나 책이 워낙 얇다보니 궁금한 점이 많다. 
- vanishing gradient를 막는 것은 pooling layer 인가 아니면 ReLU인가?
- 각각 레이어를 섞어서 쓰는데 기준은?
- 그래서 요즘은 다 activation Function으로 ReLU만 사용하나?

### [CNN초보자가 만드는 초보자가이드](https://www.slideshare.net/leeseungeun/cnn-vgg-72164295)
내용 : CNN과 전반적인 내용이 담겨있다.
 
### [Activation Functions](http://mongxmongx2.tistory.com/13)
내용 : activation 함수에 대한 설명이 나와있다.
