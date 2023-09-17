# Java
## Packages

### Table of Contents
[1. Package(패키지)란?](#➲-package패키지란)  
[2. Java 패키지의 장점](#➲-java-패키지의-장점)  
[3. 패키지 액세스 방법](#➲-패키지-액세스-방법)  
[4. 디렉토리 구조](#➲-디렉토리-구조)  
[5. 패키지와 관련된 중요 사항](#➲-패키지와-관련된-중요-사항)  
[6. 참고 자료](#➲-참고-자료)

</br>

### ➲ Package(패키지)란?

<img src="https://static.javatpoint.com/images/package.JPG" />

</br>

- Java의 패키지는 유사한 유형의 클래스, 인터페이스 및 하위 패키지 그룹이다.
- 즉, 클래스, 하위 패키지 및 인터페이스 그룹을 캡슐화한다.
- 두 가지 형태
  - 내장 패키지(Built-in Package)
  - 사용자 정의 패키지(User-Defined Package)

#### Java 패키지의 두 가지 형태

| Type of Package | Description |
| - | - |
| 내장 패키지(Built-in Package) | java, lang, awt, javax, Swing, net, io, util, sql, ... |
| 사용자 정의 패키지(User-Defined Package) |  |

#### 일반적으로 사용되는 내장 패키지
여기서 Java의 기본 내장 패키지 중 일반적으로 사용되는 일부는 다음과 같다.

| Package | Description |
| - | - |
| java.lang | - 언어 지원 클래스를 포함한다.</br>- 예시: 원시 데이터 유형과 수학을 정의하는 클래스</br> - 자동으로 `import` 된다.  |
| java.io | 입출력 작업을 지원하기 위한 클래스를 포함한다. |
| java.util | - 여러 데이터 구조를 구현하는 유틸리티 클래스를 포함한다.</br>- Date / Time 작업도 포함된다. |
| java.applet | 애플릿을 생성하기 위한 클래스를 포함한다. |
| java.awt | 그래픽 사용자 인터페이스용 구성 요소를 구현하기 위한 클래스를 포함한다. |
| java.net | 네트워킹 작업을 지원하는 클래스를 포함한다. |

</br>

### ➲ Java 패키지의 장점
- 클래스와 인터페이스를 쉽게 유지 관리할 수 있도록 분류하는 데 사용된다.
- 액세스 보호를 제공한다.
- 이름 충돌을 제거한다. (즉, 같은 클래스 이름이어도 패키지가 다르면 결과적으로 다른 클래스가 된다.)
- 데이커 캡슐화(또는 데이터 숨기기)로 간주될 수 있다.

</br>

### ➲ 패키지 액세스 방법
특정 패키지의 외부에서 패키지에 액세스하는 방법에는 세 가지가 있다. 참고로 이때 `import` 키워드는 현재 패키지에서 다른 패키지의 클래스와 인터페이스에 액세스할 수 있도록 해준다.

1. `import package.*;`
2. `import package.classname;`
3. 완전한 이름을 사용하는 방법

#### ① `import package.*;`
- `package.*`를 사용하면 이 패키지의 모든 클래스와 인터페이스에 액세스할 수 있다.
- 하지만 하위 패키지에는 액세스할 수 없다.

```Java
import java.util.*; // key point

public class ClassExample {
    public static void main(String[] args) {
        Date date = new Date();
        System.out.println(date);
    }
}
```

#### ② `import package.classname;`
- 해당 패키지의 선언된 클래스에만 액세스할 수 있다.

```Java
import java.util.Date; // key point

public class ClassExample {
    public static void main(String[] args) {
        Date date = new Date();
        System.out.println(date);
    }
}
```

#### ③ 완전한 이름을 사용하는 방법
- 완전한/정규화된 이름을 사용하면 해당 패키지의 선언된 클래스에만 액세스할 수 있다.
- `import`를 통해 가져올 필요는 없지만 클래스나 인터페이스에 액세스할 때마다 완전한 이름을 사용해야 한다.
- 일반적으로 두 패키지가 동일한 클래스 이름을 가질 때 사용된다.

```Java
public class ClassExample {
    public static void main(String[] args) {
        java.util.Date date = new java.util.Date(); // key point
        System.out.println(date);
    }
}
```

</br>

### ➲ 디렉토리 구조
- 패키지 이름은 클래스를 저장하는 데 사용되는 디렉토리 구조와 밀접하게 연관되어 있다.
- 특정 패키지에 속하는 클래스(및 기타 엔티티)는 동일한 디렉토리에 함께 저장된다.
- 예시:
  com.zzz.project1.subproject2 패키지의 `Circle` 클래스는 ${BASE_DIR}\com\zzz\project1\subproject2\Circle.class로 저장된다. 여기서 ${BASE_DIR}은 패키지의 기본 디렉토리를 의미한다.

위에서 ${BASE_DIR}로 지정된 기본 디렉토리는 파일 시스템이 어느 위치에서나 위치할 수 있다. 따라서 클래스를 찾으려면 Java 컴파일러와 런타임에 ${BASE_DIR}의 위치를 알려야 한다. 이는 CLASSPATH라는 환경 변수를 통해 수행된다.

</br>

### ➲ 패키지와 관련된 중요 사항
- 모든 클래스는 일부 패키지의 일부이다.
- 패키지가 지정되지 않으면 파일의 클래스는 이름이 지정되지 않은 *특별한 패키지로 이동된다.
- *파일의 모든 클래스/인터페이스는 동일한 패키지의 일부이다. 여러 파일이 동일한 패키지 이름을 지정할 수 있다.
- 디렉토리 이름은 패키지 이름과 일치해야 한다.
- 다음을 사용하여 이름이 지정된 다른 패키지의 공개 클래스에 액세스할 수 있다.
  </br>`packagename.classname`

*특별한 패키지: 모든 파일에 대해 이름이 지정되지 않은 동일한 패키지  
*여기서 파일은 특정 .java와 같은 파일을 의미하는 것 같다.

</br>

### ➲ 참고 자료
- https://www.javatpoint.com/package
- https://www.geeksforgeeks.org/packages-in-java/
