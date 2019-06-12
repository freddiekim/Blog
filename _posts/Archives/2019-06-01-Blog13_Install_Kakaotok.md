---

layout: post
title: "How to install kakaotok on ubuntu 18.04"
categories: Archives
tags: [documentation,Install]
image:
 feature:
 teaser:
 credit:
 creditlink:

---
#### Time : 2019-06-01
#### Title : 우분투 18.04에 kakaotok 설치하기 

카카오톡으로 정보를 많이 주고 받다 보니 리눅스에서도 PC 카카오톡이 필요할 때가 있다. 그래서 적어 놓는다. \\

[우분투 카카오톡 설치](https://hiseon.me/2018/07/02/ubuntu-kakaotalk/)

#### 참고 사이트
1) [카카오톡 다운로드](https://www.kakaocorp.com/service/KakaoTalk)

2) [gulim.ttf 다운로드](https://doubuntu.tistory.com/7)

***

우분투 카카오톡 설치를 따라하면 된다. 단 카카오톡은 xp버전이 안정적이라고 해서 xp로 하였다. 
그리고 한글도 가끔씩 써야하므로 한글도 다운 받아서 적용하였다.

#### wine xp로 변경하는 방법.


~~~
$ winecfg
~~~
위 처럼 라고 치면 applications 탭을 선택 후 window version 속성을 xp로 변경하면된다. 

#### 한글 적용하는 방법.

1) ~/.wine/drive_c/windows/Fonts 에 gulim.ttf 복사. \\
권한 변경 
~~~
chmod 644 gulim.ttf 
~~~

2) ~/.wine/system.reg 파일을 아래 처럼 수정.
~~~
"MS Shell Dlg"="Gulim"
"MS Shell Dlg 2"="Gulim"
~~~

3) ~/.local/share/applications/wine/Programs/KakaoTalk/KakaoTalk.desktop 해당 파일을 vim으로 실행 후 아래 처럼 수정한다. \\
LANG="ko_KR.UTF-8" 추가하는 것임.

~~~
Exec=env WINEPREFIX="/home/ubuntu/.wine" LANG="ko_KR.UTF-8" wine-stable C:\\\\windows\\\\command\\\\start.exe /Unix /home/ubuntu/.wine/dosdevices/c:/ProgramData/Microsoft/Windows/Start\\ Menu/Programs/KakaoTalk/KakaoTalk.lnk
~~~
