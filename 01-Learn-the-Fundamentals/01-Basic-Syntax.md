# Java Object

### 객체

- Object (객체) : State와 Behavior을 가지는 프로그램 단위

    \- 클래스로부터 생성된다

    \- State(속성)은 필드를 의미, Behavior(기능)은 메소드를 의미한다
- Class : 객체를 만들기 위한 설계도

    \- 객체를 생성하기 위한 필드와 메소드가 정의되어 있다

    \-클래서에서 만들어진 객체를 해당 클래스의 Instance라고 한다
    - Class의 구성
        - Field : 객체의 데이터가 저장되는 곳
            
            \- `int number;`

            \- 객체의 고유 데이터, 부품 객체, 상태 정보를 저장하는 곳이다

            \- 변수와 헷갈릴 수 있지만 변수가 아니다
            
            | Field (필드) | Variable (변수) |
            | --- | --- |
            | ∙ 생성자와 메소드 전체에서 사용된다<br>∙ 객체가 소멸되지 않는 한 객체와 함께 존재한다 | ∙ 생성자와 메소드 내에서 생성되고 사용된다<br>∙ 생성자와 메소드가 실행 종료되면 자동으로 소멸된다 |
        - Constructor : 객체 생성할 때 초기화를 진행하는 곳
            
            \- `ClassName() { … }`
            
            \- 메소드와 비슷하게 생겼지만, 클래스 이름으로 되어 있고 리턴 타입이 존재하지 않는다
            
        - Method : 객체의 동작에 해당하는 실행 블록
            
            \- `void methodName() { … }`

            \- 메소드를 호출하면 중괄호 블록 안에 있는 모든 코드들이 일괄적으로 실행된다

            \- 필드를 읽고 수정하며, 객체 간의 데이터를 전달하는 수단이다
            
    - 객체 지향 프로그래밍 개발
        1. 클래스를 만든다

        2. 설계된 클래스를 이용해서 객체를 생성한다

        3. 생성된 객체를 이용한다

- Instance : 클래스로부터 만들어진 객체
    
    \- 클래스를 바탕으로 실체화되어 메모리에 할당된 것이다
    
    \- 하나의 클래스로부터 여러 개의 인스턴스를 만들 수 있다
    
    \- 인스턴스가 객체에 포함된다

<br><br>

# 기본 문법

### Java Code Template

```java
package <package-path>;

public class <class-name> {
    public static void main(String[] args) {
        // 코드
    }		
}
```

<br>

### Java 기본 문법

1. 대소문자를 구분한다
2. 모든 Class 이름의 첫 글자는 대문자여야 한다
    
    ex) MyFirstJava, Dog
    
3. 모든 Method 이름의 첫 글자는 소문자여야 한다
    
    ex) myMethod(), getUser()
    
4. 파일 이름은 Class 이름과 정확히 일치해야 하며, 이름 끝에 .java를 추가해야 한다
    
    Public Class가 아닌 경우에는 이름이 달라도 된다
    
5. Java의 프로그램 처리는 모든 Java 프로그램의 필수 부분인 main()에서 시작한다
    
    ```java
    public static void main(String[] args) {
    
    }
    ```

<br>

### Identifier & Modifier

- Identifier (식별자) : 클래스, 변수, 메소드에 사용되는 이름
    
    \- 모든 식별자는 알파벳(A~Z, a~z) 또는 $, _로 시작해야 한다
    
    \- 자바 키워드는 식별자로 사용될 수 없다
    
    \- 대소문자를 구분한다
    
- Modifier (수정자) : 클래스와 메소드의 범위를 제어함
    - Access Modifier : 필드, 메소드, 생성자 또는 클래스의 접근성이나 법위를 지정
        
        | Modifier | 설명 |
        | --- | --- |
        | Default | ・ 패키지 내에서만 접근이 가능하다<br>・ 엑세스 수준을 지정하지 않으면 기본값이 된다 |
        | Public | ・ 모든 곳에서 접근이 가능하다 |
        | Protected | ・ 패키지 내에서만 접근이 가능하다<br>・ SubClass를 통해 패키지 외부에서 접근할 수 있다 |
        | Private | ・ 정의한 클래스 내에서만 접근이 가능하다 |

        | Access Modifier | Class | Package | Package 밖의 Subclass | Package |
        | --- | --- | --- | --- | --- |
        | Default | O | X | X | X |
        | Public | O | O | X | X |
        | Protected | O | O | O | X |
        | Private | O | O | O | O |
            
    - Non-access Modifier
        
        | Modifier | 설명 |
        | --- | --- |
        | Final | 수정할 수 없는 메소드, 변수, 클래스가 된다 |
        | Abstract | 클래스에 붙으면 추상 메소드가 선언되어 있다는 것을 의미, 메소드 앞에 붙으면 추상 메소드라는 것을 의미한다 |
        | Static | 모든 인스턴스에서 공통으로 사용하는 변수가 된다 |

- Variable (변수) : 프로그램이 실행되는 동안 값을 보관하는 용기
    
    \- 값을 보관하는 용기이자 메모리 위치의 이름이다
    
    | Varaiable | 설명 |
    | --- | --- |
    | Local Variable | ・ 메소드 내부에 선언된 변수이다.<br>・ 지역 변수는 해당 메소드 내에서만 사용할 수 있다 |  |
    |  Static Variable | ・ static 키워드로 선언된 변수이다<br>・ 단일 복사본을 생성하고, 같은 클래스의 모든 인스턴스 간에 공유된다 
    | Instance Variable | ・ 클래스에서 선언된 변수이다<br>・ 생성된 객체마다 값이 다르며, 각 객체 간에 공유되지 않는다

<br>

### 자바 키워드

> Java 예약어는 상수, 변수, 또는 기타 식별자 이름으로 사용할 수 없다

| 예약어 | 예약어 | 예약어 | 예약어 |
| --- | --- | --- | --- |
| abstract | assert | boolean | break |
| byte | case | catch | char |
| class | const | continue | default |
| do | double | else | enum |
| extends | fnal | finally | float |
| for | goto | if | implements |
| import | instanceof | int | interface |
| long | native | new | package |
| private | protected | public | return |
| short | static | strictfp | super |
| switch | synchronized | this | throw |
| throws | transient | try | void |
| volatile | while |  |  |

<br><br>

# 주석

### 주석

- 한 줄 주석
    
    ```java
    // 한 줄 주석 1
    /* 한 줄 주석 2 */
    ```
    
- 여러 줄 주석
    
    ```java
    /*
     * 여러 줄 주석
     */
    ```

<br><br>

# 참고 자료

[Java - Basic Syntax](https://www.tutorialspoint.com/java/java_basic_syntax.htm#)<br>
[Java Basic Syntax - GeeksforGeeks](https://www.geeksforgeeks.org/java-basic-syntax/)<br>
[Java Syntax](https://www.w3schools.com/java/java_syntax.asp)<br>
[[Java] Java Basic Syntax | 자바 기초 문법](https://dad-rock.tistory.com/1052)<br>
[[Java] 도대체 객체가 뭔데? : 객체, 클래스, 인스턴스](https://upcake.tistory.com/418)<br>
[Access modifiers in java - Javatpoint](https://www.javatpoint.com/access-modifiers)<br>