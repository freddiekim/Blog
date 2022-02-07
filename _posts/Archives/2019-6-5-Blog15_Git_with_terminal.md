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


[git ssh 설명](https://help.github.com/en/articles/connecting-to-github-with-ssh) 

[Adding a new SSH key to your GitHub account](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account)


[github desktop download](https://snapcraft.io/github-desktop)
***

#### what I understood

1) branch 만 clone 하기
~~~
git clone -b {branch_name} --single-branch {저장소 URL}
~~~

2) ssh key 등록하기
push를 했더니 안되더라 아마도 ssh를 이용해야할 것 같다.
ssh를 이용하면 id와 password를 입력없이 사용할수 있다. 
2-1)
-- 점검
-- ls -al ~/.ssh
public key 와 private key 가 존재해야함.
여기서 id_ras.pub and id_ras 가 존재해야함.
~~~
# Generating a new SSH key
ssh-keygen -t ras -b 4096 "freddiekim.sr@gmail.com"
# Adding your SSH key to the ssh-agent
    #Start the ssh-agent in the background.
    eval "$(ssh-agent -s)" 
    # Add your SSH private key to the ssh-agent.
    ssh-add ~/.ssh/id_rsa   
~~~

2-2) copy the ssh to your clipboard and then paste key on your github.
~~~
# Downloads and installs xclip.
sudo apt-get install xclip

# Copies the contents of the id_rsa.pub file to your clipboard
xclip -sel clip < ~/.ssh/id_rsa.pub
~~~

3) github desktop 사용하기 on ubuntu 18.04
snap을이용해서
~~~
sudo snap install github-desktop --beta --classic
~~~
