---

layout: post
title: "Pycharm 03"
categories: Archives
tags: [documentation,Pycharm]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2018-05-28
#### Title : Pycharm - 03
- 이번강의는 Tensor flow를 python을 이용해서 사용해보려고한다.
- 강의명 : 파이썬 텐서플로우 & 머신러닝 from youtube
- 강사 : 동빈나
- 선택이유 : 우선 동영상이 짧다. 그리고 내가 부족하고 궁금해 했던 내용이 들어있다. 30강쯤 .헉 많이 들어야함. ㅠㅠ....
- 1강 - tensor flow 설치 및 hello world! [완료](https://www.youtube.com/watch?v=qxUD7fOseBQ&index=1&list=PLRx0vPvlEmdAbnmLH9yh03cw9UQU_o7PO)
- 2강 - linear regression에대한 설명. 완료
- 3강 - linear regression에대한 설명. 완료
- 4강 - linear regression에대한 실습. [완료](https://www.youtube.com/watch?v=bttjuId61dw&list=PLRx0vPvlEmdAbnmLH9yh03cw9UQU_o7PO&index=4)
- 코드가 길면 안 넣지만 짧으므로 추가한다.
- placeholder 내용 추가 :
- global_variables_initializer 하는 역할 추가 :
- run하는 역할 추가 :

~~~ python
  import os
  import tensorflow as tf
  os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'

  xData = [1, 2, 3, 4, 5, 6, 7]
  yData = [25000, 55000, 75000, 110000, 128000, 155000, 180000]
  W = tf.Variable(tf.random_uniform([1], -100, 100))
  b = tf.Variable(tf.random_uniform([1], -100, 100))
  X = tf.placeholder(tf.float32)
  Y = tf.placeholder(tf.float32)
  H = W*X + b
  cost = tf.reduce_mean(tf.square(H-Y))
  a = tf.Variable(0.01)
  optimizer = tf.train.GradientDescentOptimizer(a)
  train = optimizer.minimize(cost)
  init = tf.global_variables_initializer()
  sess = tf.Session()
  sess.run(init)
  for i in range(5001):
      sess.run(train, feed_dict={X: xData, Y: yData})
      if i % 500 == 0:
          print(i, sess.run(cost, feed_dict={X: xData, Y: yData}), sess.run(W), sess.run(b))

  print(sess.run(H, feed_dict={X: [8]}))
~~~

5장 아나콘다 및 주피터 개발 환경
- 나중에 필요하면 듣고 설치하자!

6장 변수와 상수
-

7장 placeholder
- 가변되는 편수는 placeholder로 정의함. 즉 학십시키려는 변수와 아닌변수를 구분하기 위해서 도입한 개념임.
- a = tf.placeholder(dtype=tf.float32)
- sess.run(y, feed_dict={a : mathsore})

8장 기본함수
- 한줄 주석 : #
- 여러줄 주석 : '''
- tf.negative
- tf.sign : 부호 반환
- tf.square, tf.sqrt, tf.pow, tf.maximize, tf.minimum, tf.maximum

9장 아키텍쳐

10장 Session
- 그래프가 동작하도록 하는 역할을 함.

12장 k-means

~~~ python
  from sklearn.cluster import KMeans
  import numpy as np
  import pandas as pd
  import seaborn as sb
  import matplotlib.pyplot as plt

  df = pd.DataFrame(columns=['x','y'])


  df.loc[0] = [2,3]
  df.loc[1] = [2,11]
  df.loc[2] = [2,18]
  df.loc[3] = [4,5]
  df.loc[4] = [4,7]
  df.loc[5] = [5,3]
  df.loc[6] = [5,15]
  df.loc[7] = [6,6]
  df.loc[8] = [6,8]
  df.loc[9] = [6,9]
  df.loc[10] = [7,2]
  df.loc[11] = [7,4]
  df.loc[12] = [7,5]
  df.loc[13] = [7,17]
  df.loc[14] = [7,18]
  df.loc[15] = [8,5]
  df.loc[16] = [8,4]
  df.loc[17] = [9,10]
  df.loc[18] = [9,11]
  df.loc[19] = [9,15]
  df.loc[20] = [9,19]
  df.loc[21] = [10,5]
  df.loc[22] = [10,8]
  df.loc[23] = [10,18]
  df.loc[24] = [12,6]
  df.loc[25] = [13,5]
  df.loc[26] = [14,11]
  df.loc[27] = [15,6]
  df.loc[28] = [15,18]
  df.loc[29] = [18,12]

  points = df.values

  kmeans = KMeans(n_clusters=4).fit(points)

  print(kmeans.cluster_centers_)

  df['cluster'] = kmeans.labels_

  df.loc[30] = [kmeans.cluster_centers_[0][0], kmeans.cluster_centers_[0][1], 5]
  df.loc[31] = [kmeans.cluster_centers_[1][0], kmeans.cluster_centers_[1][1], 5]
  df.loc[32] = [kmeans.cluster_centers_[2][0], kmeans.cluster_centers_[2][1], 5]
  df.loc[33] = [kmeans.cluster_centers_[3][0], kmeans.cluster_centers_[3][1], 5]

  print(df.head(34))

  sb.lmplot('x','y',data=df, fit_reg=False, scatter_kws={"s":150}, hue="cluster")

  plt.title('k-means example')
  plt.xlabel('x')
  plt.ylabel('y')

  plt.show()
~~~

- 동영상을 보고 kmeans알고리즘을 tensroflow로 구현해봤다.
- 라이브러리이기때문에 kmeans ++ 와 kmeans의 차이 그리고 이 알고리즘의 정확한 구현을 알 수 없다.
- 그래서 인터넷을 찾아서 본 결과 각 지점에서 가장 가까운 cost를 clusterid로 할당하고 다시 centroid로 지점을 계산 후
- 다시 cost를 계산하고 이런식이다. ++는 random하게 초기값을 정하는것이 아니라 uniform에서 시작하는 것이다. 솔직히 정확하게는
- 모르겠으나 느낌은 초기값을 좀 더 현실성 있게하기 위한 예외처리 기법이다.
