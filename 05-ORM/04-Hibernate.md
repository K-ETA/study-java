# ORM - Hibernate

<br/>

> **학습 목표**  
> - Hibernate가 무엇인지 설명할 수 있다.
> - Hibernate가 동작하는 흐름을 설명할 수 있다.

## 목차
[1. Hibernate란 무엇일까?](#1-hibernate란-무엇일까)  
[2. Hibernate는 어떻게 동작할까?](#2-hibernate는-어떻게-동작할까)  
[3. Hibernate는 주로 어디에 사용될까?](#3-hibernate는-주로-어디에-사용될까)  

<br/>

## 1. Hibernate란 무엇일까?

<img src="https://hibernate.org/images/hibernate-logo.svg" width="500" />

### 1.1 Hibernate의 개념
- 가장 많이 사용되는 Java 기반의 오픈 소스 객체-관계형 매핑 도구
- JPA의 인터페이스(Interface)의 구현체로, 내부적으로는 JDBC API를 사용한다.
- EJB 2.0* 스타일의 엔티티 빈(Entity Bean) 접근 방식에 대한 획기적인 대안으로 소개되었다.
- 객체 지향 도메인 모델을 웹 애플리케이션용 관계형 데이터베이스에 매핑하는 프레임워크를 제공한다.
- 객체-관계형 모델 매핑뿐만 아니라 데이터 쿼리(HQL, Hibernate Query Language) 및 복구 기능도 제공한다.
- 이벤트 기반으로 동작하며, 각 이벤트마다 Event Listener Group이 존재하고 기본으로 등록된 Listener가 존재한다.

```plain
*EJB 2.0: Enterprise JavaBeans의 이전 버전, 인터페이스를 통한 빈의 라이프사이클 관리 등의 기능이 포함된다.
```

### 1.2 Hibernate의 기능
- 자동 DDL이 지원됨에 따라 내부적으로 테이블 생성/삭제/변경 등이 수행된다.
- 자동 기본 키(Primary Key) 생성을 지원한다.
- 자동 트랜잭션 관리 기능을 제공한다.
- 특정 데이터베이스에 종속되지 않는 HQL(Hibernate Query Language)를 지원한다.
- 캐시 메모리를 지원하며, 캐싱 기능을 통해 데이터베이스 상호 작용을 간소화하고 최적화한다.

### 1.3 Hibernate의 장점
- 객채 지향적인 코드로 데이터베이스와 상호 작용할 수 있다.
- SQL 쿼리를 대신하여 객체 지향적인 코드를 작성함으로써 개발 생산성이 향상된다.
- 다양한 데이터베이스와 호환이 되며, 여러 종류의 데이터베이스를 함께 사용할 수 있다.
- 캐시를 통해 데이터베이스로의 반복적인 접근을 최소화하고 성능을 향상시킬 수 있다.
- ACID 트랜잭션*을 지원하며, 데이터베이스와의 일관성을 보장한다.
- 객체 지향 모델을 유지하면서 데이터베이스 스키마의 변경에 대응하기 쉽다.

```plain
*ACID 트랜잭션: Atomicity(원자성), Consistency(일관성), Isolation(고립성), Durability(지속성)을 의미하며, 트랜잭션을 정의하는 4가지의 중요한 속성/성질을 말한다.
```

### 1.4 Hibernate의 단점
- 처음 접할 경우 Hibernate를 학습하는 데 러닝 커브가 존재한다.
- 복잡한 쿼리를 작성하는 데에는 HQL 또는 Criteria API를 사용해야 하며, 이는 러닝 커브가 존재한다.
- 무분별한 사용이나 잘못된 설정, 최적화되지 않은 방식 등으로 인해 성능 저하 문제가 발생할 수 있다.
- 데이터베이스 종속성을 완전히 제거하지는 못한다.
- Hibernate 사용을 위한 추가적인 라이브러리 및 설정이 필요하며, 이로 인해 약간의 오버헤드가 발생할 수 있다.
- Hibernate는 지연 로딩을 위해 프록시 객체를 사용하므로, 이때 프록시와 관련된 문제가 발생할 수 있다.

<br/>

## 2. Hibernate는 어떻게 동작할까?
Hibernate는 크게 mapping 파일과 configuration 파일로 구성되어 있으며, Java 기반 애플리케이션과 데이터베이스가 존재하는 각 계층 사이에 존재하며 둘을 연결하는 역할을 한다.

<img src="https://user-images.githubusercontent.com/55049159/111074777-068caa00-8528-11eb-8b47-e13b846b0ed2.png" width="500" />

<img src="https://media.geeksforgeeks.org/wp-content/uploads/HBArchi.png" width="500" />

### 2.1 Hibernate의 구성 요소
#### 1) Configuration
- org.hibernate.cfg 패키지에 존재하는 클래스
- Hibernate 프레임워크를 활성화한다.
- 이때, mapping 파일과 configuration 파일 모두 읽는다.

```Java
// Hibernate 프레임워크를 활성화한다.
Configuration cfg = new Congiruation(); // org.hibernate.cfg

// mapping 파일과 cfg(configuration) 파일을 모두 읽는다.
cfg.configure();
```

이때, configuration 파일이 문법적으로 올바른지 확인하며, 유효하지 않은 경우 예외를 발생시킨다. 만약 유효하다면 메모리에 메타데이터를 생성하고, configuration 파일을 나타내는 객체에 생성된 메타데이터를 반환한다.

#### 2) SessionFactory
- org.hibernate 패키지에 존재하는 인터페이스
- 세션(Session) 객체를 생성하는 데 사용된다.
- 세션을 통해 데이터베이스와 연결 및 커뮤니케이션한다.
- 본질적으로 불변한 인터페이스이며, 스레드 안전성(thread-safe)을 보장한다.

```Java
// 위에서 `Configuration` 클래스로 생성한 `cfg` 객체에 있는 메타데이터를 수집한다.
// `cfg` 객체에서 JDBC 정보를 가져와 JDBC 연결을 생성한다.
SessionFactory factory = cfg.buildSessionFactory();
```

#### 3) Session
- org.hibernate 패키지에 존재하는 인터페이스
- SessionFactory 객체를 기반으로, 즉 팩토리를 기반으로 생성된다.
- Hibernate 프레임워크를 통해 데이터베이스와의 Connection 및 Session을 연다.
- 경량 객체이며, 스레드 안정성을 보장하지 않는다.
- 주로 CRUD 작업을 수행하는 데 사용된다.

```Java
Session session = factory.buildSession();
```

#### 4) Transaction
- 트랜잭션 객체는 어떤 작업을 수행하고 그 작업에 따라 데이터베이스 변경이 있을 때마다 사용된다.
- 트랜잭션 객체는 `commit()` 메서드를 사용하여 변경 사항을 영구적으로 데이터베이스에 저장할 수 있다.

```Java
Transaction tx = session.beginTransaction();
tx.commit();
```

#### 5) Query
- org.hibernate 패키지 안에 존재하는 인터페이스
- 쿼리 인스턴스는 `Session.createQuery()` 메서드를 호출하여 생성할 수 있다.
- 조회(`find()`), 반복문(`iterate()`) 등 다양한 기능을 제공한다.
- 결과 집합의 특정 페이지를 선택하기 위해서는 `setMaxResult()`, `setFirstResult()`를 호출하면 된다.
- 명명된 쿼리 매개변수를 사용할 수 있다.

#### 6) Criteria
- Criteria 객체를 구성하여 엔티티를 검색하기 위해 간소화된 API
- 위에서 설명한 Session은 Criteria의 팩토리이다.
- Criteria 인스턴스는 일반적으로 제한된 팩토리 메서드를 통해 가져온다.

### 2.2 Hibernate 동작 흐름

아래 그림의 시스템에서 데이터베이스에 객체를 삽입하는 상황을 예시로 들어 보자. Hibernate가 어떻게 객체를 데이터베이스에 저장하거나 혹은 데이터베이스에서 어떻게 객체를 검색하는지를 계층 및 흐름과 함께 이해해 보자.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/Untitled-66.png" width="500" />

#### ① 영속성 로직을 포함한 클래스를 생성한다.
1. 먼저, 데이터베이스에 특정 작업을 수행하기 위한 영속성 로직을 가진 클래스를 생성한다.
2. 영속성 로직을 작성한 다음에는, 해당 영속성 로직을 작성한 특정 클래스의 객체를 생성한다.

#### ② 영속성 로직이 포함된 클래스를 대상으로 Hibernate 프레임워크가 추상화 작업을 수행한다.
1. 영속성 로직이 포함된 클래스를 대상으로 Hibernate 프레임워크가 일부 추상화 작업을 수행한다.
2. 이후, Hibernate 프레임워크는 그 아래에 있는 계층의 도움으로 영속성 로직을 수행해야 한다.

#### ③ Hibernate 프레임워크가 JDBC 등과 상호 작용하여 영속성 로직을 수행하기 위한 준비를 마친다.
Hibernate 프레임워크는 JDBC, JNDI, JTA 등과 상호 작용하여 영속성 로직을 수행하기 위해 데이터베이스로 이동한다.

#### ④-⑤ Hibernate 프레임워크가 데이터베이스와 상호 작용을 한다.
- Hibernate 프레임워크는 JDBC 드라이버의 도움으로 데이터베이스와 상호 작용한다.
- 이때, 영속성 로직이 수행되며 이는 CRUD 연산에 불과하다.
- 만약, 영속성 로직이 데이터베이스에 있는 값을 검색하는 것이라면 역순으로 Java 애플리케이션 콘솔의 객체 측면에서 표시된다.

<br/>

## 3. Hibernate는 주로 어디에 사용될까?
- 대규모 엔터프라이즈 애플리케이션에서 많이 사용된다.
- 복잡한 비즈니스 로직과 다양한 데이터베이스 연동이 필요한 경우에 적합하다.
- 여러 웹 애플리케이션 프레임워크(예시: Spring 등)와 통합이 용이하다.
- 프로젝트의 규모에 상관없이 사용 가능하다.
- Play Framework 기반의 웹 애플리케이션 개발 시 기본 ORM 프레임워크로 사용된다.

<br/>
