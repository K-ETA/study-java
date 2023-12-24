# ORM

<br/>

> **학습 목표**  
> - ORM이 무엇인지 설명할 수 있다.
> - ORM을 사용하는 이유를 설명할 수 있다.
> - ORM의 종류를 설명할 수 있다.

<br/>

## 목차
[1. 영속성(Persistence)이란?](#1-영속성persistence이란)  
[2. ORM(Object Relational Mapping)이란?](#2-ormobject-relational-mapping이란)  
[3. ORM의 장점](#3-orm의-장점)   
[4. ORM의 단점](#4-orm의-단점)  
[5. ORM과 RDBMS의 차이점](#5-orm과-rdbms의-차이점)  

<br/>

## 1. 영속성(Persistence)이란?
### 영속성(Persistence)
- 데이터를 생성한 애플리케이션이 종료되어도 사라지지 않는 데이터의 특성
- 영속성을 가지지 않은 데이터는 메모리 상에서만 존재하므로 애플리케이션이 종료되면 사라지는 휘발성을 가진다.
- 즉, 데이터에 영속성을 부여한다는 것은 해당 데이터를 영구적으로 저장한다는 의미이다.

### 객체 영속성(Object Persistence)
- 애플리케이션에서 생성된 데이터를 가진 객체에 영속성을 부여함으로써 애플리케이션이 종료되어도 사라지지 않도록 한다.
- 데이터를 가진 객체에 영속성을 부여하기 위해서는 파일, 데이터베이스에 해당 객체 데이터를 저장해야 한다.
- 그렇다면, 데이터를 데이터베이스에 저장하는 방법에는 어떤 것이 있을까?
  1. JDBC (Java)
  2. Spring JDBC (예시: JdbcTemplate)
  3. Persistence Framework (예시: Hibernate, MyBatis 등)

### 영속 계층(Persistence Layer)
- 애플리케이션의 아키텍처 중 데이터에 영속성을 부여해 주는 계층
- Persistence Layer를 구현하는 방법은 다음과 같다.
  1. JDBC
  2. Persistence Framework (주로 Persistence Framework를 많이 이용한다.)

### 영속성 프레임워크(Persistence Framework)
- JDBC가 가진 복잡함을 최소화하여 간단한 작업만으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있다.
- Persistence Framework는 SQL Mapper와 ORM으로 구분된다.
  1. SQL Mapper (예시: iBatis, MyBatis, Oracle SQLJ 등)
  2. ORM (예시: JPA, Hibernate 등)

<br/>

## 2. ORM(Object Relational Mapping)이란?
- ORM = Object Relational Mapping(객체-관계 매핑)
- Persistent API라고도 불린다. (예시: JPA, Hibernate 등)
- 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑한다.
- 객체 간의 관계를 바탕으로 SQL을 자동으로 생성한다.
- SQL 쿼리 없이도 데이터베이스의 데이터를 조작할 수 있다.
- 내부적으로 JDBC API를 사용하여 데이터베이스와 상호 작용한다.

<img src="https://www.javatpoint.com/images/hibernate/orm.jpg" width="500" />

| 객체 지향 프로그래밍(Object Oriented Programming) | 관계형 데이터베이스(RDB, Relational Database) |
| :---: | :---: |
| 클래스(Class) | 테이블(Table) |
| 필드(Field) | 컬럼(Column) |

위의 표는 ORM이 매핑하는 각각 객체 모델과 관계형 모델의 요소를 나타낸 것이다. 이렇듯 객체 지향 프로그래밍의 객체 모델과 관계형 데이터베이스의 관계형 모델을 연결하여 객체 모델을 통해 관계형 모델을 자동으로 생성해 주는 것이 바로 ORM이다.

<br/>

## 3. ORM의 장점
**1. 객체 지향 프로그래밍으로 더 직관적인 코드를 작성할 수 있다.**
- SQL 쿼리가 아닌 프로그래밍 언어로 코드를 작성하여 데이터를 조작할 수 있다.
- 각종 객체에 대한 코드를 별도로 작성하기 때문에 코드의 가독성을 올려준다.

**2. 비즈니스 로직에 더 집중할 수 있도록 도와준다.**
- SQL의 절차적이고 순차적인 접근이 아닌 객체 지향적인 접근으로 생산성을 증가시킨다.
- SQL 쿼리를 잘 알지 못하더라도 개발 중인 프로그래밍 언어와 ORM에 대한 이해만 어느 정도 갖고 있다면 개발이 가능하다.

**3. 재사용 및 유지 보수의 편리성이 증가한다.**
- ORM은 독립적으로 작성되며, 작성된 객체들을 재활용 할 수 있다.
- 재활용성이 높아 모델에서 가공된 데이터를 컨트롤러에 의해 뷰와 합쳐지는 형태로 디자인 패턴을 견고하게 다질 수 있다.
- 매핑 정보가 정확하며, ERD를 보는 것에 대한 의존도를 낮출 수 있다.

**4. DBMS(Database Management System)에 대한 종속성이 줄어든다.**
- 객체 간의 관계를 바탕으로 SQL을 자동 생성하므로 객체 모델과 관계형 모델의 간격을 좁힐 수 있다.
- 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적 적은 리스크와 시간이 소요된다.

<br/>

## 4. ORM의 단점
**1. 오직 ORM으로만 서비스를 구현하기는 힘들다.**
- 사용하기는 편하지만, 설계는 매우 신중해야 한다.
- 프로젝트의 복잡성이 커질 경우 난이도 또한 증가할 수 있다.
- 잘못 구현된 경우 속도 저하 및 심각할 경우 일관성이 무너질 수 있다.
- 일부 자주 사용되는 대형 쿼리는 속도를 위해 별도의 튜닝이 필요한 경우가 있다.

**2. 프로시저(Procedure)가 많은 시스템에서는 ORM의 객체 지향적인 장점을 활용하기가 어렵다.**
- 이미 프로시저가 많은 시스템에선 다시 객체로 바꿔야 하며, 그 과정에서 생산성 저하 등 리스크가 발생할 수 있다.

**3. ORM 라이브러리를 별도로 공부해야 한다.**
- 프로젝트의 프로그래밍 언어뿐만 아니라 ORM 라이브러리 문법을 따로 학습해야 한다. 즉, 언어는 같은 것을 사용하지만, 프로그래밍 언어의 문법과 ORM의 문법은 별개이다.

**4. 정확한 원리를 이해하지 않고도 사용할 수 있기 때문에 문제 대처 능력이 저하될 수 있다.**
- ORM의 기본 원리와 SQL의 이해도 없이도 사용할 수 있다는 장점으로 인해 오히려 문제 대처 능력이 떨어질 수 있다는 문제점이 발생할 수 있다.

<br/>

## 5. ORM과 RDBMS의 차이점
| 차이점 | 설명 |
| :---: | :--- |
| Granularity<br/>(세분성) | 경우에 따라 데이터베이스의 테이블보다 더 많은 클래스를 가진 객체 모델을 가질 수 있다. |
| Inheritance<br/>(상속) | RDBMS(Relational Database Management System)는 객체 지향 프로그래밍이 가진 상속이라는 개념이 존재하지 않는다. |
| Identity<br/>(일치) | RDBMS(Relational Database Management System)에서는 PK(Primary Key)가 같으면 서로 동일한 레코드(Record)로 정의하지만, 객체 지향 언어 중 하나인 Java에서는 주소 값이 같거나(`a == b`) 내용이 같은 경우(`a.equals(b)`)를 구분하여 정의한다. |
| Associations<br/>(연관성) | RDBMS(Relational Database Management System)는 외래키(Foreign Key)를 이용하여 연관성을 정의하는 반면, 객체 지향 언어는 객체 참조(Reference)를 사용하여 연관성을 정의한다.<br/><br/>RDBMS는 외래키(Foreign Key)와 SQL JOIN을 통해 각 테이블 간의 데이터 연결을 정의하며, 방향성을 가지고 있지 않다(Direction Less). 반면, 객체 지향 언어는 연관성을 정의할 때 방향성을 가지며(Directional), 양방향 관계가 필요한 경우 연관성을 각각 클래스에서 두 번 정의해야 한다.<br/><br/>- One-to-One Relationship(1:1 매핑)<br/>- One-to-Many Relationship(1:N 매핑)<br/>- ... |
| Navigation<br/>(탐색/순회) | RDBMS(Relational Database Management System)에서는 일반적으로 SQL JOIN을 사용하는 반면, 객체 지향 언어에서는 그래프 형태로 하나의 객체에서 다른 객체로 이동하면서(예시: `a.getB().getC()`) 탐색 및 순회한다. |

<br/>
