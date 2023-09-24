# Serialization

### Serialization (직렬화)

![Serialization](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2016/01/serialize-deserialize-java.png)

- Byte Stream : 클라이언트와 서버 간에 출발지, 목적지로 입출력하기 위해 데이터가 흐르는 통로
    
    - 자바는 Stream의 기본 단위를 Byte로 두고 있다
    - 따라서 네트워크, DB 등으로 전송할 때 최소 단위인 Byte Stream으로 변환하여 처리한다
    
- Serializable Interface
    
    - 아무 내용이 없는 마커 인터페이스이다
    - implements Serializable을 통해 사용할 수 있다
    
- Serialization (직렬화) : 객체를 Byte Stream으로 변환하는 과정
    
    - 객체를 Byte Stream으로 변환한 후 DB에 저장하거나 네트워크를 통해 전송할 수 있게 된다
    - 직렬화를 사용하면 휘발성이 있는 데이터를 영구 저장할 수 있다
    - ex) Hibernate, RMI, JPA, EJB, JMS 등의 기술
    
- Deserialization (역직렬화) : Byte Stream을 객체로 변환하는 과정
    
    - Byte Stream을 객체로 변환하여 다시 프로그램에서 사용할 수 있도록 한다

<br> 

### 직렬화의 장단점

- 직렬화의 장점
    1. 자바 기술이기 때문에 자바 시스템에 최적화되어 있다
    2. 자바의 다양한 자료형을 파싱 작업 없이도 제약 없이 외부에 내부낼 수 있다
- 직렬화의 단점
    1. 직렬화는 데이터 값 뿐만 아니라 타입 정보, 메타 정보 등을 가지고 있기 때문에 용량이 매우 크다
        
        직렬화로 저장하는지, JSON으로 저장하는지에 따라 파일 용량 크기가 2배 이상 차이가 난다. 따라서 장기간 저장하는 정보는 직렬화를 지양해야 한다.
        
    2. 역직렬화 과정에 위험성이 존재한다
        
        역직렬화 과정에서 호출되어 잠재적으로 위험한 동작을 수행하는 메소드인 Gadget이 존재할 수 있다. 만약 gadget이 호출된다면 프로그램 코드 전체가 공격 범위에 들어갈 수 있다

<br>   

### 직렬화, 역직렬화 방법

- ObjectOutputStream
    
    - 직렬화를 위해 ObjectOutputStream의 `writeObject()`를 사용한다
    - 직렬화된 파일이라는 것을 명시하기 위해 .ser 혹은 .obj로 파일명을 지정하는 게 좋다
    
    ```java
    Customer customer = new Customer(1, "홍길동", "123123", 40);
    String fileName = "Customer.ser";
    
    // 파일 스트림 객체 생성 (try with resource)
    try (
            FileOutputStream fos = new FileOutputStream(fileName);
            ObjectOutputStream out = new ObjectOutputStream(fos)
    ) {
        // 직렬화 가능 객체를 바이트 스트림으로 변환하고 파일에 저장
        out.writeObject(customer);
    } catch (IOException e) {
        e.printStackTrace()
    }
    ```
    
- ObjectInputStream
    
    - 역직렬화를 위해 ObjectInputStream의 `readObject()`를 사용한다
    - 직렬화 대상이 된 객체의 클래스가 내부 클래스이거나 반드시 import 된 상태여야 한다
    - 직렬화된 외부 파일이 있으면 생성자로 객체를 초기화할 필요 없이 바로 정보를 가져올 수 있다
    
    ```java
    String fileName = "Customer.ser";
    // 파일 스트림 객체 생성 (try with resource)
    try(
            FileInputStream fis = new FileInputStream(fileName);
            ObjectInputStream in = new ObjectInputStream(fis)
    ) {
        // 바이트 스트림을 다시 자바 객체로 변환 (이때 캐스팅이 필요)
        Customer deserializedCustomer = (Customer) in.readObject();
        System.out.println(deserializedCustomer);
    
    } catch (IOException | ClassNotFoundException e) {
        e.printStackTrace();
    }
    ```

<br>

### 직렬화의 기타 요소

- transient : 변수 정의 앞에 `transient` 키워드를 명시하면 직렬화 대상에서 제외할 수 있다
    
    - transient가 붙은 인스턴스 변수의 값은 그 타입의 기본값으로 직렬화된다
    - ex) Primitive Type : 각 타입의 디폴트 값, Reference Type : Null
    - 제외하기 전 해당 객체가 필요 없는지, 제외했을 때 문제가 없는지 고려해야 한다
    
    ```java
    class Customer implements Serializable {
        int id; 
        String name; 
        transient String password; // 직렬화 대상에서 제외
        int age; 
    
        public Customer(int id, String name, String password, int age) {
            this.id = id;
            this.name = name;
            this.password = password;
            this.age = age;
        }
    }
    ```
    
- serialVersionUID : 직렬화된 클래스의 고유 식별 번호
    
    - 직렬화, 역직렬화 과정에서 동일한 특성을 가지는지 확인하는 데 사용된다
    - SUID를 명시하지 않는다면 시스템이 자동으로 생성해준다
    - SUID를 직접 명시해주면 클래스의 내용이 바뀌어도 시스템 자동 생성 값으로 변경되지 않는다
    - 또한 런타임에 SUID를 생성하는 것은 시간이 많이 걸리기 때문에 미리 명시하는 것을 권장한다
    - SUID는 반드시 private static final로 선언해야 한다 
    - ex) `private static final long serialVersionUID = 123L;`
    - SUID는 정수값이라 아무 값이 가능하지만, 같은 값을 가지는 것을 방지하기 위해 serialversion 값을 생성해주는 프로그램을 사용하는 게 좋다
    
- 객체 상속 관계에서의 직렬화
    
    - 부모 클래스가 Serializable을 구현했다면 자식 클래스는 Serializable을 구현하지 않아도 직렬화가 가능하다
    - 반대로 부모 클래스는 Serializable을 구현하지 않고 자식 클래스만 구현했다면 부모 클래스의 인스턴스는 무시되고 자식 필드만 직렬화된다
    - 이 경우에 상위 클래스의 필드까지 직렬화하기 위해서는 `writeObject()`, `readObject()`를 재정의하여 직접 직렬화 코드를 추가하면 된다

<br>

### 직렬화 예외

- InvalidClassException : Serialized 또는 Deserialized를 할 수 없을 때 발생하는 오류
    
    > 아래 3가지 주요 원인으로 인해 발생한다
    > 
    1. 클래스의 SerialVersionUID 버전이 다른 경우
    2. 클래스에 다른 데이터 타입을 포함한 경우
    3. 기본 생성자가 없는 경우
        
        역직렬화 과정은 부모 클래스로부터 시작해서 상속 구조를 따라 내려가게 된다. 그런데 부모 클래스가 직렬화를 구현하지 않았다면 부모의 속성 정보를 기본 생성자를 통해 가져오게 된다. 이때 기본 생성자가 없다면 불러올 유효한 생성자가 없어 오류가 난다.
        
        ```java
        class UserAccount {
            String name;
            String password;
        
            // ! 기본 생성자 없으면 InvalidClassException : no valid constructor 발생
            // public UserAccount() {}
        
            UserAccount(String name, String password) {
                this.name = name;
                this.password = password;
            }
        }
        
        class UserInfo extends UserAccount implements Serializable {
            int age;
            int height;
            boolean marreid;
        
            UserInfo(String name, String password, int age, int height, boolean marreid) {
                super(name, password);
                this.age = age;
                this.height = height;
                this.marreid = marreid;
            }
        }
        ```
        
- NotSerializableException : 참조하고 있는 클래스가 Serializable을 구현하지 않은 경우 발생하는 오류
    
    ```java
    class UserInfo implements Serializable {
        String name;
        int age;
        boolean marreid;
        Object obj;  // Serializable을 구현하지 않음
    }
    ```

<br>

### 직렬화 주의사항

1. Serialized 인터페이스를 구현한 클래스의 모든 하위 클래스가 직렬화가 가능해야 한다
    
    - 직렬화가 불가능한 경우 `NotSerializedException`이 발생한다
    
    ```java
    public class Person implements Serializable {
        private int age;
        private String name;
        private Address country;  // Address도 직렬화가 가능해야 함
    }
    ```
    
2. Custom Serialization이 가능하다
    
    - Custom Serialization을 사용하면 직렬화할 수 없는 객체도 직렬화할 수 있다
    
<br><br>

# 참고 자료

[Serialization and Deserialization in Java with Example - GeeksforGeeks](https://www.geeksforgeeks.org/serialization-in-java/)<br>
[Serialization in Java - javatpoint](https://www.javatpoint.com/serialization-in-java)<br>
[Introduction to Java Serialization | Baeldung](https://www.baeldung.com/java-serialization)<br>
[☕ 자바 직렬화(Serializable) - 완벽 마스터하기](https://inpa.tistory.com/entry/JAVA-☕-직렬화Serializable-완벽-마스터하기)