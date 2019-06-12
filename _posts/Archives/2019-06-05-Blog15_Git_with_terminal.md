---

layout: post
title: "How to use git on the command line"
categories: Archives
tags: [documentation,Install]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2019-06-05
#### Title : command로 git 사용법 

tortoise에서 gui만 사용하다보니 terminal에서 사용법을 정리할 필요가 있는것 같다. 

#### reference

[git에서 특정 브랜치만 clone하는 방법](https://www.slipp.net/questions/577)



***

#### what I understood

1) branch 만 clone 하기
~~~
git clone -b {branch_name} --single-branch {저장소 URL}
~~~

2) ssh key 등록하기
push를 했더니 안되더라 아마도 ssh를 이용해야할 것 같다.

3) github desktop 사용하기 on ubuntu 18.04