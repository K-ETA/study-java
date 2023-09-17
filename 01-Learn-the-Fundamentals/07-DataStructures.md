# Java
## Data Structures

### Table of Contents
1. [Data Structure란?](#➲-data-structure란)
2. [Classification of Data Structure](#➲-classification-of-data-structure)
3. [Non-Primitive Data Structures](#➲-non-primitive-data-structures)
4. [참고 자료](#➲-참고-자료)

</br>

### ➲ Data Structure란?
- Data Structure(DS, 데이터 구조)
- 데이터를 저장하고 구성하는 데 사용되는 저장소
- 컴퓨터에서 데이터를 효율적으로 액세스하고 업데이트할 수 있도록 배열하는 방법
- 데이터를 메모리에 구조화하는 데 사용할 수 있는 알고리즘 집합

</br>

### ➲ Classification of Data Structure

#### ① Primitive/Non-Primitive Data Structure
| Classification | Description |
| - | - |
| 원시 데이터 구조(Primitive Data Structure) | - 기본 데이터 유형</br>- `byte`, `short`, `int`, `float`, `char`, `boolean`, `long`, `double`이 해당된다. |
| 비원시적 데이터 구조(Non-Primitive Data Structure) | -Linear Data Structure, Non-Linear Data Structure이 해당된다. |

#### ② Linear/Non-Linear Data Structure
<img src="https://media.geeksforgeeks.org/wp-content/uploads/20220520182504/ClassificationofDataStructure-660x347.jpg">

| Classification | Description |
| - | - |
| 선형 데이터 구조(Linear Data Structure) | -선형 방식으로 배열된 요소</br>- 각 요소는 하나의 다른 요소에만 연결된다.</br>- Array, Stack, Queue, Linked List가 해당된다. |
| 비선형 데이터 구조(Non-Linear Data Structure) | -비선형 방식으로 배열된 요소</br>- 각 요소는 n개의 다른 요소와 연결된다.</br>- Tree, Graph, Heap, Hash가 해당된다. |

추가로, 선형 데이터 구조는 Static Data Structure과 Dynamic Data Structure로 나눌 수 있다.
- **Linear Data Structure**
  - Static Data Structure
    - 고정된 메모리 크기를 가진다.
    - 데이터 구조의 요소에 접근하기가 용이하다.
    - 예시: Array
  - Dynamic Data Structure
    - 메모리 크기가 고정되어 있지 않으며,
    - 코드의 메모리 복잡성과 관련하여 효율적인 반면,
    - 런타임 환경에서 랜덤으로 업데이트 될 수 있다는 특징을 가지고 있다.
    - 예시: Stack, Queue, Linked List

</br>

### ➲ Non-Primitive Data Structures

#### Array (배열)

<img src="https://static.javatpoint.com/ds/images/ds-array2.png" />

- **Define**
  - 가장 간단한 데이터 구조
  - 유사한 데이터 요소의 모음이 발생하고, 각 데이터 요소에 인덱스 번호만 사용하여 직접 액세스한다.
  - Java에서는 1차원 배열, 2차원 배열 모두 생성이 가능하다.

- **Advantages**
  - 무작위로 액세스가 가능하다.
  - 정렬과 반복이 용이하다.
  - 여러 개의 변수를 대체할 수 있다.

- **Disadvantages**
  - 크기가 고정되어 있다.
  - 삽입과 삭제가 어렵다.
  - 크기가 커지고, 점유 공간이 줄어들면 메모리 낭비가 발생하기 쉽다.
  - 배열을 생성할 때 할당을 위해 연속적인 메모리가 필요하다.

- **Applications**
  - 선형 방식으로 정보를 저장하는 경우
  - 빈번한 검색이 필요한 경우

- **Example**
```Java
public static void main(String[] args) {
    // 배열 생성하는 부분
    int[] priceOfPan = new int[5];

    Scanner in = new Scanner(System.in);

    // 배열에 값을 입력하는 부분
    for (int i = 0; i < priceOfPan.length; i++)
        priceOfPan[i] = in.nextInt();
    
    // 배열의 값을 출력하는 부분
    for (int i = 0; i < priceOfPen.length; i++)
        System.out.print(priceOfPen[i] + " ");
}
```

#### Linked List (연결 리스트)

<img src="https://static.javatpoint.com/ds/images/linked-list.png" />

- **Define**
  - 노드(Node)라고 불리는 객체들의 집합으로 메모리에 무작위로 저장되는 데이터 구조이다.
  - 노드는 두 개의 필드, 즉 특정 주소에 저장된 데이터와 메모리의 다음 노드 주소를 포함하는 포인터를 포함한다.
  - 목록의 마지막 노드에는 `null`에 대한 포인터가 포함되어 있다.
  - 필요한 객체를 선형 순서로 배열하는 데 도움이 된다.

- **Advantages**
  - 동적으로 크기를 조절할 수 있다.
  - 용량과 크기가 항상 동일하므로 낭비가 없다.
  - 삽입과 삭제가 용이하다.
  - 효율적인 메모리 할당이 가능하다.

- **Disadvantages**
  - 헤드 노드(Head node)가 손실되면 연결 리스트 전체가 손실된다.
  - 임의 접근이 불가능하다.

- **Applications**
  - 사용할 수 있는 메모리가 제한된 곳에 적합하다.
  - 빈번한 삽입과 삭제가 필요한 애플리케이션에 적합하다.

- **Example**
```Java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        // LinkedList 생성
        LinkedList<String> linkedList = new LinkedList<>();

        // 요소 추가
        linkedList.add("사과");
        linkedList.add("바나나");
        linkedList.add("체리");
        linkedList.add("딸기");

        // LinkedList 요소 출력
        System.out.println("LinkedList 요소:");
        for (String fruit : linkedList) {
            System.out.println(fruit);
        }

        // 특정 인덱스에 요소 삽입
        linkedList.add(2, "포도");

        // LinkedList 요소 다시 출력
        System.out.println("\n삽입 후의 LinkedList 요소:");
        for (String fruit : linkedList) {
            System.out.println(fruit);
        }

        // 요소 제거
        linkedList.remove("바나나");

        // LinkedList 요소 최종 출력
        System.out.println("\n바나나 제거 후의 LinkedList 요소:");
        for (String fruit : linkedList) {
            System.out.println(fruit);
        }
    }
}
```

#### Stack 스택

<img src="https://static.javatpoint.com/ds/images/ds-stack.png" />

- **Define**
  - LIFO(Last In First Out, 후입선출) 원칙을 따르는 선형 데이터 구조
  - 스택의 각 노드에는 데이터와 다음 노드의 주소가 저장되어 있다.
  - 스택의 가장 높은 노드를 top이라고 한다.
  - 스택의 최상위 요소에만 액세스할 수 있다.
  - 스택의 삽입과 삭제는 위에서부터 발생한다.
  - 4가지 주요 작업
    - `push(data)`: 요소를 맨 위에 삽입하는 데 사용한다.
    - `pop()`: 스택의 맨 위 요소를 제거한다.
    - `isEmpty()`: 스택이 비어 있다면 true를 반환한다.
    - `peek()`: 스택의 최상위 요소를 가져온다.
  - 모든 작업은 일정한 시간인 O(1)로 작동한다.

- **Advantages**
  - LIFO 방식으로 데이터를 유지한다.
  - 마지막 요소(최상단에 있는 요소)는 쉽게 사용할 수 있다.
  - 모든 작업의 복잡도(Complexity)는 O(1)이다.

- **Disadvantages**
  - 모든 작업은 스택의 최상단으로 제한된다.
  - 유연성이 부족하다.

- **Applications**
  - 재귀(Recursion)
  - 파싱(Parsing)
  - 검색(Browser)
  - 편집자(Editors)

- **Example**
```Java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        // 정수형 스택 생성
        Stack<Integer> stack = new Stack<>();

        // 스택에 요소 추가 (push)
        stack.push(10);
        stack.push(20);
        stack.push(30);
        stack.push(40);
        stack.push(50);

        // 스택 요소 출력
        System.out.println("스택 요소:");
        System.out.println(stack);

        // 스택에서 요소 제거 (pop)
        int poppedElement = stack.pop();
        System.out.println("스택에서 팝된 요소: " + poppedElement);

        // 스택의 맨 위 요소 확인 (peek)
        int topElement = stack.peek();
        System.out.println("스택의 맨 위 요소: " + topElement);

        // 스택이 비어있는지 확인
        boolean isEmpty = stack.isEmpty();
        System.out.println("스택이 비어있는가? " + isEmpty);

        // 스택 크기 확인
        int stackSize = stack.size();
        System.out.println("스택 크기: " + stackSize);
    }
}
```

#### Queue (큐)

<img src="https://static.javatpoint.com/ds/images/queue.png" />

- **Define**
  - 선형 데이터 구조
  - FIFO(First In First Out, 선입선출) 방식을 사용한다.
  - 처음 저장된 데이터 항목은 큐에서 가장 먼저 액세스된다.
  - 데이터는 항상 한쪽 끝(rear)에 추가되고, 다른쪽 끝(front)에서 제거된다.
  - 4가지 주요 작업
    - `enqueue(data)`: 요소를 맨 위에 삽입하는 데 사용된다.
    - `dequeue()`: 대기열에서 맨 위 요소를 제거한다.
    - `peekfirst()`: 대기열의 첫 번째 요소를 가져온다.
    - `peeklast()`: 대기열의 마지막 요소를 가져온다.
  - 모든 작업은 일정한 시간, 즉 O(1)으로 작동한다.

- **Advantages**
  - FIFO 방식으로 데이터를 유지한다.
  - 처음부터 삽입하고 끝부터 삭제하는 데에 O(1) 시간이 소요된다.

- **Applications**
  - 스케줄링(Scheduling)
  - 재생목록 유지
  - 인터럽트(Interrupt) 처리

- **Example**
```Java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        // 정수형 큐 생성
        Queue<Integer> queue = new LinkedList<>();

        // 큐에 요소 추가 (enqueue)
        queue.add(10);
        queue.add(20);
        queue.add(30);
        queue.add(40);
        queue.add(50);

        // 큐 요소 출력
        System.out.println("큐 요소:");
        System.out.println(queue);

        // 큐에서 요소 제거 (dequeue)
        int removedElement = queue.remove();
        System.out.println("큐에서 제거된 요소: " + removedElement);

        // 큐의 맨 앞 요소 확인 (peek)
        int frontElement = queue.peek();
        System.out.println("큐의 맨 앞 요소: " + frontElement);

        // 큐가 비어있는지 확인
        boolean isEmpty = queue.isEmpty();
        System.out.println("큐가 비어있는가? " + isEmpty);

        // 큐 크기 확인
        int queueSize = queue.size();
        System.out.println("큐 크기: " + queueSize);
    }
}
```

#### Binary Tree (BS, 이진 트리)

<table>
  <tr>
    <td>
    <img src="https://static.javatpoint.com/ds/images/binary-tree.png" />
    </td>
    <td>
    <img src="https://static.javatpoint.com/ds/images/binary-tree2.png" />
    </td>
  </tr>
</table>

- **Define**
  - 계층적 데이터 구조
  - 루트 노드(root node), 부모 노드(parent node), 자식 노드(child node)로 구성될 수 있다.
  - 트리의 각 노드는 최대 2개의 하위 노드를 가질 수 있다. 즉, 부모 노드는 2개의 자식 노드를 가질 수 있다.
  - 인덱스를 사용하여 데이터 구조 요소에 무작위로 액세스할 수 있다.
  - 일반적인 순회 방법 (print: 도착한 노드에 대한 내용을 출력)
    - `preorder(root)`: print - left - right
    - `postorder(root)`: left - right - print
    - `inorder(root)`: left - print - right

- **Advantages**
  - 특정 관계가 있는 데이터를 나타낼 수 있다.
  - 삽입과 검색이 효율적이다.

- **Disadvantages**
  - 정렬이 어렵다.
  - 유연성이 별로 없다.

- **Applications**
  - 파일 시스템 계층
  - 다양한 변형에 따른 다양한 애플리케이션이 존재한다.

- **Example**
```Java
class Node {
    int key;
    Node left, right;

    public Node(int item) {
        key = item;
        left = right = null;
    }
}

public class BinaryTreeExample {
    Node root;

    BinaryTreeExample() {
        root = null;
    }

    // 이진 트리에 노드 삽입
    void insert(int key) {
        root = insertRec(root, key);
    }

    Node insertRec(Node root, int key) {
        if (root == null) {
            root = new Node(key);
            return root;
        }

        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        return root;
    }

    // 이진 트리 중위 순회 (Inorder Traversal)
    void inorderTraversal(Node root) {
        if (root != null) {
            inorderTraversal(root.left);
            System.out.print(root.key + " ");
            inorderTraversal(root.right);
        }
    }

    public static void main(String[] args) {
        BinaryTreeExample tree = new BinaryTreeExample();

        // 이진 트리에 노드 삽입
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        // 이진 트리 중위 순회 (Inorder Traversal)
        System.out.println("이진 트리 중위 순회 결과:");
        tree.inorderTraversal(tree.root);
    }
}
```

#### Binary Search Tree (BST, 이진 검색 트리)

<img src="https://static.javatpoint.com/ds/images/binary-search-tree1.png" />

- **Define**
  - 계층적 데이터 구조
  - 루트 노드(root node), 부모 노드(parent node), 자식 노드(child node)로 구성될 수 있다.
  - 트리의 각 노드는 최대 2개의 하위 노드를 가질 수 있다. 즉, 부모 노드는 2개의 자식 노드를 가질 수 있다.
  - 이진 트리에서 추가적인 제한을 가지고 있는 트리이다.
    - 왼쪽 자식은 항상 루트 노드보다 작아야 한다.
    - 오른쪽 자식은 항상 루트 노드보다 커야 한다.

- **Advantages**
  - 요소의 순서를 유지한다.
  - 트리에서 최소 및 최대 값을 가진 노드를 쉽게 찾을 수 있다.
  - 순회는 순서대로 정렬된 요소를 제공한다.

- **Disadvantages**
  - 무작위 접근이 불가능하다.

- **Applications**
  - 정렬된 계층적 데이터에 적합하다.

- **Example**
```Java
class Node {
    int key;
    Node left, right;

    public Node(int item) {
        key = item;
        left = right = null;
    }
}

public class BinarySearchTreeExample {
    Node root;

    BinarySearchTreeExample() {
        root = null;
    }

    // BST에 노드 삽입
    void insert(int key) {
        root = insertRec(root, key);
    }

    Node insertRec(Node root, int key) {
        if (root == null) {
            root = new Node(key);
            return root;
        }

        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);

        return root;
    }

    // BST에서 노드 검색
    Node search(Node root, int key) {
        if (root == null || root.key == key)
            return root;

        if (key < root.key)
            return search(root.left, key);

        return search(root.right, key);
    }

    public static void main(String[] args) {
        BinarySearchTreeExample tree = new BinarySearchTreeExample();

        // BST에 노드 삽입
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        // BST에서 노드 검색
        int searchKey = 60;
        Node result = tree.search(tree.root, searchKey);
        if (result != null) {
            System.out.println("검색 결과: " + searchKey + "을(를) 찾았습니다.");
        } else {
            System.out.println("검색 결과: " + searchKey + "을(를) 찾지 못했습니다.");
        }
    }
}
```

#### Graph

<table>
  <tr>
    <td>
    <img src="https://static.javatpoint.com/ds/images/graph-definition.png" />
    </td>
    <td>
    <img src="https://static.javatpoint.com/ds/images/directed-and-undirected-graph.png" />
    </td>
  </tr>
</table>

- **Define**
  - 기본적으로 정점(V)과 간선(E)의 집합이다.
  - 그래프는 방향이 지정되거나 방향이 지정되지 않을 수도 있다.
  - 그래프는 연결이 될 수도, 분리될 수도 있다.
  - G(V, E)로 표현한다.
    - V(G): 정점 집합을 나타낸다.
    - E(G): 간선 집합을 나타낸다.

- **Advantages**
  - 최단 경로를 찾는 것이 가능하다.

- **Disadvantages**
  - 그래프(인접 목록 및 인접 행렬)를 저장하면 복잡해질 수 있다.

- **Applications**
  - 회선 네트워크에 적합하다.
  - Facebook, LinkedIn과 같은 애플리케이션에 적합하다.

- **Example**
```Java
import java.util.LinkedList;

class Graph {
    private int V; // 그래프의 정점 개수
    private LinkedList<Integer>[] adjList; // 인접 리스트 배열

    @SuppressWarnings("unchecked")
    Graph(int v) {
        V = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; ++i) {
            adjList[i] = new LinkedList<>();
        }
    }

    // 그래프에 간선 추가
    void addEdge(int v, int w) {
        adjList[v].add(w);
        adjList[w].add(v);
    }

    // 그래프의 인접 리스트 출력
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            System.out.print("정점 " + i + "에 인접한 정점: ");
            for (Integer vertex : adjList[i]) {
                System.out.print(vertex + " ");
            }
            System.out.println();
        }
    }
}

public class GraphExample {
    public static void main(String[] args) {
        int V = 5; // 그래프의 정점 개수
        Graph graph = new Graph(V);

        // 간선 추가
        graph.addEdge(0, 1);
        graph.addEdge(0, 4);
        graph.addEdge(1, 2);
        graph.addEdge(1, 3);
        graph.addEdge(1, 4);
        graph.addEdge(2, 3);
        graph.addEdge(3, 4);

        // 그래프 출력
        System.out.println("인접 리스트 그래프:");
        graph.printGraph();
    }
}
```

</br>

### ➲ 참고 자료
- https://www.geeksforgeeks.org/data-structures/
- https://www.mygreatlearning.com/blog/data-structures-using-java/