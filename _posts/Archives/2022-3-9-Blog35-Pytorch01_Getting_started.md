---

layout: post
title: "Pytorch-01-Installation"
categories: Archives
tags: [pytorch]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: true
---

#### Time : 2022-03-09
#### Title : Pytorch-01-Installation

#### reference


***

#### Pytorch-01-Installation

우분투에 설치하면서 내용을 적어 보자!.<br>

[![IMAGE ALT TEXT](https://img.youtube.com/vi/PLqnslRFeH2UrcDBWF5mfPGpqQDSta6VK4/0.jpg)](https://www.youtube.com/watch?v=PLqnslRFeH2UrcDBWF5mfPGpqQDSta6VK4 "Video Title")



##### Prerequisites

하나하나 작업 내용을 정리해보자!

##### 1. Pytorch 설치 페이지로 가자.

- https://pytorch.org/get-started/locally/

여기서 옵션을 선택해야하는데 난 Cuda 10.2 기반으로 설치할 생각 임.
그러면 기존에 설치된 cuda 버전을 제거하고 해당 버전으로 하자.

##### 2. 기존 Nvidia driver & cuda 버전 제거.
막상하고 나니 드라이버까지 지울 필요 있을까 하는 생각이듬.
Nvidia driver 완전 삭제
~~~
sudo apt-get purge nvidia*

sudo apt-get autoremove

sudo apt-get autoclean
~~~
CUDA 완전 삭제
~~~
sudo rm -rf /usr/local/cuda*

sudo apt-get --purge remove 'cuda*'

sudo apt-get autoremove --purge 'cuda*'
~~~

다지워 졌는지 확인
~~~
sudo dpkg -l | grep nvidia

sudo apt-get remove --purge 지울 이름

sudo dpkg -l | grep cuda

sudo apt-get remove --purge 지울 이름.
~~~

출처 : https://settembre.tistory.com/447


##### 3. Nvida driver 설치
2.번에서 삭제를 했다면 driver를 설치해야한다.
여기서 좀 많이 헷갈렸다. 기존에 cuda 버전을 받아도 드라이버는 있다 근데 왜 해야하나?
cuda에 있는것은 호환되는지 모르므로 해당 버전을 설치 후 cuda버전을 다시 설치는 절차다.

잘 제거 되었는지 확인
난 제거해도 밑 명령어 치며 나왔던것 같다. 일단 무시.
~~~
nvidia-smi
~~~

설치가능한 드라이버 목록 확인
~~~
ubuntu-drivers devices
~~~

출처 : https://settembre.tistory.com/448?category=948659

##### 3. cuda 설치 
밑 출처와 약간 다르게 했다.

cuda toolkit archive에 들어간다.\

https://developer.nvidia.com/cuda-toolkit-archive 

여기서 난 10.2버전을 선택했다.

옵션을 내 설정에 맞게 선택후 runfile(local)로 선택했다.

~~~
wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
sudo sh cuda_10.2.89_440.33.01_linux.run
~~~

그리고 설치 옵션이 나오는 데 이때 toolkit 만 선택하고 나머지는 하나도 선택하지 않았다.
상식적으로 호환가능한 드라이버는 이미 깔려있기 때문에 필요 없어서 이다.

설치가 끝났으면 환경 변수를 꼭 해줘야한다. 

이것을 보면 이해가 되는데 기존에 최신 버전의 cuda가 깔려있다. 그래서 추가로 까는것이므로

꼭 해줘야한다.

~~~
gedit ~/.bashrc

export LD_LIBRARY_PATH_=/usr/local/cuda-10.2/lib64:{LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export PATH=/usr/local/cuda-10.2/bin:${PATH:+:${PATH}}

source ~/.bashrc

reboot
~~~

nvidia driver 설치 확인
~~~
cat /proc/driver/nvidia/version
~~~

버전 확인
~~~
nvcc -V
~~~

nvidia-smi 쳐보면 드라이버 버전과 다른것을 확인할 수 있다.


출처 :https://settembre.tistory.com/449?category=948659

질문 : 근데 파일로 받으면 patch가 있는데 설치해야하나?

##### 4. conda 사용법 

