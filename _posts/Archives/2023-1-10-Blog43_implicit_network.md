---

layout: post
title: "Occupancy Networks: Learning 3D Reconstruction in Function Space"
categories: Archives
tags: [documentation,template]
image:
 feature:
 teaser:
 credit:
 creditlink:
published: True
---

#### Time : 2023-1-10
#### Title : Occupancy Networks: Learning 3D Reconstruction in Function Space

#### reference

1. []() 
2. []()

***
#### Occupancy Networks: Learning 3D Reconstruction in Function Space

Occupancy Networks: Learning 3D Reconstruction in Function Space

~~~
With the advent of deep neural networks, learning-based
approaches for 3D reconstruction have gained popularity.
However, unlike for images, in 3D there is no canonical representation which is both computationally and memory efficient yet allows for representing high-resolution geometry
of arbitrary topology. Many of the state-of-the-art learningbased 3D reconstruction approaches can hence only represent very coarse 3D geometry or are limited to a restricted
domain. In this paper, we propose Occupancy Networks,
a new representation for learning-based 3D reconstruction
methods. Occupancy networks implicitly represent the 3D
surface as the continuous decision boundary of a deep neural network classifier. In contrast to existing approaches,
our representation encodes a description of the 3D output
at infinite resolution without excessive memory footprint.
We validate that our representation can efficiently encode
3D structure and can be inferred from various kinds of input. Our experiments demonstrate competitive results, both
qualitatively and quantitatively, for the challenging tasks of
3D reconstruction from single images, noisy point clouds
and coarse discrete voxel grids. We believe that occupancy
networks will become a useful tool in a wide variety of
learning-based 3D tasks.
~~~
심층 신경망의 출현으로 학습 기반
3D 재구성을 위한 접근법이 인기를 얻었다.
그러나 이미지와 달리 3D에서는 계산적이고 메모리 효율적이지만 고해상도 지오메트리를 표현할 수 있는 표준 표현이 없습니다
임의 위상의. 따라서 많은 최첨단 학습 기반 3D 재구성 접근법은 매우 거친 3D 기하학만 나타낼 수 있거나 제한된 것으로 제한된다
이 논문에서, 우리는 점유 네트워크를 제안한다,
학습 기반 3D 재구성을 위한 새로운 표현
방법들. 점유 네트워크는 암시적으로 3D를 나타낸다
심층 신경망 분류기의 연속 결정 경계로서 표면. 기존의 접근 방식과는 대조적으로,
우리의 표현은 3D 출력에 대한 설명을 암호화한다
과도한 메모리 설치 공간 없이 무한한 해상도를 제공합니다.
우리는 우리의 표현이 효율적으로 인코딩될 수 있는지 검증한다
3D 구조이며 다양한 종류의 입력으로부터 추론할 수 있다. 우리의 실험은 두 가지 모두에서 경쟁적인 결과를 보여준다
질적으로 그리고 양적으로, 도전적인 작업을 위해
단일 영상에서 3D 재구성, 노이즈가 많은 점 구름
거친 개별 복셀 그리드. 우리는 거주지가
네트워크는 매우 다양한 분야에서 유용한 도구가 될 것이다
학습 기반 3D 작업.      

##### 1. Introduction
~~~
Recently, learning-based approaches for 3D reconstruction have gained popularity [4,9,23,58,75,77]. In contrast
to traditional multi-view stereo algorithms, learned models
are able to encode rich prior information about the space of
3D shapes which helps to resolve ambiguities in the input.
While generative models have recently achieved remarkable successes in generating realistic high resolution images [36, 47, 72], this success has not yet been replicated
in the 3D domain. In contrast to the 2D domain, the community has not yet agreed on a 3D output representation
that is both memory efficient and can be efficiently inferred
from data. Existing representations can be broadly categorized into three categories: voxel-based representations
[4,19,43,58,64,69,75] , point-based representations [1,17]
and mesh representations [34, 57, 70], see Fig. 1.
Voxel representations are a straightforward generalization of pixels to the 3D case. Unfortunately, however, the
memory footprint of voxel representations grows cubically
with resolution, hence limiting na¨ıve implementations to
323 or 643 voxels. While it is possible to reduce the memory
footprint by using data adaptive representations such as octrees [61, 67], this approach leads to complex implementations and existing data-adaptive algorithms are still limited
to relatively small 2563 voxel grids. Point clouds [1,17] and
meshes [34,57,70] have been introduced as alternative representations for deep learning, using appropriate loss functions. However, point clouds lack the connectivity structure
of the underlying mesh and hence require additional postprocessing steps to extract 3D geometry from the model.
Existing mesh representations are typically based on deforming a template mesh and hence do not allow arbitrary
topologies. Moreover, both approaches are limited in the
number of points/vertices which can be reliably predicted
using a standard feed-forward network.
In this paper1
, we propose a novel approach to 3Dreconstruction based on directly learning the continuous
3D occupancy function (Fig. 1d). Instead of predicting a
voxelized representation at a fixed resolution, we predict
the complete occupancy function with a neural network fθ
which can be evaluated at arbitrary resolution. This drastically reduces the memory footprint during training. At
inference time, we extract the mesh from the learned model
using a simple multi-resolution isosurface extraction algorithm which trivially parallelizes over 3D locations.
In summary, our contributions are as follows:
• We introduce a new representation for 3D geometry
based on learning a continuous 3D mapping.
• We show how this representation can be used for reconstructing 3D geometry from various input types.
• We experimentally validate that our approach is able
to generate high-quality meshes and demonstrate that
it compares favorably to the state-of-the-art.
~~~
최근에는 3D 재구성을 위한 학습 기반 접근법이 인기를 얻고 있습니다[4,9,23,58,75,77]. 대조적으로
기존의 멀티뷰 스테레오 알고리즘, 학습된 모델에
의 공간에 대한 풍부한 사전 정보를 인코딩할 수 있습니다.
입력의 모호성을 해결하는 데 도움이 되는 3D 모양.
생성 모델은 최근 사실적인 고해상도 이미지를 생성하는 데 놀라운 성공을 거두었지만 [36, 47, 72], 이 성공은 아직 복제되지 않았습니다.
3D 도메인에서. 2D 도메인과 달리 커뮤니티는 아직 3D 출력 표현에 동의하지 않았습니다.
이는 메모리 효율적이고 효율적으로 추론할 수 있습니다.
데이터에서.

세 가지 범주: 복셀 기반 표현
[4,19,43,58,64,69,75] , 포인트 기반 표현 [1,17]
및 메쉬 표현 [34, 57, 70], 그림 1 참조.
복셀 표현은 픽셀을 3D 사례로 간단하게 일반화한 것입니다. 그러나 불행하게도
복셀 표현의 메모리 풋프린트는 입방체로 커집니다.
따라서 순진한 구현을 다음으로 제한합니다.
323 또는 643 복셀. 메모리를 줄일 수 있지만
octree[61, 67]와 같은 데이터 적응 표현을 사용하여 풋프린트, 이 접근 방식은 복잡한 구현으로 이어지고 기존 데이터 적응 알고리즘은 여전히 ​​제한적입니다.
상대적으로 작은 2563 복셀 그리드에. 포인트 클라우드[1,17] 및
메시[34,57,70]는 적절한 손실 함수를 사용하여 딥 러닝을 위한 대체 표현으로 도입되었습니다. 그러나 포인트 클라우드는 연결 구조가 부족합니다.
모델에서 3D 지오메트리를 추출하려면 추가 후처리 단계가 필요합니다.
기존 메쉬 표현은 일반적으로 템플릿 메쉬 변형을 기반으로 하므로 임의의
토폴로지. 또한 두 가지 접근 방식은
안정적으로 예측할 수 있는 점/정점의 수
표준 피드 포워드 네트워크를 사용합니다.
이 논문에서1
, 우리는 연속 학습을 기반으로 3D 재구성에 대한 새로운 접근 방식을 제안합니다.
3D 점유 기능(그림 1d). 예측하는 대신
고정 해상도에서 복셀화된 표현으로 예측합니다.
신경망 fθ를 사용한 완전한 점유 함수
임의의 해상도로 평가할 수 있습니다. 이것은 훈련하는 동안 메모리 공간을 크게 줄입니다. ~에
추론 시간, 학습된 모델에서 메쉬를 추출합니다.
3D 위치를 사소하게 병렬화하는 간단한 다중 해상도 등가면 추출 알고리즘을 사용합니다.
요약하면, 우리의 기여는 다음과 같습니다.
• 3D 지오메트리에 대한 새로운 표현을 소개합니다.
지속적인 3D 매핑 학습을 기반으로 합니다.
• 다양한 입력 유형에서 3D 형상을 재구성하는 데 이 표현을 어떻게 사용할 수 있는지 보여줍니다.
• 우리는 우리의 접근 방식이 가능하다는 것을 실험적으로 검증합니다.
고품질 메쉬를 생성하고
그것은 최신 기술에 유리하게 비교됩니다.

##### 2. Related Work
~~~
Existing work on learning-based 3D reconstruction can
be broadly categorized by the output representation they
produce as either voxel-based, point-based or mesh-based.

Voxel Representations: 
Due to their simplicity, voxels are
the most commonly used representation for discriminative
[45, 55, 63] and generative [9, 23, 58, 64, 75, 77] 3D tasks.
Early works have considered the problem of reconstructing 3D geometry from a single image using 3D convolutional neural networks which operate on voxel grids
[9, 68, 77]. Due to memory requirements, however, these
approaches were limited to relatively small 323 voxel grids.
While recent works [74, 76, 79] have applied 3D convolutional neural networks to resolutions up to 1283
, this is only
possible with shallow architectures and small batch sizes,
which leads to slow training.
The problem of reconstructing 3D geometry from multiple input views has been considered in [31, 35, 52]. Ji
et al. [31] and Kar et al. [35] encode the camera parameters together with the input images in a 3D voxel representation and apply 3D convolutions to reconstruct 3D scenes
from multiple views. Paschalidou et al. [52] introduced an
architecture that predicts voxel occupancies from multiple
images, exploiting multi-view geometry constraints [69].
Other works applied voxel representations to learn generative models of 3D shapes. Most of these methods are either based on variational auto-encoders [39, 59] or generative adversarial networks [25]. These two approaches were
pursued in [4, 58] and [75], respectively.
Due to the high memory requirements of voxel representations, recent works have proposed to reconstruct 3D
objects in a multi-resolution fashion [28, 67]. However, the
resulting methods are often complicated to implement and
require multiple passes over the input to generate the final
3D model. Furthermore, they are still limited to comparably
small 2563 voxel grids. For achieving sub-voxel precision,
several works [12,42,60] have proposed to predict truncated
signed distance fields (TSDF) [11] where each point in a
3D grid stores the truncated signed distance to the closest
3D surface point. However, this representation is usually
much harder to learn compared to occupancy representations as the network must reason about distance functions
in 3D space instead of merely classifying a voxel as occupied or not. Moreover, this representation is still limited by
the resolution of the underlying 3D grid.
~~~
학습 기반 3D 재구성에 대한 기존 작업은
출력 표현에 따라 크게 분류해야 합니다.
복셀 기반, 포인트 기반 또는 메시 기반으로 생성합니다.

복셀 표현: 단순성으로 인해 복셀은
차별에 대한 가장 일반적으로 사용되는 표현
[45, 55, 63] 및 생성 [9, 23, 58, 64, 75, 77] 3D 작업.
초기 작업에서는 복셀 그리드에서 작동하는 3D 컨볼루션 신경망을 사용하여 단일 이미지에서 3D 형상을 재구성하는 문제를 고려했습니다.
[9, 68, 77]. 그러나 메모리 요구 사항으로 인해 이러한
접근법은 상대적으로 작은 323개의 복셀 그리드로 제한되었습니다.
최근 연구[74, 76, 79]에서는 최대 1283 해상도까지 3D 컨볼루션 신경망을 적용했습니다.
, 이것은 단지
얕은 아키텍처와 작은 배치 크기로 가능
느린 훈련으로 이어집니다.
여러 입력 보기에서 3D 기하학을 재구성하는 문제는 [31, 35, 52]에서 고려되었습니다. 지
외. [31] 및 Kar et al. [35] 3D 복셀 표현에서 입력 이미지와 함께 카메라 매개변수를 인코딩하고 3D 장면을 재구성하기 위해 3D 컨볼루션을 적용합니다.
여러 보기에서. Paschalidou et al. [52] 도입
다중에서 복셀 점유를 예측하는 아키텍처
이미지, 멀티 뷰 기하학 제약을 활용[69].
다른 작업에서는 복셀 표현을 적용하여 3D 모양의 생성 모델을 학습했습니다. 이러한 방법의 대부분은 Variational Auto-Encoder[39, 59] 또는 Generative Adversarial Network[25]를 기반으로 합니다. 이 두 가지 접근 방식은
각각 [4, 58] 및 [75]에서 추구했습니다.
복셀 표현의 높은 메모리 요구 사항으로 인해 최근 작업에서 3D 재구성을 제안했습니다.
다중 해상도 방식의 개체 [28, 67]. 그러나, 그
결과 메서드는 종종 구현하기가 복잡하고
최종 결과를 생성하려면 입력을 여러 번 통과해야 합니다.
3D 모델. 또한, 그들은 여전히 ​​비교적 제한적입니다.
작은 2563 복셀 그리드. 서브 복셀 정밀도를 달성하기 위해,
몇몇 작업[12,42,60]은 잘린 부분을 예측하도록 제안했습니다.
부호 있는 거리 필드(TSDF)[11]
3D 그리드는 잘린 부호 있는 거리를 가장 가까운 거리에 저장합니다.
3D 표면 점. 그러나 이 표현은 일반적으로
네트워크가 거리 함수에 대해 추론해야 하므로 점유 표현에 비해 배우기가 훨씬 더 어렵습니다.
단순히 점유 여부로 복셀을 분류하는 대신 3D 공간에서. 또한, 이 표현은 여전히 ​​다음에 의해 제한됩니다.
기본 3D 그리드의 해상도.

~~~
Point Representations: An interesting alternative representation of 3D geometry is given by 3D point clouds which
are widely used both in the robotics and in the computer
graphics communities. Qi et al. [54, 56] pioneered point
clouds as a representation for discriminative deep learning
tasks. They achieved permutation invariance by applying a
fully connected neural network to each point independently
followed by a global pooling operation. Fan et al. [17] introduced point clouds as an output representation for 3D reconstruction. However, unlike other representations, this approach requires additional non-trivial post-processing steps
[3, 6, 37, 38] to generate the final 3D mesh.
~~~
포인트 표현: 3D 기하학의 흥미로운 대체 표현은 3D 포인트 클라우드로 제공됩니다.
로봇 공학과 컴퓨터 모두에서 널리 사용됩니다.
그래픽 커뮤니티. Qi et al. [54, 56] 개척 포인트
차별적인 딥 러닝을 위한 표현으로서의 구름
작업. 그들은 다음을 적용하여 순열 불변성을 달성했습니다.
각 지점에 독립적으로 완전히 연결된 신경망
글로벌 풀링 작업이 이어집니다. Fanet al. [17]은 3D 재구성을 위한 출력 표현으로 포인트 클라우드를 도입했습니다. 그러나 다른 표현과 달리 이 접근 방식에는 사소하지 않은 추가 후처리 단계가 필요합니다.
[3, 6, 37, 38] 최종 3D 메쉬를 생성합니다.

~~~
Mesh Representations: Meshes have first been considered for discriminative 3D classification or segmentation
tasks by applying convolutions on the graph spanned by the
mesh’s vertices and edges [5, 27, 71].
More recently, meshes have also been considered as output representation for 3D reconstruction [26,33,41,70]. Unfortunately, most of these approaches are prone to generating self-intersecting meshes. Moreover, they are only able
to generate meshes with simple topology [70], require a
reference template from the same object class [33, 41, 57]
or cannot guarantee closed surfaces [26]. Liao et al. [43]
proposed an end-to-end learnable version of the marching
cubes algorithm [44]. However, their approach is still limited by the memory requirements of the underlying 3D grid
and hence also restricted to 323 voxel resolution.
In contrast to the aforementioned approaches, our approach leads to high resolution closed surfaces without selfintersections and does not require template meshes from the
same object class as input. This idea is related to classical
level set [10, 14, 50] approaches to multi-view 3D reconstruction [18,24,32,40,53,78]. However, instead of solving
a differential equation, our approach uses deep learning to
obtain a more expressive representation which can be naturally integrated into an end-to-end learning pipeline
~~~
메쉬 표현: 메쉬는 차별적인 3D 분류 또는 세분화를 위해 처음으로 고려되었습니다.
에 걸쳐 있는 그래프에 컨볼루션을 적용하여 작업
메쉬의 정점과 가장자리 [5, 27, 71].
보다 최근에는 메시도 3D 재구성을 위한 출력 표현으로 간주되었습니다[26,33,41,70]. 불행하게도 이러한 접근 방식의 대부분은 자체 교차 메시를 생성하는 경향이 있습니다. 더군다나 그들만이 할 수 있는
간단한 토폴로지로 메쉬를 생성하려면[70],
동일한 개체 클래스의 참조 템플릿 [33, 41, 57]
또는 닫힌 표면을 보장할 수 없습니다[26]. Liaoet al. [43]
행진의 종단 간 학습 가능한 버전을 제안했습니다.
큐브 알고리즘 [44]. 그러나 그들의 접근 방식은 여전히 ​​기본 3D 그리드의 메모리 요구 사항에 의해 제한됩니다.
따라서 323 복셀 해상도로 제한됩니다.
앞서 언급한 접근 방식과 달리 우리의 접근 방식은 자체 교차가 없는 고해상도 폐쇄 표면으로 이어지며 템플릿 메시가 필요하지 않습니다.
입력과 동일한 객체 클래스. 이 아이디어는 고전과 관련이 있습니다.
레벨 세트[10, 14, 50]는 다시점 3D 재구성[18,24,32,40,53,78]에 접근합니다. 그러나 해결 대신
미분 방정식, 우리의 접근 방식은 딥 러닝을 사용하여
종단 간 학습 파이프라인에 자연스럽게 통합될 수 있는 보다 표현력 있는 표현을 얻습니다.

~~~
3. Method
In this section, we first introduce Occupancy Networks as
a representation of 3D geometry. We then describe how we
can learn a model that infers this representation from various forms of input such as point clouds, single images and
low-resolution voxel representations. Lastly, we describe a
technique for extracting high-quality 3D meshes from our
model at test time.
3.1. Occupancy Networks
Ideally, we would like to reason about the occupancy not
only at fixed discrete 3D locations (as in voxel respresentations) but at every possible 3D point p ∈ R
3
. We call the
resulting function
o : R
3 → {0, 1} (1)
the occupancy function of the 3D object. Our key insight
is that we can approximate this 3D function with a neural network that assigns to every location p ∈ R
3
an occupancy probability between 0 and 1. Note that this network is
equivalent to a neural network for binary classification, except that we are interested in the decision boundary which
implicitly represents the object’s surface.
When using such a network for 3D reconstruction of an
object based on observations of that object (e.g., image,
point cloud, etc.), we must condition it on the input. Fortunately, we can make use of the following simple functional
equivalence: a function that takes an observation x ∈ X
as input and has a function from p ∈ R
3
to R as output
can be equivalently described by a function that takes a pair
(p, x) ∈ R
3 × X as input and outputs a real number. The
latter representation can be simply parameterized by a neural network fθ that takes a pair (p, x) as input and outputs a
real number which represents the probability of occupancy:
fθ : R
3 × X → [0, 1] (2)
We call this network the Occupancy Network
~~~
3. 방법
이 섹션에서는 먼저 점유 네트워크를 다음과 같이 소개합니다.
3D 기하학의 표현. 그런 다음 우리가 어떻게
포인트 클라우드, 단일 이미지 및
저해상도 복셀 표현. 마지막으로, 우리는
고품질 3D 메쉬를 추출하는 기술
테스트 시간에 모델.
3.1. 점유 네트워크
이상적으로는 점유에 대해 추론하고 싶습니다.
고정된 불연속 3D 위치에서만(복셀 표현에서와 같이) 모든 가능한 3D 지점에서 p ∈ R
삼
. 우리는
결과 함수
또는
3 → {0, 1} (1)
3D 객체의 점유 기능. 우리의 핵심 통찰력
모든 위치 p ∈ R에 할당하는 신경망으로 이 3D 함수를 근사화할 수 있다는 것입니다.
삼
점유 확률은 0과 1 사이입니다. 이 네트워크는
결정 경계에 관심이 있다는 점을 제외하면 이진 분류를 위한 신경망과 동일합니다.
개체의 표면을 암시적으로 나타냅니다.
이러한 네트워크를 3D 재구성에 사용하는 경우
해당 객체의 관찰에 기반한 객체(예: 이미지,
포인트 클라우드 등) 입력에서 조건을 지정해야 합니다. 다행히 다음과 같은 간단한 기능을 사용할 수 있습니다.
동등성: 관측값 x ∈ X를 취하는 함수
입력으로서 p ∈ R의 함수를 가집니다.
삼
출력으로 R
쌍을 취하는 함수로 동등하게 설명할 수 있습니다.
(피, 엑스) ∈ R
3 × X를 입력으로 사용하고 실수를 출력합니다. 그만큼
후자의 표현은 (p, x) 쌍을 입력으로 취하고 a를 출력하는 신경망 fθ에 의해 간단히 매개변수화될 수 있습니다.
점유 확률을 나타내는 실수:
fθ : R
3 × X → [0, 1] (2)
우리는 이 네트워크를 Occupancy Network라고 부릅니다.

~~~
3.2. Training
To learn the parameters θ of the neural network fθ(p, x),
we randomly sample points in the 3D bounding volume of
the object under consideration: for the i-th sample in a training batch we sample K points pij ∈ R
3
, j = 1, . . . , K. We
then evaluate the mini-batch loss LB at those locations:
LB(θ) = 1
|B|
X
|B|
i=1
X
K
j=1
L(fθ(pij , xi), oij ) (3)
Here, xi
is the i’th observation of batch B, oij ≡ o(pij ) denotes the true occupancy at point pij , and L(·, ·) is a crossentropy classification loss.
The performance of our method depends on the sampling scheme that we employ for drawing the locations
pij that are used for training. In Section 4.6 we perform a detailed ablation study comparing different sampling
schemes. In practice, we found that sampling uniformly inside the bounding box of the object with an additional small
padding yields the best results.
Our 3D representation can also be used for learning probabilistic latent variable models. Towards this
goal, we introduce an encoder network gψ(·) that takes
locations pij and occupancies oij as input and predicts mean µψ and standard deviation σψ of a Gaussian distribution qψ(z|(pij , oij )j=1:K) on latent z ∈ R
L
as output. We optimize a lower bound [21, 39, 59]
to the negative log-likelihood of the generative model
p((oij )j=1:K|(pij )j=1:K):
L
gen
B
(θ, ψ) = 1
|B|
X
|B|
i=1
hX
K
j=1
L(fθ(pij , zi), oij )
+ KL (qψ(z|(pij , oij )j=1:K) k p0(z))i
(4)
where KL denotes the KL-divergence, p0(z) is a prior distribution on the latent variable zi (typically Gaussian) and
zi
is sampled according to qψ(zi
|(pij , oij )j=1:K).
~~~
3.2. 훈련
신경망 fθ(p, x)의 매개변수 θ를 학습하려면,
우리는 무작위로 3D 경계 체적의 점을
고려 대상: 교육 배치의 i번째 샘플에 대해 K 포인트 pij ∈ R을 샘플링합니다.
삼
, j = 1, . . . , K. 우리
그런 다음 해당 위치에서 미니 배치 손실 LB를 평가합니다.
LB(θ) = 1
|비|
엑스
|비|
i=1
엑스
케이
j=1
L(fθ(pij , xi), oij ) (3)
여기서, xi
는 배치 B의 i번째 관측값이고, oij ≡ o(pij)는 지점 pij에서의 실제 점유를 나타내며, L(·, ·)는 교차 엔트로피 분류 손실입니다.
우리 방법의 성능은 위치를 그리기 위해 사용하는 샘플링 방식에 따라 다릅니다.
훈련에 사용되는 pij. 섹션 4.6에서 다양한 샘플링을 비교하는 자세한 절제 연구를 수행합니다.
체계. 실제로 우리는 추가 작은
패딩이 최상의 결과를 가져옵니다.
우리의 3D 표현은 확률적 잠재 변수 모델을 학습하는 데에도 사용할 수 있습니다. 이를 향하여
목표를 달성하기 위해 인코더 네트워크 gψ(·)를 도입합니다.
위치 pij 및 점유 oij를 입력으로 사용하고 잠재 z ∈ R에서 가우시안 분포 qψ(z|(pij , oij )j=1:K)의 평균 μψ 및 표준 편차 σψ를 예측합니다.
엘
출력으로. 우리는 하한을 최적화합니다 [21, 39, 59]
생성 모델의 음의 로그 우도
p((oij )j=1:K|(pij )j=1:K):
엘
세대
비
(θ, ψ) = 1
|비|
엑스
|비|
i=1
hX
케이
j=1
L(fθ(pij, zi), oij)
+ KL (qψ(z|(pij, oij)j=1:K) k p0(z))i
(4)
여기서 KL은 KL-발산을 나타내고, p0(z)는 잠재 변수 zi(일반적으로 가우시안)에 대한 사전 분포이고
지
qψ(zi)에 따라 샘플링됩니다.
|(pij , oij )j=1:K).


~~~
3.4. Implementation Details
We implemented our occupancy network using a fullyconnected neural network with 5 ResNet blocks [29] and
condition it on the input using conditional batch normalization [13, 16]. We exploit different encoder architectures
depending on the type of input. For single view 3D reconstruction, we use a ResNet18 architecture [29]. For point
clouds we use the PointNet encoder [54]. For voxelized inputs, we use a 3D convolutional neural network [45]. For
unconditional mesh generation, we use a PointNet [54] for
the encoder network gψ. More details are provided in the
supplementary material.
~~~
3.4. 구현 세부 정보
우리는 5개의 ResNet 블록[29]과 완전히 연결된 신경망을 사용하여 점유 네트워크를 구현했습니다.
조건부 배치 정규화[13, 16]를 사용하여 입력에서 조건을 지정합니다. 다양한 인코더 아키텍처를 활용합니다.
입력 유형에 따라 다릅니다. 단일 뷰 3D 재구성을 위해 ResNet18 아키텍처를 사용합니다[29]. 포인트
우리는 PointNet 인코더[54]를 사용합니다. 복셀화된 입력의 경우 3D 컨볼루션 신경망[45]을 사용합니다. 을 위한
무조건적인 메쉬 생성을 위해 PointNet[54]을 사용합니다.
인코더 네트워크 gψ. 자세한 내용은
보충 자료.