# Build Tools - Maven

<img src="data:image/png;base64,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" />

[1. What is Maven?](#1-what-is-maven)  
[2. Maven Features](#2-maven-features)  
[3. Why Maven?](#3-why-maven)  
[4. Maven Examples](#4-maven-examples)

<br/>
<br/>

## 1. What is Maven?
### 1.1 Maven
- 주로 Java 기반의 프로젝트에서 사용되는 오픈 소스 빌드 도구
- 프로젝트의 빌드 인프라에 패턴을 적용하려는 시도로도 볼 수 있다.
- 표준 규칙과 관행을 채택하여 개발 주기를 단축하고, 동시에 빌드 성공률을 높인다.
- 본질적으로 프로젝트 관리 및 이해 도구이며, 다음과 같은 작업들의 관리를 도운다.
	- Builds
	- Documentation
	- Reporting
	- Dependencies
	- SCMs\*
	- Releases
	- Distribution

<span style="color: gray">
*SCM(Source Code Management): 소스 코드 관리, 소스 코드를 효과적으로 관리하고 추적하기 위한 도구
</span>

<br/>

### 1.2 Maven History
Maven은 Jakarta Turbine 프로젝트의 빌드 프로세스를 간소화하기 위한 시도로 시작되었다. Jakarta Turbine 프로젝트는 조금씩 다른 Ant 빌드 파일을 가진 여러 프로젝트로 이루어져 있었다. 이러한 프로젝트를 빌드하는 표준 방법, 프로젝트 구성 요소에 대한 명확한 정의, 프로젝트 정보를 쉽게 게시할 수 있는 방법, 그리고 여러 프로젝트에 JAR를 공유할 수 있는 방법을 바로 Maven에서 제공한다.

<br/>
<br/>

## 2. Maven Features
- Simple project setup(간단한 프로젝트 설정)
- Consistent usage(일관된 사용)
- Superior dependency management(뛰어난 종속성 관리)
- Able to easily work with multiple projects at the same time(동시에 여러 프로젝트 작업 가능)
- Libraries, metadata and open source to use out of the box(즉시 사용 가능한 라이브러리, 메타데이터, 그리고 오픈 소스)
- Extensibility(확장성)
- Instant access to new features with little or no extra configuration(추가 구성 없이 새로운 기능에 즉시 액세스 가능)
- Ant tasks for dependency management and deployment outside of Maven(Maven 외부의 종속성 관리 및 배포를 위한 Ant 작업)
- Model based builds(모델 기반 빌드)
- Coherent site of project information(일관된 프로젝트 정보 사이트)
- Release management and distribution publication(릴리즈 관리 및 배포 게시)
- Dependency management(종속성 관리)

### ① Simple project setup
- Simple project setup that follows best practices
- 모범 가이드라인에 따른 간단한 프로젝트 설정이 가능하다.
- Maven을 사용하여 몇 초 만에 새로운 프로젝트 또는 모듈을 시작할 수 있다.

### ② Consistent usage
- Consistent usage across all projects
- 모든 프로젝트에서 일관적으로 사용할 수 있다.
- 새로운 개발자가 프로젝트에 합류하는 데 걸리는 시간을 단축할 수 있다.

### ③ Superior dependency management
- Superior dependency management including automatic uploading, dependency closures
- 자동 업데이트, 전이 종속성\* 등 뛰어난 종속성 관리가 가능하다.

<span style="color: gray">
*전이 종속성: 프로그램이 직접 참조하는 구성 요소로 인해 발생하는 종속성이다. 예를 들어, `log()` 함수 호출 시 일반적으로 파일에 로그 메시지를 쓰는 I/O 라이브러리에 전이 종속성이 적용된다.
</span>

### ④ Able to easily work with multiple projects at the same time
- 여러 프로젝트를 동시에 쉽게 작업할 수 있다.

### ⑤ Libraries, metadata and open source to use out of the box
- A large and growing repository of libraries and metadata to use out of the box, and arrangements in place with the largest Open Source projects for real-time availability of their latest releases
- 대규모의 라이브러리 및 메타데이터 리포지토리를 즉시 사용할 수 있다.
- 최신 릴리즈를 실시간으로 이용할 수 있도록 대규모 오픈 소스 프로젝트와 협력하고 있다.

### ⑥ Extensibility
- Extensible, with the ability to easily write plugins in Java or scripting languages
- Java 또는 스크립트 언어로 플러그인을 쉽게 작성할 수 있는 확장성을 제공한다.

### ⑦ Instant access to new features with little or no extra configuration
- 추가적인 구성 없이도 새로운 기능에 즉시 액세스가 가능하다.

### ⑧ Ant tasks for dependency management and deployment outside of Maven
- Maven 외부의 종속성 관리 및 배포를 위한 Ant 작업이 가능하다.

### ⑨ Model based builds
- 모델 기반 빌드
- Maven은 사전 정의된 output 유형으로 프로젝트를 원하는 만큼 빌드할 수 있다.
	- 대부분 스크립트를 작성할 필요 없다.
	- 사전 정의된 output 유형에는 JAR, WAR 또는 프로젝트 메타데이터 기반 배포가 포함된다.

### ⑩ Coherent site of project information
- 일관된 프로젝트 정보 사이트
- 빌드 프로세스와 동일한 메타데이터를 사용하여 추가하고 싶은 문서를 포함한 웹 사이트/PDF 생성이 가능하다.
- 프로젝트의 개발 상태에 대한 표준 보고서도 추가할 수 있다.

### ⑪ Release management and distribution publication
- 릴리즈 관리 및 배포 게시
- 별다른 추가 구성 없이 SCM\*과 통합되어 특정 태그를 기반으로 프로젝트의 릴리즈를 관리한다.
- 다른 프로젝트에서 사용 가능하도록 배포 위치에 게시할 수 있다.
- 개별 결과물을 게시할 수 있다.
	- 예시) JAR, 기타 종속성 및 문서를 포함한 아카이브 또는 소스 배포 등

<span style="color: gray">
*SCM(Source Code Management): 소스 코드 관리를 의미하며, Git, Subversion, Mercurial 등이 있다.
</span>

### ⑫ Dependency management
- 종속성 관리
- JAR 및 기타 종속성의 central repository 사용을 권장한다.
- JAR central repository에서 프로젝트 빌드에 필요한 모든 JAR를 다운로드하는 메커니즘을 제공한다.
- 여러 프로젝트에서 JAR를 재사용할 수 있다.
- 프로젝트 간의 커뮤니케이션을 장려하여 이전 버전과의 호환성 문제를 해결할 수 있도록 돕는다.

<br/>
<br/>

## 3. Why Maven?
이번에는 Maven을 왜 사용해야 하는지 Maven에 대한 장점을 소개하고자 한다.
- Easy Build Process(쉬운 빌드 프로세스)
- Provide Uniform Build System(일관된 빌드 시스템 제공)
- Provide Quality Project Information(양질의 프로젝트 정보 제공)
- Better Development Practice(더 나은 개발 실습)

### ① Easy Build Process
Maven은 빌드 프로세스를 더 쉽게 만들어준다.  
Maven을 사용해도 기본 메커니즘을 아는 것은 중요하다.

### ② Provide Uniform Build System
Maven은 POM\*과 플러그인들을 사용하여 프로젝트를 빌드한다.  
하나의 Maven 프로젝트에 익숙해지면 모든 Maven 프로젝트가 어떻게 빌드되는지 알 수 있다. 이렇게 하면 많은 프로젝트를 탐색할 때 시간을 절약할 수 있다.

<span style="color: gray">
*POM(Project Object Model): 프로젝트 객체 모델로, pom.xml이라는 파일에 저장된 Maven 프로젝트의 XML 표현이다. 프로젝트의 구성 파일, 참여한 개발자와 역할, 결함 추적 시스템, 조직 및 라이선스, 프로젝트가 포함된 URL, 프로젝트의 종속성 등의 요소들이 포함되어 있다. 이러한 pom.xml 파일은 코드 없이 프로젝트에 관한 모든 것을 해결할 수 있는 중요한 역할을 담당한다.
</span>

### ③ Provide Quality Project Information
Maven은 부분적으로는 POM에서, 부분적으로는 프로젝트의 소스 코드에서 생성된 정보를 제공한다.  
Maven이 제공할 수 있는 프로젝트 정보는 아래와 같다.
- Change log created directly from source control (SCM에 의해 추적된 변경 로그)
- Cross referenced sources (각 클래스, 메서드, 변수 등의 상호 참조를 분석 후 보고서 생성)
- Mailing lists managed by the project (프로젝트 참여/지원을 위한 커뮤니케이션 채널 정보)
- Dependencies used by the project (pom.xml 파일을 기반으로 프로젝트 종속성 정보 제공)
- Unit test reports including coverage (프로젝트 테스트 커버리지를 포함한 단위 테스트 보고서)

### ④ Better Development Practice
- Maven은 모범적인 개발 가이드라인을 통해 개발 방향을 안내한다.  
- 예시 1) 단위 테스트
	- 테스트 코드를 별도의 병렬 소스 트리에 보관하기
	- 테스트 케이스의 명명 규칙을 사용하여 테스트 찾기 및 실행하기
	- 테스트 준비를 위한 환경을 테스트 케이스를 통해 설정하기
- 예시 2) 릴리즈 및 이슈 관리와 같은 프로젝트 워크플로우 지원
- 예시 3) 프로젝트의 디렉토리 구조 레이아웃에 대한 가이드라인

참고로, Maven은 프로젝트 레이아웃에 대해 독자적인 접근 방식을 가지므로, 일부 프로젝트는 해당 구조에 적합하지 않을 수 있다. Maven은 이러한 문제점을 보완하고자 다양 프로젝트의 다양한 요구에 유연하게 대응할 수 있도록 설계되었다. 하지만 그럼에도 불구하고 모든 상황을 충족시킬 수는 없다. 즉, 프로젝트에 재구성할 수 없는 비정상적인 빌드 구조가 있는 경우 Maven을 사용할 수 없다는 의미이다.

<br/>
<br/>

## 4. Maven Examples
[다음은 Maven을 사용하여 간단한 Java 프로젝트를 빌드하기 위한 예시 코드이다.](https://spring.io/guides/gs/maven/)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
		 https://maven.apache.org/xsd/maven-4.0.0.xsd"> 

	<modelVersion>4.0.0</modelVersion>
	
	<groupId>org.springframework</groupId>
	<artifactId>gs-maven</artifactId>
	<packaging>jar</packaging>
	<version>0.1.0</version>
	
	<properties>
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
	</properties>
	
	<dependencies>
		<!-- tag::joda[] -->
		<dependency>
			<groupId>joda-time</groupId>
			<artifactId>joda-time</artifactId>
			<version>2.9.2</version>
		</dependency>
		<!-- end::joda[] -->
		
		<!-- tag::junit[] -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>
		<!-- end::junit[] -->
	</dependencies>
	
	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-shade-plugin</artifactId>
				<version>3.2.4</version>
				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>shade</goal>
						</goals>
						<configuration>
							<transformers>
								<transformer
									implementation=							
										"org.apache.maven
										.plugins.shade.resource
										.ManifestResourceTransformer">
								<mainClass>hello.HelloWorld</mainClass>
								</transformer>
							</transformers>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
</project>
```

| Syntax | Description |
| - | - |
| `<project>` | Maven 프로젝트의 루트 요소 |
| `<modelVersion>` | Maven POM 모델 버전 |
| `<groupId>` | 프로젝트가 속한 그룹/조직을 나타내며, 종종 도메인 이름으로 표시되기도 한다. Maven central repository에서 프로젝트를 고유하게 식별하는 데 사용된다. |
| `<artifactId>` | 프로젝트 라이브리러 아티팩트에 부여할 이름으로, 빌드된 아티팩트(JAR, WAR 파일 이름 등)의 이름에 사용된다. |
| `<packaging>` | 프로젝트의 패키징 유형을 나타내며, 위의 코드의 경우 JAR 파일로 패키징된다. 참고로, 선택 사항이다. |
| `<version>` | 빌드할 프로젝트의 버전 |
| `<properties>` | 프로젝트에서 사용하는 속성을 정의한다. |
| `<dependency>` | 프로젝트의 종속성을 정의한다. |
| `<build>` | 빌드 관련 설정을 포함한다. |
| `<plugin>` | Maven 플러그인 설정을 정의한다. |
| `<execution>` | 플러그인 실행 구성을 정의한다. |
| `<phase>` | 빌드 라이프사이클의 어느 단계에서 실행할지를 지정한다. |
| `<goal>` | 실행할 goal을 나타낸다 |
| `<configuration>` | 변환기 설정을 정의한다. |
| `<transformer>` | JAR 파일의 매니페스트를 조작한다. |
| `<mainClass>` | JAR 파일이 실행될 때의 메인 클래스를 지정한다. |

<br/>
<br/>

> 참고로, [Maven Repository](https://mvnrepository.com/)라는 웹 사이트는 Apache Maven의 종속성을 검색하고 찾을 수 있는 서비스를 제공한다. 해당 웹 사이트의 주요 기능으로는 라이브러리 검색, 라이브러리 정보 확인, 종속성 코드 예제, 최신 버전 확인, 그리고 라이브러리 인기 차트 등이 있다.

<br/>
<br/>
