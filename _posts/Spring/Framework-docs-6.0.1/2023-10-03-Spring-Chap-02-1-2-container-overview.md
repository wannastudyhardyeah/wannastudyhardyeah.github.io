---
title: 스프링 프레임워크 - 2.1. IoC 컨테이너&#58; 2. 컨테이너 개요
author: wannastudyhardyeah
date: 2023-10-03 01:20:00 +0800
categories: [Spring-Doc]
tags: [Spring, Java]
math: true
---
<div class="toc-multiple-posts">
<b style="font-size:1.4rem">스프링 프레임워크 문서 읽기</b>
<ol class="sc-fmciRz gyCSrP"><a href="/posts/Spring-Chap-01-Frame-Work-Overview/">챕터 1. 개요</a><br>
챕터 2. 핵심 기술<br>
&nbsp;&nbsp;2.1. IoC 컨테이너<br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-1-introduction-to-the-spring-ioc-container-and-beans">2.1.1 스프링 IoC 컨테이너와 빈즈<span style="color: #808080;">Beans</span>에 대한 소개</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-2-container-overview" aria-current="page" class="active">2.1.2. 컨테이너 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-3-bean-overview">2.1.3. 빈<span style="color: #808080;">Bean</span> 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-4-dependencies">2.1.4. 의존 관계<span style="color: #808080;">Dependencies</span></a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-5-bean-scopes">2.1.5. 빈 스코프<span style="color: #808080;">Bean Scopes</span></a><br>
챕터 5. 웹 서블릿 스택<br>
&nbsp;&nbsp;5.1. 스프링 웹 MVC<br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-05-1-3-annoted-controllers">5.1.3. 애너테이션<span style="color: #808080;">Annotated</span> 컨트롤러</a><br>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">3/7</div>
</div></div>
</div>
<br>
<hr width="80%">
<h3 id="container-overview-h3"> 1.2. 컨테이너 개요</h3>

&nbsp;&nbsp;&nbsp;&nbsp;``org.springframework.context.ApplicationContext`` 인터페이스는 스프링 IoC 컨테이너이다. 즉, 빈즈를 인스턴스화하고 설정하고 모으는 역할을 한다. 이 컨테이너는 어떤 객체를 인스턴스화하고 설정하고 모을지를 설정 메타데이터<span style="color: #808080;">configuration metadata</span>를 읽어들여 해당 명령어를 얻는데, 이 설정 메타데이터는 XML, 자바 애너테이션, 자바 코드로 표현되어 있다. 즉, 이것을 통하여 애플리케이션을 만들어낼 객체들, 그리고 그 객체들 사이의 수많은 상호 의존관계를 표현할 수 있다.<br>  

&nbsp;&nbsp;&nbsp;&nbsp;그간 XML을 이용하여 설정 메타데이터를 정의해오고 있지만, 다른 방법으로 컨테이너가 자바 애너테이션 또는 코드를 메타데이터 형식으로 이용하도록 할 수도 있다. 이러한 경우엔 XML 설정의 문서 양은 크게 줄어든다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;애플리케이션의 클래스들은 설정 메타데이터를 통하여 결합되는데, 이는 ``ApplicationContext``가 생성 및 초기화된 이후에 완전하게 설정되어 시스템이나 애플리케이션을 실행 가능하도록 하기 위함이다.<br> 

<h4 id="configuration-metadata">  1.2.1. 메타데이터 설정<span style="color: #808080;">Configuration</span></h4>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 IoC 컨테이너는 설정 메타데이터 형식으로 읽어들이는데, 이 설정 메타데이터 덕분에 애플리케이션 개발자는 스프링 컨테이너가 어떻게 객체들을 인스턴스화하고 설정하고 모을지를 알 수 있다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 설정에는 최소한 하나의 빈<span style="color: #808080;">bean</span> 정의가 존재하며 보통은 여러 개가 있는데, 이 정의는 컨테이너가 관리한다.<br>
자바를 이용한 설정은 일반적으로 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code>이 붙은 클래스에서 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Bean</code>이 붙은 메서드를 이용한다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;빈 정의는, 애플리케이션을 구성하는 실제 객체들에 대응된다. 

<h4 id="instantiating-a-container">  1.2.2. 컨테이너 인스턴스화하기</h4>
<h4 id="using-the-container-h4">  1.2.3. 컨테이너 사용</h4>

&nbsp;&nbsp;&nbsp;&nbsp;``ApplicationContext`` 인터페이스는 서로다른 빈즈와 그들의 의존관계 등록을 유지해주는 발전된 팩토리 패턴이다. ``T getBean(String name, Class<T> requiredType)`` 메서드를 이용하여 찾고자 하는 빈즈의 인스턴스를 찾아올 수 있다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;아래의 예제와 같이, ``ApplicationContext``를 통하여 빈 정의를 접근하여 읽을 수 있다.<br>

```java
// create and configure beans
ApplicationContext context 
            = new ClassPathXmlApplicationContext("services.xml",
"daos.xml");

// retrieve configured instance
PetStoreService service 
            = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList 
            = service.getUsernameList();
```
