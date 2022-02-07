---

layout: post
title: "Installation Process on ubuntu 18.04"
categories: Archives
tags: [documentation,Install]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2019-06-01
#### Title : Ubuntu 18.04 설치 후 프로세스

우분투 18.04를 설치 전에 참조 했던 사이트를 적어 놓고 설치후 고생했던것을 적어놓는다.

그래서 다음에 다시 설치할때 참조하자!

1) 듀얼 부팅 \\
-- [Ubuntu 16.04 & 윈도우10 듀얼부팅 설치하기](https://cupjoo.tistory.com/53)


2) 크래픽 카드 설치(Nvidia 그래픽 카드는 따로 설치해야한다.) \\
-- [(1)우분투에서 NVIDIA 드라이버 설치 방법](https://hiseon.me/2018/02/17/install_nvidia_driver/) \\
-- [(2)NVIDIA 430.09 Released with GTX 1650 Support (How to Install)](http://ubuntuhandbook.org/index.php/2019/04/nvidia-430-09-gtx-1650-support/)

3) 한글 설정 \\
-- [Ubuntu 18.04 한글 입력기 UIM 설정하기](http://progtrend.blogspot.com/2018/06/ubuntu-1804-uim.html)

4) bash 사용법 \\
-- [Bash 입문자를 위한 핵심 요약 정리 (Shell Script)](https://blog.gaerae.com/2015/01/bash-hello-world.html)

5) 시작 프로그램 설정 \\
-- [부팅시 프로그램을 자동으로 시작하도록 설정하는 방법](https://techlog.gurucat.net/318)

6) 팁 \\
-- [10가지 팁](https://setupclass.com/2)

***

1) 듀얼 부팅 \\
-- 먼저 윈도우를 설치한다. \\
-- 파티션을 나누고 우분투 부팅 디스크를 만든다 \\
-- 우분투를 설치한다. \\
위 과정으로 진행한다. 
-- 난 윈도우 10을 설치 후 \\
-- ubuntu 18.04 이미지를 다운 받은 후 Rufus 3.0 Portable로 부팅 디스크를 만들었다. \\
-- 우분투 설치한다. \\
-- bios 셋업을 UEFI로 설정하고 보안 부팅을 off한다.


2) 그래픽 설치 방법 \\
-- 2)를 참조해서 정리한다. \\
1. 터미널을 연후 ppa에 그래픽 드라이버 등록한다.
~~~
sudo add-apt-repository ppa:graphics-drivers/ppa 
~~~
2. apt package 업데이트 한다.
~~~
sudo apt update
~~~
3. Launch Software & Updates utility, and navigate to Additional Drivers tab.

3) 한글 설정 
1. 링크되어 있는 주소로 따라하면 된다. 18.04 기본 패키지인 ibus를 disable하고 uim을 사용하는것이다. 이것을 사용하면 몇가지 장점이 있다. \\
우선 한영 전환 속도가 빠르다.18.04에서는 gui를 띄우는 바람에 전환 속도가 느리다. 그러나 uim으로 변경 후 기존 처럼 빨라져서 매우 좋다. 그리고 가장 안정적이다. 나도 visual studio code에서 이상하게 적혀서 이것을 찾아보게 되었다. 

2. enter startup on application panel. \\
-- add를 누른 후 아래 처럼 친다. 그러면 시작할때마다 셋팅이 되어서 한영 변환이 잘된다. 
~~~
sh -c "xmodmap -e 'remove mod1 = Alt_R' & xmodmap -e 'keycode 108 = Hangul' & xmodmap -e 'remove control = Control_R' & xmodmap -e 'keycode 105 = Hangul_Hanja' "
~~~

