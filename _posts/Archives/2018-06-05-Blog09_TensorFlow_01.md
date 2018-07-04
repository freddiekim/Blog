---

layout: post
title: "TensorFlow Basic"
categories: Archives
tags: [documentation,Pycharm]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2018-06-05
#### Title : TensorFlow Basic
- https://github.com/golbin/TensorFlow-ML-Exercises/blob/master/03%20-%20Gradient%20Descendent/01.py
- 좋은 예제이다. 코드만으로도 이해가 된다. 자세히 알려면 길게 늘어지는 경향이 있으므로 코드 이해만 하고 넘어가도록 하자.
- 자세한 물리적은 내용은 담에 다시 공부하도록하자!.

01 - TensorFlow Basic
~~~ python
  import tensorflow as tf

  hello = tf.constant('Hello, TensorFlow!')

  sess = tf.Session()

  print sess.run(hello)
~~~
- 모든 언어의 시작 'hello world' tensor flow는 session을 만든후 run을 해줘야 변수 내용을 볼 수 있다.
~~~ python
  sess = tf.Session()

  a = tf.constant(2)
  b = tf.constant(3)

  c = a + b

  print(c)
  print(sess.run(c))
~~~
- session을 사용하지 않으면 'Tensor("add:0", shape=(), dtype=int32)' 식으로 나온다.
~~~ python
  a = tf.placeholder(tf.int16)
  b = tf.placeholder(tf.int16)

  add = tf.add(a, b)
  mul = tf.multiply(a, b)

  with tf.Session() as sess:
      print("Addition with variables: %i" % sess.run(add, feed_dict={a: 2, b: 3}))
      print("Multiplication with variables: %i" % sess.run(mul, feed_dict={a: 2, b: 3}))
~~~
- 고정된 값이 아닌 변수선언하고 사용하고 싶을때는 placeholder를 사용한다.
- session은 필요하다.

02 - Linear Regression
~~~ python
  x_data = [1, 2, 3]
  y_data = [1, 2, 3]

  W = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
  b = tf.Variable(tf.random_uniform([1], -1.0, 1.0))

  init = tf.global_variables_initializer()
  sess = tf.Session()
  sess.run(init)

  print(sess.run(W))
  print(sess.run(b))

  hypothesis = W * x_data + b

  print(sess.run(hypothesis))

  cost = tf.reduce_mean(tf.square(hypothesis - y_data))

  a = tf.Variable(0.1)
  optimizer = tf.train.GradientDescentOptimizer(a)

  train = optimizer.minimize(cost)

  init = tf.global_variables_initializer()
  sess.run(init)

  for step in range(2001):
     sess.run(train)
     if step % 20 == 0:
         print(step, sess.run(cost), sess.run(W), sess.run(b), sess.run(a))

~~~
- GradientDescentOptimizer를 사용해서 최소값을 찾는 예제이다. 솔직히 내부가 중요하지만 그냥 이렇게 된다고 이해하고 넘어가자!.

~~~ python
  X = tf.placeholder(tf.float32)
  Y = tf.placeholder(tf.float32)

  hypothesis = W*X + b

  cost = tf.reduce_mean(tf.square(hypothesis - Y))

  a = tf.Variable(0.1)
  optimizer = tf.train.GradientDescentOptimizer(a)
  train = optimizer.minimize(cost)

  init = tf.global_variables_initializer()

  sess = tf.Session()
  sess.run(init)

  for step in range(201):
      sess.run(train, feed_dict={X: x_data, Y: y_data})
      if step % 20 == 0:
          print(step, sess.run(cost, feed_dict={X: x_data, Y: y_data}), sess.run(W), sess.run(b), sess.run(a))

  # 변수로 선언 되어 있으므로 print(sess.run(cost) 같은 명령어는 안된다.
  print(sess.run(hypothesis, feed_dict={X: 5}))
  print(sess.run(hypothesis, feed_dict={X: 2.5}))

  # output
  0 0.07728991 [1.0468608] [0.1816434] 0.1
  20 0.0009866584 [0.96351796] [0.0829323] 0.1
  40 0.00037278436 [0.9775754] [0.05097649] 0.1
  60 0.00014084911 [0.98621607] [0.03133404] 0.1
  80 5.3216005e-05 [0.9915274] [0.0192603] 0.1
  100 2.0106274e-05 [0.99479204] [0.01183888] 0.1
  120 7.5968624e-06 [0.9967988] [0.00727708] 0.1
  140 2.8704237e-06 [0.9980323] [0.00447307] 0.1
  160 1.084452e-06 [0.9987905] [0.00274946] 0.1
  180 4.09767e-07 [0.99925655] [0.00169003] 0.1
  200 1.548105e-07 [0.99954295] [0.00103882] 0.1
  [4.998754]
  [2.4998963]
~~~
- placeholder를 사용해서 x,y를 변수로 사용하는 예이다. 밑에 보면 학습이 제대로 되어서 5->4.9, 2.5 -> 2.49의 결과가 나오는것을
- 확인할 수 있다.

02 - Gradient Descendent
~~~ python
  X = [1., 2., 3.]
  Y = [1., 2., 3.]

  m = n_samples = len(X)

  W = tf.placeholder(tf.float32)

  hypothesis = tf.multiply(X, W)

  cost = tf.reduce_mean(tf.pow(hypothesis - Y, 2))/ m

  W_val = []
  cost_val = []

  sess = tf.Session()

  init = tf.global_variables_initializer()
  sess.run(init)

  for i in range(-30, 50):
      print( i*0.1, sess.run(cost, feed_dict={W: i*0.1}))
      W_val.append(i*0.1)
      cost_val.append(sess.run(cost, feed_dict={W: i*0.1}))


  plt.plot(W_val, cost_val, 'ro')
  plt.ylabel('cost')
  plt.xlabel('W')
  plt.show()
~~~
- 위 예제는 matplotlib를 사용해서 그래프를 그리는 예제이다.
- tf.pow(hypothesis - Y, 2) (w*x - y)^2 한 후 평균을 구함 입력이 3개 w가 3개 이므 평균을 구하고 /3을 한다.
- 최소값은 i = 10일때 즉 w = 1일 때 0이 나온다.

~~~ python
# exercise 2

    x_data = [1., 2., 3.]
    y_data = [1., 2., 3.]

    W = tf.Variable(tf.random_uniform([1], -10.0, 10.0))

    X = tf.placeholder(tf.float32)
    Y = tf.placeholder(tf.float32)

    hypothesis = W*X
    x = tf.Variable(0)
    cost = tf.reduce_mean(tf.square(hypothesis - Y))

    decent = W - tf.multiply(0.1, tf.reduce_mean(tf.multiply(tf.multiply(W, X) - Y, X)))
    update = W.assign(decent)

    sess = tf.Session()
    init = tf.global_variables_initializer()
    sess.run(init)

    for step in range(100):
        print(step, sess.run(update, feed_dict={X: x_data, Y: y_data}))
        print(step, sess.run(cost, feed_dict={X: x_data, Y: y_data}), sess.run(W))
~~~
- 오차 (w*x - y)*x 평균 * 0.1 즉 0.1은 step즉 반영 비율을 의미하는것 같다.
- 위 코드를 통해서 GradientDescentOptimizer를 사용하지 않고 w값을 학습시켜봤다.
- 위 코드를 이해하기 위해서 아래 assign기능을 이해해야한다. 재귀적으로 값을 계속 반영하고 싶을때는 아래처럼 assign을 사용해서
- 구성한다.
~~~ python
  x = tf.Variable(0)
  init = tf.global_variables_initializer()
  sess = tf.Session()
  sess.run(init)

  decent = 1 + x
  assign_op=x.assign(decent)

  sess.run(assign_op)
  sess.run(assign_op)
  sess.run(assign_op)
  print(sess.run(assign_op))
  print(sess.run(x))
~~~

04 - Multi-variables Linear Regression

~~~ python
  x1_data = [1, 0, 3, 0, 5]
  x2_data = [0, 2, 0, 4, 0]
  y_data = [1, 2, 3, 4, 5]

  W1 = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
  W2 = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
  b = tf.Variable(tf.random_uniform([1], -1.0, 1.0))

  hypothesis = W1 * x1_data + W2 * x2_data + b

  cost = tf.reduce_mean(tf.square(hypothesis - y_data))

  a = tf.Variable(0.1)  # learning rate
  optimizer = tf.train.GradientDescentOptimizer(a)
  train = optimizer.minimize(cost)

  init = tf.global_variables_initializer()

  sess = tf.Session()
  sess.run(init)

  for step in range(2001):
      sess.run(train)
      if step % 20 == 0:
          print(step, sess.run(cost), sess.run(W1), sess.run(W2), sess.run(b))

  print(sess.run(hypothesis))
~~~
- 이번에는 W가 2개이다 이때 어떻게 학습되는지 보여주고 있다.

~~~ python
  x_data = [[1., 0., 3., 0., 5.], [0., 2., 0., 4., 0.]]

  y_data = [1, 2, 3, 4, 5]

  W = tf.Variable(tf.random_uniform([1, 2], -1.0, 1.0))
  b = tf.Variable(tf.random_uniform([1], -1.0, 1.0))

  hypothesis = tf.matmul(W, x_data) + b

  cost = tf.reduce_mean(tf.square(hypothesis - y_data))

  a = tf.Variable(0.1)
  optimizer = tf.train.GradientDescentOptimizer(a)
  train = optimizer.minimize(cost)

  # 초기값을 이때 선언해줘야 에러가 나지 않는다.
  init = tf.global_variables_initializer()
  sess = tf.Session()
  sess.run(init)

  print(sess.run(W))

  for step in range(2001):
      sess.run(train)
      if step% 100 == 0 or step < 10 :
          print(step, sess.run(cost), sess.run(W), sess.run(b) )

  print(sess.run(hypothesis))
~~~
- 예제 1을 matrix형태로 구성한다음 계산을한 예이다. 같은 예

~~~ python
  x_data = [[1, 1, 1, 1, 1],
            [1., 0., 3., 0., 5.],
            [0., 2., 0., 4., 0.]]
  y_data = [1, 2, 3, 4, 5]

  print(x_data)
  print(y_data)

  W = tf.Variable(tf.random_uniform([1, 3], -1.0, 1.0))

  hypothesis = tf.matmul(W, x_data)

  cost = tf.reduce_mean(tf.square(hypothesis - y_data))

  a = tf.Variable(0.1)
  optimizer = tf.train.GradientDescentOptimizer(a)
  train = optimizer.minimize(cost)

  init = tf.global_variables_initializer()

  sess = tf.Session()
  sess.run(init)

  for step in range(2001):
      sess.run(train)
      if step % 100 == 0 or step <= 5:
          print(step, sess.run(cost), sess.run(W))

  result = tf.matmul(W, x_data)
  # 쉬운 예제이므로 weight가 0 1 1 로 수렴하는것을 확인 할 수 있다.
  print(sess.run(result))
~~~
- weight를 3개까지 늘려 봤을 때 예이다. 그냥 단순 입력 증가이다.

~~~ python
   script_dir = os.path.dirname(os.path.abspath(__file__))
   print(__file__)
   train_data = np.loadtxt(script_dir + '/train_04.txt', unpack=True, dtype='float32')

   # 아래 코드를 통해서 0은 시작 index -1은 끝을 말하는것을 확인 할 수 있다.
   x_data = train_data[0:-1]
   y_data = train_data[-1]

   print(x_data)
   print(y_data)

   W = tf.Variable(tf.random_uniform([1, len(x_data)], -1.0, 1.0))

   hypothesis = tf.matmul(W, x_data)

   print(hypothesis)
   cost = tf.reduce_mean(tf.square(hypothesis - y_data))

   a = tf.Variable(0.1)
   optimizer = tf.train.GradientDescentOptimizer(a)
   train = optimizer.minimize(cost)

   init = tf.global_variables_initializer()

   sess = tf.Session()
   sess.run(init)

   print(sess.run(W))
   # print(sess.run(hypothesis))


   for step in range(2001):
       sess.run(train)
       if step % 20 == 0:
           print( step, sess.run(cost), sess.run(W))

   result = tf.matmul(W, x_data)
   # 쉬운 예제이므로 weight가 0 1 1 로 수렴하는것을 확인 할 수 있다.
   print(sess.run(result))
~~~
- 위 예제는 파일로 하는 예제이다. 입력은 3개 단순한 예제이다.

<!-- 02 - Linear Regression 까지 완료
- 이것 저것 해보면서 tensroflow의 기본을 익히기에 참 좋은 예제인 것 같다.
- When in the Go to Class, Go to Symbol, or Go to File popup,
- you can ease the search by filtering the lookup list with the help of the "camel words" prefixes. -->

05 - Logistic Classification
- 임시 : http://liu.diva-portal.org/smash/get/diva2:117357/FULLTEXT05.pdf
- logistic Regression
- 해당 사이트가 설명을 잘하고 있다. [링크](https://blog.naver.com/lyshyn/221285013102)
- 해당글을 찾아보다가 이해가 안돼서 다시 찾았다. 여기 나와 있다. 어렵네....
- 파이썬 김이라는 사이트인데 좋다.[Logistic Regression]http://pythonkim.tistory.com/22?category=573319
