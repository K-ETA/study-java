# DataTypes

![Untitled](https://scaler.com/topics/images/types-of-non-primitive-data-types-in-java.webp)

<br>

### Primitive Data Types

> 사용자가 정의하지 않는 기본 데이터 유형<br>
> 변수값의 크기와 종류가 지정되며, 추가적인 메소드는 존재하지 않는다

| Data Type | 기본값 | 범위 | 기본 크기 | 예시 |
| --- | --- | --- | --- | --- |
| boolean | false | true/false | 1 bit | boolean b = true |
| char | ‘\u0000’ | ‘\u0000’ ~ ‘\uffff’ | 2 bytes | char c = ‘A’ |
| byte | 0 | -128 ~ 127 | 1 byte | byte  b = 12 |
| short | 0 | -32,768 ~ 32,767 | 2 bytes | short s = 1000 |
| int | 0 | -2,147,483,648 ~ 2,147,483,647 | 2 bytes | int i = 100000000 |
| long | 0L | 9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 | 8 bytes | long l = 1000000L |
| float | 0.0f | 32 bit floating point | 4 bytes | float f = 25.9f |
| double | 0.0d | 64 bit floating point | 8 bytes | double d = 152.3 |

<br>

### Non-primitive Data Types

> 사용자가 정의하는 사용자 정의 데이터 유형<br>
> 데이터를 저장하는 메모리 위치를 참조하기 때문에 참조 변수 혹은 객체 참조로 불리기도 한다<br>
> Primitive Data Type과 다르게 특정 작업을 위한 추가적인 메소드가 존재한다
- Class : 객체를 생성하는 데 사용되는 사용자 정의 데이터 유형
    
    \- 해당 클래스의 모든 객체에 사용되는 공통 필드와 메소드 집합이 포함되어 있다
    
- String : 문자열
    
    \- char[]과 다르게 단일 변수에 일련의 문자를 보유할 수 있다
    
    \- java.lang.String이 따로 존재하다 → 이번에 처음 알았음
    
    ```java
    String name = "떠누";
    ```
    
- Array : 동일한 데이터 유형의 요소를 연속적인 방식으로 저장하는 데 사용되는 데이터 유형
    
    \- 사용자가 직접 배열을 선언하고 초기화해야 한다
    
    \- 배열은 무조건 인덱스가 0부터 시작한다
    
    \- 배열의 크기는 무조건 정수(int)값으로 지정해야 한다
    
    \- 자바의 모든 배열은 동적으로 할당된다
    
    ```java
    int[] arr = new int[5];  // 선언만 하는 방식
    int arr[] = {1,2,3,4,5};  // 선언과 동시에 초기화하는 방식
    ```
    
- Interface : 추상화를 진행하는 도구
    
    \- Abstract method, Default & Static method, Private method를 포함할 수 있다
    
    \- 클래스가 인터페이스를 구현하는 경우, 해당 인터페이스의 모든 추상 메소드를 구현해야 한다
    
    \- 그렇지 않으면, 해당 클래스를 추상 클래스로 선언해야 한다
    
    \- 즉 인터페이스는 클래스가 구현해야 하는 메소드의 집합이다
    
    ```java
    interface Operations {
        void mult();
        void div();
    }
    
    class Solve implements Operations {
        int a = 10, b = 20, c;
    
        public void mult() {
            int c = a * b;
            System.out.println("Multiplication of numbers: " + c);
        }
    
        public void div() {
            int c = b / a;
            System.out.println("Division of numbers: " + c);
        }
    }
    ```

<br>

### Primitive Data Type VS Non-primitive Data Type

| Primitive Data Type | Non-primitive Data type |
| --- | --- |
| ・ 시스템에 미리 정의되어 있다<br>・ 변수에 한 번에 하나의 값만 저장할 수 있다<br>・ 스택에 데이터를 저장한다<br>・ Data Type 이름이 소문자로 시작한다<br>・ null 값이 불가능하다 | ・ 사용자 정의로 쉽게 생성하고 수정할 수 있다<br>・ 동일한 데이터 유형 또는 다른 데이터 유형의 여러 값을 하나의 변수에 저장할 수 있다<br>・ 스택에 힙 메모리의 객체에 대한 참조를 저장한다<br>・ Data Type 이름이 대문자로 시작한다<br>・ null 값이 가능하다 |

<br><br>

# Variables

### 변수 (Variable)

- Variable (변수) : 데이터가 저장되는 메모리 위치의 이름
    
    \- 메모리 주소가 변경될 수 없는 경우는 상수, 변경될 수 있으면 변수라고 한다
    
    \- 변수가 데이터와 함께 저장되면 메모리에 공간이 할당된다
    
    \- 숫자, 문자, 밑줄 문자의 조합을 사용하여 변수를 정의할 수 있다
    
- 변수의 종류
    | Variable | 설명 | 추가 설명 |
    | --- | --- | --- |
    | Local Variable | ・ 메소드 내부에 선언된 변수이다.<br>・ 지역 변수는 해당 메소드 내에서만 사용할 수 있다 |  |
    |  Static Variable | ・ static 키워드로 선언된 변수이다<br>・ 단일 복사본을 생성하고, 같은 클래스의 모든 인스턴스 간에 공유된다 | Static Variable |
    | Instance Variable | ・ 클래스에서 선언된 변수이다<br>・ 생성된 객체마다 값이 다르며, 각 객체 간에 공유되지 않는다 | Non-static Variable |
- 변수 이름 생성 규칙
    1. 변수의 이름은 영문자, 숫자, _, $로만 이름을 구성할 수 있다

    2. 변수의 이름은 숫자로 시작할 수 없다

    3. 변수의 이름 사이에는 공백을 포함할 수 없다

    4. 변수의 이름으로 자바 예약어(키워드)는 사용할 수 없다

<br>

### 변수 선언 방법

1. 초기화를 진행하지 않고 변수를 선언하는 방법
    
    먼저 변수를 선언하여 메모리 공간을 할당받고, 나중에 변수를 초기화하는 방법이다. 이렇게 선언된 변수는 초기화되지 않았기 때문에 해당 메모리 공간에는 쓰레기값이 들어가 있다. 이후에 변수를 사용하기 위해서는 반드시 초기화를 진행해야 한다.
    
    ```java
    int num;
    String name;
    ```
    
2. 변수의 선언과 함께 초기화를 진행하는 방법
    
    변수의 선언과 동시에 값을 초기화하는 방법이다. 선언하고자 하는 변수의 타입이 같다면 동시에 선언할 수 있다. 하지만 이미 선언된 변수를 동시에 초기화하는 것은 불가능하다.
    
    ```java
    int num = 8, age = 10;
    String name = "joeun";
    ```

<br><br>

# 참고 자료

[Basic Datatypes and Variables in Java - Java Tutorial | Intellipaat.com](https://intellipaat.com/blog/tutorial/java-tutorial/data-types-in-java/)<br>
[Variable Types and Data types in Java](https://www.stechies.com/variable-types-data-types-java/)<br>
[코딩교육 티씨피스쿨](http://www.tcpschool.com/java/java_datatype_variable)<br>
[Non-primitive Data Types in Java | Scaler Topics](https://www.scaler.com/topics/non-primitive-data-types-in-java/)<br>
[Data Types in Java | Primitive and Non-Primitive Data Types | Edureka](https://www.edureka.co/blog/data-types-in-java/)<br>