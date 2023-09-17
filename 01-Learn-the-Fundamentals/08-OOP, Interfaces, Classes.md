# Java
## OOP

이번 장에서는 OOP(Object Oriented Programming, 객체 지향 프로그래밍)에 대한 개념을 살펴볼 것이다. OOP를 학습하기 전에 가장 기초적으로 알아야 할 클래스(Class)와 객체(Object)에 대해 살펴 보고, OOP의 4가지 원칙(추상화, 캡슐화, 상속, 다형성)에 대해 살펴볼 것이다.

</br>

### Table of Contents
[1. Class & Object](#-class--object)  
[2. Abstraction](#-abstraction추상화)  
[3. Encapsulation](#-encapsulation캡슐화)  
[4. Inheritance](#-inheritance상속)  
[5. Polymorphism](#-polymorphism다형성)  
[6. 참고 자료](#-참고-자료)

</br>

### ➲ Class & Object
#### Class(클래스)
- 객체가 생성되는 사용자 정의 청사진(blueprint) 또는 프로토타입(prototype)
- 한 유형의 모든 개체에 공통된 속성 또는 매서드의 집합
- 코드를 여러 번 작성하는 대신 동일한 동작으로 여러 개체를 만들 수 있다.

| Classification | Description | Example with below |
| - | - | - |
| Modifiers | 클래스의 액세스 권한 | `public` |
| Class name | 관례에 따라 첫 글자를 대문자로 시작 | `ClassName` |
| Superclass (if any) | - 클래스의 상위 클래스가 있는 경우</br>- 클래스는 하나의 상위 클래스만 확장할 수 있다. | 클래스 이름 옆에 `extends` |
| Interfaces (if any) | 둘 이상의 인터페이스를 구현할 수 있다. | 클래스 이름 옆에 `implements` |
| Body | 클래스 본문은 중괄호 `{}`로 둘러싸여 있어야 한다. | `{}` |

```Java
public class ClassName {
    // filed

    // constructor

    // method
}
```

#### Object(객체)
- 실제 객체를 나타내는 객체 지향 프로그래밍의 기본 단위
- Java에서는 일반적으로 여러 메서드를 호출하여 상호 작용하는 많은 객체를 생성한다.

객체는 주로 다음과 같이 구성된다.

| Classification | Description |
| - | - |
| State | 객체의 속성을 표현 및 반영한다. |
| Behavior | 객체의 메서드로 표현되며, 다른 객체에 대한 객체의 반응을 반영한다. |
| ID | 다른 객체와 상호 작용할 수 있도록 객체에게 부여된 고유의 이름이다. |
| Method(메서드) | - 특정 작업을 수행하고 결과를 호출자에게 반환하는 명령문 모음이다.</br>- Java의 모든 메서드는 클래스의 일부여야 한다. |

```Java
public class ClassName {
    // field
    private int number = 0;

    // constructor
    public ClassName(int number) {
        this.number = number;
    }

    // method
    public void printNumber() {
        System.out.println(this.number);
    }
}

public class MainClass {
    public static void main(String[] args) {
        // object
        ClassName className = new ClassName(5);

        // call method of the object
        className.printNumber();
    }
}
```

</br>

### ➲ Abstraction(추상화)
- 필수 세부 정보만 사용자에게 표시되는 속성
- 관련 없는 세부 사항은 무시하고 객체의 필수 특성만 식별하는 프로세스로 정의될 수 있다.
- 객체의 속성과 동작은 유사한 유형의 다른 객체와 구별되며 객체를 분류/그룹화하는 데 도움이 된다.
- **Java에서는 인터페이스(Interface)와 추상 클래스(Abstract Class)를 통해 추상화를 수행한다.**
- 예시
  - 자동차는 개별 구성 요소가 아닌 '자동차'로만 간주된다.
  - 자동차 운전 시 가속 페달을 밟을 때 속도가 빨라지는 건 알지만, 그 원리는 모르는 것이 바로 추상화이다.

#### 추상 클래스(Abstract Class)

```Java
abstract class AbstractClassExample {
    // abstract methods declaration
    abstract void add();
    abstract void mul();
    abstract void div();
}
```

</br>

### ➲ Encapsulation(캡슐화)
- = Data-Hiding
- 단일 단위로 데이터를 정리하는 것
- 코드와 코드가 조작하는 데이터를 함께 묶는 방법
- 외부의 코드가 데이터에 액세스하는 것을 방지하는 보호 쉴드의 역할을 하기도 한다.
- **클래스의 변수/데이터가 다른 클래스로부터 숨겨지며 선언된 클래스의 멤버 함수를 통해서만 액세스할 수 있다.**
- 클래스의 모든 변수를 비공개로 선언하고 클래스에 공개 메서드를 작성하여 변수 값을 설정하고 가져옴으로써 달성한다.

```Java
// Encapsulation using private modifier

class Employee {
    private int id;
    private String name;
}
```

</br>

### ➲ Inheritance(상속)
- OOP의 중요한 기둥
- 한 클래스가 다른 클래스의 기능(필드 및 메서드)을 상속하도록 허용하는 Java의 메커니즘
- 상속을 'is-a' 관계라고도 한다.
- `extends` 키워드를 사용하여 상속을 구현할 수 있다.

아래는 상속과 관련하여 주로 사용되는 몇 가지의 중요한 용어에 대해 정리하였다.

| Classficiation | Description |
| - | - |
| Superclass(슈퍼/기본/상위 클래스) | 기능이 상속된 클래스 |
| Subclass(서브/파생/확장/하위 클래스) | - 다른 클래스를 상속하는 클래스</br>- 상위 클래스 필드 및 메서드 외에도 자체 필드 및 메서드를 추가할 수 있다. |
| Reusability(재사용성) | 새 클래스를 만들고 싶고 이미 원하는 코드 일부를 포함하는 클래스가 있는 경우 기존 클래스에서 새 클래스를 파생시킬 수 있다. 이렇게 하면 기존 클래스의 필드와 메서드를 재사용할 수 있다. |

```Java
class A {
    void method1() {}
    void method2() {}
}

class B extends A {
    void method3() {}
    void method4() {}
}
```

</br>

### ➲ Polymorphism(다형성)
- 동일한 이름을 가진 엔티티를 효율적으로 구별할 수 있다.
- 다양한 형태로 나타나는 능력
- Java의 다형성에는 주로 두 가지 유형이 있다.
  1. Overloading
  2. Overriding

```Java
public class Sum {

    public int sum(int x, int y) {
        return (x + y);
    }

    public int sum(int x, int y, int z) {
        return (x + y + z);
    }

    public double sum(double x, double y) {
        return (x + y);
    }

    public static void main(String[] args) {
        Sum s = new Sum();
        System.out.println(s.sum(10, 20));
        System.out.println(s.sum(10, 20, 30));
        System.out.println(s.sum(10.5, 20.5));
    }
}
```

</br>

### ➲ 참고 자료
- https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/