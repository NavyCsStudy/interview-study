<details>
  <summary>1. 스택, 큐, 트리, 힙 자료구조에 대해 설명해주세요</summary>
  <li> 스택: 세로로 된 바구니와 같은 구조로 먼저 넣게 되는 자료가 마지막으로 나오게 되는 First-In Last-Out(FILO) 구조이다.</li>
<li> 큐: 가로로 된 통과 같은 구조로 먼저 넣게 되는 자료가 가장 먼저 나오는 First-In First-Out(FIFO) 구조이다.</li>
<li> 트리: 정점과 간선을 이용해 사이클을 이루지 않도록 구성한 Graph의 특수한 형태로, 계층이 있는 데이터를 표현하기에 적합하다.</li>
<li> 힙: 최댓값 또는 최솟값을 찾아내는 연산을 쉽게 하기 위해 고안된 구조로, 각 노드의 키값이 자식의 키값보다 작지 않거나(최대힙) 그 자식의 키값보다 크지 않은(최소힙) 완전이진트리이다.</li>
</details>
<details>
  <summary>1-1. 각 자료구조의 용도에 대해 설명해주세요</summary>
  <li> 스택: 함수 호출, 실행 취소(undo) 기능, 괄호 검사 등</li>
<li> 큐: 대기열 관리, 너비 우선 탐색(BFS) 알고리즘, 인쇄 대기열 등</li>
<li> 트리: 파일 시스템, 데이터베이스 인덱싱, XML 문서 파싱 등</li>
<li> 힙: 우선순위 큐 구현, 힙 정렬, 데이터 스트림의 중앙값 찾기 등</li>
</details>
<details>
  <summary>1-2. 스택과 큐의 실사용 예를 들어주세요</summary>
  [Stack - 자바의 Stack 메모리 영역]<br>
지역변수와 매개변수 데이터 값이 저장되는 공간이며, 메소드 호출시 메모리에 할당되고 종료되면 메모리가 해제되며,
LIFO(Last In First Out)구조를 가집니다.<br>
[Queue - OS의 스케쥴러]<br>
자원의 할당과 회수를 하는 스케쥴러 역할을 큐가 할 수 있습니다.<br>
메모리에 적재된 다수의 프로세스 중 어떤 프로세스에게 자원을 할당할 것인가 그 순서를 결정하는 것이 자원의 효율적인 사용에 있고,
가장 단순한 형태의 스케쥴링 정책이 선입선처리(First Com First Served) 즉, 큐라고 볼 수 있습니다.
</details>
<details>
  <summary>1-3. 스택과 큐는 각각 어떠한 자료구조로 구현하는 게 좋을까요?</summary>
  스택 : List로 구현하면 객체를 제거하는 작업이 필요하다. 하지만 Array로 구현하면 삭제할 필요 없이 index를 줄이고 초기화만 하면 되므로, Array로 구현하는 것이 좋다.

큐: Array로 구현하면 poll 연산 이후 객체를 앞당기는 작업이 필요하다. 하지만 List로 구현하면 객체 1개만 제거하면 되므로 삽입 및 삭제가 용이한 LinkedList로 구현하는 것이 좋다.
</details>
<details>
  <summary>1-4. 우선순위 큐에 대해 설명해주세요</summary>
  우선순위큐는 가장 우선순위가 높은 데이터를 먼저 꺼내기 위해 고안된 자료구조입니다. 우선순위 큐를 구현하기 위해서 일반적으로 힙을 사용합니다. 힙은 완전이진트리를 통해서 구현되었기 때문에 우선순위 큐의 시간복잡도는 O(logn)입니다.<br>
우선순위 큐 구현 방식 → 배열, 연결 리스트, 힙<br>
그중 힙 방식이 worst case라도 시간 복잡도 O(logN)을 보장하기 때문에 일반적으로 완전 이진트리 형태의 힙을 이용해 구현합니다.
</details>

---

<details>
  <summary>2. Array와 List 자료구조에 대해 설명해주세요</summary>
  <li> Array: 배열은 같은 타입의 데이터를 연속적인 메모리 공간에 순서대로 저장하는 자료구조입니다. 배열의 각 요소는 인덱스를 통해 직접 접근할 수 있습니다.</li>
<li> List: 리스트는 데이터를 순서대로 저장하는 선형 자료구조입니다. 배열과 달리 크기가 동적으로 변할 수 있으며, 데이터의 삽입과 삭제가 유연합니다.</li>
</details>
<details>
  <summary>2-1. Array와 ArrayList의 차이점에 대해 설명해주세요</summary>
  Array는 크기가 고정적이고, ArrayList는 크기가 가변적입니다.<br>
Array는 초기화 시 메모리에 할당되어 ArrayList보다 속도가 빠르고,<br>
ArrayList는 데이터 추가 및 삭제 시 메모리를 재할당하기 때문에 속도가 Array보다 느립니다.
</details>
<details>
  <summary>2-2. ArrayList와 LinkedList의 차이점에 대해 설명해주세요</summary>
  ArrayList는 데이터들이 순서대로 늘어선 배열의 형식을 취하고 있지만, LinkedList는 자료의 주소값으로 서로 연결된 형식을 가지고 있습니다. 

ArrayList는 인덱스(index)로 해당 원소(element)에 접근할 수 있어 찾고자 하는 원소의 인덱스 값을 알고 있으면 O(1)에 해당 원소로 접근할 수 있습니다. 즉, RandomAccess가 가능해 속도가 빠르다는 장점이 있습니다.

하지만 삽입 또는 삭제의 과정에서 각 원소들을 shift 해줘야 하는 비용이 생겨 이 경우 시간 복잡도는 O(n)이 된다는 단점이 있습니다.

이 문제점을 해결하기 위한 자료구조가 LinkedList입니다. 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있기 때문에 이 부분만 다른 값으로 바꿔주면 삽입과 삭제를 O(1)로 해결할 수 있습니다.

하지만 LinkedList는 원하는 위치에 한 번에 접근할 수 없다는 단점이 있습니다. 원하는 위치에 삽입을 하고자 하면 원하는 위치를 Search 과정에 있어서 첫번째 원소부터 다 확인해봐야 합니다.

간단히 정리하면, ArrayList는 검색이 빠르지만, 삽입, 삭제가 느리다. LinkedList는 삽입, 삭제가 빠르지만, 검색이 느리다.
</details>

---

<details>
  <summary>3. Hash Table 자료구조와 시간복잡도에 대해 설명해주세요</summary>
  해시 테이블은 (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠르게 데이터를 검색할 수 있는 자료구조입니다.

빠른 검색 속도를 제공하는 이유는 내부적으로 배열(버킷)을 사용하여 데이터를 저장하기 때문입니다.

각 Key값은 해시함수에 의해 고유한 index를 가지게 되어 바로 접근할 수 있으므로 평균 O(1)의 시간 복잡도로 데이터를 조회합니다. 

하지만 index값이 충돌이 발생한 경우 Chanining에 연결된 리스트들까지 검색해야 하므로 O(N)까지 증가할 수 있습니다.
</details>
<details>
  <summary>3-1. 해시 충돌에 대해 설명해주세요</summary>
  두 개 이상의 key가 hash function을 거쳤을 때 동일한 해시 값을 없는 상황을 말합니다. 서로 다른 key가 같은 해시로 변경되면 같은 공간에 2개의 value가 저장되므로 key-value가 1:1로 매핑되어야 하는 해시 테이블의 특성에 위배됩니다. 
</details>
<details>
  <summary>3-2. 해시 충돌 해결 방법에 대해 설명해주세요</summary>
  충돌이 일어나면 기존 값과 새로운 값을 연결리스트로 연결하는 chiaining 방법과 충돌이 발생할 경우 비어있는 hash를 찾아 저장하는 개방주소 방법이 있습니다.
</details>
<details>
  <summary>3-2. 자바의 HashMap과 HashTable의 차이점에 대해 설명해주세요</summary>
  <li> 보조 해시 함수: HashMap은 보조 해시함수를 사용하기 때문에 HashTable에 비하여 해시 충돌 발생이 적다.</li>
<li> 동기화 지원: HashMap의 경우 동기화를 지원하지 않기 때문에 HashTable 보다 빠르다. 멀티쓰레드 환경에서도 HashTable을 사용하기 보다, HashMap을 다시 감싸서 사용한다고 한다. `Map m = Collections.syschronizedMap(new HashpMap());`</li>
<li> Null 허용: HashMap은 null을 허용하지만, HashTable은 허용하지 않는다.</li>
</details>

---

<details>
  <summary>4. BST(Binary Search Tree)와 Binary Tree에 대해 설명해주세요</summary>
  이진트리(Binary Tree)는 자식 노드가 최대 두 개인 노드들로 구성된 트리이고, 

이진 탐색 트리(BST)는 이진 탐색과 연결 리스트를 결합한 자료구조입니다. 이진 탐색의 효율적인 탐색 능력을 유지하면서, 빈번한 자료 입력과 삭제가 가능하다는 장점이 있습니다.

이진 탐색 트리는 왼쪽 트리의 모든 값은 반드시 부모 노드보다 작아야 하고, 오른쪽 트리의 값은 부모 노드보다 커야 하는 특징이 있습니다.

이진 탐색 트리의 탐색 연산은 트리의 높이에 영향을 받아 높이가 h일 때 시간 복잡도는 O(h)이며, 트리의 균형이 한쪽으로 치우쳐진 경우 worst case가 되고 O(n)의 시간 복잡도를 가집니다.

이런 worst case를 막기 위해 나온 기법이 RBT(Red-Black Tree)입니다.
</details>
<details>
  <summary>4-1. RBT(Red-Black Tree)에 대해 설명해주세요</summary>
  RBT(Red-Black Tree)는 BST를 기반으로 하는 트리 형식 자료구조이며, RBT는 BST의 삽입, 삭제 연산 과정에서 발생할 수 있는 문제점을 해결하기 위해 만들어졌습니다.

BST를 기반으로 하기 때문에 당연히 BST의 특징을 모두 갖습니다.

노드의 child가 없을 경우 child를 가리키는 포인터는 NIL 값을 저장합니다. 이러한 NIL들을 leaf node로 간주합니다.

모든 노드를 빨간색 또는 검은색으로 색칠하며, 연결된 노드들은 색이 중복되지 않습니다.
</details>

---

<details>
  <summary>5. 동적 계획법(DP, Dynamic Programming)에 대해 설명해주세요.</summary>
  주어진 문제를 풀기 위해, 문제를 여러 개의 하위 문제로 나누어 푸는 방법을 말합니다.

동적 계획법에서는 어떤 부분 문제가 다른 문제들을 해결하는데 사용될 수 있어, 답을 여러 번 계산하는 대신 한 번만 계산하고 그 결과를 재활용하는 메모이제이션(Memoization)기법으로 속도를 향상시킬 수 있습니다.
</details>
<details>
  <summary>5-1. 동적 계획법(DP, Dynamic Programming)이 갖는 2가지 조건은 무엇인가요?</summary>
  1. 중복되는 부분(작은) 문제<br>
중복되는 부분 문제는 나눠진 부분 문제가 중복되는 경우로, 메모이제이션 기법을 사용해 중복 계산을 없앱니다.<br>
2. 최적 부분 구조<br>
최적 부분 구조를 가진다는 것은 전체 문제의 최적해가 부분 문제의 최적해들로써 구성된다는 것입니다.
</details>

---

<details>
  <summary>6. 알고 있는 정렬 알고리즘이 있다면 설명해주세요</summary>
  <li> 버블 정렬 : 서로 인접한 두 원소를 비교하여 정렬하는 알고리즘으로, 0번 인덱스부터 n-1번 인덱스까지 n번까지의 모든 인덱스를 비교하며 정렬합니다. 시간 복잡도는 `O(n^2)`입니다.</li>
<li> 선택 정렬 : 선택 정렬은 정렬되지 않은 배열 중 첫 번째 값을 두번째 부터 마지막 값까지 차례대로 비교하여 최솟값을 찾아 첫 번째에 놓는 과정을 배열 전체가 정렬될 때까지 반복하는 알고리즘입니다. 시간복잡도는 `O(n^2)`입니다.</li>
<li> 삽입 정렬 : 삽입 정렬은 두 번째 값부터 시작해 그 앞에 존재하는 원소들과 비교하여 삽입할 위치를 찾아 삽입하는 정렬 알고리즘입니다. 평균 시간복잡도는 `O(n^2)`이며, Best Case 의 경우 `O(n)`까지 높아질 수 있습니다.</li>
<li> 힙 정렬 : 주어진 데이터를 힙 자료구조로 만들어 최댓값 또는 최솟값부터 하나씩 꺼내서 정렬하는 알고리즘입니다. 가장 큰 값 몇개만을 필요로 하는 경우 유용합니다. 시간 복잡도는 `O(nlogn)`입니다.</li>
<li> 병합 정렬 : 주어진 배열을 크기가 1인 배열로 분할하고 합병하면서 정렬을 진행하는 분할/정복 알고리즘입니다. 시간 복잡도는 `O(nlogn)`입니다.</li>
<li> 퀵 정렬 : 퀵 정렬은 빠른 정렬 속도를 자랑하는 분할 정복 알고리즘 중 하나로 피봇을 설정하고 피봇보다 큰 값과 작은 값으로 분할하여 정렬합니다. 병합정렬과 달리 리스트를 비균등하게 분할합니다. 시간 복잡도는 `O(nlogn)`이며 worst case 경우 `O(n^2)`까지 나빠질 수 있습니다.</li>
</details>

---

<details>
  <summary>7. Array, ArrayList 차이점</summary>
  Array, ArrayList 모두 배열 구조이다. 하지만 Array는 크기가 고정적이지만 ArrayList는 크기가 가변적이다.

따라서 Array는 초기화 시 메모리에 할당되어 ArrayList 보다 속도가 빠르고, ArrayList는 데이터 추가 및 삭제 시 메모리를 재할당하기 때문에 속도가 Array 보다 느리다.
</details>
<details>
  <summary>7-1. ArrayList가 어떻게 가변적으로 동작하나요? (add, remove 동작 과정)</summary>
  <li> add()<ul>
    <li> 현재 배열의 크기와 저장된 데이터 개수를 비교한다.</li>
    <li> 저장할 수 있으면 다음 위치에 데이터를 저장하고, `배열의 크기 == 데이터 개수`라면 배열 사이즈 변경 작업을 한다.</li>
    <li> 데이터 개수, 현재 배열 크기를 기반으로 새로운 배열의 크기를 결정한다.<ul>
        <li> 증가되는 크기 = max(1, 기존 배열의 절반 크기)</li></ul></li>
    <li> 기존 배열을 복사해 길이를 새로운 크기로 맞춘다. (필요시 잘라내거나 null로 채워서 길이를 맞춘다)</li></ul></li>
<li> remove()<ul>
    <li> 현재 데이터 개수 - 1로 새 데이터 개수를 지정하고, 만약 해당 요소가 맨 끝에 있던 요소가 아니라면 뒤에 있던 값들을 앞으로 당긴다. 이후 배열의 마지막 자리를 null로 명시적으로 표기한다!</li></ul></li>
</details>

---

<details>
  <summary>8. 퀵 정렬에 대해 설명해주세요</summary>
  pivot이라는 기준 값을 기준으로 작은 값은 왼쪽, 큰 값은 오른쪽으로 옮기는 방식으로 정렬합니다. 
(이를 반복하여 분할된 배열의 크기가 1이되면 배열이 모두 정렬된 것)
</details>
<details>
  <summary>8-1. 퀵 정렬의 시간 복잡도는 어떻게 되나요?</summary>
  O(nlogn)이나, 최악의 경우 O(n^2)이다.

이미 배열이 정렬이 되어있는 경우, 분할이 N만큼 일어나기 때문에 시간 복잡도는 O(n^2) 이 된다.
</details>
<details>
  <summary>8-2. 삽입 정렬</summary>
  현재 위치에서 앞의 요소들과 비교하여 자신이 들어갈 위치를 찾아 삽입하는 방식입니다.
</details>
<details>
  <summary>8-3. 합병 정렬</summary>
  배열을 두 개의 배열로 계속 쪼게 나간 뒤, 합치면서 정렬하는 방식입니다.
</details>
<details>
  <summary>8-4. 선택 정렬</summary>
  현재 위치에 들어갈 값을 뒤의 요소들에서 찾아 정렬하는 방식입니다.
</details>
<details>
  <summary>8-5. 자바에서는 sort 어떻게 구현하고 있나요?</summary>
  기본형 정렬할 때는 Dual-Pivot Quicksort, 객체형을 정렬할 때는 Timsort 사용한다.

- Dual-Pivot Quicksort: 두 개의 pivot을 사용하여 배열을 세 부분으로 나누어 정렬하는 방법
</details>
<details>
  <summary>8-6. Timsort란?</summary>
  합병 정렬과 삽입 정렬이 혼합된 알고리즘으로, 합병정렬을 기반으로 구현하되, 일정 크기 이하의 부분 리스트에 대해서는 이진 삽입 정렬을 수행하는 방식이다.

1. 배열을 연속된 작은 부분 배열로 분할한다. 이 부분 배열들은 이미 정렬되어있거나 거의 정렬된 상태일 수 있다. 이러한 부분 배열을 ‘런(run)’ 이라고 한다.
2. 삽입 정렬을 사용하여 각 런을 정렬한다. 작은 크기의 런에서는 삽입 정렬이 상대적으로 빠른 속도를 보인다.
3. 병합 정렬의 병합 과정을 사용하여 인접한 런들을 결합한다. 이 과정은 모든 런이 하나의 정렬된 배열이 될 때까지 반복한다.
</details>

---

<details>
  <summary>9. BST에 대해 설명해주세요</summary>
  정렬된 이진트리로, 왼쪽 서브트리의 모든 키는 루트 노드의 키보다 작고 오른쪽 서브트리의 모든 키는 루트 노드의 키보다 크다는 성질을 갖고 있다. 이를 통해 효율적인 검색이 가능하다.
</details>
<details>
  <summary>9-1. BST에서 최악의 상황과 그 때의 시간 복잡도에 대해 설명해주세요</summary>
  노드가 한 쪽으로 치우친 경우 시간 복잡도가 O(N)으로 늘어난다.
</details>
<details>
  <summary>9-2. 해당 문제를 어떻게 해결할 수 있을까요?</summary>
  자가 균형 트리를 사용한다 ⇒ 레드-블랙 트리, AVL

[레드-블랙 트리]

레드 블랙 트리란, BST의 일종으로 각 노드가 Red 또는 Black의 색상을 가짐으로써 스스로 균형을 유지하는 트리다. 레드-블랙 트리만의 규칙이 존재하고 해당 규칙을 지키기 위해 노드의 색을 변경하거나 rotation을 하며 균형을 유지한다. 그 결과로 검색, 삽입, 삭제 시 모두 `O(logN)` 이 보장된다.

[AVL 트리]

AVL 트리란 자가 균형 이진 탐색 트리 중 하나로, 각 노드의 서브트리 높이 차이가 최대 1을 유지하도록 한다. 트리가 변경되는 과정에서 균형이 깨지게 된다면 rotation을 통해 높이 차이를 유지한다.
</details>

---

<details>
  <summary>10. HashMap 자료구조에 대해 설명해주세요</summary>
  HashMap은 key-value 형태로 데이터를 저장하는데, 이때 key 값을 해시함수를 거쳐 해당 데이터가 저장될 배열에서의 index 값을 얻어 저장한다. 그렇기 때문에 key 값으로 value에 O(1)의 시간 복잡도로 접근이 가능하다.
</details>
<details>
  <summary>10-1. 문충돌이 발생하면 어떻게 하나요?제</summary>
  버킷 사이즈 조절, Chaining, Open Addressing 방식이 있다.

- 버킷을 생성할 때 threshold(임계점)을 지정하고, 해당 threshold를 넘어가면 size를 2배로 늘린다.
- Chaining은 LinkedList를 활용하여 해당 자리에 이미 다른 값이 존재한다면, 즉 충돌했다면 그 자리에서 LinkedList로 연결하여 값을 저장한다.
- Open Addressing은 충돌이 발생할 경우 빈 공간을 찾아 저장한다. (선형 탐색, 제곱 탐색)
</details>
<details>
  <summary>10-2. 자바에서는 어떻게 처리하고 있나요?</summary>
  <li> threshold → 근데 버킷 사이즈를 조절한다고 해서 충돌이 안 일어나는 것은 아니다!</li>
<li> Linked List + Red-Black Tree<ul>
    <li> 초기에는 chaining 방식으로 해결한다. 근데 충돌이 너무 자주 발생해서 chaining이 길어지면 시간 복잡도가 최악의 경우엔 O(N)이 된다.</li>
    <li> 그래서 충돌이 심해지면 Red Black Tree로 바꿔준다. (Node 객체를 TreeNode로 바꿔준 다음에 Red Black Tree로 바꿔주면 됨)</li></ul></li>
</details>

---