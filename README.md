### reference 
https://github.com/LeNPaul/Lagrange/blob/gh-pages/README.md

### before getting started
#### Git 설치하기
- http://git-scm.com/download/mac
- $ brew install git

### pbcopy 설정 for ubuntu
- https://medium.com/tech-epic/how-to-use-pbcopy-on-ubuntu-f12940e5e18c
우분투인 경우 아래 세팅한다.
~~~
gedit ~/.bashrc
alias pbcopy=’xclip -selection clipboard’
alias pbpaste=’xclip -selection clipboard -o’
source ~/.bashrc
~~~

#### ssh 등록하기
- https://www.lainyzine.com/ko/article/creating-ssh-key-for-github/
~~~
cat id_rsa.pub

pbcopy < ~/.ssh/id_rsa.pub
~~~

#### brew 설치하기
- https://brew.sh/index_ko
- /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

#### jekyll 설치하기
- 기존에 설치되어 있음.

#### 실행하기
- jekyll serve --baseurl '' --watch

### 터미널 단축기 실행
- https://blog.dork94.com/133
- comman + ctrl + T

### 이미지 연결
~~~
- 예) -- ![제목](../images/xxx.png)
~~~

### 잘라내기 붙여넣기
- command + option + v(잘라내기 - 붙여넣기)
- command + v(그냥 붙여넣기) 

### Youtube영상 연결 시키기
- an image
![image alt text](https://example.com/link-to-image)
- wrapped in a link
[link text](https://example.com/my-link "link title")
~~~
- 예) [![IMAGE ALT TEXT](https://img.youtube.com/vi/MoTbIAf-kpY/0.jpg)](https://www.youtube.com/watch?v=MoTbIAf-kpY "Video Title")
~~~

- 출처 : https://stackoverflow.com/questions/11804820/how-can-i-embed-a-youtube-video-on-github-wiki-pages

### visual studio code 에서 한글 입력이 잘 안될때
- File -> Preferences -> Settings -> Text Editor -> Font -> Font Family  에서 'Droid Sans Fallback' 을 제거한다.
- 출처 : https://smok95.tistory.com/283
