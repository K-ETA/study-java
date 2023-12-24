# ORM - Ebean

> **학습 목표**  
> - Ebean이 무엇인지 설명할 수 있다.
> - Ebean이 필요한 상황을 설명할 수 있다.

[1. Ebean이란 무엇일까?](#1-ebean이란-무엇일까)  
[2. Ebean은 어떻게 동작할까?](#2-ebean은-어떻게-동작할까)  
[3. Ebean은 주로 어디에 사용될까?](#3-ebean은-주로-어디에-사용될까)  

## 1. Ebean이란 무엇일까?

<img src="https://ebean.io/images/logo-200.png" width="300" />

### Ebean의 개념
- Java로 작성된 객체-관계형 매핑 도구
- Java에서 사용되는 ORM(Object Relational Mapping) 프레임워크 중 하나이다.
- Ebean ORM은 데이터베이스와의 상호 작용을 쉽게 처리하기 위해 설계되었다.

### Ebean의 기능
- 엔티티(Entity)를 선언하기 위한 표준 JPA Annotation를 (완벽하게) 지원한다.
- JPA Annotation뿐만 아니라 영속성을 지원하기 위한 추가 API를 지원한다.
- 쿼리 API를 지원하며, 네이티브 SQL로 쿼리를 작성할 수 있다.
- 세션이 없으며(Sessionless), 이는 엔티티를 완전히 관리하지 않는다는 것을 의미한다.
- Oracle, Postgres, MySQL, H2 데이터베이스 등을 지원한다.

### Ebean의 장점
- 간단한 설정과 직관적인 Annotation을 통해 간결한 코드를 작성할 수 있고, 그에 따라 직관성도 높아진다.
- ORM 기능을 제공함으로써 객체 지향적인 코드로 데이터베이스와 상호 작용이 가능하다.
- 영속성 컨텍스트를 통해 객체의 상태를 추적하고 관리함에 따라 객체-데이터베이스 간 일관성을 유지할 수 있다.
- 경량화된 ORM 프레임워크로 필요한 부분만을 제공하여 단순한 기능을 유지한다.

### Ebean의 단점
- Hibernate 등의 ORM 프레임워크와 비교했을 때 커뮤니티와 생태계가 상대적으로 작아 지원 및 확장성이 부족할 수 있다.
- 상대적으로 더 큰 ORM 프레임워크에 비해 고급 기능이나 복잡한 쿼리를 다루는 데 제한이 있다.
- Hibernate 등 대표적인 ORM 프레임워크에 비해 문서가 상대적으로 부족하다.

## 2. Ebean은 어떻게 동작할까?
Ebean은 개발자가 작성하는 Java 객체와 데이터베이스의 테이블 간의 매핑을 제공한다.

### 1. 먼저 Ebean을 사용하기 위한 종속성은 다음과 같다.
```XML
<dependency>
    <groupId>io.ebean</groupId>
    <artifactId>ebean</artifactId>
    <version>13.15.2</version>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.1.214</version>
</dependency>
```
    
### 2. 서버에서 관리할 수 있도록 엔티티 빈(Entity Bean)을 수정해야 하기 위해 Maven 플러그인을 추가한다.
```XML
<plugin>
    <groupId>io.ebean</groupId>
    <artifactId>ebean-maven-plugin</artifactId>
    <version>11.11.2</version>
    <executions>
        <execution>
            <id>main</id>
            <phase>process-classes</phase>
            <configuration>
                <transformArgs>debug=1</transformArgs>
            </configuration>
            <goals>
                <goal>enhance</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

### 3. 트랜잭션(Transaction)을 사용하는 엔티티와 클래스가 포함된 패키지 이름을 추가한다.
- ebean.mf 파일에 작성한다. (참고로, .mf는 Java Manifest File을 의미한다.)
```mf
entity-packages: com.baeldung.ebean.model
transactional-packages: com.baeldung.ebean.app
```

### 4. 데이터베이스 인스턴스를 생성한다.
- 서버 인스턴스를 생성하는 방법에는 아래의 2가지가 있다.
  1. 기본 속성 파일을 사용한다.
  2. 프로그래밍 방식으로 생성한다.
- 단일 데이터베이스(*Database*) 인스턴스는 단일 데이터베이스에 매핑된다.
- 두 개 이상의 데이터베이스 인스턴스를 생성할 수도 있다.

#### ① 먼저, 기본 속성 파일을 사용하는 방식이다.
- Ebean은 application.properties, ebean.properties, application.yml 중 하나를 사용한다.
- 데이터베이스 연결 세부 정보와 DDL문(Data Definition Language) 생성/실행을 지시할 수 있다.
```properties
ebean.db.ddl.generate=true
ebean.db.ddl.run=true

datasource.db.username=sa
datasource.db.password=
datasource.db.databaseUrl=jdbc:h2:mem:customer
datasource.db.databaseDriver=org.h2.Driver
```

#### ② 두 번째로, 프로그래밍 방식을 이용하여 데이터베이스 구성을 설정하는 방식이다.
- `DatabaseFactory`와 `DatabaseConfig`를 사용하여 프로그래밍 방식으로 동일하게 서버를 생성한다.

```Java
DatabaseConfig cfg = new DatabaseConfig();

Properties properties = new Properties();
properties.put("ebean.db.ddl.generate", "true");
properties.put("ebean.db.ddl.run", "true");
properties.put("datasource.db.username", "sa");
properties.put("datasource.db.password", "");
properties.put("datasource.db.databaseUrl","jdbc:h2:mem:app2";
properties.put("datasource.db.databaseDriver", "org.h2.Driver");

cfg.loadFromProperties(properties);
Database server = DatabaseFactory.create(cfg);
```

서버 인스턴스가 하나 생성되면, 서버 인스턴스의 기본 값으로 등록된다. `DB` 클래스의 정적 메서드를 사용하여 애플리케이션의 어느 곳에서나 해당 인스턴스를 액세스할 수 있다.
```Java
// 한 개의 서버 인스턴스만 생성된 경우
Database server = DB.getDefault();

// 두 개 이상의 서버 인스턴스가 생성된 경우
// 아래 메서드를 이용하여 서버 인스턴스의 기본 값을 설정할 수 있다.
cfg.setDefaultServer(true);
```

### 5. 엔티티(Entity)를 생성한다.

먼저, 여러 엔티티에 공통적으로 적용되는 속성을 포함하는 `BaseModel`을 생성한다.
```Java
@MappedSuperclass // BaseModel 정의
public abstract class BaseModel {

    @Id
    protected long id;
    
    @Version
    protected long version;
    
    @WhenCreated // io.ebean.annotation.WhenCreated
    protected Instant createdOn;
    
    @WhenModified // io.ebean.annotation.WhenModified
    protected Instant modifiedOn;

    // getters and setters
}
```

다음으로, BaseModel을 상속받는 `Customer`와 `Address` 엔티티를 생성한다.
```Java
@Entity
public class Customer extends BaseModel {

    public Customer(String name, Address address) {
        super();
        this.name = name;
        this.address = address;
    }

    private String name;

    // Customer : Address = 1 : 1 연관 관계
    // Cascade 유형을 ALL로 설정하여 상위 엔티티 업데이트 시 하위 엔티티도 업데이트되도록 설정한다.
    @OneToOne(cascade = CascadeType.ALL)
    Address address;

    // getters and setters
}
```

```Java
@Entity
public class Address extends BaseModel {

    public Address(String addressLine1, String addressLine2, String city) {
        super();
        this.addressLine1 = addressLine1;
        this.addressLine2 = addressLine2;
        this.city = city;
    }
    
    private String addressLine1;
    private String addressLine2;
    private String city;

    // getters and setters
}
```

### 6. 기본적인 CRUD 코드를 작성한다.
위에서 생성한 `Address`와 `Customer` 클래스를 이용하여 간단한 CRUD를 작성한 예제이다.
```Java
// 1. 먼저 각 클래스의 객체를 생성한다.
Address a1 = new Address("5, Wide Street", null, "New York");
Customer c1 = new Customer("John Wide", a1);

// 기본 서버 인스턴스인 DB 클래스는 요청을 프록시하는 정적 메서드를 제공하여 데이터를 유지/액세스한다.
Database server = DB.getDefault();

// 2. 서버 인스턴스의 정적 메서드 `save()`를 사용하여 생성한 객체 정보를 저장한다.
server.save(c1);

// 3. Customer 객체의 세부 정보를 업데이트한 후, 다시 `save()`를 사용하여 저장한다.
c1.setName("Jane Wide");
c1.setAddress(null);
server.save(c1);

// 4. 정적 메서드 `find()`를 사용하여 Customer 객체 데이터를 가져온다.
Customer foundC1 = DB.find(Customer.class, c1.getId());

// 5. 정적 메서드 `delete()`를 사용하여 삭제한다.
DB.delete(foundC1);
```

### 7. 쿼리를 작성한다.
- Ebean은 JPA Annotation뿐만 아니라 쿼리 API도 지원한다.
- 쿼리 API는 객체 그래프를 만드는 데에도 사용할 수 있다.
- 쿼리를 생성 및 실행하기 위해 `Ebean` 또는 `EbeanServer`를 사용할 수 있다.
```Java
Customer customer = DB.find(Customer.class)
            .select("name")           // name을 조회한다.
            .fetch("address", "city") // Customer의 address 객체의 city 필드(Field)를 가져온다.
            .where()
            .eq("city", "San Jose")   // 조회 조건을 추가한다.
            .findOne();               // 결과의 크기를 1로 제한한다.
```

Ebean은 기본적으로 새로운 **트랜잭션(Transaction)**에서 코드나 쿼리를 실행한다. 하지만 단일 트랜잭션 내에서 여러 가지의 코드나 쿼리를 실행해야 할 때가 있다. 이 경우 메서드에 <u>`@Transaction` Annotation을 추가하면 메서드 내의 모든 코드가 동일한 트랜잭션 내에서 실행된다.</u>

```Java
@Transactional // io.ebean.annotations.Transactional
public static void insertAndDeleteInsideTransaction() {
    Customer c1 = getCustomer();
    Database server = DB.getDefault();
    server.save(c1);
    Customer foundC1 = server.find(Customer.class, c1.getId());
    server.delete(foundC1);
}
```

### 8. 마지막으로, 작성한 프로젝트를 빌드 및 실행한다.
참고로, 해당 예제에서는 Maven을 사용하였다.
```sh
compile io.ebean:ebean-maven-plugin:enhance
```

## 3. Ebean은 주로 어디에 사용될까?
Ebean은 초기에 Play Framework  ORM으로 시작되었다. 초기에는 Play Framework에 내장되어 있었지만, 이후 다른 ORM 프레임워크들과 경쟁하면서 자체적인 특징과 장점을 발전시켜 독립적인 프로젝트로 발전하였다.  

이러한 Ebean의 등장 배경과 비교했을 때, 아래와 같은 상황에서 Ebean을 사용하는 것이 좋다.

- 간단한 설정과 사용성이 우선시되는 경우 (특히, 코드의 가독성과 직관성을 중요시할 때)
- 경량화된 빠른 ORM 프레임워크가 필요한 경우
- Hibernate와 JPA의 복잡성에 대한 우려가 있는 경우
- 프로젝트 규모가 중소~중간인 경우 빠른 개발과 간편한 설정이 중요한 상황에서 효과적일 수 있다.
- Play Framework 기반의 애플리케이션을 개발하는 경우 (Spring 프레임워크와 연동되기도 한다.)
