# Java - Generics

| 한글 용어 | 영문 용어 | 예시 |
| - | - | - |
| 매개변수화 타입 | parameterized type | `List<String>` |
| 실제 타입 매개변수 | actual type parameter | `String` |
| 제네릭 타입 | generic type | `List<E>` |
| 정규 타입 매개변수 | formal type parameter | `E` |
| 비한정적 와일드카드 타입 | unbounded wildcard type | `List<E>` |
| 로 타입 | raw type | `List` |
| 한정적 타입 매개변수 | bounded type parameter | `<E extends Number>` |
| 재귀적 타입 한정 | recursive type bound | `<T extends Comparable<T>>` |
| 한정적 와일드카드 타입 | bounded wildcard type | `List<? extends Number>` |
| 제네릭 메서드 | generic method | `static <E> List<E> asList(E[] a)` |
| 타입 토큰 | type token | `String.class` |

<br/>

## Table of Contents
---
1. [What is Generics?](#1-what-is-generics)
2. [Generic Wildcard](#2-generic-wildcard)
3. [Types of Java Generics](#3-types-of-java-generics)
4. [Advantages of Generics](#4-advantages-of-generics)
5. [References](#5-references)

<br/>

## 1. What is Generics?
---
### 1.1 Generic (제네릭)
- Java 5부터 사용할 수 있다.
- Generic을 사용하면 다양한 데이터 타입에서 작동하는 클래스, 메서드, 인터페이스를 만들 수 있다.
- Generic은 type parameter(타입 매개변수)를 선언부에 추가함으로써 사용할 수 있다.
	- 타입 매개변수 + 클래스 = 제네릭 클래스
	- 타입 매개변수 + 인터페이스 = 제네릭 인터페이스
	- 제네릭 클래스 + 제네릭 인터페이스 = 제네릭 타입
- <span style="color: orange;">참고로, 제네릭 엔티티는 parameterized type(매개변수화 타입)*에서 작동하는 클래스, 인터페이스, 메서드와 같은 엔티티를 모두 포함한다.</span>
- 배열과 제네릭은 잘 어우러지지 못한다. 따라서 제네릭 배열 생성은 불가능하다.
	- 배열과 달리 제네릭은 불공변(invariant)이다.
	- 배열과 달리 제네릭은 원소 타입을 컴파일 타임에만 검사하며, 런타임에는 알 수조차 없다.

| Type | Is Available | Example |
| - | - | - |
| Reference Type (참조 타입) | O | Integer, String, 사용자 정의 타입 등 |
| Primitive Type (원시 타입) | X | int, char 등 |
| Primitive Type Array | O | ArrayList<int[]> (배열이 참조 타입이므로) |

```Java
// C++와 마찬가지로 Generics을 지정할 때 <>을 사용한다.
// Generic class 객체를 생성하려면 아래와 같이 작성하면 된다.
BaseType<Type> obj = new BaseType<Type>();

// 이때 primitive type은 사용할 수 없다. 따라서 아래의 구문은 잘못된 구문이다.
BaseType<int> obj = new BaseType<int>();

// 배열은 reference type이므로 아래와 같이 사용할 수 있다.
BaseType<ArrayList<int[]> obj = new BaseType<ArrayList<int[]>>();
```

```Plain
*Parameterized type(매개변수화 타입)
	1. 먼저 클래스(혹은 인터페이스) 이름이 나오고,
	2. 이어서 <> 안에 실제 타입 매개변수들을 작성한다.

*Raw type(로 타입)
	- 위의 매개변수화 타입에서 <>를 생략한 것이다.
```

### 1.2 Parameterized Type and Raw Type
#### Parameterized Type
매개변수화 타입(Parameterized type)은 주로 아래와 같이 작성된다.
1. 먼저 클래스(혹은 인터페이스) 이름이 나오고,
2. 이어서 <> 안에 실제 타입 매개변수들을 작성한다.
```Java
// Example 1. Collection<>
private final Colection<Stamp> stamps = ...;
```

#### Raw Type
- 제네릭 타입에서 타입 매개변수(<>)를 전혀 사용하지 않은 것을 말한다.
- 제네릭이 도입되기 이전의 Java와의 호환성을 위해 존재한다. (하지만 사용은 지양해야 한다.)
로 타입(Raw type)은 주로 아래와 같이 작성된다.
```Java
// Example 1. Collection (Not Collection<>)
private final Collection stamps = ...;

// Example 2. Iterator (Not Iterator<>)
for (Iterator i = stamps.iterator(); i.hasNext();) {
	Stamp stamp = (Stamp) i.next(); // ClassCastException*
	stamp.cancel();
}
```

🚨 여기서 주의할 것은 **로 타입은 웬만해선 사용하는 것을 피해야 한다.** 이유는 아래와 같다.
- `List<Object>` 같은 매개변수화 타입이 아닌 `List` 같은 로 타입을 사용하면 <u>타입 안전성</u>을 잃는다.
- 제네릭이 안겨주는 안전성과 표현력을 모두 잃게 된다.
- 런타임에 예외가 일어날 수 있으므로 (웬만해서는) 사용하면 안 된다.

📌 **로 타입을 사용해야 하는 몇 가지 예외도 존재한다.**
- `class` 리터럴\*에는 로 타입을 사용해야 한다.
	```Java
	// 허용하는 것
	List.class
	String[].class
	int.class

	// 허용하지 않는 것
	List<String>.class
	List<?>.class
	```
- `instanceof` 사용 시 로 타입을 사용해도 된다.
	```Java
	if (o instanceof Set) {
		Set<?> s = (Set<?>) o;
	}
	```

```Plain
*ClassCastException을 일으킬 수 있는 비검사 경고를 무시하지 말자.
	- 비검사 경고는 런타임에 ClassCastException을 일으킬 수 있는 잠재적 가능성을 의미한다.
	1. 경고를 없애지 못한다면 그 코드가 타입 안전성을 보장하는지 증명하자.
	2. 가능한 한 범위를 좁혀 @SuppressWarnings("unchecked") 애너테이션으로 경고를 숨기자.
	3. 그런 다음 경고를 숨기기로 한 근거를 주석으로 남기자.

*class 리터럴
	- 특정 클래스를 나타내는 값으로, 클래스의 메타데이터를 참조한다.
	- String.class, Integer.class 등을 말한다.
	- String.class의 타입은 Class<String>, Integer.class의 타입은 Class<Integer>이다.

*타입 토큰
	- 타입을 나타내는 토큰
	- class 리터럴이 타입 토큰으로서 사용된다.
	- 예를 들어, 타입 안전성이 필요한 곳에 사용된다.
```

### 1.3 Type Parameters in Java Generics
Generic에서는 타입 매개변수(type parameter) 명명 규칙을 지키는 것이 중요하다
일반적인 타입 매개변수는 아래와 같다.

| Type Parameter | Description |
| - | - |
| T | Type |
| E | Element |
| K | Key |
| N | Number |
| V | Value |

예를 들어 Java의 `List`도 사실은 `List<E>`[List of E]를 의미한다.

참고로, 위에서 E(Element)와 T(Type)의 차이는 무엇일까? E는 그 의미로 요소라고 해석할 수 있다. 따라서 ArrayList나 List 등의 요소들에 사용하는 것이 적절하다. 즉, Collection 클래스 같이 배열 기반으로 되어 있는 구조에는 E가 어울리고, 그 외에는 T가 어울린다는 것이다.

### 1.4 Why Generic?
#### Type of Safety
Java의 Object는 다른 모든 클래스의 상위 클래스이며, Object reference는 모든 객체를 참조할 수 있다. 하지만 이러한 기능에는 **Type of Safety**(타입 안전성)가 부족하다. Object와 달리 <u>제네릭은 이러한 타입 안전성을 보장한다.</u>

```Java
// Java program to show working
// of user-defined Generic classes

// We use < > to specify Parameter type
class Test<T> {
	// An object of type T is declared
	T obj;
	Test(T obj) { this.obj = obj; } // constructor
	public T getObject() { return this.obj; }
}

// Driver class to test above
class Main {
	public static void main(String[] args)
	{
		// instance of Integer type
		Test<Integer> iObj = new Test<Integer>(15);
		System.out.println(iObj.getObject());

		// instance of String type
		Test<String> sObj
			= new Test<String>("GeeksForGeeks");
		System.out.println(sObj.getObject());
		iObj = sObj; // This results an error
	}
}
```

```sh
error:
 incompatible types:
 Test cannot be converted to Test
```

위의 Java 코드에서 보면 `iObj`와 `sObj`가 서로 같은 타입을 가지고 있음에도 불구하고, type parameter가 다르기 때문에 서로 다른 타입에 대한 참조를 가지게 된다. 이처럼 제네릭은 타입 안전성을 보장하여 에러를 방지한다.

Generic을 지원하기 전에는 Collection에서 객체를 꺼낼 때마다 형변환을 해줘야 했는데, <u>Generic을 사용함으로써 Collection이 담을 수 있는 타입을 (위처럼) 컴파일러가 알려주게 되었다.</u> 따라서 더 안전하고 명확한 프로그램을 만들 수 있지만, 코드가 복잡해진다는 단점 또한 존재한다.

#### Array and Generics

| 구분 | 배열(Array) | 제네릭(Generic) |
| - | - | - |
| Syntax | `[]` | `<>` |
| 공변/불공변 | 공변 | 불공변\* |
| 타입 정보 소거 여부 | 실체화된다. | 타입 정보가 소거된다. |
| 컴파일타임 타입 안전성 | X | O |
| 런타임 타입 안전성 | O | X |

위와 같은 다른 점 때문에 배열과 제네릭을 섞어서 사용하는 것을 쉽지 않다. 예를 들어, `List<String>[]`이 안 되는 것이 그 예이다.  이렇게 작성하면 제네릭 배열 생성 오류를 발생시킨다.

여기서 제네릭이 가지는 장점 중 '컴파일타임에서의 타입 안전성'은 가지는 의미가 크다. 따라서 둘을 섞어 사용하다가 컴파일 오류나 경고를 만나면, 가장 먼저 배열을 리스트로, 즉 제네릭으로 대체하는 방법을 적용하는 것을 추천한다.

단, 여기서 제네릭이 가지는 공변성이 Java가 가지는 객체 지향을 전혀 이용하지 못한다는 문제점이 있다. 따라서 이를 해결하기 위해 나온 것이 바로 '제네릭 와일드카드'이다. 이 부분에 대한 내용은 조금 더 아래에서 살펴볼 것이다.

```Plain
*불공변(Invariant)
	- 객체 타입에 상하 관계가 있더라도 제네릭 타입에는 상하 관계가 없다.
	- 즉, 전달받은 그 타입으로만 서로 캐스팅이 가능하다는 뜻이다.
	- 서로 다른 타입 Type1, Type2가 있을 때 List<Type1>과 List<Type2>는 아무 관계도 아니다.
	- 예시) List<String>은 List<Object>의 하위 타입이 아리나는 의미이다.
```

<br/>

## 2. Generic Wildcard
---
참고로 아래는, 위에서 정리한 용어 중 참고 목적으로 와일드카드와 관련이 있는 개념들만 가져온 것이다.

| 한글 용어 | 영문 용어 | 예시 |
| - | - | - |
| 비한정적 와일드카드 타입 | unbounded wildcard type | `List<E>` |
| 한정적 타입 매개변수 | bounded type parameter | `<E extends Number>` |
| 재귀적 타입 한정 | recursive type bound | `<T extends Comparable<T>>` |
| 한정적 와일드카드 타입 | bounded wildcard type | `List<? extends Number>` |

Java 문법 중 `<?>`라고 표현된 정의문이 있는데, 여기서 `?` 물음표가 바로 와일드카드이며, 이는 어떤 타입이든 될 수 있다는 것을 의미한다. 하지만 단순히 `<?>`로 정의하면 Object 타입과 다른 점이 없기 때문에 보통 제네릭 타입 한정 연산자와 함께 쓰인다.

| 와일드카드 | 용어 | 설명 |
| - | - | - |
| `<?>` | Unbounded Wildcard(비한정적 와일드카드) | 제한 X (모든 타입 가능) |
| `<? extends U>` | Upper Bounded Wildcard(상한 경계 와일드카드) | 상위 클래스 제한 (U와 그 자손들만 가능) |
| `<? super U>` | Lower Bounded Wildcard(하한 경계 와일드카드) | 하위 클래스 제한 (U와 그 조상들만 가능) |

<br/>

## 3. Types of Java Generics
---
### 3.1 Generic Method
- 타입 파라미터(Type parameter)를 가진다.
- 일반적인 Java 메서드보다 더 일반적으로 사용할 수 있다.
- 컴파일러가 타입 안전성을 처리하므로 각각에 Type Casting을 할 필요가 없다.
- 매개변수화 타입을 받는 정적 유틸리티 메서드는 보통 제네릭이다.
- 예시) `Collections`의 `binarySearch()`, `sort()` 등

### 3.2 Generic Class
- 일반 클래스와 동일하게 구현된다.
- 한 가지 다른 점은 Type parameter section이 포함되어 있다는 것이다.
- 쉼표(,)로 구분된 type parameter가 2개 이상 있을 수 있다.
- 하나 이상의 매개변수를 허용하는 클래스를 'Parameterized classes' 혹은 'Parameterized types'라고 부른다.

```Java
// Java program to show working of user defined
// Generic classes

// We use < > to specify Parameter type
class Test<T> {
	// An object of type T is declared
	T obj;
	Test(T obj) { this.obj = obj; } // constructor
	public T getObject() { return this.obj; }
}

// Driver class to test above
class Main {
	public static void main(String[] args)
	{
		// instance of Integer type
		Test<Integer> iObj = new Test<Integer>(15);
		System.out.println(iObj.getObject());

		// instance of String type
		Test<String> sObj
			= new Test<String>("GeeksForGeeks");
		System.out.println(sObj.getObject());
	}
}

```

```Java
// Java program to show multiple
// type parameters in Java Generics

// We use < > to specify Parameter type
class Test<T, U>
{
	T obj1; // An object of type T
	U obj2; // An object of type U

	// constructor
	Test(T obj1, U obj2)
	{
		this.obj1 = obj1;
		this.obj2 = obj2;
	}

	// To print objects of T and U
	public void print()
	{
		System.out.println(obj1);
		System.out.println(obj2);
	}
}

// Driver class to test above
class Main
{
	public static void main (String[] args)
	{
		Test <String, Integer> obj =
			new Test<String, Integer>("GfG", 15);

		obj.print();
	}
}
```

### 3.3 Generic Functions
- Generic Method에 전달된 인수의 유형에 따라 호출된다.
- 컴파일러가 각 메서드를 처리한다.

```Java
// Java program to show working of user defined
// Generic functions

class Test {
	// A Generic method example
	static <T> void genericDisplay(T element)
	{
		System.out.println(element.getClass().getName()
						+ " = " + element);
	}

	// Driver method
	public static void main(String[] args)
	{
		// Calling generic method with Integer argument
		genericDisplay(11);

		// Calling generic method with String argument
		genericDisplay("GeeksForGeeks");

		// Calling generic method with double argument
		genericDisplay(1.0);
	}
}
```

<br/>

# 4. Advantages of Generics
---
### ① Code Reuse
Generics로 작성한 메서드, 클래스, 인터페이스 모두 원하는 타입(단, 참조 타입만)에 한해 사용할 수 있다.

### ② Type Safety
Generics는 런타임이 아닌 컴파일 타임에 에러를 발생시킨다. 따라서 Type Safety를 보장한다.

아래에 한 예시가 있다. 학생 이름을 저장하는 ArrayList를 생성하려고 하는데 개발자가 실수로 문자열 대신 정수 객체를 추가한 경우 런타임에서 문제가 발생하게 된다.

```Java
// Java program to demonstrate that NOT using
// generics can cause run time exceptions

import java.util.*;

class Test
{
	public static void main(String[] args)
	{
		// Creatinga an ArrayList without any type specified
		ArrayList al = new ArrayList();

		al.add("Sachin");
		al.add("Rahul");
		al.add(10); // Compiler allows this

		String s1 = (String)al.get(0);
		String s2 = (String)al.get(1);

		// Causes Runtime Exception
		String s3 = (String)al.get(2);
	}
}
```

```Plain
Exception in thread "main" java.lang.ClassCastException: 
   java.lang.Integer cannot be cast to java.lang.String
    at Test.main(Test.java:19)
```

위의 코드를 Generics를 사용해서 수정해 보자.

```Java
// Using Java Generics converts run time exceptions into 
// compile time exception.
import java.util.*;

class Test
{
	public static void main(String[] args)
	{
		// Creating a an ArrayList with String specified
		ArrayList <String> al = new ArrayList<String> ();

		al.add("Sachin");
		al.add("Rahul");

		// Now Compiler doesn't allow this
		al.add(10); 

		String s1 = (String)al.get(0);
		String s2 = (String)al.get(1);
		String s3 = (String)al.get(2);
	}
}
```

```Plain
15: error: no suitable method found for add(int)
        al.add(10); 
          ^
```

ArrayList를 정의할 때 Generics를 사용하여 String 객체만 받도록 지정했기 때문에 위와 같이 컴파일 에러가 발생하는 것을 확인할 수 있다.

### ③ Individual Type Casting is not needed
위의 예제에서 Generics를 사용하지 않았다면 필요할 때마다 type casting을 통해 형 변환을 적용시켜야 한다. 따라서 Generics `<>`를 이용한다면, 매번 형 변환을 하지 않아도 된다.

```Java
// We don't need to typecast individual members of ArrayList

import java.util.*;

class Test {
	public static void main(String[] args)
	{
		// Creating a an ArrayList with String specified
		ArrayList<String> al = new ArrayList<String>();

		al.add("Sachin");
		al.add("Rahul");

		// Typecasting is not needed
		String s1 = al.get(0);
		String s2 = al.get(1);
	}
}
```

### ④ Generics Promotes Code Reusability
Generics를 사용하면 다양한 타입의 데이터로 작동하는 코드를 작성할 수 있기 때문에 코드 재사용성을 얻게 된다.

아래 예제를 보면, 각각 정수, 문자, 문자열 등과 같은 다양한 타입의 데이터를 가진 배열을 정렬하고 싶을 때 기본적으로는 데이터 타입에 따라 서로 다른 함수가 필요하다. 하지만 Generics를 사용하면 동일한 메서드 하나만을 사용하여 재사용할 수 있다.

```Java
public class GFG {

	public static void main(String[] args)
	{

		Integer[] a = { 100, 22, 58, 41, 6, 50 };

		Character[] c = { 'v', 'g', 'a', 'c', 'x', 'd', 't' };

		String[] s = { "Virat", "Rohit", "Abhinay", "Chandu","Sam", "Bharat", "Kalam" };

		System.out.print("Sorted Integer array : ");
		sort_generics(a);

		System.out.print("Sorted Character array : ");
		sort_generics(c);

		System.out.print("Sorted String array : ");
		sort_generics(s);
	
	}

	public static <T extends Comparable<T> > void sort_generics(T[] a)
	{
	
		//As we are comparing the Non-primitive data types 
		//we need to use Comparable class
	
		//Bubble Sort logic
		for (int i = 0; i < a.length - 1; i++) {

			for (int j = 0; j < a.length - i - 1; j++) {

				if (a[j].compareTo(a[j + 1]) > 0) {

					swap(j, j + 1, a);
				}
			}
		}

		// Printing the elements after sorted

		for (T i : a) 
		{
			System.out.print(i + ", ");
		}
		System.out.println();
	
	}

	public static <T> void swap(int i, int j, T[] a)
	{
		T t = a[i];
		a[i] = a[j];
		a[j] = t;
	}

}
```

### ⑤ Implementing Generic Algorithms
- Generics를 사용하면 다양한 유형의 객체에서 작동하는 알고리즘을 구현할 수 있다.
- 타입 안전성도 보장할 수 있다.

<br/>

## 5. References
---
- https://homoefficio.github.io/2016/11/30/%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%A6%AC%ED%84%B0%EB%9F%B4-%ED%83%80%EC%9E%85-%ED%86%A0%ED%81%B0-%EC%88%98%ED%8D%BC-%ED%83%80%EC%9E%85-%ED%86%A0%ED%81%B0/
