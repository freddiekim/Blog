---

layout: post
title: "using gdb with cuda"
categories: Archives
tags: [documentation,gdb,cuda]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2019-06-09
#### Title : build 및 gdb 사용법 with cuda

#### reference

cuda-gdb가 존재함. \\
-- [Debugging Your CUDA Applications With Cuda-Gdb](http://developer.download.nvidia.com/GTC/PDF/1062_Satoor.pdf)

내가 사용하는 gpu가 turing achitecture이므로 아래사이트 참조. \\
-- [Turing Compatibility Guide for CUDA Applications](https://docs.nvidia.com/cuda/turing-compatibility-guide/index.html#building-turing-compatible-apps-using-cuda-10-0)

gdb 사용법 정리
-- [GDB 사용하기](https://jangpd007.tistory.com/54)

***
#### what I understood


#### make파일 만들기.

gpu에 따라서 옵션 설정을 다르게 해주어야한다. \\
난 turing achitecture여서 -gencode=arch=compute_75,code=sm_75 옵션을 사용했다. \\
그리고 debugging 위해서 -g -G 옵션을 주었다. 

~~~
APPS= object file name

all: ${APPS}

%: %.cu
	nvcc -g -G  -gencode=arch=compute_75,code=sm_75 -o $@ $<
clean:
	rm -f ${APPS}
~~~

#### 