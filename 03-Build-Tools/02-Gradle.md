# Build Tools - Gradle

<img src="data:image/png;base64,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" />

[1. What is Gradle?](#1-what-is-gradle)
[2. Gradle Features](#2-gradle-features)  
[3. Why Gradle?](#3-why-gradle)
[4. Gradle Examples](#4-gradle-examples)

<br/>
<br/>

## 1. What is Gradle?
### 1.1 [Gradle](https://gradle.org/)
- 오픈 소스 <u>빌드 자동화</u> 도구
- 플러그인 기반 빌드 도구 (이때, 다양한 프로그래밍 언어로 플러그인을 만들 수 있다.)
- 소프트웨어를 테스트, 빌드, 출시할 수 있도록 도와준다.
- Apache Maven과 Apache Ant의 개념을 기반으로 하며, 이들의 문제점을 보완하고 있다.
- 주로 규모가 꽤 큰 다중 프로젝트의 빌드 자동화를 위해 개발되었다.
- 웹 및 모바일 애플리케이션의 코드 컴파일부터 패키징까지의 개발 생명주기를 도와주는 모델을 제공한다.

<br/>

### 1.2 Gradle History
- 2007년에 처음 출시되어 2019년 11월 18일에 안정적인 버전으로 출시되었다.
- 상위 20개의 오픈 소스 프로젝트에 포함되어 있다.
	- 예시) LinkedIn, Android, Netflix, Adobe, Elastic 등
- 대규묘 프로젝트에서 사용된다.
	- 예시) Spring, Hibernate, Grails 등
- 다양한 IDE에서 Gradle을 편리하게 사용할 수 있다.
	- 예시) Android Studio, IntelliJ IDEA, Eclipse, NetBeans 등

<br/>

### 1.3 Gradle Core Concepts
- Project configuration 설정에 XML 대신 Java 및 Groovy 기반의 DSL\*을 도입했다.
- 작업을 실행하는 순서를 정의하기 위해 DAG\*을 사용한다.
- 모든 Gradle 빌드에는 하나 이상의 Project\*가 포함되며, Project에는 몇 가지 Task\*가 포함된다.

#### ① Project
- 애플리케이션을 staging 혹은 production(운영) 환경에 배포하는 것을 말한다.
- Gradle의 각 프로젝트는 하나 이상의 Task로 구성된다.
- 예시) 라이브러리 JAR, 웹 애플리케이션, 다른 프로젝트에서 생성한 JAR(배포된 ZIP) 등

#### ② Task
- Gradle에서 Task는 빌드가 수행하는 단일 작업을 의미한다.
- 예시) 클래스 컴파일, JAR 생성, Javadoc 생성, (일부를) 리포지토리에 게시하는 등

<span style="color: gray">
*staging: 실제 운영 환경과 유사하며, 개발자나 QA 팀이 테스트를 수행하는 환경<br/>
*DSL(Domain Specific Language): 특정 문제에 최적화된 높은 수준의 추상화를 갖춘 프로그래밍 언어<br/>
*DAG(Directed Acyclic Graph): 비순환 그래프(일방향성)
</span>

<br/>
<br/>

## 2. Gradle Features
Gradle의 주목할 만한 기능은 다음과 같다.
- High Performance(고성능)
- Free and Open Source(무료 오픈 소스)
- Supports Ant Tasks and Maven Repositories(Ant Task 및 Maven 리포지토리 지원 제공)
- Multi-Project Build Support(멀티 프로젝트 빌드 지원)
- Extensibility(확장성)
- Incremental Builds(점진적 빌드)
- Familiar with the Java(Java 친화력)
- IDE Support(IDE 지원)
- Build Scans(빌드 스캔)

### ① High Performance
Gradle은 <u>이전 실행의 output을 재사용하여 Task를 빠르게 완료</u>한다.  
Input이 변경된 경우에만 Task를 실행하며, 이때의 Task는 병렬로 실행된다.  
따라서 불필요한 작업을 피하고, 더 빠른 성능을 제공한다.

### ② Free and Open Source
Gradle은 오픈 소스이며, Apache License\* 라이선스가 부여된다.

<span style="color: gray">
*Apache License(ASL): Apache 소프트웨어 재단에서 제공하는 소프트웨어 라이선스 중 하나로, 오픈 소스 소프트웨어 프로젝트에서 많이 사용된다.
</span>

### ③ Supports Ant Tasks and Maven Repositories
**Supports Ant Tasks**
- Gradle은 Ant 빌드 프로젝트를 지원한다.
- Gradle은 Ant 빌드 프로젝트를 가져와서(속성, 경로 등 포함) 모든 Task를 재사용할 수 있다.
- Ant 기반의 Gradle Task를 만들 수 있다.

**Supports Maven Repositories**
- Gradle은 Maven 리포지토리를 지원한다.
- Gradle은 Maven 리포지토리의 사용 가능한 모든 리포지토리 인프라를 계속 사용할 수 있다.\*

<span style="color: gray">
*Maven 리포지토리가 프로젝트의 종속성(dependency)을 게시하고 가져오도록 설계되어 있기에 가능하다.
</span>

### ④ Multi-Project Build Support
- Gradle은 멀티 프로젝트(루트 프로젝트 + 하위 프로젝트) 빌드를 지원한다.
- Gradle을 사용하여 레이아웃을 유연하게 정의할 수 있다.
- Gradle은 프로젝트의 종속성을 분석하여 재빌드가 필요한 해당 프로젝트를 부분 빌드한다.

### ⑤ Extensibility
- Task 유형이나 빌드 모델을 제공하기 위해 Gradle을 쉽게 확장할 수 있다.
- 예시) Android Build Supports는 Flavor\*과 빌드 유형 등 새로운 빌드 개념을 추가하였다.

<span style="color: gray">
*Flavor: 빌드 프로세스를 구성하는 데 사용되는 여러 가지의 빌드 구성 옵션을 정의하는 메커니즘이다. Flavor는 애플리케이션의 특정 버전 또는 환경을 나타내며, 이를 통해 여러 가지 빌드 유형을 생성하고 관리할 수 있다. Flavor를 사용하여 동일한 코드 베이스를 기반으로 한 서로 다른 버전이나 환경의 애플리케이션을 생성할 수 있다.
</span>

### ⑥ Incremental Builds
Gradle은 필요한 Task만 실행하는 Incremental Build를 지원한다.  
소스 코드 컴파일 시 이전 실행 이후 소스가 변경되었는지 확인한다. 만약 코드가 변경된 경우 빌드가 실행되지만, 코드가 변경되지 않은 경우 실행을 건너뛰고 해당 Task를 업데이트된 것으로 표시한다.  

### ⑦ Familiar with the Java
- Gradle을 실행하려면 JVM이 필요하므로, JDK가 필요하다.\*
- Gradle의 플러그인 및 사용자 지정 Task와 같은 빌드 로직에서 표준 Java API를 사용할 수 있다.
- Gradle은 JVM 상에서 실행되므로, 다양한 플랫폼에서 Gradle을 쉽게 실행할 수 있다.
- 참고로, Gradle은 JVM 프로젝트 빌드에만 국한되지 않고, 네이티브 프로젝트 빌드도 지원한다.

<span style="color: gray">
*JDK(Java Development Kit)는 JVM(Java Virtual Machine)을 포함하고 있다.
</span>

### ⑧ IDE Support
- Gradle은 여러 IDE를 지원한다.
- 마찬가지로, 여러 IDE도 Gradle 빌드를 가져오는 것을 지원한다.

### ⑨ Build Scans
- 빌드 문제를 식별하는 데 사용할 수 있는 빌드 실행에 대한 정보를 제공한다.
- 빌드 성능 문제를 진단하는 데 도움이 된다.
- 다른 사람들과 공유할 수 있어 빌드 문제를 해결하기 위한 조언을 구할 수도 있다.

### ⑩ Supports Multiple Languages
- 예시) Java, <u>Kotlin</u>, <u>Groovy</u>, Scala, C/C++, JavaScript 등의 언어와 플랫폼에서 사용된다.

<br/>
<br/>

## 3. Why Gradle?
이번에는 Gradle을 왜 사용해야 하는지 Gradle에 대한 장점을 소개하고자 한다.
- Highly Customizable(사용자 정의 가능)
- Performance(성능)
- Flexibility(유연성)
- User Experience(사용자 경험)
- Gradle is a General-Purpose Build Tool(범용 빌드 도구)

### ① Highly Customizable
- 사용자 정의가 가능하다.
- 확장성이 뛰어나다.
- Gradle은 다양한 기술을 사용하는 다양한 프로젝트에 맞게 사용자 지정이 가능하다.

### ② Performance
- 성능이 매우 빠르다.
- 모든 시나리오에서 Maven보다 약 2배 더 빠르다.
- 빌드 캐시를 사용하는 대규모 빌드에서는 Maven보다 약 100배 더 빠르다.

### ③ Flexibility
Gradle은 플러그인 기반 빌드 도구이므로, 배포 후 기능 추가가 필요한 경우 플러그인을 만들어 코드베이스에 대한 제어 권한을 부여하면 된다.

### ④ User Experience
- Gradle은 향상된 사용자 경험을 제공하기 위해 다양한 IDE를 지원한다.
- Gradle은 터미널 환경을 위한 명령어 기반 인터페이스(Command Line Interface)를 제공한다.
- 빌드 디버깅 및 최적화를 위한 대화형 웹 기반 UI(Interactive Web-based UI)도 제공한다.

### ⑤ Gradle is a General-Purpose Build Tool
- Gradle은 범용 빌드 도구이다.
- Gradle은 모든 유형의 소프트웨어를 빌드할 수 있다.

<br/>
<br/>

## 4. Gradle Examples
[다음은 Gradle을 사용하여 간단한 Java 프로젝트를 빌드하기 위한 예시 코드이다.](https://spring.io/guides/gs/gradle/)
```Groovy
apply plugin: 'java' 
apply plugin: 'eclipse' 
apply plugin: 'application' 

mainClassName = 'hello.HelloWorld' 

// tag::repositories[] 
repositories { 
	mavenCentral() 
} 
// end::repositories[] 

// tag::jar[] 
jar { 
	archiveBaseName = 'gs-gradle' 
	archiveVersion = '0.1.0' 
}
// end::jar[]

// tag::dependencies[]
sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
	implementation "joda-time:joda-time:2.2" 
	testImplementation "junit:junit:4.12" 
}
// end::dependencies[]

// tag::wrapper[]
// end::wrapper[]
```

| Syntax | Description |
| - | - |
| `apply plugin` | 특정 플러그인을 해당 프로젝트에 추가하여 실행 가능한 상태로 만든다. |
| `mainClassName` | 실행 가능한 JAR 파일이 실행될 때 찾아갈 메인 클래스를 지정한다. |
| `repositories` | Maven central repository에서 종속성을 해결하기 위한 저장소를 설정한다. 위에서는 `mavenCentral()`을 사용한다고 정의했다. |
| `jar` | JAR 파일을 생성할 때의 설정을 정의한다. |
| `jar { archiveBaseName }` | JAR 파일의 기본 이름을 지정한다. |
| `jar { archiveVersion }` | JAR 파일의 버전을 지정한다. |
| `source/targetCompatibility` | Java 소스 코드 및 대상의 호환성을 설정한다. |
| `dependencies { ... }` | 프로젝트의 종속성을 정의한다. |

<br/>
<br/>

> 참고로, Gradle을 공부하기 위해서는 Java와 Groovy 프로그래밍에 대한 기본 지식이 필요하다.

<br/>
<br/>
