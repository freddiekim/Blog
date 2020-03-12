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
3. [참조3-c# 스터디](https://www.csharpstudy.com/CSharp/CSharp-yield.aspx)

***

아래 내용들은 위 reference를 참고해서 수정해서 사용했습니다. \\

#### GOF design pattern 기초

1. Iterator Pattern 

Array나 List를 사용할 때 데이터의 집합체 임. \\
Iterator를 사용하면 데이터와 집합체간에 분리 시켜서 생각할 수 있음. 

구현 방법에는 여러가지가 있지만 가장 대중 적인 방법 1가지만 익히도록 한다.

iterator의 의미 \\
내부적으로 iterator라는 변수가 어떤 관계를 가지는 중요하지 않음. \\
일단 iterator를 가지고 온 후에는 데이터 집합체가 뭐냐에 신경을 쓸 필요가 없어짐. \\
Iterator만 가져오면, 그냥 MoveNext()와 current를 반복하면서 원소들에 대해서 처리를 하면 됨. 

#### yield 사용법
한번 호출로 여러번 return하고 싶을때 사용. \\
보통 함수에서 return은 한번밖에 사용못합니다. \\
다시 return을 사용하려면 한번 더 함수를 호출 해야함니다. \\
그러나 yield return을 사용하면 함수안에서 여러번 return을 사용할 수 있습니다. \\
그래서 보통 for문과 같이 사용됩니다.

#### 추가
일반적으로 C# 언어서 제공하는 배열관련 명령어들은 대부분 IEnumerable 상속 받아서 구현되어 있습니다.\\
그래서 C#언어에서 제공하는 배열을 명령어를 사용하면됩니다. \\
예) List<T> , float[] ( - Array로 인식함)

#### 예제 

Stack과 MusicianList로 iterator를 구현해봤다.
~~~ 
    //example 01   
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

    //example 02
    MusicianList musicianList = new MusicianList();

    musicianList.add("설현");
    musicianList.add("초아");
    musicianList.add("아이유");

    iterator = musicianList.getList().GetEnumerator();
    Console.WriteLine("\n");

    while (iterator.MoveNext())
    {
        Console.Write("{0} ", iterator.Current);
    }

~~~

예제1을 위한 클래스 정의
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

예제2를 위한 클래스 정의
~~~
    public class MusicianList
    {
        private List<String> list;
        
        public MusicianList()
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



