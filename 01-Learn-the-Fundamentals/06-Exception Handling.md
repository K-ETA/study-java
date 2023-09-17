# Java
## Exception Handling

### Table of Contents
1. [Exception이란?](#➲-exception이란)
2. [Exception 유형](#➲-exception-유형)
3. [Exception Handling이란?](#➲-exception-handling이란)
4. [Exception Handling Methods](#➲-exception-handling-methods)
5. [효율적으로 예외 처리 사용하기](#➲-효율적으로-예외-처리-사용하기)
6. [참고 자료](#➲-참고-자료)

</br>

### ➲ Exception이란?
Java에서 **예외(Exception)**는 프로그램 실행 중에 프로그램 명령의 정상적인 흐름을 방해하는 원치 않거나 예상치 못한 이벤트를 의미한다.

#### 예외가 발생하는 순서
아래는 일반적으로 예외가 발생하는 순서를 정리한 것이다.

1. 프로그램 실행 시 특정 메서드(Method) 내에서 예외가 발생한다.
2. 예외 발생 시 해당 예외에 대한 개체가 생성된다. (*예외 개체)
3. 생성된 예외 개체는 JVM(Java Virtual Machine)에 전달된다.
4. 예외 개체를 런타임 시스템에서 처리한다. (= throwing Exception)

*예외 객체(Exception Object)는 예외 이름, 설명, 예외 발생 당시 프로그램의 상태 등에 대한 정보를 포함하고 있다.

런타임 시스템에서 예외 개체는 호출 스택(Call stack)이라고 하는 호출된 메서드 목록에서 처리된다.

1. 런타임 시스템은 호출 스택에서 예외가 발생한 메서드부터 검색을 시작한다.
   </br>이때 메서드가 호출된 역순으로 검색을 진행한다.
2. 발생한 예외를 처리할 수 있는 코드 블록(*예외 처리기)이 포함된 메서드를 찾는다.
3. *적절한 핸들러(Handler)를 찾으면 발생한 예외를 핸들러에 전달한다.
4. 적절한 핸들러를 찾지 못한 경우 기본 예외 핸들러로 넘겨준다.
5. 핸들러는 아래 형식으로 예외 정보를 출력하고, 프로그램을 비정상적으로 종료한다.

```bash
Exception in thread "xxx" Name of Exception : Description
... ...... ..  // Call Stack
```

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230714113633/Exceptions-in-Java2-768.png" />

#### 예외가 발생하는 주요 이유
예외가 발생하는 주요 이유에는 아래와 같은 이유들이 있다.
- 잘못된 사용자 입력
- 장치 고장
- 네트워크 연결 오류
- 물리적인 제한 (예시: 용량 부족, 메모리 부족 등)
- 코드 오류
- 사용할 수 없는 파일 열기

#### 예외와 오류의 차이점
- 예외(Exception)
  </br>예외는 정상적인 프로그램이 포착(`try-catch`)하려고 시도할 수 있다.

- 오류(Error)
  </br>오류는 정상적인 프로그램이 포착(`try-catch`)하려고 시도할 수 없는, 시도해서는 안 되는 심각한 문제를 의미한다. 예를 들면, JVM(Java Virtual Machine)의 메모리 부족, 메모리 누수, 스택 오버플로우 오류, 라이브러리 비호환성, 무한 재귀 등과 같은 _복구 불가능한_ 상황 및 조건을 의미한다. 일반적으로 이러한 오류는 개발자의 통제 범위를 벗어나기 때문에 오류를 처리하려고 해서는 안 된다.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230613122108/Exception-Handling-768.png" />

위의 그림에서 볼 수 있듯이 예외와 오류는 그 의미와 구분을 달리한다는 것을 알 수 있다. 모든 예외와 오류는 계층 구조의 기본 클래스인 Throwable 클래스의 하위 클래스가 된다.

</br>

### ➲ Exception 유형
Java의 Exception 유형에는 크게 두 가지 방식이 있다.

1. Built-in Exception(내장 예외)
     - Checked Exception(검사 예외)
     - Unchecked Exception(비검사 예외)
2. User-Defined Exception(사용자정의예외)

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230714113547/Exceptions-in-Java-1-768.png" />

#### Built-in Exception
- Java 라이브러리에서 사용할 수 있는 예외
- 특정 오류 상황을 설명하는 데 적합하다.
- 유형
  - Checekd Exception
    </br>컴파일러(Compiler)가 컴파일 시점에 확인하기 때문에 compile-time exception이라고 불리기도 한다.
  - Unchecked Exception
    </br>컴파일러가 확인하지 못하는 예외이며, 컴파일 오류를 발생시키지 않는다.프로그램이 unckeced exception을 발생시키더라도 컴파일 오류가 발생하지 않으며, 이에 대한 예외 처리는 개발자가 따로 지정할 수 있다.

#### User-Defined Exception
- 사용자가 직접 정의하여 사용하는 예외
- Java에 내장된 예외가 특정 상황을 설명하지 못할 경우 사용한다.
- 장점
  - 완전한 프로그램 실행을 위한 제공
  - 프로그램 코드 및 오류 처리 코드를 쉽게 식별할 수 있다.
  - 오류 전달 가능
  - 의미 있는 오류 보고 가능
  - 오류 유형 식별 가능

</br>

### ➲ Exception Handling이란?
Java에서의 **예외 처리(Exception Handling)**는 런타임(Runtime) 오류를 처리하고 애플리케이션의 정상적인 흐름을 유지하기 위한 효과적인 수단 중 하나이다.

<img src="https://miro.medium.com/v2/resize:fit:4800/format:webp/1*_jXNZuPLKMTQ5IKjBzb8jA.png" />

위의 그림은 검사 예외, 비검사 예외를 포함한 Java의 예외 계층에 대해 나타낸 그림이다. 여기서 `Exception`, `RuntimeException`, `Throwable`, `Error`는 직접 재사용하는 것이 좋지 않다. 따라서 그 하위에 있는 예외 클래스들을 주로 사용하는데, 예외 처리 시 어떤 예외 클래스를 주로 사용하는지를 정리하였다.

| Exception | In use |
| - | - |
| `IllegalArgumentException` | `null`을 제외한 허용하지 않는 값이 인수로 건네졌을 때 |
| `IllegalStateException` | 객체가 메서드를 수행하기에 적절하지 않은 상태일 때 |
| `NullPointerException` | `null`을 허용하지 않는 메서드에 `null`을 건넨 경우 |
| `IndexOutOfBoundsException` | 인덱스가 범위를 넘어섰을 때 |
| `ConcurrentModificationException` | 허용하지 않는 동시 수정이 발견되었을 때 |
| `UnsupportedOperationException` | 호출한 메서드를 지원하지 않을 때 |

물론 이 외에도 많은 예외 클래스가 사용된다. 상황에 부합한다면 이러한 예외 클래스를 이용하는 것이 좋으며, API 문서 등을 참고해 어떤 상황에서 어떤 예외가 발생시키는지를 확인하는 것이 좋다.

</br>

### ➲ Exception Handling Methods

#### `try-catch-(finally)`
| Block/Keyword | Description |
| - | - |
| `try` | 예외가 발생할 수 있는 일련의 명령문을 포함한다. |
| `catch` | 블록의 불확실한 조건을 처리하는 데 사용된다. |
| `finally` | - 선택적으로 작성해도 된다.</br>- `catch` 블록 다음에 실행된다.</br>- 여러 개의 `catch` 블록이 있는 경우 `finally`를 통해 공통 코드를 작성한다.</br>

이때 `try` 블록 뒤에는 항상 연관된 `try` 블록에서 발생하는 예외를 처리하는 `catch` 블록이 와야 한다.

```Java
class Exception {
    public static void main(String args[]) {
        try {
            // code that may raise exception
        } catch(Exception e) {
            // rest of the program
        } finally {
            // common code after catch block
        }
    }
}
```

#### `try-with-resources`
- Java 7부터 등장한 구문
- 자원을 쉽게 해제 사용하는 데 사용한다.

예를 들어 문자열을 모두 출력하는 `InpusStream`은 이후 자원의 낭비를 막기 위해 `close()`를 선언해 주어야 한다. 이를 조금 더 간편하게 사용하는 방법이 바로 `try-with-resources`를 사용하는 방법이다.

```Java
public static void main(String args[]) {
    try (
         FileInputstream is = new FileInputStream("file.txt")
         BufferedInputStream bis = new BufferedInputStream(is)
    ) {
        int data = -1;
        while ((data = bis.read()) != -1) {
            System.out.print((char) data);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

이렇게 하면 위의 `try(...)` 안에 선언된 객체의 `close()` 메서드는 `try`문을 벗어나면 자동으로 호출된다. 물론, 이때 모든 객체에 대한 `close()`를 호출하는 것은 아니다. 인터페이스인 `AutoCloseable`을 구현한 객체만 가능하며, `AutoCloseable`는 Java 7부터 등장하였다. `AutoCloseable`을 `implements`하는 방법을 통해 사용자가 직접 정의한 클래스도 적용시킬 수 있다.

#### `final` vs. `finally` vs. `finalize`
| Block/Keyword | Description |
| - | - |
| `final` | 클래스, 메서드, 그리고 변수에 제한을 적용하는 데 사용한다. |
| `finally` | 예외 발생 여부에 관계없이 중요한 공통 코드를 실행하는 데 사용하는 예외 처리 블록이다. |
| `finalize` | 객체가 *Garbage Collection 되기 직전에 정리 처리를 수행하는 데 사용되는 메서드이다. |

*Garbage Collection(GC): JVM 상에서 더 이상 사용되지 않는 데이터가 할당되어 있는 메모리를 해제시켜주는 장치로, JVM에서 자동으로 동작한다.

#### `throw` vs. `throws`
| Block/Keyword | Description |
| - | - |
| `throw` | `try` 블록에서 `catch` 블록으로 제어를 전송하는 데 사용한다. |
| `throws` | - `try-catch` 블록 없이 예외 처리할 때 사용한다.</br>- 메서드가 호출자에게 예외를 던지거나</br>- 자체적으로 처리하지 않는 예외를 지정한다. |

</br>

### ➲ 효율적으로 예외 처리 사용하기
#### 예외는 진짜 예외 상황에만 사용하라.
- 예외는 오직 예외 상황에서만 사용해야 한다. **절대로 일상적인 제어 흐름용으로 사용하면 안 된다.**
- 잘 설계된 API라면 클라이언트가 정상적인 제어 흐름에서 예외를 사용할 일이 없도록 해야 한다.

코드를 `try-catch` 블록 안에 넣으면 JVM이 적용할 수 있는 최적화가 제한되기 때문에 무작위한 예외 처리는 오히려 성능 저하를 일으킬 수 있다. 예를 들어 배열을 순회하는 표준 관용구는 JVM이 알아서 최적화하기 때문에 중복 검사를 수행하지 않는다.

```Java
/**
 * 옳지 않은 방법
 * 성능을 높이기 위해 ArrayIndexOutOfBoundsException 예외를 발생시켜 배열을 끝내는 코드를 작성하였다.
 */
try {
    int i = 0;
    while(true)
        range[i++].climb();
} catch (ArrayIndexOutOfBoundsException e) {
    
}
```

```Java
/**
 * 올바른 방법
 * Java의 표준 관용구를 사용하여 반복문을 작성하였다.
 */
for (Mountain m : range)
    m.climb();
```

#### 복구할 수 있는 상황에는 검사 예외를, 프로그래밍 오류에는 런타임 예외를 사용하라.
- 검사 예외(Checked exception)
  - 호출하는 쪽에서 복구하리라 여겨지는 상황인 경우 사용한다.
  - **복구에 필요한 정보를 알려주는 메서드도 제공해야 한다.**
- 비검사 예외(Unchecked exception)
  - 프로그래밍 오류를 나타낼 때 사용한다.
  - 확실하지 않을 때 사용한다.
- 위의 경우 둘 다 해당하지 않는 throwable은 정의하지 말자.

#### 필요 없는 검사 예외 사용은 피하라.
- API 호출자가 예외 상황에서 복구할 방법이 없다면 비검사 예외를 던지자.
- 복구가 가능하고 호출자가 그 처리를 해주길 바란다면
  1. 먼저, 옵셔널(Optional)을 반환해도 될지 고민하자.
  2. 옵셔널만으로는 상황을 처리하기 위한 충분한 정보를 제공할 수 없을 때 검사 예외를 던지자.

#### 표준 예외를 사용하라.
- `Exception`, `RuntimeException`, `Throwable`, `Error`는 직접 재사용하지 않는 것을 권장한다.
- 위의 4가지의 클래스의 하위 클래스인 여러 예외 클래스를 사용하는 것이 좋다.
- 필요하다면 표준 예외를 확장해도 좋다. (하지만 이때 직렬화는 주의하자)

#### 추상화 수준에 맞는 예외를 던지라.
- 아래 계층의 예외를 예방하거나 스스로 처리할 수 없고, 그 예외를 상위 계층에 그대로 노출하기 곤란한 경우 *예외 번역을 사용하면 된다.
- 이때 *예외 연쇄를 이용하여 상위 계층에는 맥락에 어울리는 고수준 예외를 던지면서 근본 원인도 함께 알려주어 오류를 분석하기 좋게 만들 수 있다.

*예외 번역(Exception Translation): 상위 계층에서는 저수준 예외를 잡아 자신의 추상화 수준에 맞는 예외로 바꿔 던지는 방식

```Java
try {
    ... // 저수준 추상화를 이용한다.
} catch (LowerLevelException e) {
    // 추상화 수준에 맞게 번역한다.d
    throw new HigherLevelException(...);
}
```

*예외 연쇄(Exception Chaining): 근본 원인(cause)인 저수준 예외를 고수준 예외에 실어 보내는 방식으로, 예외 번역 시 저수준 예외가 디버깅에 도움이 되는 경우 주로 사용된다.

```Java
try {
    ... // 저수준 추상화를 이용한다.
} catch (LowerLevelException cause) {
    // 저수준 예외를 고수준 예외에 실어 보낸다.
    throw new HigherLevelException(cause);
}
```

#### 메서드가 던지는 모든 예외를 문서화하라.
- 각 예외가 발생하는 상황을 Javadoc의 `@throws` 태그를 사용하여 정확히 문서화하는 것이 좋다.
- 한 클래스에 정의된 많은 메서드가 같은 이유로 같은 예외를 던지는 경우 그 예외를 각각의 메서드가 아닌 클래스 설명에 추가하는 방법도 있다.
- 검사 예외는 항상 따로따로 선언하는 것이 좋다. 예를 들어 메서드 선언의 `@throws` 문에 일일이 선언하는 것이다.
- 비검사 예외는 메서드 선언에는 기입하지 않는 것이 좋다.

이때 예외는 검사 예외, 비검사 예외를 모두 포함하며, 메서드도 추상 메서드, 구체 메서드 모두 마찬가지이다. 발생 가능한 예외를 문서로 남기지 않으면 다른 사람이 그 클래스나 인터페이스를 효과적으로 사용하기 어렵거나 심지어 불가능할 수도 있다.

#### 예외의 상세 메시지에 실패 관련 정보를 담으라.
- 실패 순간을 호착하려면 발생한 예외에 관여된 모든 매개변수와 필드의 값을 실패 메시지에 담아야 한다. 이때 주로 `toString()` 메서드를 활용한다.
- 단, 보안과 관련된 정보(예시: 비밀번호, 암호 키 등)는 상세 메시지에 담으면 안 된다.

#### 가능한 한 실패 원자적으로 만들어라.
- 호출된 메서드가 실패하더라도 해당 객체는 메서드 호출 전 상태를 유지해야 한다. (*실패 원자적)
- 메서드 명세에 기술한 예외가 발생했을 때 실패 원자성을 지키지 못한다면 실패 시의 객체 상태를 API 설명에 명시해야 한다.

물론 실패 원자성을 달성하기 위한 비용이나 복잡도가 아주 큰 경우 항상 이 규칙을 따라야 한다는 것은 아니다.

*실패 원자적(failure-atomic) 메서드를 만드는 방법
  1. 불변 객체로 설계
  2. 불변 객체가 아니라면 작업 수행에 앞서 매개변수의 유효성을 검사한다.
  3. 객체의 임시 복사본에서 작업을 수행한 후 작업이 성공적으로 완료되면 원래 객체와 교체한다.
  4. 작업 도중 발생하는 실패를 가로채는 복구 코드를 작성하여 작업 전 상태로 되돌린다.

#### 예외를 무시하지 말라.
- `catch` 블록을 비워두면 예외가 존재할 이유가 없어진다.
- 예외를 무시하기로 했다면 `catch` 블록 안에 그 이유를 주석으로 남기고, 예외 변수의 이름도 `ignored`로 바꿔 놓는 것이 좋다.

</br>

### ➲ 참고 자료
- https://www.geeksforgeeks.org/exceptions-in-java/
- https://www.youtube.com/watch?v=W-N2ltgU-X4
- https://www.geeksforgeeks.org/try-catch-throw-and-throws-in-java/
- https://codechacha.com/ko/java-try-with-resources/
- https://www.javatpoint.com/difference-between-final-finally-and-finalize
- https://tecoble.techcourse.co.kr/post/2021-08-30-jvm-gc/
- https://www.javatpoint.com/difference-between-throw-and-throws-in-java
- 조슈아 블로크, 『이펙티브 자바 Effective Java 3/E』, 프로그래밍인사이트, 2018. 12. 18.