---
title: 1.1. 프로젝트 생성
author: wannastudyhardyeah
date: 2023-06-15 01:17:00 +0800
categories: [Spring]
tags: [Spring, JAVA]
math: true

---
<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">spring initializr를 통해 생성</h2>
<p style="font-size:1.3em"><b><a href="https://start.spring.io/">spring initializr(클릭)</a>를 통해 생성하기</b></p>
- Project<br>
``Gradle - Groovy`` 선택<br>
- Language<br>
``Java`` 선택<br>
- Spring Boot(버전)<br>
``2.7.12``(3.0 미만의 버전) 선택<br>
(3.0 이상의 버전을 선택하게 되면, JAVA 17 이상을 설치해야 함)<br>
- Project Metadata<br>
    - Group<br>
    임의로 입력하면 됨<br>
    - Artifact<br>
    <a href="https://github.com/spring-io/start.spring.io/blob/main/USING.adoc#other-options">"프로젝트명을 암시한다"</a>
    - Name<br>
    프로젝트의 표시되는 이름<br>
    - Description<br>
    프로젝트 설명<br>
    - Package name<br>
    <a href="https://github.com/spring-io/start.spring.io/blob/main/USING.adoc#other-options">"본 프로젝트의 루트 패키지로, 보통의 경우에는 ``Group`` 속성의 값을 사용함."</a>
    - Packaging<br>
    ``Jar`` 선택<br>
    - Java<br>
    ``11`` 선택<br>
- Dependencies<br>
어떤 라이브러리를 쓸 것인가?<br>
"ADD DEPENDENCIES..." 클릭<br>
``Spring Web`` 선택<br>
``Thymeleaf`` 선택<br>
(템플릿 엔진 中 1)<br>

- GENERATE<br>
``GENERATE`` 누르기<br>
``"(name).zip"`` 파일 다운로드 받은 뒤 압축 풀기<br>
<br>

<p style="font-size:1.3em"><b>IntelliJ에서 열기</b></p>
``Open or Import`` 클릭 후,<br>
압축을 푼 폴더에서 ``(name) > build.gradle`` 파일을<br>
``Open as Project``로 열기<br>

- ``(name) > src``<br>
    - ``\main``
        - ``\java``
        - ``\resources``<br>
        \: java 코드 파일을 제외한, 여러 파일들(html, xml 등)이 있음<br>
    - ``\test``<br>
    \: 테스트 코드 영역
- ``(name) > build.gradle``<br>
\: spring initializr를 통해 설정했던 것들이 있음<br>
<br>
<p style="font-size:1.3em"><b>프로젝트 실행</b></p>

아래 메서드 ``main``을 실행<br>
```java
// hello-spring > ~ > main > java > ~ > HelloSpringApplication.java   
    public static void main(String[] args) {
        SpringApplication.run(HelloSpringApplication.class, args);
    }
```
<br>

이때, 아래 콘솔창에서<br>

```
Executing ':HelloSpringApplication.main()'...

> Task :compileJava
> Task :processResources
> Task :classes

> Task :HelloSpringApplication.main()

2023-06-16 20:14:24.559  INFO 23696 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
```
<br>

``Tomcat``과 ``8080``에 주목!<br>

그리고 웹 브라우저에서<br>
``localhost:8080``을 주소창에 입력한다.<br>
그러면,<br>
이렇게 에러 페이지가 뜨는 걸 확인할 수 있다.<br>

<!-- fig_001 -->
<img src="https://github.com/wannastudyhardyeah/wannastudyhardyeah.github.io/blob/master/images/Spring/2023-06-15-Spring-01-01-Start-Project/fig_001_browser.png?raw=true" width="100%">

<br>
