# Spark

### Spark

- Spark : 웹 애플리케이션 구축을 위한 마이크로 프레임워크
    
    - Apache Spark랑 다른 프레임워크이다!!!!!!!! (중요)
    
    - 구분을 위해 SparkJava로 부르기도 한다
    
    - Java/Kotlin을 사용하여 개발이 가능하다
    
- Spark의 특징
    
    - 번거로운 구성 없이 신속한 개발을 위해 간단하고 가볍게 구축되었다
    
    - Graal Native Compiler를 이용하여 간단하게 컴파일할 수 있다
    
    - Jetty 서버가 내장되어 있다
    
    - 빠르고 간편하게 REST API를 만들 수 있다

<br>    

### Spark의 장점

1. 간단한 구성 및 상용구를 사용하여 몇 분 안에 시작하고 실행할 수 있다 (= 생산성이 높다)
2. MVC 패턴을 따르지 않는다
3. 주석이 많이 필요없다
4. 마이크로 서비스에 적합하다
5. 기본적으로 Jetty WAS에서 실행되지만, 다른 웹 서버에서 실행하도록 구성할 수 있다

<br>

### Spark의 단점

1. SparkJava에 대한 정보가 많이 없다
2. Graal에 적용이 가능한 라이브러리가 많이 없다
3. 네이티브 이미지의 컴파일 속도가 매우 느리다

<br>

### 경로의 구성 요소

> Spark는 경로와 핸들러를 기반으로 구축된다
- 동사 : HTTP 메소드
    
    - ex) GET, POST, PUT, DELETE, HEAD 등
    
- 경로 (경로 패턴) : 경로가 수신 대기하고 응답을 제공해야 하는 URI
- 콜백 : 해당 HTTP 요청에 대한 응답을 생성하고 반환하기 위해 호출되는 핸들러
    
    - 요청 객체와 응답 객체를 인수로 사용한다
    

```java
get("/your-route-path/", (request, response) -> {
    // your callback code
});
```

<br><br>

# 참고 자료

[Spark Framework: An expressive web framework for Kotlin and Java](https://sparkjava.com/)<br>
[Intro to Spark Java Framework | Baeldung](https://www.baeldung.com/spark-framework-rest-api)<br>
[spark framework](https://lng1982.tistory.com/263)<br>
[How to Build a Simple Spark Web Application | Engineering Education (EngEd) Program | Section](https://www.section.io/engineering-education/build-your-first-spark-web-application/)<br>
[Knowing the SparkJava Framework](https://medium.com/keleno/knowing-the-sparkjava-framework-11e57739b143)<br>
[Guide to the Spark Framework | JRebel by Perforce](https://www.jrebel.com/blog/spark-java-web-framework)<br>
[Web microservices development in Java that will Spark joy](https://blogs.oracle.com/javamagazine/post/web-microservices-development-in-java-that-will-spark-joy)<br>
[Spark Java Framework로 API 구축](https://recordsoflife.tistory.com/1387)<br>
[Microservices Deployment Cookbook](https://subscription.packtpub.com/book/web-development/9781786469434/1/ch01lvl1sec14/writing-rest-apis-with-sparkjava)<br>
[Native microservices with SparkJava and Graal | Codurance](https://www.codurance.com/publications/2018/12/28/native-microservices-with-sparkjava-and-graal)<br>
[Native microservices with SparkJava and Graal - Java Code Geeks](https://www.javacodegeeks.com/2019/01/native-microservices-sparkjava-graal.html)