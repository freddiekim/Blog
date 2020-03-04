---

layout: post
title: "GOF Design Pattern-Template"
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
#### Title : GOF Design Pattern-template

#### reference

1. [3실청년-adapter-예 ](http://iilii.egloos.com/3806897) 
2. [디자인패턴 - 템플릿 메소드 패턴](https://jusungpark.tistory.com/24?category=630296)
3. [head first Design Pattern - 템플릿 메소드 패턴](http://wiki.gurubee.net/pages/viewpage.action?pageId=1507409)

***
#### Template Method Pattern 이란?

예제는 위 reference를 참고해서 수정해서 사용했습니다. \\

메소드에서 알고리즘의 골격을 정의한다. \\
알고리즘의 여러 단계 중 일부는 서브클래스에서 구현할 수 있다. \\
템플릿 메소드를 이용하면 알고리즘의 구조는 그대로 유지하면서 서브클래스에서 특정 단계를 재정의 할 수 있다.

|:--------:|:--------:|:--------:|
| coffee | tea | 기타 |
| boilWater() | boilWater() |  공통적인 부분은 templat으로 만듬 |
| steepTeaBag() | brewCoffeeGrinds() |   | 
| pourInCup() | pourInCup() | 공통적인 부분은 templat으로 만듬 |
| addLemon() | addSugarAndMilk() |   |

만일 위 처럼 Tea를 만드는 절차와 Coffee를 만드는 절차가 위와 같다면 \\
공통적인 부분은 template class로 만들 수 있다.

#### 필요한 경우만 함수를 다시 덮어 씌우고 싶을때 
추상 class에서 abstract으로 선언하면 무조건 상속받는 클래스에서는 구현을 해야함. \\
그러나 가끔 상속받는 쪽에서 구현 하기 싫을 때도 존재함. \\
이런 경우는 추상 class에서 함수를 기본만 구현해 놓고 밑에서 덮어 씌우도록 권한을 주는 방법이 존재함. \\
즉 상속 받은 class에서 필요시 작성해서 추가로 기능을 넣을 수 있음. \\
이런 방식을 hook라고 함. \\
후크(hook)는 추상클래스에서 선언되는 메소드긴 하지만 \\
기본적인 내용만 구현되어 있거나 아무 코드도 들어있지 않은 메소드.

커피나 차에서 설탕등 옵션을 추가로 제공하고 싶을떄 사용 가능함. \\
기본은 yes로 커피는 설탕, 차는 레몬을 추가함. 여기서 사용자의 옵션에 따라 추가하고 싶은 경우 \\
Hook 방법을 사용하면 쉽게 구현 할 수 있음.

메인 함수.
~~~

    Coffee coffee = new Coffee();

    Console.WriteLine("\n커피 준비중...");
    coffee.prepareReceipe();

    TeaWithHook teaHook = new TeaWithHook();
    CoffeeWithHook coffeeHook = new CoffeeWithHook();

    Console.WriteLine("\n (옵션) 차 준비중...");
    teaHook.prepareRecipe();

    Console.WriteLine("\n (옵션) 커피 준비중...");
    coffeeHook.prepareRecipe();

~~~

~~~

    public abstract class CaffeinBeverageWithHook
    {

        public void prepareRecipe()
        {
            boilWater();
            brew();
            pourInCup();
            if (customerWantsCondiments())
            {
                addCondiments();
            }
        }

        public abstract void brew();

        public abstract void addCondiments();

        void boilWater()
        {
            Console.WriteLine("물 끓이는 중");
        }

        void pourInCup()
        {
            Console.WriteLine("컵에 따르는 중");
        }

        public virtual bool customerWantsCondiments()
        {    //이 메소드는 서브클래스에서 필요에 따라
            return true;                                    //오버라이드 할수 있는 메소드이므로 후크이다.
        }
    }

~~~

~~~
    public class CoffeeWithHook : CaffeinBeverageWithHook
    {
        public override void addCondiments()
        {
            Console.WriteLine("우유와 설탕을 추가하는 중");
        }

        public override void brew()
        {
            Console.WriteLine("필터로 커피를 우려내는 중");
        }

        /*
         * 후크 메소드: 서브클래스에서 재정의
         */
        public override bool customerWantsCondiments()
        {
            String answer = getUserInput();

            if (answer.ToLower().StartsWith("y"))
                return true;
            else
                return false;
        }

        private String getUserInput()
        {
            String answer = null;

            Console.WriteLine("커피에 우유와 설탕을 넣어 드릴까요? (y/n) ");

            try
            {
                answer = "yes";
                Console.WriteLine(answer);
            }
            catch (Exception ex)
            {
                Console.WriteLine("IO 오류");
            }

            if (answer == null)
            {
                return "no";
            }
            return answer;
        }
    }
~~~

~~~
    public class TeaWithHook : CaffeinBeverageWithHook
    {
        public override void addCondiments()
        {
            Console.WriteLine("레몬을 추가하는 중");
        }

        public override void brew()
        {
            Console.WriteLine("차를 우려내는 중");
        }

        public override bool customerWantsCondiments()
        {
            String answer = getUserInfo();

            if (answer.ToLower().StartsWith("y"))
                return true;
            else
                return false;
        }

        private String getUserInfo()
        {
            String answer = null;

            Console.WriteLine("차에 레몬을 넣어 드릴까요? (y/n) ");

            try
            {
                answer = "yes";
                Console.WriteLine(answer);
            }
            catch (Exception ex)
            {
                Console.WriteLine("IO 오류");
            }

            if (answer == null)
            {
                return "no";
            }
            return answer;
        }
    }
~~~
