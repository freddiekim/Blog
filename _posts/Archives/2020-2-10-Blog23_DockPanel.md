---

layout: post
title: "Dock Panel on windows"
categories: Archives
tags: [documentation,DockPanel]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2020-02-10
#### Title : How to use Dock Panel Suite

#### reference

1. [WEIFEN LUO DOCKPANELSUITE](http://www.independent-software.com/weifen-luo-dockpanelsuite-tutorial-and-cookbook.html) 
2. [set Theme](http://docs.dockpanelsuite.com/themes/existing-themes.html)

***
#### 

위 내용을 참조하면 쉽게 panel을 제작 할 수 있다.

테마 설정하고 \\
~~~
    var theme = new VS2015DarkTheme();
    this.dockPanel1.Theme = theme;
~~~

생성된 form을 넣어 주면 끝.
~~~
    var dockContent = new NewDockContent();
    dockContent.Show(this.dockPanel1, DockState.DockLeft);

    dockContent2 = new Form1();

    dockContent2.Show(this.dockPanel1, DockState.DockRight);

    var dockContent3 = new Form1();

    dockContent3.Show(this.dockPanel1, DockState.Document);
~~~







