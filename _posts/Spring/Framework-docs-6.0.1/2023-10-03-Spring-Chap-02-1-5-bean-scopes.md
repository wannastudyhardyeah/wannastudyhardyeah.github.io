---
title: 스프링 프레임워크 - 2.1. IoC 컨테이너&#58; 5. 빈 스코프
author: wannastudyhardyeah
date: 2023-10-03 23:58:00 +0800
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
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-2-container-overview">2.1.2. 컨테이너 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-3-bean-overview">2.1.3. 빈<span style="color: #808080;">Bean</span> 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-4-dependencies">2.1.4. 의존 관계<span style="color: #808080;">Dependencies</span></a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-5-bean-scopes" aria-current="page" class="active">2.1.5. 빈 스코프<span style="color: #808080;">Bean Scopes</span></a><br>
챕터 5. 웹 서블릿 스택<br>
&nbsp;&nbsp;5.1. 스프링 웹 MVC<br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-05-1-3-annoted-controllers">5.1.3. 애너테이션<span style="color: #808080;">Annotated</span> 컨트롤러</a><br>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">6/7</div>
</div></div>
</div>
<br>
<hr width="80%">
<h3 id="dependencies-h3"> 1.5. 빈 스코프</h3>

&nbsp;&nbsp;&nbsp;&nbsp;빈을 정의한다는 것은, 바로 그 정의에 있는 클래스의 실제 인스턴스에 대한 레시피를 만드는 것이다. 빈 정의를 레시피에 빗댄 표현은 중요한데, 이는 곧 클래스와 함께 단일 레시피로부터 수많은 객체 인스턴스들을 생성할 수 있다는 뜻이기 때문이다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;개발자가 제어할 수 있는 것은 특정 빈 정의로부터 생성된 객체에 연결돼있는 다양한 의존관계와 값 설정 뿐만 아니라, 마찬가지로 이로부터 생성된 객체의 스코프<span style="color: #808080;">scope</span>도 해당된다. 이는 매우 강력하면서도 유동성 있는 접근법으로, 이로써 자바 클래스 단계에 있는 객체의 스코프를 건드려야 하는 대신에, 설정을 통해 생성한 객체의 스코프를 선택할 수 있기 때문이다. 빈즈는 여러 스코프들 중 하나로 정의될 수 있고, 스프링 프레임워크에서 지원하는 스코프는 여섯 가지이며, 이 중 4개는 웹 개발에 ``ApplicationContext``를 사용할 경우 사용가능한 것이다. 또한 개발자는 커스텀 스코프를 생성할 수 있다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;아래 테이블은 공식적으로 지원하는 여섯 가지의 스코프에 대한 설명이다.<br>

| <b>Scope</b> | <b>Description</b> |
| singleton | {기본설정}<br>각 스프링 IoC 컨테이너의 단일 객체 인스턴스에 대한<br>단일 빈 정의의 범위<span style="color: #808080;">scope</span> |
| prototype | 여러 개의 객체 인스턴스들에 대한<br>단일 빈 정의의 범위 |
| request | 단일 HTTP 요청의 생명주기<span style="color: #808080;">lifecycle</span>에 대한<br>단일 빈 정의의 범위.<br>즉, 각 HTTP 요청은 싱글 빈 정의로부터 생성된<br>단일 빈의 인스턴스를 가진다.<br>웹 개발에 ``ApplicationContext``를 사용할 경우 사용가능. |
| session | 하나의 HTTP ``session``의 생명주기에 대한 <br>단일 빈 정의의 범위.<br>웹 개발에 ``ApplicationContext``를 사용할 경우 사용가능. |
| application | ``ServletContext``의 생명주기에 대한 <br>단일 빈 정의의 범위.<br>웹 개발에 ``ApplicationContext``를 사용할 경우 사용가능. |
| websocket | ``WebSocket``의 생명주기에 대한 <br>단일 빈 정의의 범위.<br>웹 개발에 ``ApplicationContext``를 사용할 경우 사용가능. |

<h4 id="the-singleton-scope-h4">  1.5.1. 싱글톤<span style="color: #808080;">Singleton</span> 스코프</h4>

&nbsp;&nbsp;&nbsp;&nbsp;싱글톤 빈의 공유 인스턴스는 오직 하나만 관리되며, 해당 빈 정의와 일치하는 ID 또는 여러 ID를 가진 빈즈에 대한 모든 요청이 주어지면 특정한 하나의 빈 인스턴스가 스프링 컨테이너에 의해 반환된다.<br>

&nbsp;&nbsp;&nbsp;&nbsp;달리 말하면, 개발자가 빈 정의를 정하고 이것의 스코프를 싱글톤으로 설정할 때, 스프링 IoC 컨테이너는 해당 빈 정의에 의해 정의된 객체의 단 하나의 인스턴스를 생성한다. 이 단일 객체는 싱글톤 빈즈와 같은 캐시<span style="color: #808080;">cache</span>에 저장되며, 그 뒤에 해당 특정 빈에 대하여 뒤따르는 모든 요청들 및 참조를 통하여, 캐시된 객체가 반환된다.

&nbsp;&nbsp;&nbsp;&nbsp;스프링의 "싱글톤" 컨셉은 GoF 디자인 패턴에서 정의된 싱글톤 패턴과는 차이가 존재한다.<br>
GoF의 경우, 객체의 스코프가 특정 클래스에 대하여 클래스로더<span style="color: #808080;">ClassLoader</span>당 오직 하나의 인스턴스만 생성되기 때문이다. 반면, 스프링 싱글톤의 스코프는 컨테이너 단위<span style="color: #808080;">per-container</span>와 빈 단위<span style="color: #808080;">per-bean</span>라는 형태로 잘 설명되고 있다. 이는 즉, 단일 스프링 컨테이너의 특정 하나의 클래스에 대하여 하나의 빈을 정의한다면, 스프링 컨테이너는 빈 정의에 의해 정의된 클래스의 오직 하나의 인스턴스를 생성한다는 것이다. 스프링에서 기본 스코프는 싱글톤 스코프이다.<br>

<h4 id="the-prototype-scope-h4">  1.5.2. 프로토타입<span style="color: #808080;">Prototype</span> 스코프</h4>

<h4 id="singleton-beans-with-prototype-bean-dependencies-h4">  1.5.3. 프로토타입형 빈 의존관계와 싱글톤 빈즈</h4>

<h4 id="request-session-application-and-websocket-scopes-h4">  1.5.4. 요청, 세션, 애플리케이션, 웹소켓 스코프<span style="color: #808080;">Request, Session, Application, and Websocket Scopes</span></h4>

<h5 id="initial-web-configuration-h4">   초기 웹 설정<span style="color: #808080;">Initial Web Configuration</span></h5>
<h5 id="request-scope-h4">   요청 스코프<span style="color: #808080;">Request Scope</span></h5>
<h5 id="session-scope-h4">   세션 스코프<span style="color: #808080;">Session Scope</span></h5>
<h5 id="application-scope-h4">   애플리케이션 스코프<span style="color: #808080;">Application Scope</span></h5>
<h5 id="websocket-scope-h4">   웹소켓 스코프<span style="color: #808080;">WebSocket Scope</span></h5>
<h5 id="dependency-injection-h4">   의존관계로서의 빈의 스코프<span style="color: #808080;">Scoped Beans as Dependencies</span></h5>

<h4 id="custom-scopes-h4">  1.4.5. 커스텀 스코프<span style="color: #808080;">Custom Scopes</span></h4>

<h4 id="method-injection-h4">  1.4.6. 메서드 주입 <span style="color: #808080;">Dependency Injection</span></h4>


<br>
<br>








