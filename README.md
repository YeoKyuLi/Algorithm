# Algorithm

**가장 중요한 주제들을 먼저 공부한 뒤에는 가능한 많은 문제를 풀어 보며 겨험을 쌓자.**

**기존에 접했던 문제가 온전히 경험이 되려면 그 원리를 완전히 이해하고 변형할 수 있어야 한다.**

## <<기초 지식 - 알고리즘 문제해결전략>>
1. 알고리즘의 시간 복잡도 분석 (done)
2. 무식하게 풀기
3. 분할 정복
4. 동적 계획법
5. 선형 자료 구조
6. 큐와 스택, 데크
7. 트리의 구현과 순회
8. 이진 검색 트리
9. 우선순위 큐와 힙
10. 그래프의 표현과 정의
11. 깊이 우선 탐색
12. 너비 우선 탐색
13. 최단 경로 알고리즘


## **2021-03-13**
회고
- algorithm 정리를 여러군데 하다보니 헷갈린다. 앞으론 git에 정리하도록 하겠다.
- 정리하는것을 귀찮아 하다보니깐 자꾸 미루게된다. 앞으론 시간을 투자해서 정리하도록 하자.

## 알고리즘 해결 6단계
1. 문제를 일고 이해한다.
2. 문제를 익순한 용어로 재정의한다.
3. 어떻게 해결할지 계획을 세운다.
4. 계획을 검증한다.
5. 프로그램을 구현한다.
6. 어떻게 풀었는지 돌아보고, 개선할 방법이 있는지 찾아본다.

## 시간복잡도
1. 선형 시간 알고리즘: 수행 시간은 N에 정비례 - O(N)
2. 선형 이하 시간 알고리즘: 입력의 크기가 커지는 것보다 수행시간이 느리게 증가하는 알고리즘 - O(logN)
   - 이진 탐색
**다항 시간 알고리즘:  N / N^2, 그 외 N의 거듭제곱들의 선형 결합으로 이루어진 식들을 다항식이라고 부름.(선형 시간 알고리즘, 선형 이하 시간 알고리즘)**
3. 지수 시간 알고리즘
  - 모든 답 후보를 평가하기: 재귀
  - 지수 시간 (exponential time): 선택지가 M개라면 2^M가지
4. 시간 복잡도의 분할 상환 분석: 각 작업에 걸리는 시간은 모두 다르지만 전체 작업에 걸리는 시간이 일정한 경우 이런 방법을 적용할 수 있다.



## **Study list**
  * String / Array
    - [Stack](https://github.com/YeoKyuLi/Data-Structure/blob/master/String%20Array/stack.md)  
    - [Queue](https://github.com/YeoKyuLi/Data-Structure/blob/master/String%20Array/queue.md)
    
  * Sorting and Searching

  * [Tree](https://github.com/YeoKyuLi/Data-Structure/blob/master/Tree/tree.md) / Binaray Search Tree

  * [Graph](https://github.com/YeoKyuLi/Data-Structure/blob/master/Graph/graph.md)

  * [Linked List](https://github.com/YeoKyuLi/Data-Structure/blob/master/Linked_List/linked_list.md)

  * [Hash](https://github.com/YeoKyuLi/Data-Structure/blob/master/Hash/hash.md)

  * [Dynamic Programming]

  * [Number Theory]

  * [Bit Manipulation]
