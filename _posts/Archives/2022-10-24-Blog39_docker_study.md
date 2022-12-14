---

layout: post
title: "docker study"
categories: Archives
tags: [documentation,docker]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: True
---

#### Time : 2022-12-18
#### Title : docker study

#### reference

1. []() 
2. []()

***
#### 처음 docker를 시작할때 ...

sudo 쳐야만 동작할때
$ sudo usermod -aG docker $USER # 현재 접속중인 사용자에게 권한 주기

모든 컨테이너 삭제
$ sudo docker rm 'docker ps -a -q'

https://intrepidgeeks.com/tutorial/open-the-default-point-of-the-application-gui-in-docker

xhost

컨테이너 다시 시작
docker start <container name>

가동중인 컨테이너 재실행
docker restart <container name>

#가동중인 컨테이너에 접속
#docker attach <container name>

가동중인 컨테이너에 접속
docker exec -it <container name> /bin/bash






