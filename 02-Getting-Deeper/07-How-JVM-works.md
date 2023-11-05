# JVM (Java Virtual Machine)

### JDK와 JRE

- JDK (Java Development Kit) : Java를 사용하기 위해 필요한 모든 기능을 갖춘 Java용 SDK
    
    - 프로그램을 생성, 실행, 컴파일할 수 있다
    - JDK에 JRE가 포함된다
    - 컴파일러(javac)와 jdb, javadoc과 같은 도구들을 포함한다
    
- JRE (Java Runtime Environment) : JVM + Java Class Library
    
    - 컴파일 된 Java 프로그램을 실행하는 데 필요한 패키지이다
    - JRE (Java Runtime Environment)에 JVM이 포함되어 있다
    
<br>

### JVM (Java Virtual Machine)

- JVM (Java Virtual Machine) : Java 프로그램을 실행하기 위한 가상 머신
    
    - Java 코드의 `main()` 함수를 호출한다
    - 자바 바이트 코드가 실행될 수 있는 환경을 제공한다
    - OS에 종속받지 않고 CPU가 Java를 인식, 실행할 수 있게 해준다
    
- JVM 기능
    1. Java 프로그램이 모든 장치나 운영 체제에서 실행되도록 하는 것 (Write Once, Run Anywhere)
        
        현재는 JVM이 Java 뿐만 아니라 다른 언어도 지원한다. 예를 들어 Scala와 Groovy, Kotlin 모두 JVM 언어로 간주된다. 
        
    2. 프로그램 메모리를 관리하고 최적화하는 것
        
        Java 이전에는 모든 프로그램 메모리를 프로그래머가 관리했다. 하지만 Java에서는 프로그램 메모리를 JVM이 관리한다. JVM은 Garbage Collection을 통해 Java 프로그램에서 사용되지 않는 메모리를 지속적으로 식별하고 제거한다.

<br>

### Java 코드 컴파일 과정

- 바이트 코드 : 가상머신(VM)에서 돌아가는 실행 프로그램을 위한 이진 표현법
    
    - 자바 바이트 코드는 JVM이 이해할 수 있는 언어로 변환된 자바 소스코드를 의미한다
    - 자바 컴파일러에 의해 변환된 코드의 명령어 크기가 1 byte이다
    - 바이트 코드는 다시 Interpreter 혹은 JIT 컴파일러에 의해 바이너리 코드로 변환된다
    
- Java 코드 컴파일 과정
    
    ![Java 코드 컴파일 과정](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0kg24%2Fbtq4YOOQH4J%2FEF2ISOpkYA36a1flwtLEmK%2Fimg.png)
    
    1. 자바 컴파일러가 `.java` 파일을 JVM이 인식할 수 있는 `.class` 파일, 즉 자바 바이트 코드로 변환한다
        
        자바 컴파일러는는 JDK에 포함되어 있는 javac.exe이다
        
    2. JVM이 OS가 바이트 코드를 이해할 수 있도록 해석해준다
        
        이 과정을 통해 바이트 코드가 JVM 위에서 OS에 상관 없이 실행될 수 있게 된다

<br><Br>

# JVM Architecture

![JVM Architecture](https://static.javatpoint.com/images/jvm-architecture.png)

### ClassLoader

- ClassLoader의 기능
    - 로딩 : .class 파일을 사용하여 바이너리 데이터를 생성하고 메소드 영역에 저장한다
        
        - .class 파일을 로드한 후 JVM은 힙 메모리에 이 파일을 표시하기 위해 Class 유형의 객체를 생성한다
        - Class 객체에는 클래스 이름, 상위 클래스 이름, 메소드 및 변수 정보와 같은 정보가 저장되어 있다
        - `Object.getClass()`를 통해 정보를 얻을 수 있다
        
    - 연결 : 확인, 준비 및 해결을 수행한다
        1. 확인 : `.class` 파일이 올바른 형식으로 지정됐는지, 유효한 컴파일러에 의해 생성되었는지 여부를 확인한다
            
            - 확인에 실패하면 `java.lang.VerifyError`가 발생한다
            - 이 활동이 완료되면 클래스 파일을 컴파일할 수 있게 된다
            
        2. 준비 : 클래스의 정적 변수에 메모리를 할당하고 메모리를 기본값으로 초기화한다
        3. 해결 : 해당 타입의 symbolic reference를 direct reference로 바꾼다
    - 초기화 : 모든 정적 변수가 코드 및 정적 블록에 있는 값으로 할당된다
        
        - 초기화는 클래스의 위에서 아래로, 계층 구조의 부모에서 자식으로 실행된다
        
- ClassLoader의 종류
    
    ![ClassLoader](https://media.geeksforgeeks.org/wp-content/uploads/jvmclassloader.jpg)
    
    - Bootstrap ClassLoader
        
        - Extension ClassLoader의 상위 클래스로 첫 번째 ClassLoader이다
        - `java.lang`, `java.net` 등 Java Standard Edition의 모든 클래스 파일을 포함하는 `rt.jar` 파일을 로드한다
        
    - Extension ClassLoader :
        
        - System ClassLoader의 상위 클래스이다
        - `$JAVA_HOME/jre/lib/ext`에 있는 jar 파일을 로드한다
        
    - System/Application ClassLoader :
        
        - 클래스 경로에서 클래스 파일을 로드한다
        - 기본적으로 클래스 경로는 현재 디렉토리로 결정된다
        - `-cp` 또는 `-classpath`를 이용하여 클래스 경로를 변경할 수 있다

<br>

### 알아두면 좋은 것들

1. Java는 멀티 스레드 환경으로 모든 스레드는 Heap, Method Area를 공유한다
2. JVM는 스택 기반 가상 머신으로 CPU에 직접 접근하지 않고 Stack에서 주소를 뽑아서 가져온다

<br>

### JVM Memory

> 프로그램을 수행하기 위해 OS로부터 할당받은 메모리 영역

1. Class/Method Area 
    
    클래스 정보를 처음 메모리에 올릴 때 초기화되는 대상을 저장한다. 
    
    | Information | Description |
    | --- | --- |
    | Field Information | 멤버 변수에 대한 정보 (이름, 타입, 접근 지정자 등) |
    | Method Information | 메소드에 대한 정보 (이름, 리턴 타입, 파라미터, 접근 지정자 등) |
    | Type Information | Class & Interface 여부, Type의 속성, 이름, super class의 이름 등 |
    
    + Runtime Constant Pool : 상수 자료형을 저장하여 참조하고 중복을 막는 역할을 수행한다
    
2. Heap
    
    객체를 동적으로 생성하게 되면 인스턴스가 Heap에 저장된다. 단, 레퍼런스 변수의 경우 인스턴스가 아닌 포인터가 저장된다. Garbage Collection의 대상이 되는 영역이다.
    
3. Stack 
    
    호출된 메소드의 파라미터, 지역 변수, 리턴 값 및 연산 값 등이 저장된다. 메소드 호출 시마다 스택에 각각의 스택 프레임이 생성되고, 수행이 끝나면 스택 포인트에서 해당 프레임을 제거한다.
    
4. PC Register (Program Counter Register)
    
    현재 실행해야 할 명령어의 주소를 저장한다. 스레드가 시작될 때 생성되며, 각 스레드마다 별도의 PC Register가 존재한다.
    
5. Native Method Stack
    
    Java 이외의 언어에 제공되는 Method의 정보가 저장된다. Java Native Interface를 통해 바이트 코드로 저장된다. Kernel이 자체적으로 Stack을 잡아 독자적으로 프로그램을 실행시키는 영역이다. 각 스레드마다 별도의 네이티브 스택이 생성된다.

<br>

### Execution Engine 

> 자바 바이트 코드를 명령어 단위로 읽어서 실행한다

1. Garbage Collector : 참조되지 않은 객체를 삭제한다
2. Interpreter : 바이트 코드를 한 줄씩 해석한 후 실행한다
    
    - 하나의 메소드를 여러 번 호출할 때도 계속해서 해석을 해야 한다
    
3. Just-In-Time(JIT) compiler : 전체 바이트 코드를 컴파일하고 Native code로 변경한다
    
    - 반복되는 메소드 호출을 볼 때마다 JIT가 해당 부분에 대한 네이티브 코드를 제공하기 때문에 재해석이 필요없다
    - 인터프리터의 단점을 보완하기 위해 도입되었다

<br>

### Java Native Interface & Native Method Libraries

- Java Native Interface
    
    - Native Method Libraries와 상호작용하며 실행에 필요한 네이티브 라이브러리(C, C++ 등)를 제공한다
    - 이를 통해 JVM은 C/C++ 라이브러리를 호출할 수 있다
    
- Native Method Libraries
    
    - Execution Engine에서 요구하는 Native Libraries(C, C++)의 모음이다

<br><br>

# 참고 자료

[JVM | Java Virtual Machine - Javatpoint](https://www.javatpoint.com/jvm-java-virtual-machine)<br>
[How JVM Works - JVM Architecture? - GeeksforGeeks](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)<br>
[What is the JVM? Introducing the Java virtual machine](https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html)<br>
[What is the JVM? Introducing the Java virtual machine](https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html)<br>
[[IT 기술 면접] JVM (자바 가상 머신) 이란?](https://backendcode.tistory.com/161)<br>
[[JAVA] JVM이란? 개념 및 구조 (JDK, JRE, JIT, 가비지 콜렉터...)](https://doozi0316.tistory.com/entry/1주차-JVM은-무엇이며-자바-코드는-어떻게-실행하는-것인가)