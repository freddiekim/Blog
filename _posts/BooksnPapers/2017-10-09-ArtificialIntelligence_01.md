---

layout: post
title: "인공지능을 이용한 빅데이터 처리 입문-01"
categories: BooksnPapers
tags: [documentation,diary]
image:
 feature:
 teaser:
 credit:
 creditlink:

---

#### Time : 2017-11-14
#### Title : 2장 탐색
이 글은 "인공지능을 이용한 빅데이터처리 입문"을 읽고 정리해 놓은 글임.<br>
탐색에는 맹목적 탐색과 경험적 탐색이 존재함.
##### 맹목적 탐색은
- 너비 우선 탐색(breath first search)<br>
- 깊이 우선 탐색(depth first search)<br>

##### 경험적 탐색은
- 최상 우선 탐색<br>
- 등산법(Hill climbimg)<br>
- 최적 경로 탐색<br>
- A 알고리즘<br>
- A* 알고리즘<br>
에대해서 설명하고 있음.

- 너비 우선 탐색
struct node{
   int nodeid; /* 노드번호 */
   int parentid; /* 상위 노드번호*/
}
위와 같이 구조체를 만든 후 openlist와 closedlist를 만듬.
어차피 search는 너비 우선 탐색으로 하게 되므로 순차적으로 searching함.
단 searching이 끝난 노드는 closedlist에 넣어 둠.

- 깊이 우선 탐색
너비 우선 탐색과 비슷하지만 새로운 노드가 발견되었을때 openlist뒤에 넣는 것이 아나라 앞에 넣는 것이 다르다.

- 최상 우선 탐색
openlist와 closedlist두개를 사용함. 이것은 같음.
그러나 openlist를 매번 휴리스틱 함수로 정렬함. 여기서는 목적지 까지 거리를 휴리스틱 함수로 가지고 정렬함.

- 등산법(hill climbing)
openlist와 closedlist두개를 두지 않고 openlist만으로 탐색하는 방법.
잘못가면 되돌아 갈수가 없으므로 끝임.

- 최적 경로 탐색 법
최상 우선 탐색법과 비슷하지만 휴리스틱 함수를 이때까지 지나온 길의 합을 사용해서 정렬한다는것이 다름.

- 상대가 있는 탐색
alpha-beta법, minimax탐색
and분기 : 최소값이 되는 가지를 선택
or분기 : 최대값이 되는 가지를 선택
예시를 보면 결과를 내고 역으로 값을 구해서 평가값을 계산하지만 바둑같은 복잡한것은 모를것 같다.

#### Time : 2017-11-14
#### Title : 3장 지식 표현
