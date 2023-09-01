# Loops (반복문)

> 반복문은 일부 조건이 true로 평가되는 동안 일련의 명령문을 반복적으로 실행하는 것이다

### For문

- For문 : 프로그램의 일부를 여러 번 반복하는 반복문
    
    ![For문 동작 흐름](https://media.geeksforgeeks.org/wp-content/uploads/loop2.png)
    
    \- 한 줄에서 초기화, 조건 및 증가/감소를 사용하기 때문에 짧고 간편하게 반복문을 사용할 수 있다
    
    \- 코드를 반복하려는 횟수를 정확히 알고 있는 경우에 사용하면 좋다
    
    ```java
    for(초기값; 실행 조건; 증감) {
        // 명령문
    }
    ```
    
- for-each문 : 배열 혹은 Collection을 순회하는 데 사용하는 반복문
    
    \- 값을 초기화하거나 증가시키는 과정이 필요없기 때문에 for문보다 사용이 간편하다
    
    \- 인덱스가 아닌 요소를 기반으로 작동한다
    
    ```java
    for(Data Type 변수명 : 배열 이름) {
        // 명령문
    }
    ```

<br>    

### While문

- While문 : 주어진 boolean 조건에 따라 코드가 반복적으로 실행될 수 있도록 하는 반복문
    
    ![While문 동작 흐름](https://media.geeksforgeeks.org/wp-content/uploads/Loop1.png)
    
    \- 반복 횟수가 정해지지 않은 경우에 사용하면 좋다
    
    \- while문은 조건을 검사하면서 시작되기 때문에 진입 제어 루프라고 불리기도 한다
    
    \- 조건이 false가 되면 반복문이 종료된다
    
    ```java
    while(조건) {
        // 명령문
        // 다음 반복을 위한 업데이트 값이 주로 포함
    }
    ```
    
- do-while문 : 명령문을 먼저 한 번 실행한 후 조건을 확인하는 while문
    
    ![do-while문 동작 흐름](https://media.geeksforgeeks.org/wp-content/uploads/loop3.png)
    
    \- 반복 횟수가 정해져 있지 않지만, 루프를 무조건 한 번 이상 실행해야 하는 경우에 사용하면 좋다
    
    \- 명령문을 먼저 실행한다는 점을 제외하면 while문과 유사하다
    
    \- 명령문을 처음 실행할 때는 아무 조건도 검사하지 않는다

<br>

### Break와 Continue

- Break : 명령문을 빠져나오고 싶을 때 사용
    
    ```java
    for (int i = 0; i < 10; i++) {
        if (i == 4) {  // i가 4일 때 반복문을 빠져나옴
            break;
        }
    }
    ```
    
- Continue : 반복문의 한 반복을 중단하고 다음 반복으로 넘어가고 싶을 때 사용
    
    ```java
    for (int i = 0; i < 10; i++) {
        if (i == 4) {  // i가 4일 때는 건너뛰고 바로 5로 넘어감
            continue;
        }
    }
    ```

<br>

### 반복문의 활용

- 중첩 반복문 : 루프를 다른 루프 안에 배치하는 것
    
    \- 내부 반복문은 외부 반복문이 반복될 때마다 한 번씩 실행된다
    
    \- 다양한 종류의 반복문을 중첩으로 사용할 수 있다
    
    ```java
    for(int i = 0; i < 10; i++) {
        for(int j = 0; j < 10; j++) {
                // 명령문
        }
    }
    ```
    
- 반복문의 label
    
    \- Label : 반복문의 이름을 나타내는 변수 이름
    
    \- 요구 사항에 따라 특정 루프를 break하거나 continue할 때 유용하게 사용할 수 있다
    
    \- ex) 내부 for문에서 외부 for문을 break하고 싶을 때
    
    ```java
    반복문 이름:    
    for (초기화; 조건; 증감) {    
    		//루프의 기능    
    }
    ```

<br> 

### 무한 루프

> 반복문을 사용할 때는 무한 루프에 빠지지 않도록 주의해야 한다
- 무한 for문
    
    ```java
    for(;;) {
        // 명령문
    }
    ```
    
- 무한 while문
    
    ```java
    while(true) {
        // 명령문
    }
    ```

<br><br>

# 참고 자료

[Java For Loop](https://www.w3schools.com/java/java_for_loop.asp)<br>
[Loops in Java - GeeksforGeeks](https://www.geeksforgeeks.org/loops-in-java/)<br>
[Loops in Java | Java For Loop (Syntax, Program, Example) - Javatpoint](https://www.javatpoint.com/java-for-loop)<br>
[Labeled Loop in Java - Javatpoint](https://www.javatpoint.com/labeled-loop-in-java)<br>
[Java Break and Continue](https://www.w3schools.com/java/java_break.asp)