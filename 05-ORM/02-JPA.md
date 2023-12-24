# ORM - JPA

<br/>

> **학습 목표**  
> - JPA가 무엇인지 설명할 수 있다.
> - JPA 내부 구조 및 원리를 이해할 수 있다.

<br/>

## 목차
[1. JPA란 무엇일까?](#1-jpa란-무엇일까)  
[2. JPA는 어떻게 동작할까?](#2-jpa는-어떻게-동작할까)
[3. JPA는 주로 어디에 사용될까?](#3-jpa는-주로-어디에-사용될까)   

<br/>

## 1. JPA란 무엇일까?

<img src="https://blog.kakaocdn.net/dn/cYta7d/btrLF4Iytyb/hBJxHuc15KFsp5EkOvwMN1/img.png" width="300" />

### 1.1 JPA의 개념
- JPA는 Java Persistence API의 약자이다.
- Java에서 사용하는 표준 ORM(Object Relational Mapping) 기술
- Java에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스(Interface)
- JPA는 인터페이스(Interface)이므로, 실제로 개발에 사용하기 위해서는 ORM 프레임워크를 선택해야 한다.

| 버전 | 날짜 | 설명 |
| :---: | :---: | :--- |
| JPA 1.0 (JSR* 220) | 2006년 5월 | - 초기 버전<br/>- 복합 키와 연관 관계 기능 부족 |
| JPA 2.0 (JSR 317) | 2009년 12월 | - 대부분의 ORM 기능 포함<br/>- JPA Criteria API* 추가<br/>- Annotation 도입<br/>- 표준 쿼리 언어 지원(JPQL, JPA Query Language) 향상<br/>- 네이티브 쿼리 사용 가능 |
| JPA 2.1 (JSR 338) | 2013년 5월 | - 스토어드 프로시저, 컨버터, 엔티티 그래프 기능 추가 |
| JPA 2.2 (JSR 338) | 2017년 8월 | - Java 8 지원<br/>- 같은 타입의 Annotation을 여러 번 사용할 수 있는 기능 추가<br/>- `@ElementCollection`을 사용한 값 타입 컬렉션에 대한 매핑 향상 |
| JPA 2.2.1 (JSR 338) | 2018년 3월 | 버그 수정 및 소프트웨어 업데이트 |

```
*JSR(Java Specification Request): Java Community Process(JCP)에서 정의된 Java 명세서
*JPA Criteria API: 동적 쿼리 작성을 지원한다.
```

### 1.2 JPA의 기능
- JPA는 Java 애플리케이션에서 관계형 데이터를 관리할 수 있는 객체/관계형 매핑 기능을 제공한다.
- 객체-관계형 모델 간의 패러다임 불일치 문제를 개발자 대신 해결한다.
- 상속(Inheritance), 다형성(Polymorphism), 다형성 쿼리를 지원한다.
- 매핑(객체-관계형 데이터베이스)을 정의하기 위한 메타데이터 Annotation/XML descriptor를 지원한다.
- 정적/동적 쿼리 등 SQL과 유사한 풍부한 쿼리 언어를 지원한다.
- 성능 튜닝을 위해 2가지의 캐시(1단계, 2단계)를 통한 캐싱 기능을 지원한다.
- Hibernate, MyBatis 등을 지원한다.

### 1.3 JPA의 장단점
#### 1) JPA의 장점
- Java 진영에서 표준으로 사용되는 API로서 ORM 프레임워크 간의 비교적 쉬운 이식성을 제공한다.
- 객체-관계형 모델 매핑을 쉽게 처리하도록 도움으로써 패러다임 불일치를 해결한다.
- 객체 지향 쿼리 언어(JQPL)를 통해 SQL과 별도로 객체를 대상으로 쿼리할 수 있다.
- 데이터베이스 종속성을 감소시키고, 코드가 덜 복잡해짐에 따라 유지 보수가 용이해진다.
- 지연 로딩(Lazy Loading), 즉시 로딩(Eager Loading)을 지원하여 성능 최적화 및 상황에 맞는 전략을 선택할 수 있다.
- 지루하고 반복적은 CRUD용 SQL을 개발자가 직접 작성하지 않아도 되므로 생산성을 향상시킨다.

#### 2) JPA의 단점
- ORM의 개념 및 JPA의 기능을 학습해야 하므로 학습 곡선이 존재한다.
- 매우 복잡하거나 대량의 데이터를 다룰 때 성능에 안 좋은 영향을 줄 수 있다.
- 복잡한 쿼리나 성능 최적화가 필요한 경우에는 JPA 기능만으로는 불가능하며 네이티브 쿼리를 사용해야 한다.
- 특정 비즈니스 요구 사항에 따라 유연한 매핑이 필요한 경우 JPA만으로는 복잡할 수 있다.

### 1.4 JPA와 MyBatis의 차이점
| 구분 | JPA(Java Persistence API) | MyBatis |
| :---: | :---: | :---: |
| 분류 | ORM(Object Relational Mapping) | SQL Mapper |
| 설명 | 객체-관계형 모델 매핑 | 객체-SQL 매핑 |
| 특징 | 객체와 테이블을 매핑만 하면 ORM 프레임워크가 SQL을 만들어서 데이터베이스와 관련된 처리를 해준다. 따라서 개발자가 직접 SQL 쿼리를 작성할 필요가 없다. | SQL과 매핑할 객체를 지정한 후, SQL Mapper가 JDBC API 사용과 응답 결과를 객체로 매핑한다. 하지만, 개발자가 직접 SQL 쿼리를 작성해야 한다. (SQL 의존적인 개발) |

<br/>

## 2. JPA는 어떻게 동작할까?

<img src="https://images.velog.io/images/blackbean99/post/42444e7e-826d-4d65-86a8-bf9535de15f9/image.png" width="500" />

### 2.1 JPA 구성 요소
#### 1) Persistence Context(영속성 컨텍스트)
- JPA의 내부 흐름 또는 동작 원리 그 자체를 의미한다. 즉, 논리적인 개념에 가깝다.
- Entity를 영구 저장하는 환경을 의미한다.
- Entity Manager에 의해 Entity를 저장/조회하는 경우 Entity Manager는 Persistence Context에 Entity를 저장/관리한다.
- Entity Manager를 통해 Persistence Context에 접근/관리할 수 있다.
- 물론, 여러 Entity Manager가 같은 Persistence Context에 접근할 수도 있다.

#### 2) Entity(엔티티)
##### (1) Entity의 개념
- 데이터베이스에 존재하는 하나의 테이블(Table)을 클래스(Class)로 구현한 것
- 데이터베이스 테이블의 컬럼(Column)과 대응하는 필드(Field)를 가진 클래스
- Entity 객체를 Entity라고 부른다.

##### (2) Entity의 생명주기(Lifecycle)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCgyiI%2FbtrvuPaRU6q%2FvwPry29ROM8yZe8I1tMMJ1%2Fimg.png" width="500" />

1) Transient(new, 비영속 상태)
   - Entity가 생성된 후, Entity Manager에게 등록되지 않은 상태
   - Entity가 Persistence Context에 저장되지 않은 상태
  ```Java
  public class Jpa {
    public static void main(String[] args) {
        Member memberA = new Member();
        memberA.setId("A");
        memberA.setName("memberA");
    }
  }
  ```
  <img src="https://velog.velcdn.com/images/chlgustjr/post/d188471a-9de3-4858-8c42-f44e3c07a472/image.png" width="300" />

2) Managed(영속 상태)
   - Entity가 Persistence Context에 등록된 상태
   - Entity가 Persistence Context에 의해 관리되는 상태
   - 1차 캐시 내부에 Entity의 값이 기록되어 있는 경우
   - Transient 상태에서 `EntityManager.persist()` 메서드를 사용할 경우 Managed 상태가 된다.
   - 이미 저장된 데이터의 경우 `EntityManager.find()` 메서드를 통해 Managed 상태가 된다.
   - 단, Managed 상태가 되었다고 데이터베이스에 바로 저장되는 것은 아니다. `commit()` 메서드를 호출하여 하나의 트랜잭션이 완전히 종료된 시점에 데이터베이스에 저장된다.
  ```Java
  public class Jpa {
    public static void main(String[] args) {
        Member memberA = new Member();
        memberA.setId("A");
        memberA.setName("memberA");

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPA");
        EntityManager em = emf.createEntityManager();

        // 트랜잭션 시작
        em.getTransaction.begin();

        // Persistence Context에 Entity를 저장함으로써 Managed 상태가 된다.
        em.persist(memberA);
    }
  }
  ```

  <img src="https://velog.velcdn.com/images/chlgustjr/post/5f52d65f-972f-4ed1-8f81-2095d63122e6/image.png" width="300" />

3) Detached(준영속 상태)
   - Entity가 Persistence Context에 한 번 저장되었다가 분리된 상태
   - Persistence Context에 의해 관리되던 Entity가 Persistence Context로부터 분리되어 더 이상 관리를 받지 않는 상태
   - Detached 상태의 Entity는 Persistence Context가 제공하는 기능을 사용할 수 없다.
     - 식별자 값을 가진 Transient 상태에게 가깝다. (단, Transient 상태는 식별자 값이 없다.)
     - 지연 로딩(Lazy Loading)을 사용할 수 없다.
   - Managed -> Detached 상태로 만드는 방법은 크게 3가지이다.
     1. `em.detach(entity)`: 특정 Entity만 준영속 상태로 전환한다.
     2. `em.clear()`: Persistence Context를 완전히 초기화한다.
     3. `em.close()`: Persistence Context를 종료한다. (주로 사용)
  - Detahced -> Managed 상태로 만드는 방법은 병합(`merge()`)을 사용하는 것이다.
    - `member = em.merge(member);`
    - 병합(`merge()`)은 Transient -> Managed 상태로의 전환도 가능하다.
  ```Java
  public class Jpa {
    public static void main(String[] args) {

        // [=> Transient] Entity 생성
        Member memberA = new Member();
        memberA.setId("A");
        memberA.setName("memberA");

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPA");
        EntityManager em = emf.createEntityManager();

        // 트랜잭션 시작
        em.getTransaction.begin();

        // [=> Managed] Entity를 Persistence Context에 등록
        em.persist(memberA);

        // [=> Detached] Entity를 Persistence Context에서 분리
        em.detach(memberA);
    }
  }
  ```
1) Removed(삭제 상태)
   - 데이터베이스에 저장된 Entity가 삭제된 상태
   - 즉, 데이터베이스로부터 삭제된 Entity의 상태
  ```Java
  // Entity 객체를 삭제한다.
  em.remove(memberA);
  ```


#### 3) Entity Manager(엔티티 매니저)
##### (1) Entity Manager의 개념
- Entity 구현체, 즉 Entity 객체의 생명 주기를 관리한다.
- Entity와 Persistence Context 사이에 존재하며, Entity 객체를 영속성 컨텍스트(Persistence Context)에 저장하여 관리한다.
- Entity를 데이터베이스에 등록/수정/삭제/조회할 수 있다.
- 데이터베이스 Connection과 밀접한 관계가 있으므로 스레드 간에 공유하거나 재사용하면 안 된다.
- Entity Manager는 [persistence.xml](#1-persistencexml-설정) 설정 정보를 사용하여 생성된 Entity Manager Factory로부터 생성된다.

```plain
*Entity Manager Factory: 애플리케이션 전체에서 딱 한 번만 생성하고 공유해서 사용해야 한다.
```

```Java
import java.persistence.*;
// ...

public class Jpa {
    public static void main(String[] args) {
        // Entity Manager Factory 생성
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("jpa");
        
        // Entity Manager 생성
        EntityManager em = emf.createEntityManager();

        // 트랜잭션 획득
        EntityTransaction tx = em.getTransaction();

        try {
            // 트랜잭션 시작
            tx.begin()

            // 비즈니스 로직 실행

            // 트랜잭션 커밋
            tx.commit();

        } catch(Exception e) {
            // 트랜잭션 롤백
            tx.rollback();

        } finally {
            // Entity Manager 종료
            // 사용이 끝난 경우 반드시 종료해야 한다.
            em.close();

        }

        // Entity Manager Factory 종료
        // 애플리케이션을 종료할 때 반드시 종료해야 한다.
        emf.close();
    }
}
```

##### (2) Entity Manager의 역할
**1. Entity Manager는 Entity와 Persistence Context 사이에 위치한다.**
- Entity 객체 데이터를 Persistence Context에 바로 저장하면 데이터 후처리를 진행할 수 없으므로 중간 위치에 존재한다.

**2. Entity를 Persistence Context에 등록/저장한다.**
- Entity를 Persistence Context에 등록/저장한다.

##### (3) Entity Manager + Persistence Context의 기능
📌 아래부터는 EntityManager를 통해 Persistence Context에 접근할 수 있기 때문에 갖는 기능이다.  
📌 즉, Persistence Context가 가진 기능이다.  

**1. 1차 캐시를 가지고 있다.**
- Entity Manager를 통해 Entity를 Persistence Context에 등록하면 1차 캐시에 등록된다.
- Entity Manager는 하나의 트랜잭션이 시작하면서 생성되고 종료되면서 삭제된다.
  - 따라서 1차 캐시는 하나의 트랜잭션 안에서만 사용된다.
  - 참고로, 애플리케이션 전체가 공유하는 캐시는 2차 캐시이다.
- Entity Manager를 통해 Entity를 조회하는 경우 데이터베이스를 조회하기 전에 1차 캐시를 우선 조회한다.
  - 1차 캐시를 우선 조회하는 경우 응답 속도가 훨씬 빨라진다.
- 만약 1차 캐시에 존재하지 않는 다른 Entity를 조회하는 경우, 1차 캐시를 조회한 후 데이터베이스에 접근하여 조회한다.
  - 이후 데이터베이스에서 반환된 값을 EntityManager의 1차 캐시에 저장한 후, 클라이언트에게 반환한다.
```Java
public class Jpa {
    public static void main(String[] args) {
        Member member1 = new Member();
        member1.setId("member1");
        member1.setName("member1");

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPA");
        EntityManager em = emf.createEntityManager();

        em.getTransaction().begin();
        em.persist(member1);

        // Entity Manager의 1차 캐시에서 Entity를 조회한다.
        em.find(member1);
    }
}
```

<img src="https://velog.velcdn.com/images/chlgustjr/post/96588125-ad44-45b9-9c76-8b9cfa5e3827/image.PNG" width="500" />

<img src="https://velog.velcdn.com/images/chlgustjr/post/89445d32-9014-4709-ad65-3b73bf6e95ad/image.PNG" width="500" />

**2. 영속된 Entity의 동일성을 보장한다.**
- Entity Manager는 소속된 트랜잭션과 동일한 생명주기를 가진다.
- 하나의 트랜잭션 안에서 동일한 객체를 여러 번 조회하면 이를 같은 값으로 처리한다.
- 데이터베이스가 아닌 Entity Manager의 1차 캐시에서 객체를 조회하기 때문에 동일성이 보장되는 것이다.
```Java
public class Jpa {
    public static void main(String[] args) {
        Member memberA = new Member();
        memberA.setId("A");
        memberA.setName("memberA");

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPA");
        EntityManager em = emf.createEntityManager();

        em.getTransaction().begin();
        em.persist(memberA);

        Member a = em.find(memberA);
        Member b = em.find(memberA);

        // Java에서 a와 b는 서로 다른 주소 값을 가진 다른 객체이지만,
        // JPA는 하나의 트랜잭션 안에서 조회되는 동일한 객체에 대해서 같은 객체로 처리한다. 즉, 동일성이 보장된다.
        System.out.println(a == b); // true
    }
}
```

**3. 쓰기 지연**
- `commit()` 메서드를 통해 하나의 트랜잭션을 완전히 종료하기 전까지 EntityManager는 객체를 데이터베이스에 저장하지 않는 기능
- 쓰기 지연을 통해 데이터베이스에 접근하는 횟수를 줄임으로써 서비스 또는 시스템의 부하를 감소시킬 수 있다.
- 데이터베이스에서 한 번의 커밋은 하나의 트랜잭션을 의미한다.
- 다수의 쿼리를 묶어서 한 번에 커밋하는 기능으로 JDBC Batch가 있으며, Hibernate에는 hibernate.jdbc.batch_size 옵션을 이용하여 설정할 수 있다. (persistence.xml에 설정)

<img src="https://velog.velcdn.com/images/chlgustjr/post/d8e59a4f-682b-4dc4-915d-18a23ab61d4e/image.PNG" width="500" />

<img src="https://velog.velcdn.com/images/chlgustjr/post/e6bd00a8-f964-4f8c-8fa3-0bb5cfb95dde/image.PNG" width="500" />

**4. Entity 수정 및 변경 감지(Direct Checking)**
- 데이터베이스의 데이터를 객체처럼 다루기 때문에 Java Collection에 데이터를 삽입/삭제하는 것처럼 데이터베이스의 데이터를 조작한다.
- 따라서 한 번 Persistence Context에 등록되어 데이터베이스에 저장된 객체는 그 값을 변경해도 `persist()`를 해주지 않아도 된다.
```Java
public class Jpa {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPA");
        EntityManager em = emf.createEntityManager();
        EntityTransaction transaction = em.getTransaction();

        transaction.begin();

        // 데이터베이스에 저장된 member A를 조회한다.
        // 데이터베이스에서 조회한 시점에 데이터베이스로부터 반환된 값이 1차 캐시에 저장된다. (snapshot 속성에 값과 함께 저장된다.)
        Member memberA = em.find(Member.class, "A");

        memberA.setName("Changed");

        // 1. `transaction.commit()` 호출 시 데이터베이스에 쿼리를 전달하기 전에 내부적으로 `flush()`가 호출된다.
        // 2. `flush()` 호출 시 `memberA` 객체 값과 1차 캐시에 저장된 snapshot을 비교하여 데이터의 변경을 감지한다.
        // 3. 데이터의 변경이 감지된 경우 UPDATE 쿼리를 실행한 후, 쓰기 지연 SQL 저장소에 저장한다.
        // 4. 이후 쓰기 지연 SQL 저장소에 쌓인 쿼리를 데이터베이스에 전달한다.
        transaction.commit();
    }
}
```

<img src="https://velog.velcdn.com/images/chlgustjr/post/60338415-7c7f-4e9b-837e-229d21fb7b51/image.png" width="500" />

#### 4) `flush()`
##### (1) `flush()`의 개념
- Persistence Context의 변경 내용을 데이터베이스에 반영/동기화한다.
- Persistence Context가 가지고 있는 SQL을 데이터베이스에 전달한다.

##### (2) `flush()`의 역할
- 변경 감지(Direct Checking)
- 변경된 Entity의 내용을 쓰기 지연 SQL 저장소에 등록
- 쓰기 지연 SQL 저장소에 등록되어 있는 쿼리를 데이터베이스에게 전달한다.

##### (3) `flush()` 사용 방법
1. 직접 호출 방법
  ```Java
  EntityManager.flush();
  ```
2. 트랜잭션 커밋 시 자동 호출
  ```Java
  EntityTransaction.commit();
  ```
3. JPQL 쿼리 실행 시 자동 호출
  ```Java
  EntityTransaction.createQuery();
  ```

참고로, `flush()`를 자동으로 실행시키는 것과 관련한 설정을 Entity Manager에 지정할 수 있다. 이를 "Entity Manager에 Flush Mode를 지정한다."라고 한다. Flush Mode를 별도로 설정하지 않으면 자동으로 호출된다.
```Java
// javax.persistence.FlushModeType
// FlushModeType.AUTO: 커밋이나 쿼리를 실행할 때 호출 (기본 값)
// FlushModeType.COMMIT: 커밋할 때만 호출
em.setFlushMode(FlushModeType.COMMIT);
```

#### 5) JPQL(java Persistence Query Language)
##### (1) JPQL 등장 배경
- 예를 들어, 애플리케이션이 필요한 데이터만 데이터베이스에서 불러오려면 검색 조건이 포함된 SQL을 사용해야 한다.
- 이러한 문제를 JPA는 JPQL이라는 쿼리 언어로 해결한다.

##### (2) JPQL의 개념
- SQL을 추상화한 객체 지향 쿼리 언어
- JPQL은 데이터베이스의 테이블을 전혀 알지 못한다.
- SQL 문법과 거의 유사해서 SELECT, FROM, WHERE, GROUP BY, HAVING, JOIN 등을 사용할 수 있다.
- SQL은 데이터베이스 테이블을 대상으로 쿼리하는 반면, JPQL는 Entity 객체를 대상으로(클래스, 필드) 쿼리한다.
- SQL과 달리 대소문자를 명확하게 구분한다.
- 예시) `SELECT M.ID, M.NAME, M.AGE FROM MEMBER M`

```Java
// 1. 쿼리 객체를 생성한다.
em.createQuery(JPQL, 반환 타입);

// 쿼리 객체의 `getResultList()` 메서드를 호출한다.
```

<br/>

### 2.2 JPA 동작 원리
#### 1) persistence.xml 설정
- JPA는 persistence.xml 파일을 사용해서 필요한 설정 정보를 관리한다.
- persistence.xml 파일은 META-INF/persistence.xml classpath 경로에 있으면 별도의 설정 없이도 JPA가 인식할 수 있다.
```XML
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.1">
    <persistence-unit-name="jpa"> <!-- 고유한 이름 사용자 설정 -->

        <!-- 옵션 -->
        <!-- JPA가 자동으로 Entity를 인식하지 못하는 경우 명시적으로 작성해줄 수 있다. -->
        <class>jpa.entity.Member</class>

        <properties>
            <!-- 필수 속성 (사용자 설정) -->
            <property name="hibernate.persistence.jdbc.driver" value="JDBC 드라이버" />
            <property name="hibernate.persistence.jdbc.user" value="데이터베이스 접속 아이디" />
            <property name="hibernate.persistence.jdbc.password" value="데이터베이스 접속 비밀번호" />
            <property name="hibernate.persistence.jdbc.url" value="데이터베이스 접속 URL" />

            <!-- 옵션 -->
            <!-- Hibernate가 실행한 SQL을 출력한다. -->
            <property name="hibernate.show_sql" value="true" />

            <!-- Hibernate가 실행한 SQL을 출력할 때 보기 쉽게 정렬한다. -->
            <property name="hibernate.format_sql" value="true" />

            <!-- 쿼리 출력 시 주석도 함께 출력한다. -->
            <property name="hibernate.use_sql_comments" value="true" />

            <!-- JPA 표준에 맞춘 새로운 키 생성 전략을 사용한다. -->
            <property name="hibernate.id.new_generator_mapping" value="true" />

            <!-- ... --->
```
- 위에서 `<persistence-unit>`은 일반적으로 연결할 데이터베이스당 하나의 Persistence Unit을 등록한다.
- 위에서 데이터베이스 방언* 문제를 해결하기 위해 Hibernate를 포함한 대부분 JPA 구현체들은 다양한 데이터베이스 방언 클래스를 제공한다.

```plain
*데이터베이스 방언(Dialect): JPA에서 SQL 표준을 지키지 않거나 특정 데이터베이스만의 고유한 기능을 가리키는 말
```

## 3. JPA는 주로 어디에 사용될까?
### 3.1 JPA를 사용하면 좋은 경우
- 데이터베이스와의 효과적인 상호 작용이 필수적인 경우
- 데이터베이스의 액세스를 간소화하고 싶은 경우
- 객체 지향적인 프로그래밍 모델을 유지하면서 데이터베이스와 상호 작용해야 하는 경우
- 프로토타이핑 및 빠른 개발 단계에서 생산성을 높이고 싶은 경우
- ...

### 3.2 JPA가 주로 사용되는 경우
- 웹 애플리케이션 개발 (예시: Spring, Java EE, Jakarta EE 웹 프레임워크 등)
- 마이크로서비스 아키텍처(MSA, Microservice Architecture)
- ...

<br/>
