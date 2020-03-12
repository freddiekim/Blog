---

layout: post
title: "GOF Design Pattern-singleton"
categories: Archives
tags: [documentation,GOF]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: false
---

#### Time : 2020-03-12
#### Title : singleton

#### reference

1. [3실청년 - 싱글톤](http://iilii.egloos.com/3807664) 
2. [명월 일지 - 싱글톤](https://nowonbun.tistory.com/431)
3. [head first - singleton](http://wiki.gurubee.net/pages/viewpage.action?pageId=1507403)
***

아래 내용들은 위 reference를 참고해서 수정해서 사용했습니다. \\

#### singleton 을 공부하기 앞서...
1,2,3을 순서대로 읽으면 도움이 많이 될것이다. 난이도 순이다.\\
정의는 head first가 가장 깔끔하다 그러므로 위 정의를 이용할 생각임.

#### singleton 이란?
싱글턴패턴은 인스턴스가 하나 뿐인 특별한 객체를 만들 수 있게 해주는 패턴이다. \\
어떤 용도로 쓰는 건가?  \\
스레드 풀이라던가, 캐시, 대화상자, 사용자설정, 디바이스드라이버 등등 객체가 전체프로그램에서 오직 하나만 생성되어야 하는 경우에 사용한다. \\
그럼 전역변수로 static 으로 선언해서 사용하면 되지 않느냐? \\
전역 변수로 객체를 생성하면 어플리케이션이 실행 될 때 객체가 생성될 것이다. \\
그 객체가 자원을 많이 차지 한다면 사용도 되기전에, 괜히 자원만 차지한다. 사용하지 않는다면 아무 쓸 데 없는 객체가 되겠지.


#### synchronized in c# ???
[synchronized c#에서 하는법](https://stackoverflow.com/questions/541194/c-sharp-version-of-javas-synchronized-keyword)

first method
~~~
[MethodImpl(MethodImplOptions.Synchronized)]
public void SomeMethod() {/* code */}
~~~

second method
~~~
private readonly object syncLock = new object();
public void SomeMethod() {
    lock(syncLock) { /* code */ }
}
~~~

#### 그래서 어떻게 하는것이 최선 일까?(So what is the best for a singleton pattern?)
메소드를 동기화하면 성능이 100배 정도 저하된다는 것은 기억해 두자! \\
그래서 글을 읽어보면 아래 2가지 방법 중 1개를 선택하면 좋을 듯하다. \\
메모리를 절약하고 싶으면 두번째 방법, 코드를 간단하게 짜고 싶으면 첫번째 방법으로 구현 하면된다.

first method
~~~
public class Singleton {
  private static Singleton uniqueInstance = new Singleton();

  private Singleton() {}

  public static Singleton getInstance() {
    return uniqueInstance;
  }
}
~~~

second method
~~~
public class Singleton {
  private volatile static Singleton uniqueInstance;

  private Singleton() {}

  private readonly object syncLock = new object();

  public static Singleton getInstance() {
    if (uniqueInstance == null) {
      //이렇게 하면 처음에만 동기화 된다
      lock(syncLock){
        if (uniqueInstance == null) {
          uniqueInstance = new Singleton();
        }
      }
    }
    return uniqueInstance;
  }
}
~~~

#### 사용 코드 예로 이해도를 높여 보자!.