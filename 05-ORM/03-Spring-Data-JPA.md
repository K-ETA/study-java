# ORM - Spring Data JPA

<br/>

> **학습 목표**  
> - Spring Data JPA가 무엇인지 설명할 수 있다.
> - Spring Data JPA와 JPA의 다른 점을 설명할 수 있다.

<br/>

## 목차
[1. Spring Data JPA란 무엇일까?](#1-spring-data-jpa란-무엇일까)  
[2. Spring Data JPA는 어떻게 동작할까?](#2-spring-data-jpa는-어떻게-동작할까)  
[3. Spring Data JPA는 주로 어디에 사용될까?](#3-spring-data-jpa는-주로-어디에-사용될까) 

<br/>

## 1. Spring Data JPA란 무엇일까?

<img src="https://blog.kakaocdn.net/dn/KZ9nb/btrIxCbVCM2/Wb4B9BtIZ4CxYi6oNPHFL0/img.png" width="500" />

### 1.1 Spring Data JPA의 개념
- Spring 프레임워크에서 제공하는 프로젝트 중 하나
- Spring 프레임워크에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트
- JPA를 기반으로 한 데이터 액세스 계층을 간소화하고, 개발자들이 데이터베이스에 더 쉽게 접근할 수 있도록 지원한다.
- JPA 표준 스펙을 기반으로 한다.
- `JPARepository` 인터페이스를 통해 데이터베이스의 CRUD 작업을 추상화하고 일반적인 쿼리 메서드를 제공한다.

<img src="https://3827551924-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M26jG1r8fNWiAQrZyfg%2F-M4hJIiL_CbaMtV-iVnw%2F-M4hJKM-HtsfBTEDejCj%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2019-07-16_%EC%98%A4%ED%9B%84_7.54.42.png?generation=1586676988366911&alt=media" width="500" />

### 1.2 Spring Data JPA의 기능
- CRUD를 처리하기 위한 공통 인터페이스를 제공한다. (`JpaRepository`)
- Repository를 개발할 때 인터페이스만 작성하면 실행 시점에 Spring Data JPA가 구현 객체를 동적으로 생성해서 주입한다.
- 즉, 데이터 접근 계층을 개발할 때 구현 클래스 없이 인터페이스만 작성해도 개발을 완료할 수 있다.
- 동적으로 쿼리를 작성해야 하는 경우에는 `@Query` Annotation을 사용하거나 Querydsl 같은 별도의 라이브러리를 도입해야 한다.

### 1.2 Spring Data JPA의 장점
- 데이터 접근 계층을 개발할 때 지루하게 반복되는 CRUD 문제(JPA)를 해결한다.
- 개발자가 직접 JPA의 구현체를 개발하지 않아도 된다.
- 다양한 데이터 저장소에 대한 접근을 추상화함으로써 개발자 편의를 제공한다.
- 지루하게 반복하는 데이터 접근 코드를 줄인다.
- [🔗 정해진 메서드 명명 규칙](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html)에 따라 JPQL을 실행시킬 수 있다.
  - 예시) `findByLastnameAndFirstname()`, `findByLastnameNot()`, `findByFirstnameIngoreCase()` 등

### 1.3 Spring Data JPA의 단점
- 복잡한 쿼리 작성이 필요한 경우에는 별도의 JPQL이나 네이티브 쿼리를 작성해야 한다. (특히 JOIN 등)
- Spring Data JPA를 사용하려면 JPA에 대한 이해도 필요하므로 학습 곡선이 다소 높을 수 있다.
- Spring Data JPA는 지연 로딩(Lazy Loading)을 위해 프록시 객체를 사용하는데, 이로 인해 관련 문제가 생길 수 있다.

<br/>

## 2. Spring Data JPA는 어떻게 동작할까?
- Spring Data JPA는 JPA를 기반으로 하므로 대부분 JPA와 비슷한 방식으로 작동된다.
- 디른 점은 JPA와는 달리 Repository에 대한 구현을 자동으로 생성하여 제공한다는 점이다.
- 또, JPA와는 달리 Entity Manager, Entity 등을 개발자가 직접 생성하여 구현할 필요가 없다.

먼저, Spring 프로젝트에 아래와 같은 의존성을 추가한다.
```Groovy
dependencies {
    // Spring Data JPA 추상화 라이브러리
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
}
```

JPA와 제일 크게 다른 점은 바로 이 `JpaRepository`라고 할 수 있다.
```Java
public interface MemberRepository extends JpaRepository<Member, Long> {
    Optional<Member> findById(Long id);
    Optional<Member> findByName(String name);
}
```

**`JpaRepository`**
- 아래 그림과 같은 상속 관계를 가진다.
- 상속받고 있는 각 클래스 가진 메서드 모두를 지원한다.
- 예시)
  - `CrudRepository` 인터페이스의 기본적인 CRUD 메서드 (예시: `save()`, `findById()`, `count()`, `deleteById()` 등)
  - `GqueryByExampleExecutor` 인터페이스의 CRUD 메서드 (예시: `findOne()`, `findAll()`, `count()`, `exist()` 등)

<img src="https://3827551924-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M26jG1r8fNWiAQrZyfg%2F-M4hJIiL_CbaMtV-iVnw%2F-M4hJKM-HtsfBTEDejCj%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2019-07-16_%EC%98%A4%ED%9B%84_7.54.42.png?generation=1586676988366911&alt=media" width="500" />

위와 같이 작성한 Repository를 아래처럼 사용할 수 있다. (이 외에는 생략)

```Java
@Service
public class MemberService {
    private final MemberRepository memberRepository;

    @Autowired
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    public Member findMemberByName(String name) {
        return memberRepository.findByName(name)
            .orElseThrow(() -> new IllegalArgumentException("Member doesn't exist."));
    }
}
```

<br/>

## 3. Spring Data JPA는 주로 어디에 사용될까?
- 데이터베이스 액세스를 위한 빠르고 간단한 CRUD 기능이 필요한 경우
- Spring 프레임워크 + JPA를 사용하려는 경우
- 쿼리 메서드를 통해 간단한 쿼리를 작성하고 싶은 경우
- 간편한 트랜잭션 관리를 선호하는 경우 (Spring Data JPA는 Spring 트랜잭션 관리를 활용)
- 마이크로서비스 아키텍처(MSA, Microservice Architecture)를 구현하는 경우

<br/>
