---

layout: post
title: "Machine Learning - basic01"
categories: archive
tags: [documentation,sample]
meta: ""
topic: "Machine Learning"
image:
 feature:
 teaser:
 credit:
 creditlink:

---

### 글 출처

지금 현재 "알고리즘 중심의 머신러닝 가이드"를 보고 있지만 [SanghyukChun's Blog](http://sanghyukchun.github.io/)블로그가 괜찮아서 이 글을 읽고 먼저 정리해보려고 한다.

2017-05-09
: 처음에는 정리하면서 적으려고 했는데 공부해보니 정리되어 있는것을 또 정리할 필요는 없을 것 같다.
: 모르는 용어, 새로운 용어 정리 부터 필요한것 같다.

--- 읽어볼 만한 글 ---
- 17번 : open source란?
- 21번 : 빅데이터 이야기
- 24번 : 수학을 공부해야하는 이유
- 25번 : latex수식 사용하는 방법
- 37번/38번 : [Distance Metric Learning](http://sanghyukchun.github.io/37/)(와우 이런게 있었다니..)

### Repo of study about machine learning.

##### 3

머신러닝 정의 : 관계를 알 수 없는 수 많은 데이터들 사이에서 관계를 찾아내주는 기술.

종류 :

##### supervised Learning

###### regression : continuous 한거

-	hypothesis, linear regression : 예측 되는 데이터와 결과 값 사이의 관계
-	cost function, loss function : 가장 좋은 hypothesis를 선택하기위해 사용하는 기준
-	dradient descent : gradient계산을 통해서 함수의 local minimum을 찾아가는 과정.
	: 적절한 hypothesis찾기 --> loss function 최소 값 : how ? --> gradient descent --> 단점 존재(overfitting and local minimum) : Model selection and Regulation(이건 뭥미?)

###### classification : discrete 한거

##### unsupervised learning
