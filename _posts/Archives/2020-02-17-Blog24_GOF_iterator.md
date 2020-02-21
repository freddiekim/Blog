---

layout: post
title: "GOF Design Pattern-Iterator"
categories: Archives
tags: [documentation,GOF]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2020-02-05
#### Title : GOF Design Pattern iterator

#### reference

0. [GOF 디자인 패턴](http://iilii.egloos.com/tag/디자인패턴)
0. [클린코드 & 디자인 패턴](https://hyesun03.github.io/archive/)
1. [참조1](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/concepts/iterators)
2. [참조2](http://iilii.egloos.com/3788564)

***
#### GOF design pattern 기초

위 참조 사이트를 참조해서 작성했습니다. 

1. Iterator Pattern \\

Array나 List를 사용할 때 데이터의 집합체 임. \\
Iterator를 사용하면 데이터와 집합체간에 분리 시켜서 생각할 수 있음. \\

구현 방법에는 여러가지가 있지만 가장 대중 적인 방법 1가지만 익히도록 한다.

iterator의 의미 \\
내부적으로 iterator라는 변수가 어떤 관계를 가지는 중요하지 않음. \\
일단 iterator를 가지고 온 후에는 데이터 집합체가 뭐냐에 신경을 쓸 필요가 없어짐. \\
Iterator만 가져오면, 그냥 MovNext()와 current를 반복하면서 원소들에 대해서 처리를 하면 됨. \\

~~~    
    Stack<int> theStack = new Stack<int>();

    //  Add items to the stack.
    for(int number = 0; number <= 9; number++)
    {
        theStack.Push(number);
    }

    IEnumerator iterator = theStack.GetEnumerator();

    while(iterator.MoveNext())
    {
        Console.Write("{0} ", iterator.Current);
    }

    //example 03
    SensorDevelperList develpList = new SensorDevelperList();

    develpList.add("설현");
    develpList.add("초아");
    develpList.add("정아");

    iterator = develpList.getList().GetEnumerator();
    Console.WriteLine("\n");

    while (iterator.MoveNext())
    {
        Console.Write("{0} ", iterator.Current);
    }

~~~

~~~
    public class Stack<T> : IEnumerable<T>
    {
        private T[] values = new T[100];
        private int top = 0;

        public void Push(T t)
        {
            values[top] = t;
            top++;
        }

        public T Pop()
        {
            top--;
            return values[top];
        }

        // This method implements the GetEnumerator method. It allows
        // an instance of the class to be used in a foreach statement.
        public IEnumerator<T> GetEnumerator()
        {
            for (int index = top - 1; index >= 0; index--)
            {
                yield return values[index];
            }
        }

        IEnumerator IEnumerable.GetEnumerator()
        {
            return GetEnumerator();
        }
    }

~~~
~~~
    public class SensorDevelperList
    {
        private List<String> list;
        
        public SensorDevelperList()
        {
            list = new List<string>();
        }

        public void add(String name)
        {
            list.Add(name);
        }

        public List<String> getList()
        {
            return list;
        }
    }
~~~



