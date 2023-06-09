# 🎯 Tree
- - -

Tree는 하나의 root 노드에서 시작하여 여러 개의 자식 노드를 가질 수 있는 자료구조입니다. 각 노드는 부모-자식 관계로 이어져 있으며, 루트 노드는 부모가 없는 특수한 노드입니다. Tree는 계층적인 구조를 나타내는 데에 유용하게 사용됩니다.

<br>

### **_Tree의 용어_**
- - -

<img width="450" alt="스크린샷 2023-03-26 오후 4 25 15" src="https://user-images.githubusercontent.com/55771326/227761536-0340811a-953a-43f7-b810-e39ba3735ef9.png">

- 루트노드 : 트리의 최상위에 있는 노드 [A]
- 자식노드 : 노드 하위에 연결된 노드
  [B,C,D]는 [A]의 자식노드
- 부모노드 : 노드의 상위에 연결된 노드
  [A]는 [B,C,D]의 부모노드
- 차수(Degree) : 자식노드의 수
  [A]의 Degree는 3
- 이파리노드(Leaf) : 자식이 없는 노드(= 단말노드 : Terminal Node)
  [K,L,F,M,N,I,O,P]
- 형제노드 : 동일한 부모를 가지는 노드
  [B,C,D]는 부모가 [A]인 형제노드
- 조상노드 : 루트노드까지의 경로상에 있는 모든
  노드들의 집합
  [P]의 조상노드는 [J,D,A]
- 후손노드 : 노드 아래로 매달린 모든 노드들의 집합
  [H,I,N]은 [C]의 자손
- 서브트리 : 노드 자신과 후손노드로 구성된 트리
  [C]를 루트노드로 하는 서브트리는 [C]와 [C]의
  자손노드들로 구성된 트리
- 레벨 : 루트노드(레벨1)를 기준으로 아래로 한 층씩
  레벨이 1씩 증가
- 높이 : 트리의 최대 레벨  높이 4
- 키 : 탐색에 사용되는 노드에 저장된 정보



<br>

### **_Tree의 순회_**
- - -

트리의 순회(Traversal)란, Tree의 모든 노드를 한 번씩 방문하는 것을 말합니다. Tree를 순회하는 방법은 크게 두 가지로 나뉩니다: 깊이 우선 순회(DFS: Depth-First Search)와 너비 우선 순회(BFS: Breadth-First Search)입니다.

1. 깊이 우선 순회 (DFS)
   * 깊이 우선 순회는, Tree의 최대 깊이까지 내려가서 노드를 탐색하는 방법입니다. 깊이 우선 순회는 다시 두 가지 방법으로 나뉩니다: 전위 순회(Preorder Traversal), 중위 순회(Inorder Traversal), 후위 순회(Postorder Traversal)입니다.


2. 너비 우선 순회 (BFS)
   * 너비 우선 순회는, 레벨 순서대로 Tree를 탐색하는 방법입니다. 최상위 레벨부터 한 레벨씩 내려가면서 탐색하며, 같은 레벨의 노드들은 좌에서 우로 순서대로 방문합니다.


<br>

* 전위 순회 (Preorder Traversal)

<img width="450" alt="스크린샷 2023-03-26 오후 4 36 31" src="https://user-images.githubusercontent.com/55771326/227761973-d7e6f339-180f-4742-99a1-555d040ad989.png">

전위 순회는, 현재 노드를 가장 먼저 탐색하고, 그 다음에 왼쪽 자식 노드를 탐색하고, 마지막으로 오른쪽 자식 노드를 탐색하는 방법입니다.

<br>


* 중위 순회 (Inorder Traversal)

<img width="450" alt="스크린샷 2023-03-26 오후 4 40 20" src="https://user-images.githubusercontent.com/55771326/227762117-8568e513-2084-4753-9cf7-5701676d9117.png">

중위 순회는, 현재 노드의 왼쪽 자식 노드를 탐색한 다음, 현재 노드를 탐색하고, 마지막으로 오른쪽 자식 노드를 탐색하는 방법입니다. 중위 순회는 이진 탐색 트리(Binary Search Tree)에서 정렬된 상태로 출력하는 데에 사용됩니다.

<br>


* 후위 순회 (Postorder Traversal)

<img width="450" alt="스크린샷 2023-03-26 오후 4 41 39" src="https://user-images.githubusercontent.com/55771326/227762177-6741ab06-9bab-42cf-a8b0-1530e8ec2c07.png">

후위 순회는, 현재 노드의 자식 노드들을 먼저 탐색한 다음, 마지막으로 현재 노드를 탐색하는 방법입니다. 후위 순회는 Leaf 노드를 먼저 방문하는 등의 방법으로 활용될 수 있습니다.



<br>

### **_Tree의 활용_**
- - -

1. 계층적인 데이터를 다룰 때
   * 파일 시스템, 디렉토리 구조 등과 같이 계층적인 데이터를 표현하는데 트리 구조가 많이 사용됩니다.
2. 검색과 정렬
   * 이진 탐색 트리는 검색과 정렬을 위해 매우 효과적으로 사용됩니다.
3. 인공지능
   * 의사결정나무(decision tree)는 인공지능 분야에서 많이 사용되며, 데이터 마이닝, 패턴 인식 등에 활용됩니다.
4. 네트워크
   * 라우팅 테이블, 인터넷 프로토콜(IP) 등에서 트리 구조가 사용됩니다.
5. 그래픽스
   * 게임, 애니메이션 등에서 캐릭터나 객체의 위치를 계층적으로 표현하기 위해 트리 구조가 사용됩니다.
6. 컴파일러
   * 컴파일러는 소스 코드를 분석하고 그 결과를 트리 형태의 추상 구문 트리(Abstract Syntax Tree, AST)로 나타내기도 합니다.