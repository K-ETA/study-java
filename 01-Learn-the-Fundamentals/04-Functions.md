# Functions

### Function (함수)

- Function (함수) : 하나의 기능을 수행하는 일련의 코드
    
    \- 필요한 곳에서 함수를 호출하여 사용한다
    
    \- 한 번 생성되면 계속해서 사용할 수 있기 때문에 재사용 가능하다
    
    \- 기능이 분리되어 작성되기 때문에 가독성이 좋고 유지보수에 도움이 된다
    
    \- 클래스 내부에 함수가 있어야 한다
    
    - 내장 함수 : Java에서 정의한 함수
        
        \- 원할 때 언제든지 사용할 수 있다
        
        \- ex) min(), length()
        
    - 사용자 정의 함수 : 특정 작업을 수행하기 위해 프로그래머가 정의하거나 생성하는 함수
- 함수 != 메소드
    
    \- 함수는 호출되면 메모리 스택에 저장되며, 동작이 끝나면 메모리에서 사라진다
    
    \- 메소드는 위에서 생성한 객체의 기능을 구현하기 위해 클래스 내부에 구현되는 함수이다
    
    \- 메소드를 구현함으로 인해 객체의 기능을 하게 된다
    
<br>

### 함수의 구조

- 함수의 구조
    
    \- 함수 이름, 매개변수, 리턴값, 함수 몸체로 구성된다
    
    \- 매개변수와 리턴값은 경우에 따라 생략이 가능하다
    
    - 함수의 이름
        
        \- 함수의 이름은 클라리언트에 맞게 짓는 게 좋다
        
        \- 예를 들어 getName()을 서버 입장에서 생각해보면 sendName()이 될 수 있는데, send보다는 get을 사용하는 게 좋다고 한다
        
- 함수의 인수 전달
    
    > 추가로 알아본 결과에 의하면, 형식 인수는 매개변수(Parameter), 실제인수는 인수(Argument)라고 한다
    
    \- 형식 인수 : 함수의 () 안에 사용되는 인수 또는 매개변수
    
    \- 실제 인수 : 함수에 입력을 제공할 때 사용되는 인수 또는 매개변수
    
    ```java
    public static int myFunction(int x) {  // 여기의 x는 형식 인수
        // 내용
    }
    
    public static void main(String[] args) {  
        int x = 1;
        myFunction(x);  // 여기의 x는 실제 인수
    }
    ```
    
    - Call by value : 변수 값이 함수의 형식 인수에 전달된다
        
        \- 실제 인수의 값은 형식 인수 값을 변경해도 영향을 받지 않는다
        
        \- Java는 C와 달리 Pass by reference 혹은 Call by reference를 지원하지 않는다
        
        [Java의 Call by value, 메모리를 잘 정리해둔 거 같아서 가지고 온 블로그](https://bcp0109.tistory.com/360)
        
- 리턴값
    
    \- void : 리턴값이 없는 경우에 사용
    
    \- 그 외 : 리턴값이 있는 경우에는 해당 리턴값의 데이터 타입을 작성한다
    
    ⇒ int, float, double, char, String 등 모두 가능
    
<br><br>

# 참고 자료

[Functions - Learn Java - Free     Interactive Java Tutorial](https://www.learnjavaonline.org/en/Functions)<br>
[[JAVA] 함수(Function), 메서드(Method), 인스턴스(Instance) 개념 및 구현](https://peemangit.tistory.com/389)<br>
[Function in Java Programming | Dremendo](https://www.dremendo.com/java-programming-tutorial/java-function)<br>
[Java Methods](https://www.w3schools.com/java/java_methods.asp)<br>
[[Java] 클래스와 객체 - 함수와 메서드](https://velog.io/@foeverna/Java-클래스와-객체-함수와-메서드)<br>
[[Java] 매개변수(Parameter)와 인수(Argument)](https://hyeonic.tistory.com/215)<br>
[[ JAVA ] 헷갈리는 용어! 매개변수,인자(parameter)와 인수(argument)](https://dev-cini.tistory.com/56)<br>
[[JAVA] 메소드(Method), 리턴(return)](https://jong99.tistory.com/77)