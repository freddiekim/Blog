---

layout: post
title: "docker 사용법"
categories: Archives
tags: [documentation,docker]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: false
---

#### Time : 2022-9-2
#### Title : template

#### reference

1. []() 
2. []()

***
#### docker 사용법

기존 https://hub.docker.com 에서 이미지를 다운 받을 수 있음. <br>
$ docker pull deeplearningzerotoall/pytorch<br>
<br>
- 이미지 존재 확인<br>
$ docker images<br>
~~~
REPOSITORY                      TAG       IMAGE ID       CREATED         SIZE
hello-world                     latest    feb5d9fea6a5   11 months ago   13.3kB
deeplearningzerotoall/pytorch   latest    2b3fd7327ec7   3 years ago     4.14GB
~~~
<br>
- 도커 켜져 있는지 확인<br>
$ docker ps -a<br>
~~~
CONTAINER ID   IMAGE                           COMMAND       CREATED      STATUS                    PORTS     NAMES
7ae07faf7b7b   deeplearningzerotoall/pytorch   "/bin/bash"   5 days ago   Exited (130) 4 days ago             pt
a6dd132c3833   hello-world                     "/hello"      5 days ago   Exited (0) 5 days ago               loving_tu
~~~
<br>
- 도커 시작하기/attach 같이하기<br>
위에 보면 pt가 이름이다. 그러므로 아래처럼 치면 시작할 수 있다.<br>
~~~
$ docker start -a pt
~~~
<br>
- 이미지 삭제/컨테이너 삭제 등등<br>
출처 : https://brunch.co.kr/@hopeless/10<br>
<br>
- 나가기<br>
$ exit <br>
<br>
- 주피터 실행<br>
root@[고유번호]:~/PyTorch# sh run_jupyter_docker.sh<br>
<br>

curl -fsSL https://get.docker.com > docker.sh<br>
<br>
sudo docker run hello-world<br>
<br>
https://github.com/deeplearningzerotoall/PyTorch/blob/master/docker_user_guide.md<br>
<br>
<br>
token : 9f25bf064ddb3792c6c03f84ab0abaef8b00c37fa13afec1<br>
<br>
도커 설치 : https://github.com/deeplearningzerotoall/PyTorch/blob/master/docker_user_guide.md<br>



