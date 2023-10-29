# Java - Streams

<br/>

## Table of Contents
---
[1. What is Java Stream?](#1-what-is-java-stream)
[2. Java Stream Features](#2-java-stream-features)
[3. Different Operations on Streams](#3-different-operations-on-streams)
[4. Java Stream Interface Methods](#4-java-stream-interface-methods)
[5. How to make good use of Stream](#5-how-to-make-good-use-of-stream)
[6. References](#6-references)

<br/>

## 1. What is Java Stream?
---
### 1.1 Stream in Java 8
- Java 8에 도입된 Stream API (즉, Java 8 이상부터 사용 가능)
- java.util.stream 패키지에서 제공되는 함수형 API
- Stream API로 인해 데이터 원소의 sequence 처리를 라이브러리 차원에서 지원하기 시작하였다.
- Object의 Collection을 처리하는 데 사용된다.
- 파이프라인을 통해 원하는 결과를 얻을 수 있는 다양한 방법을 지원하는 객체의 sequence이다.

### 1.2 Use of Stream in Java
- Stream API는 객체의 Collection을 표현하고 처리하는 방법
- Filtering, mapping, reducing, sorting 같은 작업 수행 가능

### 1.3 Syntax
```Java
// 여기서 T는 선언에 따라 달라지며, 클래스나 객체 또는 데이터 타입이 될 수 있다.
Stream<T> stream;
```

<br/>

## 2. Java Stream Features
---
- Stream은 data structure가 아니라 Collections, Arrays 또는 I/O 채널에서 input을 가져온다.
- Stream은 원래의 data structure가 아니라 파이프라인에 따라 결과를 제공할 뿐이다.
	- 즉, 원래의 객체 값을 변경하지 않고 파이프라인된 메서드에 따라 요소를 연산하는 데 사용된다.

<br/>

## 3. Different Operations on Streams
---
Stream에는 두 가지 유형의 연산이 있다.
1. Intermediate Operations (중간 연산)
2. Terminate Operations (종료/종단 연산)

여기서, Stream 파이프라인은 **지연 평가(lazy evaluation)** 된다는 특징을 가지고 있다. 연산은 종단 연산이 호출될 때 이루어지며, 종단 연산에 쓰이지 않는 데이터 원소는 연산에 쓰이지 않는다. (참고로, 이러한 지연 평가가 무한 스트림을 다룰 수 있게 해주는 열쇠이다.) 따라서 종단 연산이 없는 Stream 파이프라인은 아무 일도 하지 않는 명령어인 `no-op`과 같으므로 종단 연산을 빼먹는 일은 없어야 한다.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705133732/Stream-in-Java-768.png" />

### 3.1 Intermediate Operations
- 여러 메서드가 연속적으로 연결되어 있다.
- Stream을 다른 Stream으로 변환한다.
- 한 메서드가 데이터를 필터링하여 처리한 후 다른 메서드로 전달하는 것이 가능하다.
- Lazy Evaluation을 기반으로 실행되며, 모든 메서드가 다음 메서드로 이동하기 전에 고정된 값(terminal operation)을 반환한다.

#### `map()`
- 해당 Stream에 인자로 주어진 함수를 적용한 결과로 이루어진 Stream을 반환한다.
```Java
List number = Arrays.asList(2,3,4,5);
List square = number
	.stream()
	.map(x->x*x).collect(Collectors.toList());
```

#### `filter()`
- 인자로 전달된 Predicate에 따라 각각의 요소를 선택하는 데 사용된다.
```Java
List names = Arrays.asList("Reflection","Collection","Stream");
List result = names
	.stream()
	.filter(s->s.startsWith("S")).collect(Collectors.toList());
```

#### `sorted()`
- Stream 안의 요소들을 정렬하는 데 사용된다.
```Java
List names = Arrays.asList("Reflection","Collection","Stream");
List result = names
	.stream()
	.sorted().collect(Collectors.toList());
```

### 3.2 Terminate Operations
- 결과를 반환한다.
- 최종 결과 값을 반환하며, Intermediate Operation과 달리 더 이상 연속된 작업을 처리하지 않는다.

#### `collect()`
- Stream에서 수행된 결과를 반환한다.
```Java
List number = Arrays.asList(2,3,4,5,3);
Set square = number
	.stream()
	.map(x->x*x).collect(Collectors.toSet());
```

#### `forEach()`
- Stream의 각 요소들을 반복하는 데 사용된다.
- 부작용이 없도록 Stream이 수행한 계산 결과를 보고할 때만 이용해야 한다.
- 부작용이 없도록 연산/계산 자체에는 이용하지 말자.
```Java
List number = Arrays.asList(2,3,4,5);
number
	.stream()
	.map(x->x*x).forEach(y->System.out.println(y));
```

#### `reduce()`
- Stream의 요소를 단일 값으로 줄이는 데 사용된다.
- `reduce()` 메서드는 매개변수로 BinaryOperator를 받는다.
```Java
List number = Arrays.asList(2,3,4,5);
int even = number
	.stream()
	.filter(x->x%2==0)
	.reduce(0, (ans,i) -> ans+i); // ans 변수에 초기값으로 0을 할당하고, i를 더한다.
```

<br/>

## 4. Java Stream Interface Methods
---

| Method Syntax | Description |
| - | - |
| `allMatch()` | 모든 요소가 주어진 조건과 일치하는지 확인한다. |
| `anyMatch()` | 요소 중 하나 이상이 주어진 조건과 일치하는지 확인한다. |
| `builder()` | 비어 있는 상태의 `Builder`를 반환하여 Stream을 빌드한다. |
| `collect()` | 요소를 가져와 원하는 형태(Collection 등)로 반환한다. |
| `concat()` | 두 개의 Stream을 하나로 결합하여 새로운 Stream을 생성한다. |
| `count()` | Stream에 있는 요소의 개수를 반환한다. |
| `distinct()` | Stream에 있는 중복 요소를 제거한 새로운 Stream을 생성한다. |
| `empty()` | 비어 있는 Stream을 반환한다. |
| `filter()` | 주어진 조건에 따라 요소를 필터링한다. |
| `findAny()` | 임의의 요소를 반환한다. |
| `findFirst()` | 첫 번째 요소를 반환한다. |
| `flatMap()` | 각 요소를 다른 요소의 Stream으로 매핑하고, 이를 하나의 Stream으로 연결한다. |
| `flatMapToDouble()` | 각 요소를 double Stream으로 매핑하고, 이를 하나의 double Stream으로 연결한다. |
| `flatMapToInt()` | 각 요소를 int Stream으로 매핑하고, 이를 하나의 int Stream으로 연결한다. |
| `flatMapToLong()` | 각 요소를 long Stream으로 매핑하고, 이를 하나의 long Stream으로 연결한다. |
| `forEach()` | 각 요소에 대해 주어진 함수 및 동작을 실행한다. |
| `forEachOrdered()` | 각 요소에 대해 정해진 순서대로 함수 및 동작을 실행한다. |
| `generate()` | Supplier에서 생성된 요소를 사용하여 무한 요소를 생성한다. |
| `iterate()` | 초기 값 및 UnaryOperator를 사용하여 요소를 생성한다. |
| `limit()` | Stream의 요소 개수를 제한한다. |
| `map()` | 각 요소를 다른 형태로 변환하거나 특정 속성에 매핑한다. |
| `mapToDouble()` | 각 요소를 double로 매핑한다. |
| `mapToInt()` | 각 요소를 int로 매핑한다. |
| `mapToLong()` | 각 요소를 long으로 매핑한다. |
| `max()` | 최대 값을 반환한다. |
| `min()` | 최소 값을 반환한다. |
| `noneMatch()` | 모든 요소가 주어진 조건과 일치하지 않는지 확인한다. |
| `of()` | 주어진 요소로 Stream을 생성한다. |
| `peek()` | 각 요소에 대해 특정 함수 및 동작을 수행하고 원래 Stream을 반환한다. |
| `reduce()` | Stream의 요소를 줄여 하나의 값으로 반환한다. |
| `skip()` | 처음 n개의 요소를 건너뛴 새로운 Stream을 생성한다. |
| `sorted()` | 요소를 정렬한 새로운 Stream을 생성한다. |
| `toArray()` | 요소를 배열로 반환한다. |

<br/>

## 5. How to make good use of Stream
---
- 배열과 Stream 중 무엇을 사용해야 할지 모르겠다면, 둘 다 사용해 보고 좋은 것을 사용하자.
<br/>

- Stream 파이프라인에서 사용하는 모든 함수 객체에는 부작용이 없어야 한다.
	예를 들어, 연산 자체에 이용되는 함수가 아닌데 연산이나 계산에 이용해서는 안 된다.
<br/>

- Stream을 올바로 사용하려면 수집기(Collector)를 잘 알아야 한다.
	- java.util.stream.Collectors 클래스에서 자세한 내용을 확인할 수 있다.
	- Stream의 원소를 손쉽게 Collection으로 모을 수 있다.
	- 수집기가 생성하는 객체는 일반적으로 Collection이다.
	- 가장 중요한 수집기 팩토리는 `toList`, `toMap`, `groupingBy`, `joining`이다.
	```Java
	List<String> topTen = freq.keySet() // Map의 key 집합을 가져온다.
		.stream()                       // key 집합을 Stream으로 반환한다.
		.sorted(comparing(freq::get).reversed()) // Map 값에 따라 내림차순 정렬
		.limit(10)
		.collect(toList());
	```
<br/>

- 반환 타입으로는 (현재로서는) Stream보다 Collection을 권장한다.
	- 원소 sequence를 반환하는 메서드를 작성할 때 Stream/반복문 둘 다 고려했을 때 Collection이 낫다.
	- Collection을 반환하는 것이 불가능하면 Stream, Iterable 중 더 자연스러운 것을 반환하자.
	- 만약 나중에 Stream 인터페이스가 Iterable을 지원하게 되면 안심하고 Stream을 반환하자.
<br/>

- 올바른 계산과 성능에 확신이 없으면 Stream 파이프라인 병렬화는 시도하지 말자.
	- 병렬화를 잘못하면 프로그램이 오작동하거나 성능이 급격하게 떨어진다.
	- 병렬화를 도입하더라도 운영 코드에 바로 적용시키지 말자.
	- 병렬화를 도입하더라도 수정 후의 코드의 정확도와 성능지표를 유심하게 관찰하자.
	- 계산도 정확하고 성능도 좋아졌음이 확실할 때만 병렬화 버전을 운영 코드에 반영하자.

<br/>

## 6. References
---
- https://www.geeksforgeeks.org/stream-in-java/
- https://www.javatpoint.com/java-8-stream
- https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html
- https://hirlawldo.tistory.com/101

<br/>
