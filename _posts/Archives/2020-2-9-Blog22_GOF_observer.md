---

layout: post
title: "GOF Design Pattern-Observer"
categories: Archives
tags: [documentation,GOF]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2020-02-09
#### Title : GOF Design Pattern Basic

#### reference

0. [GOF 디자인 패턴](http://iilii.egloos.com/tag/디자인패턴)
0. [클린코드 & 디자인 패턴](https://hyesun03.github.io/archive/)
1. [참조1](http://iilii.egloos.com/m/3902774) 
2. [참조2](https://flowarc.tistory.com/entry/디자인-패턴-옵저버-패턴Observer-Pattern?category=562154) 
3. [참조3](https://docs.microsoft.com/ko-kr/dotnet/standard/events/observer-design-pattern#applying-the-pattern) 

#### GOF design pattern 기초
어려워서 공부를 못했는데 쉽게 적어 놓은 사이트를 알게 되어서 위 참고 자료를 보고 공부해야겠다.

1. Observer Pattern 

난이도 순이다. 참조하자! \\
참조 1을 구현해보자!. 

옵저버 패턴은 \\
-- 어떤 클래스에 변화가 일어 났을 때 다른 클래스에 통보를 해주는 패턴 임. \\
-- 보통 어떤 클래스를 Observable이라고 함 주체 객체를 의미함. \\
-- 통보를 받는 클래스를 Observer라고 함 관찰 객체를 의미함. \\
-- 주체 객체와 관찰 객체는 1:1 관계를 가질 수 있지만 보통 1 : N 관계를 가짐. 

위 예제를 응용해서 C# 버전으로 만들어 봤다. 나중에 git에 정리해서 올리겠다. \\
구독자가 해지가능하도록 만들었다.

~~~
메인 코드
            NewsMachine newsMachine = new NewsMachine();
            Subscriber person1 = new Subscriber("철수");
            Subscriber person2 = new Subscriber(newsMachine,"순이");

            newsMachine.setNewsInfo("오늘 한파", "전국 영하 18도");

            newsMachine.add(person1);

            newsMachine.setNewsInfo("다시 전달 : 오늘 한파", "전국 영하 18도");

            newsMachine.delete(person1);

            newsMachine.setNewsInfo("밤꽃 축제", "3월 ~ 4월");

            person1.withraw();

            newsMachine.setNewsInfo("다시 전달 : 밤꽃 축제", "3월 ~ 4월");
~~~

~~~
    public class NewsInfo
    {
        public string title;
        public string news;
    }


    public class NewsMachine : IObservable
    {
        private List<IObserver> observers;
        private NewsInfo newsInfo;
        public NewsMachine()
        {
            observers = new List<IObserver>();
            newsInfo = new NewsInfo();
        }

        public void add(IObserver obs)
        {
            observers.Add(obs);
        }

        public void delete(IObserver obs)
        {
            int index = observers.IndexOf(obs);
            observers.RemoveAt(index);
        }

        public void setNewsInfo(String title, String news)
        {
            newsInfo.title = title;
            newsInfo.news = news;
            notifyObserver(newsInfo);
        }

        public void notifyObserver(object obj)
        {
            foreach(IObserver obs in observers)
            {
                obs.update(this, obj);
            }
        }
    }    
~~~

~~~
    public class Subscriber : IObserver
    {
        private IObservable observable = null;
        private string obj;

        public Subscriber(IObservable observable, string name)
        {
            this.observable = observable;
            obj = name;
            observable.add(this);
        }

        public Subscriber(string name)
        {
            obj = name;
        }

        public void update(IObservable o, Object arg)
        {
            if (observable != null)
            {
                if (ReferenceEquals(observable, o))
                {
                    NewsInfo newinfo = (NewsInfo)arg;
                    display(newinfo.title, newinfo.news);
                }
            }
            else
            {
                NewsInfo newinfo = (NewsInfo)arg;
                display(newinfo.title, newinfo.news);
            }
        }

        public void withraw()
        {
            if(observable != null)
            {
                observable.delete(this);
            }
        }

        public void display(string title, string news)
        {
            string newsString = "title : " + title + "\n -------- \n" + news + "\n";

            Console.WriteLine("구독자 : {0} \n\n<< 오늘의 뉴스 >> \n {1}" , obj, newsString);

        }


    }
~~~

~~~
    public interface IObservable
    {
        void add(IObserver observer);
        void delete(IObserver observer);
        void notifyObserver(Object arg);
    }
~~~

~~~
    public interface IObserver
    {
        void update(IObservable o, Object arg);
    }
~~~


