# Collections

### Collection

- Collection : 객체 그룹을 저장하고 조작하기 위한 아키첵처를 제공하는 프레임워크
    
    ![https://static.javatpoint.com/images/java-collection-hierarchy.png](https://static.javatpoint.com/images/java-collection-hierarchy.png)
    
    - 검색, 정렬, 삽입, 조작, 삭제 등 데이터에 대해 수행하는 모든 작업을 수행할 수 있다
    - List, Set, Queue는 Collection 인터페이스를 상속받지만, Map은 별도로 정의된다
    
- Collection을 사용하는 이유
    
    - Collection의 일관된 API를 사용하여 통일된 메소드를 사용할 수 있다
    - OOP 추상화의 기본 개념이 성공적으로 구현되어 있다
    - Collection을 활용한 데이터 구조 및 알고리즘을 사용하여 성능을 향상시킬 수 있다
    
- Collection 주요 Method
    
    | 메소드 | 설명 |
    | --- | --- |
    | boolean add(E e) | 해당 Collection에 요소를 추가한다 |
    | void clear() | 해당 컬렉션의 모든 요소를 제거한다 |
    | boolean contains(Object o) | 해당 컬렉션이 전달된 객체를 포함하고 있는지를 확인한다 |
    | boolean equals(Object o) | 해당 컬렉션과 전달된 객체가 같은지를 확인한다 |
    | boolean isEmpty() | 해당 컬렉션이 비어있는지를 확인한다 |
    | Iterator<E> iterator() | 해당 컬렉션의 반복자(iterator)를 반환한다 |
    | boolean remove(Object o) | 해당 컬렉션에서 전달된 객체를 제거한다 |
    | int size() | 해당 컬렉션의 요소의 총 개수를 반환한다 |
    | Object[] toArray() | 해당 컬렉션의 모든 요소를 Object 타입의 배열로 반환한다 |

<br><br>

# List

### List

- ArrayList : 데이터를 추가하고 삭제하면 크기가 자동으로 조정되는 동적 리스트
    
    - 인덱스를 이용해 배열 요소에 빠르게 접근할 수 있다
    
    ```java
    ArrayList<Integer> list = new ArrayList<Integer>();
    ```
    
- LinkedList : 데이터를 연속된 위치가 아닌 데이터, 주소 부분으로 나누어진 노드에 저장하는 리스트
    
    - 포인터와 주소를 사용해서 데이터를 가져온다
    
    ```java
    LinkedList<Integer> list = new LinkedList<Integer>();
    ```
    
- Vector : ArrayList와 유사하지만 Thread-safe를 이용하여 동기화가 가능한 동적 리스트
    
    - 과거에 대용량 처리를 위해 주로 사용했다
    - 멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있다
    - 내부에서 자동으로 동기화 처리가 일어나 비교적 성능이 무거워 잘 쓰이지 않는다
    - 현재는 기존 코드와의 호환성을 위해 남아있고 사용은 되지 않는다
    
    ```java
    Vector<Integer> vector = new Vector<Integer>();
    ```
    
<br><br>

# Stack과 Queue

### Stack

- Stack : LIFO을 원칙으로 하는 자료구조
    
    - List의 Vector Class를 상속 받는다
    
    ```java
    Stak<Integer> stack = new Stack<>();
    ```
    
- Stack의 Method
    
    | 메소드 | 설명 |
    | --- | --- |
    | boolean empty() | 해당 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환한다 |
    | E peek() | 해당 스택의 제일 상단에 있는 요소를 반환한다 |
    | E pop() | 해당 스택의 제일 상단에 있는 요소를 반환하고, 해당 요소를 스택에서 제거한다 |
    | E push(E item) | 해당 스택의 제일 상단에 요소를 삽입한다 |
    | int search(Object o) | 상단 다음부터 탐색을 진행해 해당 객체가 존재하는 위치의 인덱스를 반환한다 |

<br>

### Queue

- Queue : FIFO를 원칙으로 하는 자료구조
    
    ```java
    Queue<Integer> queue = new LinkedList<>();
    ```
    
- Queue의 Method
    
    | 메소드 | 설명 |
    | --- | --- |
    | boolean add(E e) | 해당 큐의 맨 뒤에 전달된 요소를 삽입한다 |
    | E element() | 해당 큐의 맨 앞에 있는 요소를 반환한다 |
    | boolean offer(E e) | 해당 큐의 맨 뒤에 요소를 삽입한다 |
    | E peek() | 해당 큐의 맨 앞에 있는 요소를 반환한다 |
    | E poll() | 해당 큐의 맨 앞에 있는요소를 반환하고, 해당 요소를 큐에서 제거한다 |
    | E remove() | 해당 큐의 맨 앞에 있는 요소를 제거한다 |

- PriorityQueue : 우선 순위에 따라 객체를 처리하는 Queue
    
    - 기본적으로 FIFO를 원칙으로 하지만, 우선 순위에 따라 먼저 처리할 것이 있다면 Heap을 기반으로 처리한다
    
    ```java
    PriorityQueue<Integer> pQueue = new PriorityQueue<Integer>();
    ```
    
- Deque : 양쪽 끝에서 요소를 추가하고 제거할 수 있는 양방향 Queue
    
    - 데이터를 어떤 쪽으로 입력하고 어떤 쪽으로 출력하는지에 따라 스택 혹은 큐로 사용할 수 있다
    - 한 쪽으로만 입력 가능하도록 설정한 덱을 Scroll, 한 쪽으로만 출력 가능하도록 설정한 덱을 Shelf라고 한다
    
    ```java
    Deque<String> stack = new ArrayDeque<>();
    ```

<br><br>

# Set

### Set

- Set : 중복 값을 저장할 수 없는 정렬되지 않은 데이터의 모음
    
    - 중복을 방지하고 고유한 데이터만 저장해야 하는 경우에 사용한다
    
- HashSet : 데이터의 저장 순서를 보장하지 않는다 (대표적인 Set 자료구조)
    
    - NULL 삽입을 허용한다
    
    ```java
    HashSet<String> hs = new HashSet<String>();
    ```
    
- LinkedHashSet : HashSet과 유사하지만 데이터의 저장 순서를 유지한다
    
    ```java
    LinkedHashSet<String> lhs = new LinkedHashSet<String>();
    ```
    
- TreeSet : Tree를 사용하여 데이터를 저장하는 Set
    
    - 데이터는 오름차순으로 정렬된다
    
    ```java
    TreeSet<String> ts = new TreeSet<String>();
    ```

<br><br>

# Map

### Map

- Map : 데이터를 Key:Value 값으로 매핑하여 저장하는 데이터 구조
    
    - 중복 키는 지원하지 않는다
    - 키를 기반으로 프로그래밍을 하는 경우에 유용하게 사용된다
    
- HashMap : 자바 Map의 기본적인 방식
    
    - Hashing 기술을 사용하여 인덱싱 및 검색 작업을 빠르게 처리할 수 있다
    
    ```java
    HashMap<Integer, String> hm = new HashMap<Integer, String>();
    ```
    
- HashTable : HashMap과 유사하지만 동기화를 지원한다
    
    - Null 삽입이 불가능하다
    - HashMap보다는 성능이 느리지만 동기화를 지원한다
    - 멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있다
    
    ```java
    Map<String, String> map = new HashTable<>();
    ```
    
- TreeMap : Tree를 사용하여 데이터를 저장하는 Map
    
    - 이진 트리로 구성되어 있다
    - TreeSet처럼 데이터를 오름차순으로 정렬한다

<br><br>

# Iterable & Iterator

### Iterable

- Iterable : Collection의 상위 인터페이스, 반복할 수 있는 데이터 구조를 나타낸다
    
    ![Iterable](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgbJkF%2FbtrSCLQz8Qd%2Fe94GtwAHsKuND48KMFhEf1%2Fimg.jpg)
    
    - Iterable 인터페이스 안에는 iterator가 abstract method로 선언되어 있다
    - Iterable의 역할은 하위 클래스에서 무조건 `iterator()` 메소드를 포함하도록 하기 위함이다
    - 이 과정을 통해 Collection은 `iterator()`를 사용할 수 있게 된다
    - Iterable을 상속 받는 클래스는 Iterator를 사용하여 for-each문을 사용할 수 있게 된다
    
<br>

### Iterator

- Iterator : Collection과 별개로 존재하는 인터페이스
    
    - Collection의 데이터를 하나씩 읽어올 때 사용하는 표준화된 인터페이스이다
    - Set은 Iterator를 이용해야만 출력이 가능하다
    - `hasNext()` : 다음 요소가 존재하면 true를 반환한다
    - `next()` : 다음 요소를 반환한다
    - `remove()` : iterator로 반환된 요소를 제거한다
    
    ```java
    LinkedList<String> list = new LinkedList<>();
    list.add("Lee"); 
    list.add("ekk"); 
    list.add("eww");
    
    Iterator it = list.iterator();
    while (it.hasNext()) {
        System.out.print(it.next() + " ");
    }
    ```

<br><br>

# Comparable & Comparator

### Comparable & Comparator

> Comparable과 Comparator는 인터페이스기 때문에 선언된 메소드를 반드시 구현해야 한다
- Comparable과 Comparator가 필요한 이유
    
    두 인터페이스 모두 객체를 비교할 수 있도록 해준다. Primitive Type은 자바 자체에서 제공되기 때문에 부등호를 이용하여 별다른 처리 없이 비교가 가능하다. 하지만 객체는 사용자가 기준을 정해주지 않는 이상 프로그램이 우선 순위를 판단할 수 없다. 이런 상황에서 Comparable과 Comparator가 필요하다.
    
- Comparable : 자기 자신과 매개변수 객체를 비교한다
    
    - lang package에 있기 때문에 따로 import할 필요가 없다
    - 자기 자신과 상대방을 비교하기 때문에 자기 자신을 기준으로 삼아 대소관계를 파악한다
    - compareTo 메소드를 반드시 구현해야 한다
    
    ```java
    class Student implements Comparable<Student> {
    		int age;  // 나이
    		int classNumber;	// 학급
    		
    		Student(int age, int classNumber) {
    				this.age = age;
    				this.classNumber = classNumber;
    		}
    		
    		@Override
    		public int compareTo(Student o) {
    				/*
    				 * 만약 자신의 age가 o의 age보다 크다면 양수가 반환 될 것이고,
    				 * 같다면 0을, 작다면 음수를 반환할 것이다.
    				 */
    				return this.age - o.age;
    		}
    }
    ```
    
- Comparator : 두 매개변수 객체를 비교한다
    
    - util package에 있기 때문에 따로 import가 필요하다
    - 자기 자신을 배제하고 매개변수로 들어오는 o1, o2의 값을 비교한다
    
    ```java
    import java.util.Comparator;	
    class Student implements Comparator<Student> 
    		int age;	// 나이
    		int classNumber;	// 학급
    		
    		Student(int age, int classNumber) {
    				this.age = age;
    				this.classNumber = classNumber;
    		}
    		
    		@Override
    		public int compare(Student o1, Student o2) {
    				// o1의 학급이 o2의 학급보다 크다면 양수
    				if(o1.classNumber > o2.classNumber) {
    					return 1;
    				}
    				// o1의 학급이 o2의 학급과 같다면 0
    				else if(o1.classNumber == o2.classNumber) {
    					return 0;
    				}
    				// o1의 학급이 o2의 학급보다 작다면 음수
    				else {
    					return -1;
    				}
    		}
    }
    ```

<br><br>

# 참고 자료

[Collections in Java - javatpoint](https://www.javatpoint.com/collections-in-java)<br>
[Java - Collections Framework](https://www.tutorialspoint.com/java/java_collections.htm)<br>
[[JAVA] 컬렉션(Collection)이란?(추가 : Collecion의 요소 상세설명)](https://crazykim2.tistory.com/557)<br>
[[JAVA] Java 컬렉션(Collection) 정리](https://gangnam-americano.tistory.com/41)<br>
[코딩교육 티씨피스쿨](http://www.tcpschool.com/java/java_collectionFramework_concept)<br>
[코딩교육 티씨피스쿨](http://www.tcpschool.com/java/java_collectionFramework_stackQueue)<br>
[자바 [JAVA] - Comparable 과 Comparator의 이해](https://st-lab.tistory.com/243)<br>
[[Java] Iterable 과 Iterator 이란?](https://devlog-wjdrbs96.tistory.com/84)<br>
[Java Iterable Iterator 차이점 정리](https://wildeveloperetrain.tistory.com/209)<br>
[Java - Collection과 Map의 종류(List, Set, Map)](https://memostack.tistory.com/234)<br>
[Java Map 컬렉션(Collection) 개념 및 종류](https://lelecoder.com/49)<br>