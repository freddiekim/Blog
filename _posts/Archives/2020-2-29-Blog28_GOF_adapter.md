---

layout: post
title: "GOF Design Pattern-Adapter"
categories: Archives
tags: [documentation,GOF]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: true
---

#### Time : 2020-02-29
#### Title : GOF Design Pattern-adapter

#### reference

1. [3실청년-adapter - 예 ](http://iilii.egloos.com/3789009) 
2. [Adapter 패턴-쉬운예](https://jusungpark.tistory.com/22)

***
#### 

변환 해주는 class이다. 보통 두개의 서로다른 interface를 연결해주는 class이다.

~~~

    float[] array_float = new float[3];
    array_float[0] = 1;
    array_float[1] = 2;
    array_float[2] = 3;

    Console.WriteLine("\n");

    EnumeratorFactory EnumToIterator = new EnumeratorFactory(array_float.GetEnumerator());

    iterator Iiterator = EnumToIterator;
    Iiterator.Reset();
    Iiterator.MoveNext();
    Iiterator.remove(Iiterator.Current);

    while (Iiterator.MoveNext())
    {
        Console.Write("{0} ", Iiterator.Current);
    }
    
~~~

interface 새롭게 만든 iterator
~~~
    public interface iterator
    {
        object Current { get; }

        bool MoveNext();
        void Reset();
        void remove(object current);

    }

~~~

기존에 C#에서 제공해주는 interface IEnumerator
~~~        
    public interface IEnumerator
    {
        object Current { get; }

        bool MoveNext();
        void Reset();
    }
~~~

Enumerator를 iterator로 변경해주는 Factory 클래스
~~~

    public class EnumeratorFactory : iterator
    {
        IEnumerator emnumeration;
        List<object> emun_array;
        public EnumeratorFactory(IEnumerator input)
        {
            emun_array = new List<object>();

            while (input.MoveNext())
            {
                emun_array.Add(input.Current);
            };
            emnumeration = emun_array.GetEnumerator();
        }

        object iterator.Current
        {
            get
            {
                return emnumeration.Current;
            }
        }

        bool iterator.MoveNext()
        {
            return emnumeration.MoveNext();
        }

        void iterator.Reset()
        {
            emnumeration.Reset();
        }

        void iterator.remove(object Current)
        {
            emun_array.Remove(Current);
            emnumeration = emun_array.GetEnumerator();
        }
    }

~~~





