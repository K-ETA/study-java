# Memory Management

### Java의 메모리 관리

> Java는 Garbage Collector를 이용하여 자동 메모리 관리 시스템을 사용한다
- 메모리 관리
    
    모든 프로그램에서 메모리를 필수적인 요소지만, 우리는 항상 메모리 부족 문제에 시달리고 있다. 따라서 철저하게 메모리를 관리하는 것이 중요하다. Java에서는 다른 프로그래밍 언어와 달리 Garbage Collector가 알아서 불필요한 메모리를 정리해준다. 하지만 다른 프로그래밍 언어는 프로그래머가 직접 메모리를 해제해야 하기 때문에 메모리 누수 가능성이 커진다.

- 메모리 관리 프로그래머 주의 사항
    
    Java 자체에서 메모리를 관리해주기 때문에 프로그래머의 명시적인 개입이 필요하지 않다. 하지만 그렇다고 해서 프로그래머가 아예 메모리 관리에 신경을 쓰지 않아도 되는 것은 아니다. 메모리 관리가 어떻게 작동하는지 모르면 JVM에서 관리하지 않는 작업을 수행하여 Garbage Collector가 작동하지 않을 수 있다. 따라서 사용자도 메모리 관리에 대한 주의가 필요하다.

<br><br>

# Garbage Collection

### Garbage Collector

- Garbage Collector : 메모리에 있는 모든 객체를 관찰하며 프로그램의 일부에서 더이상 참조를 하지 않는 객체를 찾아내는 백그라운드에서 수행되는 프로그램
    
    - JVM(Java Virtual Machine)에 의해 제어된다
    - JVM은 Garbage를 수집할 시기를 결정하고, 실행을 요청한다
    - JVM은 메모리 부족을 감지하면 가비기 수집기를 실행한다
    - Garbage Collector는 해당 데이터에 접근할 일이 없다고 생각됐을 때 삭제를 진행한다
    
- Garbage Collection : 새로운 객체 할당을 위하여 Heap의 공간을 확보하는 처리 과정
    
    ```java
    Person person = new Person();
    person.setName("Mang");
    person = null;
    
    // 가비지 발생
    person = new Person();
    person.setName("MangKyu");
    ```

<br>

### Reachable/Unreachable

> 특정 개체가 Garbage인지 아닌지 판단하기 위해 Reachable이라는 개념을 적용한다
> 
- Reachable : 객체가 참조되고 있는 상태
- Unreachable : 객체가 참조되고 있지 않은 상태 (GC의 대상이 된다)

<br>

### Garbage Collection의 동작 방식

> 메모리 영역에 따라 세부적인 동작이 다르긴 하지만, 기본적으로 아래 두 가지 단계를 따른다
1. Stop The World : Garbage Collection 작업을 실행하기 위해 JVM이 앱의 실행을 멈추는 작업
    
    GC가 실행될 때는 GC를 실행하는 스레드를 제외한 모든 스레드의 작업이 중단된다. 그 후 GC가 완료되면 작업이 재개된다. 모든 스레드의 작업이 중단되면 앱이 멈추기 때문에 튜닝을 통해 Stop The World 시간을 단축하는 작업을 실행한다.
    
2. Mark and Sweep
    
    ☑️ Mark : 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
    
    ☑️ Sweep : Mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업
    
    Stop The World를 통해 모든 작업을 중단시키면, GC는 스택의 모든 변수 또는 Reachable 객체를 스캔하면서 각각이 어떤 객체를 참고하고 있는지 탐색한다. Mark를 통해 사용되지 않는 메모리를 식별하고, Mark가 되지 않은 객체들을 메모리에서 제거하는 Sweep 과정을 거친다.
    
3. Compact : Sweep 후에 분산된 객체들을 Heap의 시작 주소로 모아 메모리가 할당된 부분과 그렇지 않은 부분으로 압축하는 작업
    
    새로운 객체를 위한 메모리 할당의 성능을 향상시켜준다
    
<br>

### Minor GC와 Major GC

- Heap 영역의 설계 전제
    1. 대부분의 객체는 금방 Unreachable 상태가 된다
    2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다
    
    ⇒ 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드물다
    
- Young 영역과 Old 영역
    
    > 생존 기간에 따라 물리적인 Heap 영역을 나누게 되었다<br>
    초기에는 Perm 영역도 존재하였지만, Java8부터 제거되었다

    
    ![핵심 정리](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdM4wqf%2FbtqUWs2lW8H%2FGvRECmsUIfZ2jhDoKhSCD0%2Fimg.png)
    
    - Young 영역 (Young Generation) : 새롭게 생성된 객체가 할당되는 영역
        
        - 대부분의 객체가 금방 Unreachable 상태가 되기 때문에 많은 객체가 Young 영역에 생성되었다가 사라진다
        - Young 영역에 대한 GC를 Minor GC라고 부른다
        
    - Old 영역 (Old Generation) : Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
        
        - Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생한다.
        - Old 영역에 대한 GC를 Major GC라고 부른다
        - Old 영역이 Young 영역보다 크게 할당되는 이유는 Young 영역의 객체들은 수명이 짧아 큰 공간이 필요하지 않고, 큰 공간이 필요한 객체들은 Young 영역이 아니라 Old 영역에 바로 할당되기 때문이다
        
- GC 영역의 흐름 (일반적인 흐름)
    
    ![GC 영역의 일반적인 흐름](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fva8qQ%2FbtqUSpSocbS%2FkxTvtnmrdhf4bnVPXth0UK%2Fimg.png)
    
- Old 영역에 있는 객체가 Young 영역을 참고하는 경우
    
    ![Old 영역에 있는 객체가 Young 영역을 참고하는 경우](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFOLU3%2FbtqUOBF35cJ%2FBMKuD1iqfq6R0lAqMlfkC0%2Fimg.png)
    
    - 예외적으로 Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우도 존재한다
    - 이런 경우를 대비하여 Old 영역에는 512 bytes로 되어 있는 카드 테이블이 존재한다
    - 카드 테이블에는 Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때마다 그에 대한 정보가 표시된다

<br>

### Garbage Collection Type

- Serial GC : Young 영역, Old 영역을 대상으로 Mark and Sweep 방식을 사용한다
    
    - Minor 및 Major GC가 Serial GC에 해당한다
    
- Parallel GC : Serial GC와 비슷하지만 Young 영역의 GC을 위해 N개의 스레드를 생성한다
    
    - N은 시스템의 CPU 코어 수이다
    
- Parallel Old GC : Parallel GC와 비슷하지만, Young과 Old 모두에 N개의 스레드를 생성한다
- Concurrent Mark Sweep (CMS) Collector : Old 영역을 대상으로 하는 GC
    
    - `XX:ParalleCMSThreads=JVM`을 사용하여 CMS 수집기의 스레드 수를 제한할 수 있다
    -  Concurrent Low Pause Collector라고도 한다
    
- G1 Garbage Collector : CMS Collector를 대체하기 위해 만들어진 Parallel, concurrent, CMS Collector
    
    - Young 영역 혹은 Old 영역을 위한 공간이 존재하지 않는다
    - 힙을 동일한 크기의 여러 힙으로 나누고, 실시간 데이터가 적은 지역을 수집한다

<br>

### 참조 유형

> Java의 참조 유형에 따라 GC의 실행 대상 여부, 시점이 달라진다
> 
- Strong Reference : Java의 기본 참조 유형
    
    - 변수가 참조를 가지고 있는 한 GC의 대상이 되지 않는다
    
    ```java
    StringBuilder sb = new StringBuilder();
    ```
    
- Soft Reference
    
    - 대상 객체의 참조가 Soft Reference에만 존재할 때 GC의 대상이 된다
    - 다만 JVM 메모리가 부족한 경우에만 Heap 영역에서 제거되고 메모리가 부족하지 않다면 굳이 제거하지 않는다
    
    ```java
    SoftReference<StringBuilder> soft = new SoftReference<>(new  StringBuilder());
    ```
    
- Weak Reference
    
    - 개상 객체의 참조가 Weak Reference에만 존재할 때 GC의 대상이 된다
    - 다음 GC 실행 시 무조건 Heap 메모리에서 제거된다
    
    ```java
    WeakReference<StringBuilder> weak = new WeakReference<>(new  StringBuilder());
    ```
    
- Phantom Reference
    
    - 생성자에서 무조건 ReferenceQueue를 사용해야 한다
    - 객체 내부의 참조를 null로 설정하지 않고 참조된 객체를 Phantomly reachable 객체로 만든 후에 ReferenceQueue에 enqueue된다
    
    ```java
    ReferenceQueue<MyClass> phantom = new ReferenceQueue<MyClass>();
    ```

<br><br>

# JVM

### JVM

- JVM (Java Virtual Machine) : 컴퓨터가 자바 프로그램을 실행할 수 있도록하는 추상적 컴퓨팅 장치
    
    ![JVM 메모리 구조](https://static.javatpoint.com/core/images/memory-management-in-java.png)
    
    - 프로그램 실행 중에 사용되는 다양한 런타임 데이터 영역을 정의한다
    - 자바와 운영체제 사이에서 중개자 역할을 하며, 운영체제에 구애 받지 않고 프로그램을 실행할 수 있도록 돕는다
    - 스택 기반으로 동작한다
    
- JVM의 구조
    
    ![JVM의 구조](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpjywN%2FbtqSduBXLIK%2F2QEL5c2nEJXRm0cyhvwxF1%2Fimg.png)
    
    1. Class Loader
        
        - JVM 내로 .class 파일을 로드하고, 로딩한 클래스들을 Runtime Data Area에 배치한다
        - 런타임 시에 동적으로 클래스를 로드한다
        
    2. Execution Engine
        
        - Runtime Data Area에 배치된 Bytecode를 해석한다
        - 일정 기준까지는 Interpreter 방식을 사용하고, 그 이후에는 JIT 컴파일러 방식으로 실행한다
        
    3. Garbage Collector
        
        - 힙 메모리 영역에 생성된 객체들 중에서 참조되지 않은 객체들을 탐색 후 제거한다
        
    4. Runtime Data Area
        
        - 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역
        - Method Area, Heap Area, Stack Area, PC Register, Native Method Stack로 나눌 수 있다

<br>     

### JVM 메모리 구조

> JVM은 프로그램 실행 중에 사용되는 다양한 런타임 데이터 영역을 정의한다

![JVM 메모리 구조](https://media.geeksforgeeks.org/wp-content/uploads/Memory.png)

- Method Area : Class, Interface, Method, Field, Static 변수 등의 바이트 코드를 보관한다
    
    - JVM이 시작될 때 생성된다
    - 모든 스레드에서 공유되는 힙 메모리 영역이다
    
- Heap Area : new 키워드로 생성된 Instance와 Array가 저장된다 (GC와 가장 관련이 깊은 부분)
    
    - 모든 스레드에서 공유되는 힙 메모리 영역이다
    - Heap에는 메모리를 할당하는 Instruction만 존재하고, 메모리 해제는 GC를 통해서만 수행된다
    - 데이터의 생존 시간에 따라 Young 영역과 Old 영역이 나뉜다
    - Old 영역에 할당된 메모리가 허용치를 넘게 되면 참조되지 않는 객체를 한꺼번에 삭제하는 GC가 실행된다
    - JVM은 요구 사항에 따라 힙 크기를 초기화하거나 변경하는 사용자 제어 기능을 제공한다
    
- Stack Area : 호출된 메소드의 매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장한다
    
    - 메소드 호출 시마다 각각의 스택 프레임이 생성된다 (해당 메소드를 위한 공간)
    - 선언된 블록 안에서만 유효한 로컬 변수와 매개변수가 스택 영역에 저장되는 것이다
    - Heap 영역에 할당된 Object 타입 데이터들의 참조를 위한 값이 할당된다
    
- Native Method Stack : 자바 외 언어로 생성된 네이티브 코드를 위한 메모리 영역
    
    - 언어에 맞게 스택이 형성되는 구역이다
    
- Program Counter(PC) Register : 현재 수행 중인 JVM 명령의 주소값을 저장한다
    
    - 스레드가 시작될 때 생성되며, 스레드마다 하나씩 존재한다
    - 스레드가 어떤 부분을 무슨 명령으로 실행할지에 대한 기록을 진행한다

<br><br>

# 참고 자료

[Java Memory Management - GeeksforGeeks](https://www.geeksforgeeks.org/java-memory-management/)<br>
[Memory Management in Java - Javatpoint](https://www.javatpoint.com/memory-management-in-java)<br>
[JAVA) JAVA 메모리관리에 대해](https://velog.io/@baek1008/JAVA-JAVA-메모리관리에-대해)<br>
[자바가상머신(JVM)에서 자바 메모리 관리](https://docs.oofbird.me/java/article/java-memory-management.html)<br>
[[Java] Garbage Collection(가비지 컬렉션)의 개념 및 동작 원리 (1/2)](https://mangkyu.tistory.com/118)<br>
[Garbage Collector 제대로 알기](https://velog.io/@recordsbeat/Garbage-Collector-제대로-알기)<br>
[☕ 가비지 컬렉션 동작 원리 & GC 종류 💯 총정리](https://inpa.tistory.com/entry/JAVA-☕-가비지-컬렉션GC-동작-원리-알고리즘-💯-총정리)<br>
[[Java] 참조 유형 (Strong Reference / Soft Reference / Weak Reference / Phantom Reference)](https://jangjjolkit.tistory.com/31)<br>
[JVM 메모리 구조란? (JAVA)](https://steady-coding.tistory.com/305)<br>
[[JVM Internal] JVM 메모리 구조](https://12bme.tistory.com/382)<br>
[[Java] 자바 JVM 내부 구조와 메모리 구조에 대하여](https://coding-factory.tistory.com/828)<br>
[Method Area와 JVM Stack, Heap 메모리의 구조와 용도](https://hanna97.tistory.com/entry/Method-Area와-JVM-Stack-Heap-메모리의-구조와-용도)