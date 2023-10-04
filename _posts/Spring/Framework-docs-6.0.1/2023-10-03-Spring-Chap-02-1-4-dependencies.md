---
title: 스프링 프레임워크 - 2.1. IoC 컨테이너&#58; 4. 의존 관계
author: wannastudyhardyeah
date: 2023-10-03 20:20:00 +0800
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
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-4-dependencies" aria-current="page" class="active">2.1.4. 의존 관계<span style="color: #808080;">Dependencies</span></a><br>
&nbsp;&nbsp;&nbsp;&nbsp;<a href="/posts/Spring-Chap-02-1-5-bean-scopes">2.1.5. 빈 스코프<span style="color: #808080;">Bean Scopes</span></a><br>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">5/6</div>
</div></div>
</div>
<br>
<hr width="80%">
<h3 id="dependencies-h3"> 1.4. 의존 관계<span style="color: #808080;">Dependencies</span></h3>

<h4 id="dependency-injection-h4">  1.4.1. 의존 관계 주입<span style="color: #808080;">Dependency Injection</span></h4>
<h5 id="constructor-based-dependency-injection-h5">   ① 생성자 기반 의존 관계 주입</h5>
<h5 id="constructor-based-dependency-injection-h5">   ② 설정자 기반 의존 관계 주입</h5>

<h5 id="constructor-based-dependency-injection-h5">   ③ 의존 관계 결정 과정</h5>

&nbsp;&nbsp;&nbsp;&nbsp;컨테이너는 빈의 의존 관계 결정을 다음과 같이 수행한다.<br>

1. `ApplicationContext`가 메타데이터와 함께 생성되고 초기화 되는데, 이때 이 메타데이터는 모든 빈에 대한 정보가 있고, 설정 관련 메타데이터는 XML이나 자바 코드, 또는 애너테이션으로 작성된다.
2. 빈의 의존관계는 속성, 혹은 생성자의 인수나 정적 팩토리 메서드(일반적인 생성자 대신 사용할 경우)의 인수의 형태로 표현된다. 이러한 의존관계가 빈에 전달되는 시점은 빈이 실제로 생성되었을 때이다.
3. 속성 혹은 생성자 인수는, 설정하고자 하는 실제 값 정의, 또는 해당 컨테이너에 있는 다른 빈에 대한 참조가 된다.
4. 속성 혹은 생성자 인수가 값인 경우에, 해당 특정 형식에서 그 속성이나 생성자 인수의 실제 타입으로 변환된다. 스프링은 기본적으로, 문자열 형식으로 제공된 값을 모든 기본 타입들(`int`, `long`, `String`, `boolean`)로 변환 가능하다.

<div style="margin-top: 10px; margin-bottom: 10px; position: relative; display: inline-block; text-align: left; padding: 10px 10px 10px 10px; height: 100%; border: 1px dotted black;"><div style="margin-top: 10px; margin-bottom: 10px; text-align: center !important;"><b>순환 의존관계</b></div><br>
&nbsp;&nbsp;생성자로 주입을 하게되면 대부분의 경우, 해결 불가능한 순환 의존 상황을 맞닦뜨릴 수 있다.<br>
<br>
&nbsp;&nbsp;예를 들어,<br>
`Class` `A` 는 생성자를 통한 주입으로 `Class` `B`의 인스턴스를 필요로 하고, `Class` `B`도  생성자를 통한 주입으로 `Class` `A`의 인스턴스를 필요로 하는 상황을 상정해볼 수 있다.<br>
이때, `Class` `A`와 `Class` `B`에 대하여 서로가 서로를 주입하도록 빈을 설정한다면, 스프링의 IoC 컨테이너는 런타임 단계에서 순환 참조circular reference를 감지하고는 `BeanCurrentlyInCreationException` 에러를 발생시킬 것이다.<br>
<br>
&nbsp;&nbsp;한 가지 해결책은, 생성자를 사용하는 대신에 설정자setter를 이용하여 클래스를 설정하도록 코드를 고치는 것이다. 달리 말하면, 생성자를 통한 주입 대신에 설정자를 통한 주입만을 사용한다는 것이다. 즉, 이 방법은 그리 추천되지는 않는 방법이지만, 설정자 주입을 통해 순환 의존을 (에러 없이) 설정할 수 있을 것이다.<br>
<br>
&nbsp;&nbsp;이러한 특수 케이스가 아닌 경우에 빈 `A`와 빈 `B` 사이의 순환 의존 관계는, 한 쪽 빈이 다른 한 쪽으로 주입되어 그 자체로 완전한 설정이 이뤄질 것이다.(고전적인 닭-계란 문제처럼)</div>

&nbsp;&nbsp;&nbsp;&nbsp;빈 `A`가 빈 `B`에 대해 의존 관계를 가질 경우, 스프링 IoC 컨테이너는 빈 `B`를 먼저 완전히 설정하고, 그 다음에 빈 `A`에 있는 설정자 메서드를 불러온다.

달리 말하면,

1. 빈을 초기화한다.(먼저 인스턴스화가 이뤄진 싱글톤이 아니라면.)
2. 해당 빈의 의존관계를 설정한다.
3. 관련된 생명주기 메서드들을 불러온다.
    
    (설정된 초기화 메서드나 빈을 초기화하는initializingBean 콜백 메서드와 같은 것들)

<h5 id="constructor-based-dependency-injection-h5">   ④ 의존 관계 주입 사례들</h5>

```java
public class ExampleBean {
    private AnotherBean beanOne;

    private YetAnotherBean beanTwo;

    private int i;

    public void setBeanOne(AnotherBean beanOne) {
        this.beanOne = beanOne;
    }
    
    public void setBeanTwo(YetAnotherBean beanOne) {
        this.beanTwo = beanTwo;
    }

    public void setIntegerProperty(int i) {
        this.i = i;
    }
}
```

```java
public class ExampleBean {
    private AnotherBean beanOne;

    private YetAnotherBean beanTwo;

    private int i;
		
		public ExampleBean(
				AnotherBean anotherBean,
				YetAnotherBean yetAnotherBean,
				int i) {
				this.beanOne = anotherBean;
				this.beanTwo = yetAnotherBean;
				this.i = i;
		}
}
```

```java
public class ExampleBean {		
		// private으로 설정
		private ExampleBean(...)
				...
				...
		}

		public static ExampleBean createInstance (
				AnotherBean anotherBean,
				YetAnotherBean yetAnotherBean,
				int i) {
				ExampleBean eb = new ExxampleBean(...);
				// 다른 연산 코드들
				return eb;
		}
}
```

<h4 id="dependencies-and-configuration-in-detail-h4">  1.4.2. 의존 관계와 설정에 대하여<span style="color: #808080;">Dependency Injection</span></h4>

<h4 id="using-depends-on-h4">  1.4.3. <code class="language-java highlighter-rouge" style="color: #9E880D;">depends-on</code> 이용</h4>

<h4 id="lazy-initialized-bean-h4">  1.4.4. 빈 초기화 지연<span style="color: #808080;">Dependency Injection</span></h4>

<h4 id="autowiring-collaborators-h4">  1.4.5. 컬래버레이터 자동주입<span style="color: #808080;">Dependency Injection</span></h4>

<h4 id="method-injection-h4">  1.4.6. 메서드 주입 <span style="color: #808080;">Dependency Injection</span></h4>

<h5 id="dependency-injection-h4">   생성자 인자 결정<span style="color: #808080;">Argument Resolution</span></h5>

<br>
<br>








