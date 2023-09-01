# Conditionals

**Conditionals**

- 조건

    \- 조건을 검사하기 위해서 boolean 변수를 사용한다
    
    \- 만약 boolean값이 true라면 조건문을 실행하고, false면 실행하지 않는다
    
- Boolean operators
    1. Less than: a < b.

    2. Less than or equal to: a <= b.

    3. Greater than: a > b.

    4. Greater than or equal to: a >= b.

    5. Equal to a == b.

    6. Not Equal to: a != b.

<br><br>

# Conditional Statement (조건문)

> 조건문 : 조건에 따라 실행될 수 있는 코드 분기, 조건에 따라 실행 흐름을 제어할 수 있다


### if~else문

- if~else문 : 조건에 따라 두 경우 중 하나가 수행되는 조건문
    
    \- if문은 조건식의 내용에 따라 true 혹은 false를 반환한다
    
    \- if문은 조건식이 true일 경우에 실행, else문은 조건식이 false일 경우에 실행된다
    
    \- else문은 필요하지 않은 경우에 생략할 수 있다
    
- if~else문 쓸 때 참고 (이건 내가 예전에 개인적으로 알아본 건데 자료를 못 찾겠도다)
    
    \- if문을 단독으로 사용할 때는 조건문에 {  }를 붙이지 않아도 된다
    
    \- 그 외의 경우에는 {  }를 붙이는 게 안전하다고 한다
    
    ```java
    if(5 < 6) result = 5;  // 가능
    
    if(5 < 6) result = 5;  // 불가능
    else result = 6; 
    ```
    
- 활용
    
    ```java
    if (조건) {
        실행 문장 1;
    } else {
        실행 문장 2;
    }
    ```

<br>

### if~else if문

- if~else if문 : 다중 조건에 따라 여러 경우 중 하나가 수행되는 조건문
    
    \- 조건은 위에서 아래로 순차적으로 검사를 진행한다
    
    \- 예를 들어 위에서 조건식이 참으로 평가되면, 해당 경우를 수행한 후 조건문을 빠져나가게 된다
    
    \- 즉, 위에서 조건식이 참이면 아래에 참인 조건이 있다고 해도 실행되지 않는다
    
    \- 좁은 조건에서 넓은 조건으로 넓혀나가야 조건문을 제대로 활용할 수 있다
    
- 활용
    
    ```java
    if(조건 1)
        실행 문장 1;
    else if(조건 2)
        실행 문장 2;
    ...
    else
        실행 문장 3;
    ```

<br>

### Switch문

- Switch문 : 다중 선택이 가능한 조건문
    
    \- 각 case에 따른 실행이 가능하다
    
    \- break를 만나거나 마지막 case문, 혹은 default문에 도달할 때까지 계속 실행된다
    
    \- 만약 break를 생략하면 실행이 바로 밑에 있는 case문으로 넘어가게 된다
    
    \- 이 점을 활용해서 여러 개의 case를 하나의 시행문으로 지정할 수 있다
    
- 활용
    
    ```java
    switch(수식) {
        case 값 1:
            실행 문장 1;
           break;
        case 값2:
             실행 문장 2;
            break;
      .....
        case 값 n:
            실행 문장 n;
            break;
        defulat:
            디폴트 실행 문장;
    }
    ```
    
- 다중 선택 활용
    
    ```java
    int month = 3;
    
    String season = null;
    
    switch (month) {
    case 1:
    case 2:
    case 12:
        season = "winter";
        break;
    case 3:
    case 4:
    case 5:
        season = "spring";
        break;
    case 6:
    case 7:
    case 8:
        season = "summer";
        break;
    case 9:
    case 10:
    case 11:
        season = "autumn";
        break;
    default:
        break;
    }
    ```

<br>

### 삼항 연산자

- 삼항 연산자 : 조건 검사 결과에 따라 값을 반환하는 연산자
    
    \- 짧고 단순한 코드로 if~else문을 대체할 수 있다
    
    \- `(조건) ? (참일 때 리턴값) : (거짓일 때 리턴값);`
    
- 활용
    
    ```java
    result = (a == 1) ? 'T' : 'F';  // a가 1이면 T를, 1이 아니면 F를 반환
    ```

<br><br>

# 참고 자료

[Java If ... Else](https://www.w3schools.com/java/java_conditions.asp)<br>
[Java 제어문(Control statement)의 조건문(Conditional statement)](https://www.devkuma.com/docs/java/conditional-statement/)<br>
[Conditionals - Learn Java - Free     Interactive Java Tutorial](https://www.learnjavaonline.org/en/Conditionals)<br>
[How To Write Conditional Statements in Java  | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-write-conditional-statements-in-java)<br>
[Java | Conditionals | Codecademy](https://www.codecademy.com/resources/docs/java/conditionals)<br>
[Coding Ninjas Studio](https://www.codingninjas.com/studio/library/what-are-conditional-statements-in-java)