---

layout: post
title: "the first thing i did after i format on my computer"
categories: Archives
tags: [documentation,git]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2020-02-02
#### Title : hello cuda

#### reference

1. [jekyll사용법 github사용법(동영상)](https://youtu.be/oiNVQ9Zjy4o?list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k)
2. [ruby 권한 버그 수정](https://jojoldu.tistory.com/288)

***
#### the first thing i did after i format on my computer.
내가 컴퓨터를 포멧 후 한일 적어 놓기. \\
오랜 만에 포멧을 하니 기억이 가물 가물 하다.
1. visual studio code 깔기
2. github desktop 깔기
3. 위 reference 1번 참조해서 설치하기 \\
-- terminal을 연다 \\
-- command line developer tools 설치( 명령어 : xcode-select --install ) \\
-- homebrew 설치 ( 명령어 : /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" ) \\
-- ruby 설치 (명령어 : brew install ruby) \\
-- jekyll 설치 (명령어 : gem install jekyll) \\
--- 에러 발생시 : 루비 버전 확인( $ ruby -v) \\
--- ruby 설치 : $ brew install rbenv ruby-build \\
--- 최신 버전 검색 : $ rbenv install -l \\
--- 최신 버전 설치 : $ rbenv install 2.7.0 ( 2020년 1월 기준) \\
--- 버전 확인 : $ rbenv versions \\
--- global 로 세팅 : $ rbenv global 2.6.4 \\
--- 버전 확인 : $ rbenv versions \\
--- vim ~/.bash_profile 로 열어서 :wq붙여 넣기 후 저장 후 나옴.
~~~
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
~~~
-- 다시 jekyll 설치 (명령어 : gem install jekyll) \\
-- jekyll 위치 확인 및 버전 확인 하기( $ which jekyll , $ jekyll -v )

4. jekyll 설치 완료 되었으면 github 로컬에서 돌려서 확인하기 \\
-- 확인 명령어 : #jekyll serve --watch --baseurl '' \\
-- 브라우져에서 : localhost:4000 사용

5. windows에서 anaconda 설치하기.

6. anaconda에서 pytorch설치하기.
-- ![윈도우 설정](../images/Install_pytorch_01.png)
PREREQUISITES \\
--- Installing on Windows
7. visual studio code에 pytorch 연결 하기.

위 2가지를 하면 우선 실습을 할 수 있는 환경은 된것이다.


