# Garbage

### Garbage

- Garbage : 참조되지 않은 객체
    
    - Java 프로그램이 JVM에서 실행되면 Heap에 객체가 생성된다
    - 일부 객체를 더 이상 필요하지 않게 되고, Garbage Collector는 이러한 객체를 찾아 삭제하여 메모리를 확보한다
    - 보통 객체를 null로 지정하여 객체에 대한 참조를 해제한다
    
- Garbage Collection : Java 프로그램이 자동 메모리 관리를 수행하는 프로세스
    
    - Unreachable Memory를 정리하여 힙 메모리를 확보한다
    - 메모리 누수를 방지하기 위해 Gargabe Collector가 주기적으로 검사하여 메모리를 정리한다
    - Garbage Collection은 힙 메모리만 다룬다
    
- Garbage Collection의 장점
    1. 더 이상 사용되지 않는 객체나 Unreachable 객체를 자동으로 삭제하여 메모리 리소스를 확보한다
    2. Garbage Collector에 의해서 자동으로 수행된다
        
        GC가 없는 C, C++ 등의 언어에서는 코드에서 수동으로 메모리 관리를 구현해야 한다

<br>     

### Reachable & Unreachable Object

- Reachable & Unreachable Object
    
    - Reachable Object : 객체에 대한 참조가 존재한다
    - Unreachable Object : 객체에 대한 참조가 존재하지 않는다
    
- Unreachable Object 예시
    1. 객체가 null인 경우
    2. 객체가 블럭 안에서 생성되고 블럭이 종료된 경우
    3. 부모 객체가 null이 된 경우

<br><br>

# Garbage Collection

### Garbage Collection의 동작 방식

1. Stop The World
    
    GC를 실행하기 위해 JVM이 애플리케이션의 실행을 멈추는 작업. GC가 실행될 때는 GC를 실행하는 스레드를 제외한 모든 스레드의 작업이 중단되고, GC가 완료되면 작업이 재개된다. 모든 스레드의 작업이 중단되면 애플리케이션이 멈추기 때문에 GC의 성능 개선을 위해 Stop The World의 시간을 줄이는 작업을 진행한다.
    
2. Mark and Sweep
    
    Mark : 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
    Sweep : Mark 단계에서 사용되지 않음으로 식벽된 메모리를 해제하는 작업
    
    Stop The World를 통해 모든 작업을 중단시키면 GC는 스택의 모든 변수 또는 Reachable 객체를 스캔하면서 각각이 어떤 객체를 참고하고 있는지 탐색한다. 그리고 사용되지 않는 메모리를 식별하는 Mark 작업을 한다. 이후에 Mark가 되지 않은 객체를 메모리에서 제거하는 Sweep 작업을 진행한다. 마지막으로 효과적으로 Memory를 사용하기 위해 Compaction을 진행한다
    
<br>

### Garbage Collector와 Heap Memory

![Heap Memory](https://stackify.com/wp-content/uploads/2017/05/Java-Garbage-Collection.png)

- Young Generation : 새로 생성된 객체가 저장된다
    
    Eden에 새로운 객체가 저장된다. 그 이후에 한 번의 GC 주기에서 살아남으면 두 개의 Survivor 영역으로 이동된다. Young 영역에서 Garbage가 수집되는 경우에는 Minor Garbage Collection이라고 한다.
    
    Eden 영역에 객체를 빠르게 할당하기 위해 Eden 영역에 마지막으로 할당된 객체의 주소를 캐싱해두는 bump the pool 방식을 사용한다. 추가로 각각의 스레드마다 Eden 영역에 객체를 할당하기 위한 주소를 부여하는 TLABs 기술을 도입하였다.
    
- Old Generation : 수명이 긴 객체를 Young 영역에서 Old 영역으로 복사된다
    
    Young Generation에서 일정 기간 이상 살아남으면 Old 영역으로 복사된다. Old 영역에서 Garbage가 수집되는 경우에는 Major Garbage Collection이라고 한다. Young 영역보다 크기가 크기 때문에 Garbage가 덜 발생한다. 객체의 크기가 큰 경우에는 Young 영역을 거치지 않고 바로 Old 영역에 할당된다.
    
- Permanent Generation : Class, Method와 같은 메타데이터를 저장한다
    
    Garbage Collector는 더 이상 사용되지 않는 Permanent 영역의 클래스를 수집한다.

<br>

### Garbage Collection의 종류

> 대부분의 객체는 금방 접근 불가능한 상태가 된다 <br>
> 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다 <br>
> ⇒ 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우가 드물다

1. Minor Garbage Collection
    
    ![Minor Garbage Collection](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCyho2%2FbtqURvZRql6%2F4a7u6mMGofkpuURKQz0RT1%2Fimg.png)
    
    Eden 영역이 꽉 차면 Minor GC가 발생한다. 이때 사용되지 않는 메모리는 해제되고 Eden 영역에 존재하는 객체는 Survivor 영역으로 옮겨진다. Survivor 영역은 2개 중 중 1개의 영역에만 데이터가 존재해야 한다. (한 개는 빈 상태로 존재해야 함) Eden → Survivor 과정을 반복하다가 Survivor 영역이 가득 차게 되면 Survivor 영역의 남은 객체를 다른 Survivor 영역으로 이동한다. 이 과정을 반복하며 살아남은 객체는 Old 영역으로 이동된다.
    
    객체의 생존 횟수를 세기 위해 Minor GC에서 객체가 살아남은 횟수를 의미하는 age를 Object Header에 기록한다. 그리고 Minor GC 때 Object Header에 기록된 age를 보고 Promotion(Old 영역으로 이동) 여부를 결정한다.
    
2. Major Garbage Collection
    
    Old 영역의 메모리가 부족해지면 발생한다. Young 영역은 일반적으로 Old 영역보다 크기가 작기 때문에 GC가 보통 0.5초~1초 사이에 끝난다. 하지만 Old 영역은 Young 영역보다 크기가 크고 Young 영역을 참조할 수도 있기 때문에 Minor GC의 10배 이상의 시간을 사용한다.
    
3. Full Garbage Collection
    
    Young 영역과 Old 영역을 동시에 처리한다.

<br>

### Garbage Collector

- Serial GC
    
    - 모든 GC 이벤트가 하나의 스레드에서 직렬로 수행된다
    - CPU 코어가 하나만 있을 때 사용하기 위해서 만든 방식이기 때문에 운영 서버에는 잘 사용하지 않는다
    - 마지막 단계에서 객체가 존재하는 부분과 없는 부분으로 나누는 Compaction을 진행한다
    
- Parallel GC (Throughput GC)
    
    ![Parallel GC](https://d2.naver.com/content/images/2015/06/helloworld-1329-4.png)
    
    - GC 이벤트를 여러 스레드에서 처리한다 → 빠르게 객체를 처리할 수 있다
    - 메모리가 충분하고 코어의 개수가 많을 때 유리하다 
    
- Parallel Old GC
    
    - 앞의 두 GC와 Old 영역의 GC 알고리즘이 다르다
    - Mark-Summary-Compaction 단계를 거치며 앞서 GC를 수행한 영역에 대해서 별도로 살아 있는 객체를 식별한다는 점이 다르다
    
- CMS (Concurrent Mark Sweep) GC
    
    ![CMS GC](https://d2.naver.com/content/images/2015/06/helloworld-1329-5.png)
    
    - 다른 스레드가 실행되고 있는 상황에서 진행되기 때문에 Stop The World 시간이 매우 짧다
    
    1. Initial Mark 단계에서 ClassLoader에서 가장 가까운 객체 중 살아있는 객체만 찾는다
    2. Concurrent Mark 단계에서는 방금 살아있다고 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인한다
    3. Remark 단계에서는 Concurrent Mark 단계에서 새로 추가되거나 참조가 끊긴 객체를 확인한다
    4. Concurrent Sweep 단계에서는 Garbage를 정리하는 작업을 한다
- G1 (Garbage First) GC
    
    ![G1 GC](https://d2.naver.com/content/images/2015/06/helloworld-1329-6.png)
    
    - 바둑판의 각 영역에 객체를 할당하고 GC를 실행한다
    - 해당 영역이 꽉 차면 다른 영역에서 객체를 할당하고 GC를 실행한다
    - Young 영역에서 Old 영역으로 이동하는 단계가 사라진 GC 방식이라고 생각하면 된다
    - CMS GC를 대체하기 위해서 만들어졌고, GC 성능이 가장 좋다
    
<br>

### Garbage Collection을 유발하는 요인

1. 객체 할당 실패 
    
    사용 가능한 연속 여유 공간이 충분하지 않아 객체를 힙에 할당할 수 없는 경우 JVM은 가비지 수집을 트리거하여 메모리를 확보한다.
    
2. 힙 크기
    
    힙이 특정 용량 임계값에 도달하면 JVM은 GC를 통해 메모리를 회수하고 `OutOfMemoryError`를 방지한다.
    
3. `System.gc()`
    
    `System.gc()` 메서드를 호출하면 Garbage Collector의 실행을 요청한다.
    
4. 시간 기반
    
    G1 GC와 같은 일부 GC 알고리즘은 시간 기반 트리거를 사용하여 GC를 시작한다.
    
<br>

### Garbage Collector의 실행을 요청하는 법

> Object를 unreachable로 만든 후에 Garbage Collector 프로그램이 실행되면 객체가 삭제된다. (바로 삭제되는 게 아님) 또한, 사용자가 JVM에 Garbage Collector의 실행을 요청할 수 있다.

- `System.gc()` : JVM에 GC의 실행을 요청한다
    
    - JVM에 실행을 요청하는 것일 뿐 반드시 GC가 발생한다는 보장은 없다
    - 시스템의 성능에 매우 큰 영향을 끼치기 때문에 사용하지 않는 게 좋다
    
- `Runtime.getRuntime().gc()` : JVM에 GC의 실행을 요청한다
    
    - JVM에 실행을 요청하는 것일 뿐 반드시 GC가 발생한다는 보장은 없다
    - 시스템의 성능에 매우 큰 영향을 끼치기 때문에 사용하지 않는 게 좋다
    
- JConsole 또는 VisualVM : JDK에 포함된 프로파일링 도구
    
    - 개발자가 Java 애플리케이션의 메모리 사용량을 실시간으로 모니터링할 수 있는 그래픽 사용자 인터페이스를 제공한다
    - 또한 버튼을 클릭하면 GC를 요청할 수 있다
    
- 명령어 사용
    
    - `-Xmx` 를 사용하면 GC 이벤트의 빈도와 기간에 영향을 줄 수 있는 최대 힙 크기를 지정할 수 있다
    - `XX: +DisableExplicitGC` 를 사용하면 `System.gc()`, `Runtime.getRuntime().gc()`를 이용한 명시적 호출을 비활성화한다
    
- Heap Dump : Heap Dump를 분석하여 메모리 누수 또는 기타 메모리 관련 문제를 식별할 수 있다
    
    - 명령줄이나 프로파일링 도구를 통해 GC의 실행을 요청할 수 있다
    - GC를 너무 자주 요청하면 성능에 부정적인 영향을 미칠 수 있기 때문에 필요할 때만 요청해야 한다
    
- + `finalize()` : Garbage Collector는 finalize()를 호출하여 객체를 정리한다
    
    - JVM이 아닌 Garbage Collector에 의해 호출된다
    - 하나의 객체에 반드시 한 번만 호출된다
    - finalize()에 의해 포착되지 않은 예외가 발생하면 해당 예외는 무시되고 객체를 정리한다

<br>

### 프로그래머가 Garbage Collection을 이해해야 하는 이유

Java 기술을 향상시키려는 프로그래머의 경우 GC의 작동 방식과 조정 방법을 이해하는 것이 중요하다. GC는 비결정적이며 런타임에 GC가 언제 발생할지 예측할 수 없다. 명시적으로 GC의 실행을 요청할 수는 있지만 실제로 실행된다는 보장도 없다!

<br>

### Garbage Collection 모범 사례

> JVM에 플래그를 설정하는 것

힙의 초기 및 최대 크기, 힙 섹션의 크기와 같은 다양한 플래그를 사용하여 Garbage Collector를 조정할 수 있다. 예를 들어 Parallel Garbage Collector는 효율적이지만 Stop the world를 자주 발생시키기 때문에 긴 일시중지가 허용되는 백엔드 처리에 더 적합하다. 반면 CMS Garbage Collector는 일시 중지를 최소화하도록 설계되어 응답성이 중요한 GUI 응용 프로그램에 이상적이다. 

<br>

### Demon Thread

- Daemon Thread : Garbage Collection 작업이나 사용자 스레드에 서비스를 제공하기 위해 백그라운드에서 실행되는 우선순위가 낮은 스레드
    
    - 백그라운드에서 작업을 처리하여 사용자의 작업을 방해하지 않고 기본 실행을 지원하는 작업을 수행한다
    - 데몬 스레드의 수명은 사용자 스레드에 따라 달라진다
    - 즉, 모든 사용자 스레드가 실행을 마치면 JVM이 자동으로 데몬 스레드를 종료한다
    
- Daemon Thread 속성
    
    - 모든 사용자 스레드가 작업을 완료하면 데몬 스레드 실행 여부와 관계없이 JVM이 종료된다
    - 데몬 스레드는 Java의 모든 스레드 중에서 가장 낮은 우선순위를 가진다
    - 상위 스레드가 데몬 스레드라면, 하위 스레드도 데몬 스레드이다

<br><br>

# Garbage Collection의 활용

> 회사에서 근무하는 직원 수를 계산하는 프로그램을 작성하라 (인턴 제외)

### Garbage Collector를 사용하지 않는 경우

- 코드
    
    ```java
    class Employee {
        private int ID;
        private String name;
        private int age;
        private static int nextId = 1;
       
        public Employee(String name, int age) {
            this.name = name;
            this.age = age;
            this.ID = nextId++;
        }
    
        public void show() {
            System.out.println("Id=" + ID + "\nName=" + name
                               + "\nAge=" + age);
    		}
    
        public void showNextId() {
            System.out.println("Next employee id will be=" + nextId);
        }
    }
     
    class UseEmployee {
        public static void main(String[] args) {
            Employee E = new Employee("GFG1", 56);
            Employee F = new Employee("GFG2", 45);
            Employee G = new Employee("GFG3", 25);
            E.show();
            F.show();
            G.show();
            E.showNextId();
            F.showNextId();
            G.showNextId();
     
            {  // 인턴 정보
                Employee X = new Employee("GFG4", 23);
                Employee Y = new Employee("GFG5", 21);
                X.show();
                Y.show();
                X.showNextId();
                Y.showNextId();
            }
               
            E.showNextId(); 
        }
    }
    ```
    
- 출력
    
    ```java
    Id=1 
    이름=GFG1 
    나이=56 
    Id=2 
    이름=GFG2 
    나이=45 
    Id=3 
    이름=GFG3 
    나이=25 
    다음 직원 ID=4 
    다음 직원 ID=4 
    다음 직원 ID=4 
    Id= 4 
    이름=GFG4 
    나이=23 
    ID=5 
    이름=GFG5 
    나이=21 
    다음 직원 ID=6 
    다음 직원 ID=6 
    다음 직원 ID=6
    ```

<br>

### Garbage Collector를 사용하는 경우 (올바른 방법)

1. 사용하지 않는 객체를 null로 처리한다 (인턴을 제외함)
2. `System.gc()` 를 호출해서 Garbage Collector를 실행한다
3. `System.runFinalization()` 을 호출해서 객체를 정리한다
- 코드
    
    ```java
    class Employee {
        private int ID;
        private String name;
        private int age;
        private static int nextId = 1;
    
        public Employee(String name, int age) {
            this.name = name;
            this.age = age;
            this.ID = nextId++;
        }
    
        public void show() {
            System.out.println("Id=" + ID + "\nName=" + name + "\nAge=" + age);
        }
    
        public void showNextId() {
            System.out.println("Next employee id will be=" + nextId);
        }
    
    		protected void finalize() {
            --nextId;  // GC가 finalize를 호출
        }
    }
     
    public class UseEmployee {
        public static void main(String[] args) {
            Employee E = new Employee("GFG1", 56);
            Employee F = new Employee("GFG2", 45);
            Employee G = new Employee("GFG3", 25);
            E.show();
            F.show();
            G.show();
            E.showNextId();
            F.showNextId();
            G.showNextId();
     
            {  // 인턴에 대한 정보를 제거
                Employee X = new Employee("GFG4", 23);
                Employee Y = new Employee("GFG5", 21);
                X.show();
                Y.show();
                X.showNextId();
                Y.showNextId();
                X = Y = null;  // 객체에 대한 참조를 해제
                System.gc();  // Garbage Collector를 호출
                System.runFinalization();  // finalize를 호출
            }
    
    				E.showNextId();
        }
    }
    ```
    
- 출력
    
    ```java
    Id=1 
    이름=GFG1 
    나이=56 
    Id=2 
    이름=GFG2 
    나이=45 
    Id=3 
    이름=GFG3 
    나이=25 
    다음 직원 ID=4 
    다음 직원 ID=4 
    다음 직원 ID=4 
    Id= 4 
    이름=GFG4 
    나이=23 
    ID=5 
    이름=GFG5 
    나이=21 
    다음 직원 ID=6 
    다음 직원 ID=6 
    다음 직원 ID=4  // 인턴에 대한 정보를 제거
    ```

<br><br>

# 참고 자료

[Garbage Collection in Java: Types, How It works, Example - javatpoint](https://www.javatpoint.com/Garbage-Collection)<br>
[Garbage Collection in Java - GeeksforGeeks](https://www.geeksforgeeks.org/garbage-collection-java/)<br>
[What is Java Garbage Collection? Best Practices, Tutorials & More](https://stackify.com/what-is-java-garbage-collection/)<br>
[Daemon Thread in Java - GeeksforGeeks](https://www.geeksforgeeks.org/daemon-thread-java/)<br>
[[Java] Garbage Collection(가비지 컬렉션)의 개념 및 동작 원리 (1/2)](https://mangkyu.tistory.com/118)<br>
[Java Garbage Collection](https://d2.naver.com/helloworld/1329)<br>
[💡 [CS지식] Garbage Collection에 대하여](https://meoru-tech.tistory.com/81)