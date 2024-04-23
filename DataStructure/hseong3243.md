<details>
  <summary>1. 정렬 알고리즘에 대해 알고 있는 것들을 설명해주세요.</summary>

#### 버블 정렬(Bubble sort)
버블 정렬은 서로 인접한 두 원소를 비교하여 정렬하는 알고리즘입니다. 인접한 두 원소의 크기가 순서대로 되어 있지 않다면 서로 교환합니다.

첫번째 루프가 종료되면 (오름차순인 경우) 가장 큰 자료가 가장 마지막으로 이동하므로 두번째 루프에서는 마지막 자료는 정렬에서 제외됩니다. 이처럼 루프를 반복할수록 정렬에서 제외되는 데이터가 하나씩 늘어납니다.
```java
public void bubble(int[] arr) {
    for (int i = 0; i < arr.length-1; i++) {
        for (int j = 1; j < arr.length - i; j++) {
            if (arr[j] < arr[j - 1]) {
                int temp = arr[j - 1];
                arr[j - 1] = arr[j];
                arr[j] = temp;
            }
        }
    }
}
```

시간복잡도는 `(n-1)+(n-2)+(n-3)+...+2+1=n(n-1)/2`번의 비교를 수행하므로 O(n^2)입니다. 정렬되어 있는지 여부에 상관없이 비교를 수행하기 때문에 최선, 평균, 최악의 경우 모든 시간 복잡도가 O(n^2)으로 동일합니다.

#### 선택 정렬(Selection sort)
선택 정렬은 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘입니다.

첫번째 루프에서 가장 처음의 원소부터 마지막 원소까지 차례로 비교하면서 가장 작은 값을 찾습니다. 그런 다음 첫번째 원소와 가장 작은 원소를 서로 교환합니다. 두번째 루프에서는 첫번째 원소를 정렬에서 제외합니다. 이처럼 루프를 반복할수록 정렬에서 제외되는 데이터가 하나씩 늘어납니다.
```java
public void selection(int[] arr) {
    for(int i=0; i<arr.length-1; i++) {
        int idxMin = i;
        for(int j=i+1; j<arr.length; j++) {
            if(arr[j] < arr[idxMin]) {
                idxMin = j;
            }   
        }
        int temp = arr[idxMin];
        arr[idxMin] = arr[i];
        arr[i] = temp;
    }
}
```

시간복잡도는 `(n-1)+(n-2)+(n-3)+...+2+1=n(n-1)/2`번의 비교를 수행하므로 O(n^2)입니다.

#### 삽입 정렬(Insertion sort)
삽입 정렬은 배열의 모든 원소를 앞에서부터 차례대로 이미 정렬된 부분과 비교하여 자신의 위치를 찾아 삽입하는 알고리즘입니다.

두번째 원소부터 시작하여 앞의 원소들과 비교하여 삽입할 위치를 지정한 뒤, 원소를 뒤로 옮기고 지정한 자리에 삽입합니다. 
```java
public void insertion(int[] arr) {
    for(int i=1; i<arr.length; i++) {
        int temp = arr[i];
        int prev = i-1;
        while(prev >= 0 && arr[prev] > temp) {
            arr[prev+1] = arr[prev];
            prev--;
        }
        arr[prev+1] = temp;
    }
}
```

시간복잡도는 최악의 경우 `(n-1)+(n-2)+(n-3)+...+2+1=n(n-1)/2`번의 비교를 수행하므로 O(n^2)입니다. 그러나 최선의 경우 내부 루프에 진입하지 않고 `n-1`의 비교만 수행하므로 O(n)입니다.


#### 힙 정렬(Heap sort)
힙 정렬은 힙 트리를 구성하여 정렬을 수행하는 방법입니다. 힙은 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료 구조입니다.

```java
void heapSort(int[] arr) {
    int n = arr.length;
    for(int i=n/2-1; i>=0; i--) {
        heapify(arr, n, i);
    }
}

void heapify(int[] arr, int n, int i) {
    int max = i;
    int left = 2*i+1;
    int right = 2*i+2;
    
    if(left < n && arr[left] > arr[max]) {
        max = left;
    }
    if(right < n && arr[right] > arr[max]) {
        max = right;
    }
}
```

시간복잡도는 O(nlogn)입니다.

#### 퀵 정렬(Quick sort)
퀵 정렬은 분할 정복 방법을 통해 정렬을 수행하며 평균적으로 매우 빠른 수행 속도를 가집니다.

배열 안에 있는 한 요소, 피벗을 선택합니다. 피벗을 기준으로 작은 요소들은 왼쪽으로, 큰 요소들은 오른 쪽으로 옮깁니다. 피벗을 제외한 왼쪽 배열과 오른쪽 배열에 대해 다시 정렬을 수행합니다. 이 과정을 더 이상 배열의 분할이 불가능할 때까지 진행합니다.
```java
public void quick(int[] arr, int left, int right) {
    if(left >= right) {
        return;
    }    
    
    int pivot = partition(arr, left, right);
    quick(arr, left, pivot - 1);
    quick(arr, pivot + 1, right);
}

private void pivot(int[] arr, int left, int right) {
    int pivot = arr[right];
    int sortedIndex = left;
    for(int i=left; i<right; i++) {
        if(arr[i] <= pivot) {
            swap(arr, i, sortedIndex);
            sortedIndex++;
        }   
    }
    swap(arr, sortedIndex, right);
    return sortedIndex;
}
```

시간복잡도는 배열의 길이가 2^n인 경우 logn의 깊이를 가지고 각 단계마다 n번의 비교를 수행하기 때문에 평균적으로 O(nlogn)입니다. 그러나 한쪽의 깊이만 계속해서 깊어지는 최악의 경우 n의 높이를 가지기 때문에 O(n^2)입니다.


#### 합병 정렬(Merge sort)
병합 정렬은 분할 정복 방법을 이용합니다.

정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눕니다. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬합니다. 나뉜 부분 리스트는 다시 하나의 정렬된 리스트로 합병합니다.
```java
public void mergeSort(int[] arr, int left, int right) {
    if(left >= right) {
        return;
    }
    int mid = (left + right) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}

void merge(int[] arr, int left, int mid, int right) {
    int leftIdx = left;
    int rightIdx = mid + 1;
    int sortedIdx = left;
    
    int[] temp = new int[right+1];
    while(leftIdx <= mid && rightIdx <= right) {
        if(arr[leftIdx] <= arr[rightIdx]) {
            temp[sortedIdx++] = arr[leftIdx++];
        } else {
            temp[sortedIdx++] = arr[rightIdx++];
        }   
    }
    
    if(leftIdx > mid) {
        for(int i=rightIdx; i<=right; i++) {
            temp[sortedIdx++] = arr[i];        
        }       
    } else {
        for(int i=leftIdx; i<=mid; i++) {
            temp[sortedIdx++] = arr[i];
        }
    }
    
    for(int i=left; i<=right; i++) {
        arr[i] = temp[i];
    }
}
```

</details>
<details>
  <summary>1-1. 자바에서 사용하는 정렬이 무엇인지 알고 있나요?</summary>

#### Arrays.sort()
`Arrays.sort()`의 경우 듀얼 피봇 퀵 정렬(Dual-Pivot Quicksort)를 사용합니다. 2개의 피벗을 두고 3개의 구간을 만들어 퀵 정렬을 사용합니다. 이는 모든 데이터 셋에 대해 O(nlogn)의 시간복잡도를 제공하며 기존 퀵 정렬의 구현보다 빠릅니다.

#### Collections.sort()
`Collections.sort()`의 경우 Tim sort를 사용합니다. 이는 삽입 정렬(Insertion sort)와 합병 정렬(Merge sort)를 결합하여 만든 정렬입니다. Insertion sort는 인접한 메모리와의 비교를 통해 참조 지역성의 원리를 잘 만족합니다. 이 때, Insertion sort의 상수 Ci와 O(nlogn) 정렬 알고리즘 중 C 값이 가장 작다고 알려진 Quick sort의 상수 Cq라 할 때, 작은 n에 대하여 `Ci*n^2 < Cq*nlogn`이 성립합니다.

이를 이용하여 전체를 작은 덩어리로 잘라 각각의 덩어리를 Insertion sort로 정렬한 뒤 병합하면 좀 더 빠르지 않을까 하는 것이 기본 아이디어입니다.

Tim sort는 실생활의 특성을 적용하여 여러 가지 최적화 기법을 도입한 정렬 알고리즘으로 일정한 패턴이 있는 일반적인 데이터에 대해서는 빠른 성능을 보여주며 O(nlogn)의 시간복잡도를 가집니다.

참고: https://d2.naver.com/helloworld/0315536


</details>
<details>
  <summary>1-2. 안정 정렬이란</summary>

정렬을 했을 때 중복된 값들의 순서가 변하지 않는다면 안정(stable) 정렬, 변하면 불안정 정렬이라고 합니다. 만일 학생 데이터와 같이 이름순으로 정렬된 데이터가 있을 때 성적 순으로 정렬하게 되면 안정 정렬의 경우 이름순이 유지되지만 불안정 정렬은 순서가 유지되지 않습니다.

- 안정 정렬
  - 거품 정렬
  - 삽입 정렬
  - 합병 정렬
- 불안정 정렬
  - 힙 정렬
  - 퀵 정렬
</details>

---

<details>
  <summary>2. 재귀에 대해서 설명해주세요.</summary>

재귀는 문제의 정의할 때 자기 자신을 참조하는 것을 뜻합니다. 재귀함수를 정의하는 경우 적절한 탈출조건을 설정해주어야 하며 탈출조건을 설정해주더라도 depth가 깊어지는 경우 스택 오버 플로우가 발생할 수 있습니다.
</details>
<details>
  <summary>2-1. 분할 정복에 대해 설명해주세요.</summary>

분할 정복은 커다란 문제를 작은 문제로 나눠가면서 용이하게 풀 수 있는 문제 단위로 나누어 해결하는 방법입니다.
</details>
<details>
  <summary>2-2. 그리디에 대해 설명해주세요.</summary>

그리디는 각 단계마다 최선의 방법을 선택하여 문제를 해결하는 방법입니다. 
</details>
<details>
  <summary>2-3. 동적 계획법에 대해 설명해주세요.</summary>

동적 계획법이란 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법을 말합니다. 분할 정복과 유사한 접근 방식을 가지며 이미 계산한 부분 문제를 다시 이용하는 경우 이전에 계산해 둔 정답을 이용하여 속도를 향상시킵니다.
</details>

---

<details>
  <summary>3. 배열에 대해 설명해주세요.</summary>

배열은 연관된 데이터를 메모리상의 연속적인 공간에 순차적으로 미리 할당된 크기만큼 저장하는 자료 구조입니다. 인덱스를 통해 각 요소에 빠르게 접근 가능하며 데이터의 추가가 빠르나 배열의 중간에 데이터를 삽입하거나 삭제하는 경우 O(n)의 시간이 소요됩니다.

#### 동적인 배열
기본적으로 배열은 고정된 크기를 가지고 있기 때문에 크기를 넘어서는 데이터를 저장할 수 없습니다. 이 경우 더 큰 크기의 배열은 선언하여 기존 배열의 데이터를 모두 옮긴 뒤, 기존 배열을 메모리에 삭제하는 방식으로 동적인 배열을 구성할 수 있습니다.
</details>
<details>
  <summary>3-1. 링크드 리스트에 대해 설명해주세요.</summary>

링크드 리스트는 연관된 데이터를 메모리 상에 비연속적으로 저장하는 자료 구조입니다. 각각의 노드는 다음 노드를 가리키는 링크를 가지고 있으며 이를 통해 논리적인 연속성을 가집니다. 각 요소에 접근하기 위해서는 탐색을 수행해야하기 때문에 O(n)의 시간이 소요되나 리스트의 중간에 데이터 삽입, 삭제는 더 빠르게 수행할 수 있습니다. 

</details>
<details>
  <summary>3-2. 스택과 큐에 대해 설명해주세요.</summary>

스택은 후입선출(LIFO) 형태의 자료 구조이며, 큐는 선입선출(FIFO) 형태의 자료 구조입니다.

스택은 언두(undo), 괄호 유효성 검사 등에 활용할 수 있습니다. 큐는 대기열에 활용할 수 있습니다.
</details>

---

<details>
  <summary>4. 해시 테이블에 대해 설명해주세요.</summary>

해시 테이블은 키-값 쌍의 데이터를 효율적으로 탐색하기 위한 자료 구조입니다. 해시 함수에 키를 입력으로 넣은 해시값을 위치로 지정하여 키-값 쌍의 데이터를 저장합니다.
</details>
<details>
  <summary>4-1. 해시 충돌을 해결하기 위한 방법에 대해 설명해주세요.</summary>

#### Open addressing
개방 주소법은 충돌이 발생하는 경우 미리 정의한 규칙에 따라 해시 테이블의 비어 있는 슬롯을 탐색합니다. 별도의 자료구조를 사용하지 않으므로 추가적인 메모리를 적게 사용합니다. 빈 슬롯을 탐색하는 방법은 다음과 같은 것들이 있습니다.

- Linear probing(선형 조사법)
- Quadratic probing(이차 조사법)
- Double hashing(이중 해싱)

충돌 횟수가 많아지는 경우 특정 영역에 데이터가 집중되는 현상이 발생하여 평균 탐색 시간이 증가합니다.

#### Separate chaining
Separate chainig은 충돌이 발생하는 경우 링크드 리스트에 노드를 추가하여 데이터를 저장하는 방법입니다. 기본적으로 삽입, 검색, 삭제의 경우 O(1)의 시간복잡도를 가지지만 최악의 경우 (삽입한 요소의 길이만큼) O(m)의 시간복잡도를 가집니다.

</details>
<details>
  <summary>4-2. Separate chaining 방식에서 최악의 경우 시간복잡도를 개선하기 위한 방법</summary>

자가 균형 이진 탐색 트리(self-balancing Binary Search Tree)를 이용하여 최악의 경우 O(logm)으로 시간복잡도를 개선할 수 있습니다. 자바의 HashMap의 경우 일정 크기 이상에서는 레드-블랙 트리를 이용하여 시간복잡도를 개선하고 있습니다.

#### 이진 탐색 트리(Binary Search Tree, BST)
이진 탐색 트리는 정렬된 트리입니다. 부모 노드의 왼쪽 서브 트리에는 해당 노드보다 작은 값을 가진 노드들로, 오른쪽 서브 트리에는 해당 노드보다 큰 값을 가진 노드들로 구성되어 있는 이진 트리입니다. 삽입과 검색, 삭제는 모두 O(logn)의 시간복잡도를 가지나 트리가 한 쪽으로 치우쳐지는 경우  O(n)의 시간복잡도를 가집니다.

#### 레드-블랙 트리
레드-블랙 트리에서 모든 노드는 빨간색 혹은 검은색입니다.
루트 노드와 리프 노드는 검은색으로 구성되어 있으며 빨간색 노드의 자식은 검은색입니다. 이때, 모든 리프 노드에서의 black depth는 동일합니다. 

새롭게 삽입되는 노드는 항상 빨간색이며, 빨간색 노드가 연속되는 경우 Restructuring, Recoloring 두 가지 방법을 이용합니다.

새롭게 삽입할 노드를 N(new), 부모 노드를 P(parent), 조상 노드를 G(grand parent), 삼촌 노드를 U(uncle)이라고 할때 삼촌 노드가 검은색인 경우 Restructuring, 빨간색인 경우 Recoloring을 수행합니다.

##### Restructuring
1. 새로운 노드 N, 부모 노드 P, 조상 노드 G를 오름차순으로 정렬합니다.
2. 셋 중 중간값을 부모로 만들고 나머지 둘을 자식으로 만듭니다.
3. 새로 부모가 된 노드를 검은색으로 만들고 나머지 자식들을 빨간색으로 만듭니다.

##### Recoloring
1. 부모 노드 P, 삼촌 노드 U를 검은색으로 바꾸고 조상 노드 G를 빨간색으로 바꿉니다.
2. 조상 노드 G가 루트 노드인 경우 검은색으로 바꿉니다.
3. 조상 노드 G를 빨간색으로 바꿨을 때 다시 빨간색이 연속되는 경우 Restructuring 또는 Recoloring을 진행합니다.
</details>

---

<details>
  <summary>5. 다익스트라 알고리즘과 플로이드 워셜</summary>

#### 다익스트라
다익스트라 알고리즘은 한 정점에서 다른 모든 정점으로 가능 최단 경로를 구하는 알고리즘입니다. 방향 유무는 상관 없으며 음수 간선이 존재한다면 사용할 수 없습니다. 우선순위 큐를 사용하는 경우 해당 알고리즘의 시간복잡도는 O(|E|+|V|log|V|)입니다. 

#### 플로이드-워셜
플로이드-워셜 알고리즘은 그래프에서 가능한 모든 노드 쌍에 대해 최단 거리를 구하는 알고리즘입니다. 다익스트라와 달리 모든 노드 쌍에 대해 최단 거리를 구하고, 음의 가중치를 가지는 그래프에도 쓸 수 있다는 차이점이 있습니다. 시간복잡도는 O(V^3)입니다.

#### 벨먼-포드
벨먼-포드 알고리즘은 한 정점에서 다른 정점 사이의 최단 경로를 구하는 알고리즘입니다. 그래프가 가중치를 가지는 방향있는 간선으로 이루어져있을 때 서로 다른 두 정점 사이의 최단 경로를 구할 수 있습니다. 이 때, 다익스트라와는 달리 간선의 가중치가 음수인 경우에도 사용할 수 있습니다. 시간복잡도는 O(|V||E|)입니다.
</details>
<details>
  <summary>5-1. 크루스칼 알고리즘</summary>

#### 스패닝 트리
스패닝 트리는 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프를 뜻합니다.

#### 최소 스패닝 트리(MST)
최소 스패닝 트리는 최소한의 비용으로 구성되는 스패닝 트리를 말합니다.

#### 크루스칼 알고리즘
크루스칼 알고리즘은 최소 싱장 트리 알고리즘으로 간선의 가중치 합이 최소가 되도록 모든 노드를 연결시킵니다. 크루스칼 알고리즘은 다음 과정을 따라서 동작합니다.
1. 그래프의 모든 간선을 가중치를 기준으로 오름차순 정렬합니다.
2. 간선을 하나씩 확인하며 싸이클이 발생하는지 확인합니다. 싸이클이 발생하지 않는 경우 트리에 추가하고, 발생하는 경우 추가하지 않습니다.

이는 유니온 파인드를 이용하여 구현할 수 있습니다. 간선을 하나씩 추가하며 싸이클이 발생하지 않게 집합(union)을 구하면 최소 신장 트리를 구할 수 있습니다. 

</details>
<details>
  <summary>5-2. 깊이 우선 탐색과 너비 우선 탐색</summary>

#### 깊이 우선 탐색(DFS)
그래프 상에 존재하는 임의의 한 정점으로부터 시작하여 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법입니다. 모든 노드를 방문하고자 하는 경우 이를 사용할 수 있으며 순환 호출 또는 스택을 이용하여 구현할 수 있습니다.

시간복잡도는 인접 리스트로 표현된 그래프의 경우 O(n+e)이며 인접 행렬인 경우 O(n^2)입니다.

#### 너비 우선 탐색(BFS)
그래프 상에 존재하는 임의의 한 정점으로부터 시작하여 인접한 노드를 먼저 탐색하는 방법입니다. 두 노드 사이의 경로를 찾고 싶을 때 이를 사용할 수 있으며 큐를 사용하여 구현할 수 있습니다.

시간복잡도는 인접 리스트로 표현된 그래프의 경우 O(n+e)이며 인접 행렬인 경우 O(n^2)입니다.
</details>

---