# Build Tools - Ant

<img src="data:image/png;base64,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" />

[1. What is Ant?](#1-what-is-ant)  
[2. Ant Features](#2-ant-features)  
[3. Why Ant?](#3-why-ant)  

<br/>
<br/>

## 1. What is Ant?
### 1.1 Apache Ant
- Apache Ant(Another Neat Tool)
- 오픈 소스 프로젝트
- Java 라이브러리이자 명령어 기반 도구
- Java 애플리케이션의 컴파일, 실행, 테스트 및 어셈블리와 같은 소프트웨어 빌드 프로세스를 자동화한다.
- Java 외에도 C 또는 C++ 애플리케이션을 빌드하는 데 효과적으로 사용할 수 있다.
- build.xml이라는 XML 파일을 통해 빌드 코드를 정의한다.
- 빌드 파일에서 서로 의존하는 대상 및 확장 지점으로 정의된 프로세스를 구동하는 것이 임무이다.
- 일반적으로 Target과 Task로 설명될 수 있는 모든 유형의 프로세스를 파일럿하는 데 사용할 수 있다.
- Ant 사용자는 Ant Task와 Type을 포함하는 자신만의 Antlibs를 개발할 수 있다.
- 이미 만들어진 수많은 상용 또는 오픈 소스 Antlibs를 제공받을 수도 있다.
- Apache Ivy\*를 함께 사용하면 빌드 도구와 종속성 관리를 결합한 솔루션을 사용할 수 있다.

<span style="color: gray">
*Apache Ivy: 소프트웨어 프로젝트 종속성 관리를 위한 오픈 소스 프로젝트로, 프로젝트가 필요로 하는 외부 라이브러리 및 모듈을 효과적으로 관리하고 가져오는 데 사용된다.
</span>

<br/>

### 1.2 Apache Ant History
- James Duncan Davidson에 의해 시작되었다.
- 2000년 7월 19일에 처음 출시되었다.
- 2002년까지 대부분의 Java 개발 프로젝트에서 사용되는 가장 까다로운 빌드 도구였다.
- Unix의 `Make` 빌드 도구의 더 나은 대안이다.
- XML 지시어를 이용하여 Tomcat을 빌드할 수 있는 플랫폼에 독립적인 간단한 도구를 만드는 것이 목표였다.

<br/>
<br/>

## 2. Ant Features
Apache Ant는 높은 성능과 호환성 외에도 아래와 같은 특징들을 가진다.
- Flexibility(유연성)
- Easy To Use(사용성)
- Cross Platform(다양한 플랫폼에서 실행 가능)
- Extensible Architecture(확장성)
- Scalable(규모)
- Large Community(활발한 커뮤니티)

### ① Flexibility
- 유연성
- 본질적으로 매우 유연하므로 다양한 프로그래밍 언어를 손쉽게 사용할 수 있다.
- Java 외에도 C, C++와 같은 다른 유용한 프로그래밍 언어에서도 빌드를 자동화할 수 있다.

### ② Easy to Use
- 사용성
- 배우기 쉽고 사용하기 쉬운 매우 간단한 구문을 삭제한다.
- Ant 빌드 파일은 XML 태그를 통해 생성되므로 XML을 이미 알고 있는 사용자라면 더 쉽게 사용할 수 있다.

### ③ Cross Platform
- Java 클래스 경로와 파일 디렉터리 구조를 이식 가능한 방식으로 처리한다.
- 따라서 다양한 플랫폼에서 실행할 수 있다.

### ④ Extensible Architecture
- 본질적으로 확장 가능하며, 확장이 쉽다.
- Java 및 기타 프로그래밍 언어를 사용하여 확장할 수 있다.

### ⑤ Scalable
- EJB\* 컴파일 및 패키징과 같은 J2EE\* 개발을 위한 기본 지원 기능을 갖추고 있다.
- 소규모 개인 프로젝트에서 사용 가능하다.
- 대규모 소프트웨어 프로젝트에서도 사용 가능하다.

<span style="color: gray">
*EJB(Enterprise Java Bean): 기업 환경의 시스템 구현을 위한 서버 측 컴포넌트 모델 
<br/>
*J2EE(Java 2 Enterprise Edition): Java 기술로 기업 환경의 애플리케이션을 만드는데 필요한 스펙들을 모아둔 스펙 집합
</span>

### ⑥ Large Community
Apache Ant는 Apache Software Foundation의 프로젝트이다.  
따라서 활발한 커뮤니티와 문서화가 제공된다.  
[공식 웹사이트](https://ant.apache.org/)에서도 다양한 플러그인, 도구, 예제 코드 등 빠르고 정확한 정보를 얻을 수 있다.

<br/>
<br/>

## 3. Ant Examples
Ant는 build.xml이라는 XML 파일을 사용하여 애플리케이션을 빌드, 테스트 및 배포한다.  
아래와 같은 XML을 사용하면 개발자가 모든 XML 편집기에서 직접 파일을 편집할 수 있다.  
이를 통해 런타임에 빌드 파일을 쉽게 파싱하거나 생성할 수 있으며, 손쉽게 템플릿을 생성할 수 있다.  
```XML
<?xml version="1.0"?>
<project name="Hello" default="compile">
    <target name="clean" description="remove intermediate files">
        <delete dir="classes"/>
    </target>
    <target name="clobber" depends="clean" description="remove all artifact files">
        <delete file="hello.jar"/>
    </target>
    <target name="compile" description="compile the Java source code to class files">
        <mkdir dir="classes"/>
        <javac srcdir="." destdir="classes"/>
    </target>
    <target name="jar" depends="compile" description="create a Jar file for the application">
        <jar destfile="hello.jar">
            <fileset dir="classes" includes="**/*.class"/>
            <manifest>
                <attribute name="Main-Class" value="HelloProgram"/>
            </manifest>
        </jar>
    </target>
</project>
```

<br/>
<br/>

> Apache Ant를 배우기 위해서는 Java와 XML에 대한 지식이 있어야 한다. 또한 Eclipse 또는 NetBeans와 같은 IDE에도 익숙해야 한다. Apache Ant에 대해 더 알아보고 싶다면 [Apche Ant Tutorial](https://www.tutorialspoint.com/ant/index.htm) 링크를 참고해도 좋다.

<br/>
<br/>
