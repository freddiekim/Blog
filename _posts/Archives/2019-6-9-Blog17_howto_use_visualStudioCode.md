---

layout: post
title: "how to build and use gdb on visual studio code"
categories: Archives
tags: [documentation,Sample]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2019-xx-xx
#### Title : visual studio code에서 빌드 및 디버깅 하기.

참조한 사이트 정리.

task 설정하기 \\
-- [Visaul Studio Code 설치 및 사용법](https://evols-atirev.tistory.com/4?category=1003210)


공식 메뉴얼 \\
-- [User Guide - Basic Editing](https://code.visualstudio.com/docs/editor/codebasics)

***

내가 이해한 내용 정리.

기본 단축키 설명
빌드 구성 : '' Ctrl + Shift + b '' \\
실행 옵션 : Ctrl + p \\ 
start debugging : F5 \\
단축키 설정 : Ctrl + k then Ctrl + s

1) make 파일을 만든다. \\
난 visual studio code에서 make 파일 만 호출 할 것이므로 우선 make 파일을 만든다. \\
디버깅을 위해 옵션 -g -G 를 추가했다. \\ 

Makefile
~~~
APPS=hello

all: ${APPS}

%: %.cu
	nvcc -g -G  -gencode=arch=compute_75,code=sm_75 -o $@ $<
clean:
	rm -f ${APPS}
~~~

Makefile은 all 과 clean을 구성한다.

2) tasks.json 파일을 만든다.

코드를 짠다음 build의 단축키인 ''Ctrl + Shift + B''를 눌러 작업 구성을 한다.

~~~
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Clean",
            "type": "shell",
            "command": "make",
            "args": ["clean"],
            "group": {
                "kind": "build",
                "isDefault": true
            }

        },
        {
            "type": "shell",
            "label": "Rebuild",
            "command":"make",
            "args": [],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
~~~

3) launch.json 파일을 만든다.
F5를 누르면 기본으로 생성되는 template이 있다. 여기서 추가 해줘야하는 몇가지 옵션이 있다. 

~~~
"program": "${workspaceFolder}/${fileBasenameNoExtension}",
"externalConsole": false,
~~~

위 처럼 변경하고 아래처럼 설정해주면된다. \\ 
C에서는 "miDebuggerPath": "/usr/bin/gdb", 를 추가해주먄 디버깅을 할 수 있다. \\
~~~
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            //"MIMode": "gdb",
            "preLaunchTask": "Rebuild",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
            //"miDebuggerPath": "/usr/bin/cuda-gdb",
            //"logging": { "engineLogging": true, "trace": true, "traceResponse": true } 
        }
    ]
}
~~~