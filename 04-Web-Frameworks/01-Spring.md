# Spring

### Spring

- Spring Framework : Java 기반 오픈 소스 애플리케이션 프레임워크
    
    - 대규모 데이터 처리와 여러 사용자의 트랜잭션 처리에 중점을 두었다
    
    - 애플리케이션 개발의 전 과정을 빠르고 효과적으로 진행할 수 있도록 돕는다
    
    - 공기관 서비스, 오래된 기업의 서비스는 모두 Spring으로 개발되었다고 해도 무방하다! (자바공화국 skrr)
    
- Spring의 특징
    
    - 엔터프라이즈 개발의 고급 기술을 사용할 수 있으면서도 코드와 개발 과정이 단순하다
    
    - 아주 가벼운 웹 서버인 톰캣에서도 동작한다  ← 경량 프레임워크
    
    - 비즈니스 로직이 복잡하고 자주 수정이 필요한 점을 해결하기 위해 객체 지향을 선택했다
    
<br>

### Spring의 핵심

1. 경량 컨테이너로 자바 객체를 직접 관리한다
2. POJO(Plain Old Java Object) 방식의 프레임워크이다
3. IoC(Inversion of Control)를 지원한다
4. DI(Dependency Injection)를 지원한다
5. AOP(Aspect-Oriented Programming)을 지원한다
6. 영속성과 관련된 다양한 서비스를 지원한다
7. 확장성이 높다

<br>

### POJO (Plain Old Java Object)

- POJO (Plain Old Java Object) : 자바로 생성하는 순수한 객체
    
    - Getter, Setter과 같은 기본적인 기능만 가진 자바 객체이다
    
    - 다른 클래스나 인터페이스를 상속받지 않았다
    
    - 객체 지향적인 원리에 충실하면서 환경과 기술에 종속되지 않는다
    
    ⇒ 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트
    
- POJO 프로그래밍 : POJO에 애플리케이션의 핵심 로직과 기능을 담아 설계하고 개발하는 방법
    1. Java나 Java 스펙에 정의된 것 이외에는 다른 기술이냐 규약에 얽매이지 않아야 한다
        
        Java에서 지원하는 기술만 사용하면 POJO라고 부를 수 있다. Java가 아닌 외부 라이브러리 혹은 언어에 종속되어 있으면 POJO가 아니다.
        
    2. 특정 환경에 종속적이지 않아야 한다
        
        POJO는 환경 독립적이기 때문에특정한 프레임워크에서만 동작이 가능하면 안된다. 특히 비즈니스 로직을 담고 있는 POJO 클래스는 웹 기반의 환경 정보나 기술을 담고 있는 클래스나 인터페이를 사용하면 안된다.
        
- POJO 프로그래밍이 필요한 이유
    
    - 특정 환경이나 기술에 종속적이지 않기 때문에 재사용이 가능하고, 확장 가능한 유연한 코드를 작성할 수 있다
    
    - 저수준 레벨의 기술과 환경에 종속적인 코드를 제거하여 코드가 간결해지고 디버깅하기 쉽다
    
    - 특정 기술이나 환경에 종속적이지 않기 때문에 테스트가 단순해진다
    
    - 객체지향적인 설계를 제한 없이 적용할 수 있다

<br><br>

# MVC 구조

### Spring MVC

- MVC : Model-View-Controller
    
    ![MVC 패턴](https://developer.mozilla.org/ko/docs/Glossary/MVC/model-view-controller-light-blue.png)
    
    - 어플리케이션을 구성하는 요소를 역할에 따라 세 가지 모듈로 나누어 구분한 패턴이다
    
    - UI 영역과 비즈니스 영역을 구분하여 서로에게 영향을 주지 않도록 할 수 있다
    
    - 개발과 유지보수가 보다 간편하다
    
- Model : 작업의 처리 결과 (데이터)
    
    - Service 계층에서 비즈니스 로직을 통해 처리한 작업의 결과이다
    
- View : Model을 이용하여 웹 브라우저와 같은 애플리케이션의 화면에 보이는 리소스를 제공
    
    - HTML 페이지 출력, PDF & Excel 등의 문서 형태로 출력,
    
    - XML, JSON 등 특정 형식의 포맷으로 변환하는 등의 작업을 한다
    
- Controller : 클라이언트 측의 요청을 전달받는 엔드포인트
    
    - Model과 View의 중간에서 상호작용을 진행한다
    
    - 클라이언트의 요청을 받아 비즈니스 로직을 거친 후 Model 데이터가 만들어지면, Model 데이터를 View로 전달한다

<br>

### HTTP 요청 처리 과정

![HTTP 요청 처리 과정](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F566eb042-5ddf-45cb-99ee-3ee1153e7e6b%2Fa.png)

1. DispatcherServlet : 제일 앞단에서 Request를 처리하는 Controller
    
    - HTTP Request를 처리할 Controller를 지정한다 (Super Controller)
    
    - 이렇게 앞쪽에서 처리하는 컨트롤러를 두는 패턴을 Front Controller 패턴이라고 한다
    
2. Controller (Handler) : HTTP Request를 처리해 Model을 만들고 View를 지정
    
    - Service에서 HTTP Request를 처리하고 필요한 데이터를 뽑아 Model에 저장한다
    
    - 또한 HTTP가 보여줄 View Name을 지정하거나 View를 직접 반환한다
    
    - 이곳에서 View에 Model의 데이터를 직접 세팅하지는 않는다
    
3. Model & View
    
    - Controller에 의해 반환된 Model과 View가 Wrapping된 객체
    
    - Model는 Map 자료구조로 HTTP Request 속의 데이터를 파싱해 저장한다
    
4. ViewResolver : Model & View 객체를 처리하여 View를 그림
    
    - Model에 저장된 데이터를 사용해 View를 그려준다
    
    - 여기서 그려지는 View가 유저에게 반환된다

<br><br>

# **IoC Container 및 Bean**

### Bean

- Bean : 스프링 컨테이너에 등록된 객체
    
    - `@Bean`을 통해 메소드로부터 반환된 객체를 스프링 컨테이너에 등록한다
    
    - 클래스의 등록 정보, Getter/Setter 메소드, 컨테이너에 대한 설정 메타데이터가 포함된다
    
- Spring Bean 등록하는 방법
    1. `@Component` 사용하기
        
        ```java
        @Controller
        public class HelloController {
        		...
        }
        ```
        
        `@Controller`의 내부를 살펴보면 `@Component`가 존재한다. 이렇게 `@Component`가 붙어있는 어노테이션을 사용하면 스프링이 자동으로 Bean을 등록해준다.
        
    2. Bean Configuration File에 직접 등록하기
        
        ```java
        @Configuration
        public class HelloConfiguration {
            @Bean
            public HelloController sampleController() {
                return new SampleController;
            }
        }
        ```
        
        `@Configuration`을 이용해서 스프링 프로젝트에서 Configuration 역할을 하는 클래스를 지정한다. Configuration 파일에서 Bean으로 등록하고자 하는 클래스에 `@Bean`을 사용하면 Bean을 등록할 수 있다.

<br>

### IoC

- IoC (Inversion of Control) : 제어의 역전
    
    어플리케이션 안에서 객체를 생성/해체 및 참조하는 작업을 개발자가 아닌 프레임워크가 관리하는 형태. 스프링 프레임워크에서는 객체의 생명주기 및 타 객체와의 의존관계 설정을 객체 자신이 아닌 스프링 컨테이너에서 진행한다. IoC 개념은 스프링 프레임워크 뿐만 아니라 다른 프레임워크 및 디자인 패턴과 같이 범용적인 곳에서 많이 사용된다.
    
- 스프링 의존 관계 → 다른 IoC 프레임워크와의 차별점
    
    ![제어의 역전](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx4WUU%2Fbtq9gXndYek%2FCwB8xqIdfQh1ox2P9H6bV1%2Fimg.png)
    
    스프링에서 의존이란 객체 간의 의존을 의미한다. 예를 들어, 한 클래스 A가 다른 클래스 B의 메소드를 실행할 때, A가 B에 의존한다고 표현한다.
    
- DL (Dependency Lookup) : 의존관계가 있는 객체를 외부에서 주입 받는 것이 아닌, 의존관계가 필요한 객체에서 직접 검색하는 방식
    
    - 클라이언트 객체는 의존하고자 하는 인터페이스 타입만 지정해서 검색을 진행하며, 이외의 작업은 IoC에서 진행한다
    
    - DL 사용시 컨테이너 종속이 증가하기 때문에 주로 DI를 사용한다
    
- DI (Dependency Injection) : 런타임 시점에 객체간의 의존관계를 연결해주는 방식
    
    - 인터페이스를 이용해서 클래스 간의 의존관계를 느슨하게 해준다 → 유연성 확보, 결합도 하락
    
    - 의존관계가 느슨해지면 런타임 시점에 어떤 클래스를 사용할지 알 수 없게 된다
    
    - 설계 시점에서 알 수 없는 런타임 시점의 의존관계를 스프링 컨테이너에서 연결해주는 것이 DI이다!
    
    - Setter Injection (수정자 주입) : Setter 혹은 사용자 정의 메소드에 `@Autowired`를 사용하여 의존성을 주입한다.
        
        ```java
        private Service service;
        
        @Autowired
        public setService(Service service){
        		this.service = service;
        }
        ```
        
        객체가 변경될 필요가 있을 때만 사용한다.
        
    - Constructor Injection (생성자 주입) : 생성자에 `@Autowired`를 사용하여 의존성을 주입한다.
        
        ```java
        private Service service;
        
        @Autowired 
        public Controller(Service service){
        		this.service = service; 
        }
        ```
        
        생성자는 인스턴스 생성시 반드시 1회 호출되는 것이 보장되기 때문에, 주입받은 객체가 변하지 않거나 반드시 객체주입이 필요한 경우에 강제를 위해 사용된다. 세 가지 방법 중 생성자 주입을 추천한다.
        
    - Method Injection (필드 주입) : 필드에 `@Autowired`를 사용하여 의존성을 주입한다.
        
        ```java
        @Autowired 
        private Service service;
        ```
        
        코드가 간결하고 편하지만 의존관계를 정확히 파악하기 힘들다.
        
- + DI가 필요한 이유
    
    ```java
    public class Store {
        private Pencil pencil;
    
        public Store() {
            this.pencil = new Pencil();
        }
    }
    ```
    
    1. 두 클래스가 강하게 결합되어 있다
        
        위 방식을 사용하면 클래스가 강하게 결합된다. 만약 Store에서 다른 상품을 판매하고 싶으면 Store 생성자에 변경이 필요하다. 즉, 유연성이 떨어지게 된다. 이 문제는 상속으로 해결할 수 있지만, 상속은 제약이 많고 확장성이 떨어지기 때문에 피하는 것이 좋다.
        
    2. 객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐
        
        위 방식은 객체들 간의 관계가 아닌 클래스 간의 관계가 형성된다. 이 방식을 올바른 객체지향적 설계에서 벗어난다.

<br>

### IoC Container

> 컨테이너 : 객체의 생명주기를 관리, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것
- IoC 컨테이너 : 객체를 생성하고 관리하고 책임지고 의존성을 관리해주는 컨테이너
    
    > 스프링 컨테이너 = IoC 컨테이너 = DI 컨테이너
    
    - IoC 컨테이너는 객체의 생성을 책임지고 의존성을 관리한다
    
    - POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가진다
    
    - 인스턴스 생성부터 소멸까지의 인스턴스 생명주기 관리를 컨테이너가 대신 해준다
    
- IoC 컨테이너의 장점
    
    - 개발자들이 POJO를 생성하지 않고 컨테이너에 맡기기 때문에 비즈니스 로직에 집중할 수 있다
    
    - 객체 생성 코드가 없으므로 TDD가 용이하다
    
    - 객체관리의 주체가 프레임워크(컨테이너)가 되기 때문에 개발자는 로직에 집중할 수 있다
    
<br>

### IoC Container의 종류

- BeanFactory : 스프링 빈을 관리하고 조회하는 역할
    
    - 스프링 컨테이너의 최상위 인터페이스이다
    
    - `getBean()`을 통해 Bean을 조회할 수 있다
    
    - 보통 BeanFactory를 확장한 ApplicationContext를 사용한다
    
- ApplicationContext : 컨테이너에서 객체를 생성하고 DI를 처리한다
    
    - 스프링 빈을 관리하고 조회하는 역할 뿐만 아니라 스프링의 각종 기능을 추가로 제공한다
    
    - 빈을 스프링 컨테이너에 등록하고, 빈 조회 요청시 새로 생성하지 않고 스프링 컨테이너에서 빈을 찾아서 반환한다
    
    - 빈을 싱글톤으로 관리해준다 → 싱글톤의 장점인 매번 인스턴스를 생성할 필요가 없다는 것만 챙김!

<br>

### 스프링 컨테이너의 생성과 빈 등록 과정

1. 스프링 컨테이너 생성
    
    ![스프링 컨테이너 생성](https://3513843782-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LxjHkZu4T9MzJ5fEMNe%2Fsync%2F9704dddc07d85c1fa52b4b3df81c0f06b6cab26f.png?generation=1618042929816980&alt=media)
    
    ```java
    ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
    ```
    
    AppConfig.class를 활용하여 매개변수로 구성 정보를 전달한다 ← 얘가 원래 있던가??
    
2. 스프링 빈 등록
    
    ![스프링 빈 등록](https://3513843782-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LxjHkZu4T9MzJ5fEMNe%2Fsync%2F8f14ee1b526e82841d4b714df72cd37ae04b692e.png?generation=1618042932406166&alt=media)
    
    스프링 컨테이너는 <key: 빈 이름, value: 빈 객체> 형태로 빈을 저장한다
    key는 메소드의 이름으로 사용하고, value는 return할 실제 객체를 저장한다
    
3. 스프링 빈 의존관계 설정
    
    ![스프링 빈 의존관계 설정](https://3513843782-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LxjHkZu4T9MzJ5fEMNe%2Fsync%2F927127e605612b1db360aa8f545f0fcf55ff736e.png?generation=1618042936612892&alt=media)
    
    스프링은 설정 정보를 참고해서 의존 관계 주입(DI)을 진행한다
    
<br><br>

# Spring Event

### Spring Event

![Spring Event](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYpcAx%2FbtrUsPdK81f%2FRzbwUa4oaJnWx56k1lBES1%2Fimg.jpg)

- Spring Event : 스프링 프레임워크를 사용할 때 내부에서 데이터를 전달하는 방법
    
    - 이벤트를 발생(publish)시키고 이벤트를 수신(subscribe)하는 로직을 분리해서 작성할 수 있다  → 서비스간의 의존성을 줄일 수 있다
    
    - 이벤트가 발생했을 때 처리하는 코드는 리스너를 통해 처리하기 때문에 핵심 로직을 간결하게 유지할 수 있다
    
- EventListener
    1. Event Class : 이벤트를 처리하는 클래스
        
        ```java
        public class OrderedEvent {
            private String productName;
        
            public OrderedEvent(String productName) {
                this.productName = productName;
            }
        
            public String getProductName() {
                return productName;
            }
        }
        ```
        
    2. Event Publisher
        
        ```java
        ApplicationEventPublisher publisher;
        
        public void order(String productName) {
          publisher.publishEvent(new OrderedEvent(productName));
        }
        ```
        
        ApplicationEventPublisher를 사용한다. `publishEvent()` 메소드를 통해 생성한 이벤트 객체를 넣어준다.
        
    3. Event Listener 
        
        ```java
        @EventListener
        public void sendPush(OrderedEvent event) throws InterruptedException {
            log.info(String.format("푸시 메세지 발송 [상품명 : %s]", event.getProductName()));
        }
        ```
        
        `@EventListener`를 통해 발생하는 이벤트를 캐치한다
        
- TransactionalEventListener
    
    - 부가적인 코드는 트랜잭션이 성공한 후 실행되어야 한다
    
    - `@TransactionalEventListener`를 통해 이벤트의 발생과 트랜잭션 처리를 결합할 수 있다
    
    ```java
    @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT)
    public void sendPush(OrderedEvent event) throws InterruptedException {
        log.info(String.format("푸시 메세지 발송 [상품명 : %s]", event.getProductName()));
    }
    ```
    
    | phase | 기능 |
    | --- | --- |
    | AFTER_COMMIT | 트랜잭션이 성공했을 때 실행 |
    | AFTER_ROLLBACK | 트랜잭션 롤백시 실행 |
    | AFTER_COMPLETE | 트랜잭션 완료시 실행 (COMMIT + ROLLBACK) |
    | BEFORE_COMMIT | 트랜잭션이 커밋되기 전에 실행 |

<br><br>

# VO, DTO, DAO

### VO, DTO, DAO

- DAO (Data Access Object) : DB의 데이터에 접근하기 위한 객체
    
    - 비즈니스 로직과 DB에 접근하기 위한 로직을 분리하기 위해 사용한다
    
    - 직접 DB에 접근하여 데이터를 삽입, 삭제, 조회 등 조작할 수 있는 기능을 수행한다
    
    - ex) DAO, Repository
    
    ```java
    Optional<User> findById(Long id);
    ```
    
- DTO (Data Transfer Object) : 계층 간 데이터 교환을 위해 사용하는 객체
    
    - DTO는 로직을 가지지 않고 Getter, Setter만 가진다
    
    - ex) 유저가 DTO에 데이터를 담아서 전송, 서버가 DTO를 이용하여 유저에게 데이터를 전송
    
    ```java
    static class ResponseDto {
        private String name;
        private String result = "결과";
    }
    ```
    
- VO (Value Object) : 값을 위해 쓰인다?
    
    - Read-Only 속성을 가지며 Getter 기능만 존재한다
    
    - 값 자체에 의미가 있다????????????

<br><br>

# AOP (Aspect Oriented Programming)

### AOP 주요 개념

- Aspect : 공통적인 기능들을 모듈화한 것
- Target : Aspect가 적용될 대상
    
    - ex) 메소드, 클래스
    
- JointPoint : Aspect가 적용될 수 있는 시점
    
    - ex) 메소드 실행 전, 후
    
- Advice : Aspect의 기능을 정의한 것
    
    - 메소드의 실행 전, 후, 예외 처리 발생 시 실행되는 코드를 의미한다
    
- PointCut : Advice를 적용할 메소드의 범위를 지정

<br>

### AOP (Aspect Oriented Programming)

- 핵심 관심사와 공통 관심사
    
    - Core Concern (핵심 관심사) : 각 객체가 가져야 할 본래의 기능
    
    - Cross-cutting Concern (공통 관심사) : 여러 객체에서 공통적으로 사용되는 코드
    
- AOP (Aspect Oriented Programming) : 관점 지향 프로그래밍
    
    - 메소드나 객체의 기능을 핵심 관심사와 공통 관심사로 나누어 프로그래밍한다
    
    - 모듈화 : 어떤 공통된 로직이나 기능을 하나의 단위로 묶는 것
    
    - 핵심적인 관점 : 핵심 비즈니스 로직
    
    - 부가적인 관점 : 핵심 로직을 실행하기 위한 DB 연결, 로깅, 파일 입출력 등
    
- Spring AOP의 특징
    
    - 프록시 패턴 기반의 AOP 구현체이다 → 프록시 객체를 쓰는 이유는 접근 제어 및 부가 기능을 위해서이다
    
    - 스프링 빈에만 AOP를 적용할 수 있다
    
    - 스프링 IoC와 연동하여 엔터프라이즈 애플리케이션의 흔한 문제점들을 해결하는 것이 목적이다

<br>

### AOP 적용하는법

1. 여러 개의 클래스에서 반복해서 사용하는 코드가 있다면 해당 코드를 모듈화하여 공통 관심사로 분리한다
2. 이렇게 분리한 공통 관심사를 Aspect로 정의한다
3. Aspect를 적용한 메소드나 클래스에 Advice를 적용하여 공통 관심사와 핵심 관심사를 분리한다
4. 이렇게 공통 관심사를 별도의 모듈로 관리하여 코드의 재사용성과 유지 보수성을 높일 수 있다

<br><br>

# AOT (Ahead-Of-Time)

### AOT (Ahead-Of-Time)

- AOT (Ahead-Of-Time) : 빌드 시 스프링 애플리케이션을 분석하고 최적화하는 도구
    
    - AOT 엔진은 GraalVM Native Configuration이 필요로 하는 reflection configuration을 생성해준다

    - Spring Native 실행 파일로 컴파일 하는데 사용된다
    
- AOT 적용시 효과
    
    - 기존 JVM 방식에서는 프로그램이 올라갈 때 바이트 코드를 컴파일한다

    - AOT는 네이티브 이미지라는 것을 만들어서 미리 컴파일할 수 있도록 한다

    - 추가로 메모리 사용량도 줄여서 경량화 애플리케이션을 구축하는 데 도움을 준다

<br><br>

# 참고 자료

[Spring Framework Overview :: Spring Framework](https://docs.spring.io/spring-framework/reference/overview.html)<br>
[Introduction to the Spring IoC Container and Beans :: Spring Framework](https://docs.spring.io/spring-framework/reference/core/beans/introduction.html)<br>
[[Spring] IoC 컨테이너 (Inversion of Control) 란?](https://dev-coco.tistory.com/80)<br>
[[Spring] 스프링 컨테이너 - ApplicationContext, IoC, DI](https://m42-orion.tistory.com/98)<br>
[[Spring] IoC(Inversion of Control : 제어의 역전)컨테이너란?](https://choicode.tistory.com/31)<br>
[[Spring] 스프링 빈(Bean)이란 무엇인가?](https://ittrue.tistory.com/221)<br>
[스프링 빈(Spring Bean)이란? 개념 정리 - Easy is Perfect](https://melonicedlatte.com/2021/07/11/232800.html)<br>
[[스프링] Spring IoC / DI / DL 개념](https://velog.io/@dusdn2424/스프링-Spring-IoC-DI-DL-개념-정리)<br>
[[Spring] 의존성 주입(Dependency Injection, DI)이란? 및 Spring이 의존성 주입을 지원하는 이유](https://mangkyu.tistory.com/150)<br>
[Spring DI 스프링 의존성 주입 3가지 방법](https://cheershennah.tistory.com/227)<br>
[[Spring] 스프링 컨테이너(ApplicationContext)](https://velog.io/@max9106/Spring-ApplicationContext)<br>
[스프링 이벤트 기능을 사용할 때의 고려할 점](https://findstar.pe.kr/2022/09/17/points-to-consider-when-using-the-Spring-Events-feature/)<br>
[spring 이벤트 사용하기(event publisher, event listener)](https://wildeveloperetrain.tistory.com/217)<br>
[[Spring] Spring 기본 개념](https://velog.io/@dnjscksdn98/Spring-Framework-개념-정리)<br>
[Spring Framework란? Spring 의 특징과 핵심 개념](https://anywaydevlog.tistory.com/61)<br>
[[Spring] Spring 기초](https://programforlife.tistory.com/103)<br>
[Spring) Spring MVC 동작 구조](https://ss-o.tistory.com/160)<br>
[[Spring MVC] 스프링 MVC란 무엇인가? - 스프링 MVC 구조 이해](https://ittrue.tistory.com/234)<br>
[Spring MVC Framework란 무엇인가?  Spring MVC의 구조와 의의](https://kotlinworld.com/326)<br>
[[Java] DAO, DTO, VO의 개념](https://velog.io/@leesomyoung/Java-DAO-DTO-VO의-개념)<br>
[DAO, DTO, VO 란? 간단한 개념 정리 - Easy is Perfect](https://melonicedlatte.com/2021/07/24/231500.html)<br>
[[Spring] DAO와 DTO의 차이 그리고 VO](https://dkswnkk.tistory.com/500)<br>
[Spring의 기본 특징-POJO](https://velog.io/@galaxy/Spring의-기본-특징-POJO)<br>
[[Spring] POJO란 무엇인가?](https://ittrue.tistory.com/211)<br>
[[Spring] 스프링 AOP (Spring AOP) 총정리 : 개념, 프록시 기반 AOP, @AOP](https://engkimbs.tistory.com/entry/스프링AOP)<br>
[[Java] Spring Boot AOP(Aspect-Oriented Programming) 이해하고 설정하기](https://adjh54.tistory.com/133)<br>
[Spring AOT(Ahead-Of-Time) 경험 이야기](https://stir.tistory.com/349)<br>
[Spring AOT 란?](https://thenicesj.tistory.com/399)<br>
[스프링 컨테이너와 스프링 빈](https://dodeon.gitbook.io/study/kimyounghan-spring-core-principle/04-spring-container-and-bean)