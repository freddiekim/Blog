---

layout: post  
title: "Welcome to github blog"  
categories: blog  
tags: [documentation,sample]  
image:  
 feature:  
 teaser:  
 credit:  
 creditlink:

---

### 준비물

-	homebrew
-	github desktop
-	mac os
-	jekyll
-	jekyll-paginate
-	brew-gem
-	Ruby
-	atom

### 헤맸던 부분 정리(자문자답)

-	질문1 : 난 github으로 블로그를 만들려고 한다. 그런데 많은 블로그 관리 프로그램이 있다 뭘 써야하나?
-	답 :
	-	hugo
	-	octopress
	-	jekyll  

등등 많은 프로그램이 있었다. 그래서 다 한번씩 설치를 해봤다. 다 2분 3분만에 설치하고 블로그를 만들 수 있다고 광고해서 해봤지만 난 솔직히 시간이 많이 걸렸다. 시간은 Top secret이다. 이유는 모든게 다 처음이기때문이다. 예로 git을 terminal로는 처음 사용해봐서 이해를 못했다. 그래서 실수를 많이 했다.

지금 느끼는 거지만 다 비슷할것이라고 생각된다. 그러나 아무것도 모르는 상태에서는 어렵다. theme받아서 자기 블로그로 이름 변경하는 부분도 어렵다. 영어가 짧아서 일수도 있지만 나한테는 어려웠다. 우선 github에서 테마를 이용하지 않고 하나하나 만들어 보니 좀 이해가 됬고 테마를 받아도 수정할 수 있게 되었다. 즉 초보자는 jekyll로 익히는것이 답인것 같다. 추후 부족하면 다른것으로 갈아타도 늦지 않으니.

-	질문2 : 에디터는 뭘 써야하나?
-	답 : 윈도우는 word, notepad, notepad++ 정도면 모든 것을 다 커버한다고 생각한다. 뭐 ultra-editor를 사용하는사람도 있지만 솔직히 기본 프로그램으로 대부분 수행된다. 그러나 리눅스나 mac os에서는 파일하나 못 열겠다. vi라는 툴이 기본으로 내장되어 있지만 너무 어렵다.ㅡ.ㅡ;; 가장 많은 사람들이 사용하는 툴은 sublime이라는 editor인것 같다. 그러나 이 프로그램 사용법 나한테는 너무 어렵다. 지금도 깔려있지만 잘 안쓴다. atom은 설치 후 "atom 파일명" 치면 열리므로 그나마 환경 변수 설정을 안해줘도 돌아가서 쉽다. 그러나 시간 날때 sublime사용법도 익힐 것이다. 만일 atom을 사용한다면 해당 동영상이 좋다. [생활코딩 atom](https://opentutorials.org/module/1579)

### 참조 했던 블로그

-	까먹기 전에 참조했던 블로그를 적어 놔야겠다.
	-	[jekyll사용법 github사용법(동영상)](https://youtu.be/oiNVQ9Zjy4o?list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k)
	-	[생활 코딩 atom사용법](https://opentutorials.org/module/1579)
	-	[markdown 사용법](http://moodle.co.kr/old/help.php?file=advanced_markdown.html#linebreaks)
	-	[댓글기능 Disqus장착법](https://youtu.be/etvHFmVCvj8?list=PLm_Qt4aKpfKijgP0rDH7FSJOlS9IBGbT1)
	-	[jekyll관련 사이트(글))](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/)

### 명령어 정리

-	로컬 컴퓨터에서 확인할 때 : #jekyll serve --watch --baseurl ""
-	markdown 글자체 설치: sudo gem install redcarpet

### Step1

-	github.com 홈페이지 들어가서 repository를 만든다.  
-	master로 되어있는 부분을 gh-pages로 변경한다. 그 다음 branch로 가서 gh-pages로 변경하고 master는 삭제한다.  
-	setting에가 보면 자기가 만든 주소를 확인할 수있는데 그 주소를 누르면 자신이 github에서 만든 사이트를 확인 할 수 있다. 내 주소는이다.

### step2

-	github desk라는 프로그램을 설치한다. 이 프로그램 없이 터미널로 할 수 있지만 써보면 왜 이프로그램을 써야하는지 알 수 있다. 정말 편하다.
-	File - clone repository를 클릭하면 만들수있다.
-	repository - repository settings 부분에가서 gitignore 부분에 _site를 넣어 준다.

### step3

-	1번 동영상을 참조하는것이 훨씬 더 좋다.
