# Thread

### Thread

- Process : CPU에 의해 메모리에 올려져 실행 중인 프로그램
    
    - 자신만의 메모리 공간을 포함한 독립적인 실행 환경을 가지고 있다
    - JVM은 주로 하나의 프로세스로 실행되며, 동시에 여러 작업을 수행하기 위해서 멀티 스레드를 지원한다
    
- Thread : 프로세스 안에서 실질적으로 작업을 실행하는 단위 (실행 흐름의 단위)
    
    - JVM에 의해 관리된다
    - 프로세스에는 적어도 1개 이상의 스레드가 있으며, Main Thread로 시작한다
    - 각 스레드는 프로세스의 리소스를 공유하기 때문에 효율적이지만 자원 공유 관련 문제가 발생할 수 있다
    
    - Main Thread
        
        - 일반적으로 모든 프로그램에는 JVM 또는 JVM이 제공하는 메인 스레드가 하나 이상 존재한다
        - 메인 스레드에서 `main()`이 호출된다
        
- Thread의 우선순위
    
    - JVM에서 생성된 모든 스레드에는 우선순위가 부여된다
    - 각 스레드의 우선순위는 다양하며, 우선순위가 높은 스레드부터 실행된다
    - `main()`의 우선순위 초기값은 5이다
    <br>

    | 우선순위 | 값 |
    | --- | --- |
    | Thread.MIN_PRIORITY | 1 |
    | Thread.NORM_PRIORITY | 5 |
    | Thread.MAX_PRIORITY | 10 |

<br>

### Thread의 생성자 & 메소드

- 생성자
    
    - `Thread()` : 새로운 스레드 객체 할당
    - `Thread(String name)` : 새로운 스레드 객체를 할당하고 이름을 부여한다
    - `Thread(Runnable target)` : Runnable target이 구현된 스레드 객체 할당
    - `Thread(Runnable target, String name)` : Runnable target과 이름을 부여한 스레드 객체 할당
    
- 메소드
    
    | run() | 스레드의 작업을 수행한다 |
    | --- | --- |
    | start() | 스레드를 실행하고 run()을 호출한다 |
    | sleep(long milisec) | 현재 실행 중인 스레드를 밀리초 동안 실행 중지 상태로 만든다 |
    | join() | 스레드가 죽을 때까지 기다린다 |
    | getPriority() | 스레드의 우선순위를 반환한다 |
    | setPriority(int priority) | 스레드의 우선순위를 변경한다 |
    | getId() | 스레드의 ID를 반환한다 |
    | getState() | 스레드의 상태를 반환한다 |
    | stop() | 스레드가 살아있는지 테스트한다 |
    | isDeamon() | 스레드가 데몬 스레드인지 테스트한다 |
    | interrupt() | 스레드를 중단한다 |
- Thread.sleep() 시 try-catch문이나 throws로 예외 처리를 해주는 이유
    
    `Thread.sleep()`을 호출하면 주어진 시간 동안 스레드는 일시정지 상태가 되고 시간이 지나면 다시 실행 대기 상태로 돌아간다. 일시정지 상태에서 주어진 시간이 되기 전 `interrupt()`가 호출되면 `InterruptedException`이 발생하기 때문에 예외 처리를 해주는 것이다!

<br>

### Thread의 메소드 더 잘 이해하기!

- `sleep()` : 주어진 시간 동안 일시정지한다
    
    실행 중인 스레드를 일정 시간 멈추게 하고 싶을 때 사용한다. `Thread.sleep()` 메소드를 호출한 스레드는 주어진 시간 동안 일시정지 상태가 되고, 시간이 지나면 다시 실행 대기 상태로 돌아간다.
    
- `yield()` : 다른 스레드에게 실행을 양보한다
    
    스레드는 반복적인 실행을 위해 반복문을 포함하는 경우가 많다. 이 반복문이 무의미한 반복을 하는 경우 다른 스레드에게 실행을 양보하고 자신은 실행 대기 상태로 가는 것이 전체 프로그램 성능이 도움이 된다. `yield()`를 호출한 스레드는 실행 대기 상태로 돌아가고 높거나 같은 우선순위를 가진 다른 스레드가 실행 기회를 가질 수 있도록 한다.
    
- `join()` : 다른 스레드의 종료를 기다린다
    
    보통 스레드는 다른 스레드와 독립적으로 실행하지만, 가끔 다른 스레드가 종료될 때까지 기다렸다가 실행해야 하는 경우가 있다. 만약 메인 스레드에서 `sumThread.join()`을 호출하면 메인 스레드는 sumThread가 종료될 때까지 일시정지된다.
    
- `wait()`, `notify()`, `notifyAll()` : 스레드 간 협업을 진행한다
    
    경우에 따라서 두 개의 스레드를 교대로 번갈아가며 실행해야 하는 경우가 있다. 자신의 작업이 끝나면 상대방 스레드를 일시정지 상태에서 풀어주고 자신을 일시정지 상태로 만든다. 한 스레드가 작업을 완료하면 `notify()` 메소드를 호출하여 일시정지 상태에 있는 다른 스레드를 실행 대기 상태로 만들고, 자신은 `wait()`을 호출하여 일시정지 상태로 만든다.
    
- `interrupt()` : 스레드를 안전하게 종료한다
    
    스레드는 자신의 `run()` 메소드가 모두 실행되면 자동으로 종료된다. 하지만 경우에 따라서 실행 중인 스레드를 즉시 종료해야 할 때가 있다. `interrupt()`를 사용하면 스레드를 정상 종료시킬 수 있다.

<br>

### Thread의 수명 주기

> 스레드의 탄생부터 소멸까지의 상태 변화

![Thread의 수명 주기](https://static.javatpoint.com/core/images/life-cycle-of-a-thread.png)

1. NEW : 스래드의 실행 준비가 완료된 상태
2. RUNNABLE : 스레드가 실행 가능한 상태
    
    스레드가 대기열에서 실행을 기다리고 있음을 의미한다. `start()`를 호출하면 실행 가능한 상태가 된다. Runnable 상태에 있는 스레드가 스레드 스케쥴링으로 CPU를 점유하고 `run()`을 실행하게 되면 RUNNING 상태가 된다.
    
3. BLOCKED : 스레드가 차단되어 있는 상태
4. WAITING : 스레드가 대기 중인 상태
    
    다른 스레드가 작업을 완료하기를 기다리고 있는 상태이다.
    
5. TIMED_WAITING : 스레드가 정해진 시간 동안 대기하는 상태
    
    WAITING과 달리 정해진 시간 동안 대기를 진행한다.
    
6. TERMINATED : 스레드가 종료되거나 죽은 상태
    
    `run()` 함수가 종료되거나 `stop()`을 호출하면 스레드가 종료된다. 오류, 예외 등과 같이 비정상적인 이벤트로 스레드가 종료되는 경우 비정상 종료라고 한다. 종료된 스레드는 더 이상 사용할 수 없다.

<br>

### Thread 생성

> 사용자가 스레드 객체를 생성하고 실행 요청을 하더라도 스레드의 실행은 JVM에 의한 스케줄러를 따른다

- java.lang.Thread를 상속받는 방법
    1. Thread 클래스를 상속한 클래스를 정의한다
    2. `run()`을 override하여 실행할 코드를 작성한다
    3. 스레드 객체를 생성한다
    4. `start()`로 스레드를 시작한다
    
    ```java
    public class MyThread extends Thread {
        public void run() {
            System.out.println("RUN");
        }

        public static void main(String[] args) {
            MyThread thread = new MyThread();
            thread.start();
        }
    }
    ```
    
- Runnable 인터페이스를 구현하는 방법
    1. Runnable 인터페이스를 구현하는 클래스를 정의한다
    2. `run()`을 override하여 실행할 코드를 작성한다
    3. Runnable 객체를 생성한다
    4. Thread 객체를 생성한다
    5. `start()`로 스레드를 시작한다
    
    ```java
    public class MyThread implements Runnable {
        public void run() {
            System.out.println("RUN");
        }

        public static void main(String[] args) {
            Thread thread = new Thread(new MyThread());
            thread.start();
        }
    }
    ```

<br>

### Thread 사용 예제

- Thread 클래스 정의
    
    ```java
    public class MyThread extends Thread {
        public MyThread(String string) {
            super(string);
        }
    
        public void run() {
            int count = 0;
            while (!this.isInterrupted()) {
                System.out.print(this.getName());
                HelloWorld.threadSleep(this, 500);
    
                count++;
                if (count == 20) {
                    this.interrupt();
                    System.out.printf("%n[5]." + this.toString() + "-인터럽트됨]");
                }
            }
        }
    }
    ```
    
- Thread 객체 생성 및 실행
    
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            MyThread mt1 = new MyThread("*");		
            MyThread mt2 = new MyThread("#");		
            mt1.start();		
            mt2.start();
            
            System.out.printf("%n[1].mt1:" + mt1.isInterrupted() + ", mt2:" + mt2.isInterrupted() + "]");
            
            threadSleep(Thread.currentThread(), 2000);
            mt1.interrupt();
            System.out.printf("%n[2].mt1:" + mt1.isInterrupted() + ", mt2:" + mt2.isInterrupted() + "]");
            
            threadJoin(mt2);
            System.out.printf("%n[3].mt1:" + mt1.isInterrupted() + ", mt2:" + mt2.isInterrupted() + "]");
        }
        
        static void threadSleep(Thread t, long time) {
            try {
                Thread.sleep(time);
            } catch (InterruptedException e) {
                System.out.printf("%n[4]." + t.toString() + "-인터럽트됨]");
                t.interrupt();
            }
        }
        static void threadJoin(Thread t) {
            try {
                t.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    ```
    
- 실행 결과
    
    ```java
    [1].mt1:false, mt2:false]#**#*##*
    [2].mt1:true, mt2:false]
    [4].Thread[*,5,main]-인터럽트됨]################
    [5].Thread[#,5,main]-인터럽트됨]
    [3].mt1:true, mt2:true]
    ```

<br><br>

# Multi-Thread

### Multi-Thread

- Multi Thread : 여러 스레드가 동시에 수행되면서 공유가 가능하다
    1. 몇 개의 작업을 병렬로 실행할지 결정하고
    2. 각 작업별로 스레드를 생성한다
        
        Main Thread는 기본적으로 존재하기 때문에 메인 작업을 제외하고 추가적인 작업의 수만큼 스레드를 생성하면 된다

<be> 

### JVM의 스케쥴링 규칙

1. 우선순위 (Priority)
    
    우선순위가 높은 스레드를 우선적으로 실행한다. 개발자가 직접 스레드 객체에 우선순위를 부여할 수 있다.
    
2. 순환 할당 (Round-Robin)
    
    시간 할당량(Time Slice)를 정해서 하나의 스레드를 정해진 시간만큼 실행하고 다시 다른 스레드를 실행한다. 우선순위가 같은 경우 이 방식을 따른다. JVM에 의해 결정되기 때문에 개발자가 제어할 수 없다.

<br>

### 동기화 메소드 & 동기화 블록

> 싱글 스레드 프로그램은 한 개의 스레드가 객체를 독차지해서 사용하면 된다

- 멀티 스레드 프로그램은 스레드들이 객체를 공유해서 작업해야 하는 경우가 있다
    
    - 이 경우, 스레드 A가 사용하던 객체가 스레드 B에 의해 상태가 변경될 수 있기 때문에 A가 의도한 결과와 다른 결과를 산출할 수 있다
    - 스레드 작업이 끝날 때까지 객체에 잠금을 걸어서 다른 스레드가 사용할 수 없도록 해준다
    
- 임계영역 : 하나의 스레드만 실행할 수 있는 코드 영역
    
    - Java는 임계영역 지정을 위해 동기화 메소드와 블록을 제공한다
    - 동기화 메소드 혹은 블록을 실행하는 즉시 객체에 잠금이 일어나고, 종료되면 잠금이 풀린다
    
    ```java
    public synchronized void method(){
        // 임계영역 : 단 하나의 스레드만 실행!
    }
    ```
    
    ```java
    public void method(){
        synchronized(공유객체){
            // 임계 영역 (단 하나의 스레드만 실행 !)
        }
    }
    ```

<br>   

### 교착상태 (DeadLock)

- DeadLock : 두 개의 스레드에서 서로가 가지고 있는 락이 해제되기를 기다리는 상태
    
    - 교착상태(DeadLock)이 되면 어떤 작업도 실행하지 못하고 서로 상대방의 작업이 끝나기를 기다리는 무한 대기 상태가 된다
    
- DeadLock 발생 조건
    
    > 아래 4가지 조건을 모두 충족할 경우 데드락이 발생한다
    
    - 상호 배제 (Mutual Exclusion) : 한 자원에 대해 여러 스레드가 동시에 접근할 수 없을 때
    - 점유와 대기 (Hold and Wait) : 자원을 가지고 있는 상태에서 다른 스레드가 사용하고 있는 자원 반납을 기다릴 때
    - 비선점 (Non Preemptive) : 다른 스레드의 자원을 실행 중간에 강제로 가져올 수 없을 때
    - 환형 대기 (Circle Wait) : 각 스레드가 순환적으로 다음 스레드가 요구하는 자원을 가지고 있을 때

<br>

### Thread Pool

- Pool : 필요할 때마다 개체를 할당하고 파괴하는 대신, 사용 준비된 상태로 초기화된 개체 집합
- Thread Pool : 스레드 제어 문제를 해결할 수 있는 방법
    
    - 매번 생성 및 수거 요청이 올 때마다 스레드를 생성하고 수거하는 것이 아닌 스레드 사용자가 설정해둔 개수만큼 미리 생성해두는 방식이다
    - 비용적인 측면이나 Context Switch가 발생하는 상황에서 딜레이를 줄일 수 있다
    - 다만, 스레드 풀에 너무 많은 양의 스레드를 만들어두면 메모리 낭비가 심해질 수 있다
    
- Thread Pool의 동작 방식
    1. 병렬 작업 형태로 동시 코드를 작성한다
    2. 실행을 위해 스레드 풀의 인스턴스에 제출한다
    3. 제출한 인스턴스에서 실행하기 위해 재사용되는 여러 스레드를 제어한다

<br><br>

# 참고 자료

[Thread in Java [Complete Guide]](https://www.simplilearn.com/tutorials/java-tutorial/thread-in-java)<br>
[Java Threads - GeeksforGeeks](https://www.geeksforgeeks.org/java-threads/)<br>
[Creating a thread in Java - javatpoint](https://www.javatpoint.com/how-to-create-a-thread-in-java)<br>
[[Java] 자바 - Thread란? 스레드 개념 및 사용방법](https://kadosholy.tistory.com/121)<br>
[자바(Java)의 기초 박살내기 - 스레드(Thread)](https://raccoonjy.tistory.com/15)<br>
[[Java] Thread 란? (Thread 총 정리)](https://myeongdev.tistory.com/74)<br>
[[Java] 멀티 스레드](https://velog.io/@sezzzini/Java-멀티-스레드)<br>
[[Java] 자바 쓰레드 교착상태(deadlock)](https://math-coding.tistory.com/175)<br>
[JAVA 쓰레드란(Thread) ? - JAVA에서 멀티쓰레드 사용하기](https://honbabzone.com/java/java-thread/)