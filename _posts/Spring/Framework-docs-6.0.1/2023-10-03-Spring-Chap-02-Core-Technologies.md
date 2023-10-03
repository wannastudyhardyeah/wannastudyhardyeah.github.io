---
title: 스프링 프레임워크 - 2. 핵심 기술
author: wannastudyhardyeah
date: 2023-10-03 01:20:00 +0800
categories: [Spring-Doc]
tags: [Spring, Java]
math: true
---
<div class="toc-multiple-posts">
<h2>스프링 프레임워크 문서 읽기</h2>
<ol class="sc-fmciRz gyCSrP"><a href="/posts/Spring-Chap-01-Frame-Work-Overview/">챕터 1. 개요</a><br>
<a href="/posts/Spring-Chap-02-Core-Technologies/" aria-current="page" class="active">챕터 2. 핵심 기술</a>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">2/2</div>
</div></div>
</div>
<br>
<hr width="80%">
이 파트는 스프링 프레임워크로 통합된 모든 기술들에 대하여 다루는 문서가 될 것이다.<br>

이 중에서도 가장 중요한 것은 스프링 프레임워크의 제어 역전<span style="color: #808080;">Inversion of Control</span> (IoC)이다. 이 IoC 컨테이너는 스프링의 관점 지향 프로그래밍<span style="color: #808080;">Aspect-Oriented Programming</span> (AOP) 기술에 대해 대부분의 포괄적인 내용을 철저히 준하고 있다. 스프링 프레임워크에는 스프링만의 AOP 프레임워크가 존재한다. 이는 이해하기 쉬운 데다 자바 EE<span style="color: #808080;">Enterprise Programming</span>에서 요하는 AOP 필수사항의 80퍼센트 정도의 핵심을 아주 잘 다루고 있다.<br>

스프링은 AspectJ 역시 통합하여 제공하고 있다.<br>
<br>
<hr width="80%">
<h2 id="ioc-container-h2">1. IoC 컨테이너</h2>

&nbsp;&nbsp;&nbsp;&nbsp;이 챕터에서는 스프링의 제어 역전에 대하여 다룬다.<br>

<h3 id="introduction-to-the-spring-ioc-container-and-beans"> 1.1. 스프링 IoC 컨테이너와 빈즈<span style="color: #808080;">Beans</span>에 대한 소개</h3>

&nbsp;&nbsp;&nbsp;&nbsp;이번 챕터에서는 스프링 프레임워크가 제어 역전(IoC) 원칙을 어떻게 구현하였는가를 다루는데, IoC는 의존관계(의존성) 주입<span style="color: #808080;">dependency injection</span> (DI)으로도 알려져 있다.<br>
<b><i>이것은 객체가 자신의 의존관계(즉, 다른 객체들과의 작동 방식)를 설정하는 것에 의한 과정</i></b><span style="color: #808080;">process</span><b>인데, 이는 오직 생성자 인수와 팩토리 메서드로의 인수를 통해서, 또는 팩토리 메서드로부터 반환되거나 생성된 이후에 객체 인스턴스에서 설정된 속성을 통해서만 설정된다.</b> 그리고, 컨테이너가 빈을 생성할 때 이러한 의존관계를 주입한다.<br>
이러한 과정은, 빈<span style="color: #808080;">bean</span>이 자신의 의존관계에 대한 위치나 인스턴스화가 이뤄지는 것을 스스로 제어하는 경우가 역전된 것에 기반하고 있다. 또한, 이러한 것에는 클래스의 직접적인 생성자 또는 서비스 로케이터 패턴<span style="color: #808080;">Service Locator Pattern</span>과 같은 메커니즘이 이용된다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 프레임워크의 IoC 컨테이너 중 기본이 되는 패키지는 ``org.springframework.beans``와 ``org.springframework.context``이다. 이 중에 ``BeanFactory`` 인터페이스는 어떤 타입의 객체든 사용 가능하도록 하는 고급 설정<span style="color: #808080;">configuration</span>을 제공하고, ``ApplicationContext``는 ``BeanFactory``의 하위 인터페이스로서 다음의 기능을 제공한다.<br>
- 스프링 AOP 기능들에 대하여 더 쉬워진 통합<br>
- (국제화<span style="color: #808080;">internationalization</span> 목적의) 메시지 리소스 핸들링<br>
- 이벤트 퍼블리케이션<span style="color: #808080;">Event publication</span><br>
- 웹 애플리케이션의 경우 ``WebApplicationContext``와 같은 애플리케이션 계층에 특화된 문맥<span style="color: #808080;">contexts</span><br>

요약하자면, ``BeanFactory``은 설정<span style="color: #808080;">configuration</span> 프레임워크와 기본적인 기능을, ``ApplicationContext``는 기업에 보다 특화된 기능을 제공한다.<br>
그리고 ``ApplicationContext``는 ``BeanFactory``의 완전한 상위집합이며, 이번 챕터에서 IoC 컨테이너를 설명하는 데에 오직 이것만 사용하였다.<br> ``ApplicationContext`` 대신에 ``BeanFactory``를 이용하는 것에 대해선 ``BeanFactory`` API에 관한 섹션을 참조하면 된다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;스프링에서는, 애플리케이션의 중추<span style="color: #808080;">backbone</span>를 이루고 스프링 IoC 컨테이너에 의해 관리되는 객체를 빈즈<span style="color: #808080;">beans</span>라고 부른다. 즉, 이러한 컨테이너에 의하여 인스턴스화되고 모아지고<span style="color: #808080;">assembled</span> 관리되는 객체를 빈이라고 한다. 이러한 점을 제외한다면, 빈은 그저 애플리케이션에 존재하는 수많은 객체들 중 하나에 불과하다.<br>
빈즈, 그리고 그 빈즈 사이의 의존관계는 설정 메타데이터에 반영되고, 이는 컨테이너가 사용하게 된다.<br>

<h3 id="container-overview-h3"> 1.2. 컨테이너 개요</h3>

&nbsp;&nbsp;&nbsp;&nbsp;``org.springframework.context.ApplicationContext`` 인터페이스는 스프링 IoC 컨테이너이다. 즉, 빈즈를 인스턴스화하고 설정하고 모으는 역할을 한다. 이 컨테이너는 어떤 객체를 인스턴스화하고 설정하고 모을지를 설정 메타데이터<span style="color: #808080;">configuration metadata</span>를 읽어들여 해당 명령어를 얻는데, 이 설정 메타데이터는 XML, 자바 애너테이션, 자바 코드로 표현되어 있다. 즉, 이것을 통하여 애플리케이션을 만들어낼 객체들, 그리고 그 객체들 사이의 수많은 상호 의존관계를 표현할 수 있다.<br>  

&nbsp;&nbsp;&nbsp;&nbsp;그간 XML을 이용하여 설정 메타데이터를 정의해오고 있지만, 다른 방법으로 컨테이너가 자바 애너테이션 또는 코드를 메타데이터 형식으로 이용하도록 할 수도 있다. 이러한 경우엔 XML 설정의 문서 양은 크게 줄어든다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;애플리케이션의 클래스들은 설정 메타데이터를 통하여 결합되는데, 이는 ``ApplicationContext``가 생성 및 초기화된 이후에 완전하게 설정되어 시스템이나 애플리케이션을 실행 가능하도록 하기 위함이다.<br> 

<h4 id="configuration-metadata">  1.2.1. 설정 메타데이터<span style="color: #808080;">Configuration Metadata</span></h4>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 IoC 컨테이너는 설정 메타데이터 형식으로 읽어들이는데, 이 설정 메타데이터 덕분에 애플리케이션 개발자는 스프링 컨테이너가 어떻게 객체들을 인스턴스화하고 설정하고 모을지를 알 수 있다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 설정에는 최소한 하나의 빈<span style="color: #808080;">bean</span> 정의가 존재하며 보통은 여러 개가 있는데, 이 정의는 컨테이너가 관리한다.<br>
자바를 이용한 설정은 일반적으로 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code>이 붙은 클래스에서 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Bean</code>이 붙은 메서드를 이용한다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;빈 정의는, 애플리케이션을 구성하는 실제 객체들에 대응된다. 

<h4 id="using-the-container">  1.2.2. 컨테이너 사용</h4>

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

<h3 id="bean-overview-h3"> 1.3. 빈<span style="color: #808080;">Bean</span> 개요</h3>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 IoC 컨테이너는 하나 이상의 빈을 관리한다. 이 빈즈는 개발자가 컨테이너에 제공한 설정 메타데이터를 통해 생성된다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;컨테이너 내부에는 이러한 빈 정의들이 ``BeanDefinition`` 객체로서 표현되어 있다. 그리고 아래와 같은 메타데이터들도 포함되어 있다.<br>
- 패키지 단위의 클래스명<br>
\: 일반적으로, 정의가 이뤄진 빈의 실제 클래스 구현이 있다.<br>
- 빈이 역할에 대한 설정 정보들<br>
\: 빈이 컨테이너 안에서 무엇을 해야하는지 정해져 있다.<br>
- 해당 빈에 요구되는 다른 빈에 대한 참조 사항<br>
\: 이러한 참조를 <b>컬래버레이터</b> 또는 <b>의존관계(의존성)</b>라고도 부른다.<br>
- 새로 생성되는 객체에서 설정해야 할 다른 사항들<br>
\: 예를 들어, 커넥션 풀을 관리하는 빈에서는 사용 가능한 연결들의 수나 풀의 크기 제한과 같은 것들을 들 수 있다.<br>

이러한 메타데이터는 각각의 빈 정의를 이루는 속성 정보들<span style="color: #808080;">a set of properties</span>로 변환된다. 속성들로는 아래의 테이블을 참조하면 된다.<br>

| <b>Property</b> | <b>Explained in...</b> |
|Class |Instantiating Beans |
|Name |Naming Beans |
|Scope |Bean Scopes |
|Constructor arguments |Dependency Injection |
|Properties |Dependency Injection |
|Autowiring mode |Autowiring Collaborators |
|Lazy initialization mode |Lazy-initialized Beans |
|initialization method |Initialization Callbacks |
|Destruction method |Destruction Callbacks |


<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;">&nbsp;&nbsp;&nbsp;&nbsp;빈 메타데이터, 그리고 기본적으로 제공되는 싱글톤 인스턴스들은 최대한 일찍 등록되어야 한다. 왜냐하면 자동주입, 그리고 다른 인트로스펙션 단계에서 컨테이너가 적절한 판단을 내릴 수 있도록 하기 위해서이다. 존재하는 메타데이터나 싱글톤 인스턴스를 오버라이딩 하는 건 어떤 부분에선 지원이 되는 반면, 런타임 단계에서 새로운 빈을 등록하는 건 공식적으로 지원되지 않을 뿐더러 이 경우에 빈 컨테이너에 대하여 동시 접근 예외<span style="color: #808080;">concurrent access exceptions</span>나 모순된 상태<span style="color: #808080;">inconsistent state</span>(혹은 두 가지 모두)가 발생할 수 있기 때문이다.
</div>
