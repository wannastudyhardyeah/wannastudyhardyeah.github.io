---
title: 스프링 프레임워크 - 2.1. IoC 컨테이너&#58; 3. 빈 개요
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
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-2-container-overview">2.1.2. 컨테이너 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-3-bean-overview" aria-current="page" class="active">2.1.3. 빈<span style="color: #808080;">Bean</span> 개요</a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-4-dependencies">2.1.4. 의존 관계<span style="color: #808080;">Dependencies</span></a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-5-bean-scopes">2.1.5. 빈 스코프<span style="color: #808080;">Bean Scopes</span></a><br>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">4/6</div>
</div></div>
</div>
<br>
<hr width="80%">
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

<h4 id="naming-beans">  1.3.1. 빈즈 명명<span style="color: #808080;">Naming Beans</span></h4>
<h5 id="aliasing-a-bean-outside-the-bean-definition">   ① 빈 정의 이외에 빈 alias 명명</span></h5>

<h4 id="Instantiating-beans">  1.3.2. 빈즈 인스턴스화하기<span style="color: #808080;">Instantiating Beans</span></h4>

&nbsp;&nbsp;&nbsp;&nbsp;빈 정의는 하나 이상의 객체를 생성하는 것에 관한 필수 레시피이다. 그리고 컨테이너는 요청을 받았을 때 이 레시피를 통해 특정 이름의 빈을 참조하며, 바로 이 빈 정의에 의해 캡슐화된 설정 메타데이터를 사용하여 실제 객체를 생성(또는 취득)한다.<br>

<h5 id="abcd">   ① 생성자를 통한 인스턴스화</h5>

<h5 id="abcd-e">   ② 정적 팩토리 메서드를 통한 인스턴스화</h5>

<h5 id="abcd-ef">   ③ 정적 팩토리 메서드를 통한 인스턴스화</h5>

<h5 id="abcd-efg">   ④ 빈즈의 런타임 시 타입 결정</h5>
