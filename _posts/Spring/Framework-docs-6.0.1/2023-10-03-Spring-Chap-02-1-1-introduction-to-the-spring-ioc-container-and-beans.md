---
title: 스프링 프레임워크 - 2.1. IoC 컨테이너&#58; 1. 스프링 IoC 컨테이너와 빈즈에 대한 소개 
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
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-1-introduction-to-the-spring-ioc-container-and-beans" aria-current="page" class="active">2.1.1 스프링 IoC 컨테이너와 빈즈<span style="color: #808080;">Beans</span>에 대한 소개</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-2-container-overview">2.1.2. 컨테이너 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-3-bean-overview">2.1.3. 빈<span style="color: #808080;">Bean</span> 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-4-dependencies">2.1.4. 의존 관계<span style="color: #808080;">Dependencies</span></a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-5-bean-scopes">2.1.5. 빈 스코프<span style="color: #808080;">Bean Scopes</span></a><br>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">2/6</div>
</div></div>
</div>
<br>
<hr width="80%">
이 파트는 스프링 프레임워크로 통합된 모든 기술들에 대하여 다루는 문서가 될 것이다.<br>

이 중에서도 가장 중요한 것은 스프링 프레임워크의 제어 역전<span style="color: #808080;">Inversion of Control</span> (IoC)이다. 이 IoC 컨테이너는 스프링의 관점 지향 프로그래밍<span style="color: #808080;">Aspect-Oriented Programming</span> (AOP) 기술에 대해 대부분의 포괄적인 내용을 철저히 준하고 있다. 스프링 프레임워크에는 스프링만의 AOP 프레임워크가 존재한다. 이는 이해하기 쉬운 데다 자바 EE<span style="color: #808080;">Enterprise Programming</span>에서 요하는 AOP 필수사항의 80퍼센트 정도의 핵심을 아주 잘 다루고 있다.<br>

스프링은 AspectJ 역시 통합하여 제공하고 있다.<br>
<br>
<hr width="80%">

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