---
title: Java의 Annotation 알아보기 - &#64;Configuration
author: wannastudyhardyeah
date: 2023-09-30 01:59:00 +0800
categories: [Java]
tags: [Spring, Java, Annotation]
math: true

---
<div class="toc-multiple-posts">
<h2>스프링 애너테이션<span style="color: #808080;">Annotation</span> 시리즈</h2>
<ol class="sc-fmciRz gyCSrP"><li><a href="/posts/Searching-for-Annotation-in-Java/">Java의 Annotation 알아보기 - 애너테이션</a></li>
<li><a href="/posts/Searching-for-Annotation-AliasFor-in-Java/">Java의 Annotation 알아보기 - &#64;AliasFor</a></li>
<li><a href="/posts/Searching-for-Annotation-Component-in-Java/">Java의 Annotation 알아보기 - &#64;Component</a></li>
<li><a href="/posts/Searching-for-Annotation-Configuration-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - &#64;Configuration</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">4/4</div>
</div></div>
</div>

출처: <a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/annotation/AliasFor.html">Package org.springframework.core.annotation / Annotation Interface AliasFor</a>
<hr width="50%">
<h2 id="what-is-Configuration-annotation-h2"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">@Configuration</code></h2>

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Configuration {

	@AliasFor(annotation = Component.class)
	String value() default "";

	boolean proxyBeanMethods() default true;

	boolean enforceUniqueMethods() default true;
}
```

> <div style="color:black; font-size:1.15rem">Indicates that a class declares one or more <code class="language-java highlighter-rouge" style="color: #83060e;">@Bean</code> methods and may be processed by the Spring container to generate bean definitions and service requests for those beans at runtime, for example:</div>

<code class="language-java highlighter-rouge" style="color: #83060e;">@Configuration</code> 애너테이션은 다음을 가리킨다.<br>
해당 클래스가 하나 이상의 <code class="language-java highlighter-rouge" style="color: #83060e;">@Bean</code> 메서드를<br>
선언하며, 스프링 컨테이너로 처리된다.<br>
또한, 이 컨테이너는 빈의 정의<span style="color: #808080;">bean definitions</span>와<br>
런타임 때 해당 빈의 서비스 요청을 생성한다.<br>
예시는 다음과 같다.<br>

```java
@Configuration
public class AppConfig {

     @Bean
     public MyBean myBean() {
         // 인스턴스화
         // 설정(configure)
         // 빈을 리턴
     }
 }
```

<br>
<hr width="50%">
<!-- 1 (h2) -->
<h2 id="bootstrapping-configuration-classes-h2">1. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">@Configuration</code> 클래스 부트스트랩 과정</h2>
<b style="font-size:1.2rem">Bootstrapping <code class="language-java highlighter-rouge" style="color: #83060e;">@Configuration</code> classes</b><br>
<!--------------->

<!-- 1.1 (h3) -->
<h3 id="via-annotation-config-application-context-h3"> 1.1. AnnotationConfigApplicationContext를 통한 과정</h3>
<b style="font-size:1.2rem">Via AnnotationConfigApplicationContext</b><br>

일반적으로는<br>
``AnnotationConfigApplicationContext`` 클래스 또는<br>
웹 전용인 ``variant``를 사용하여<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code>을<br> 초기화할 수 있다.<br>
전자의 경우에 대한 코드 예제는 다음과 같다.<br>

```java
AnnotationConfigApplicationContext ctx 
    = new AnnotationConfigApplicationContext();
ctx.register(AppConfig.class);
ctx.refresh();
MyBean myBean = ctx.getBean(MyBean.class);
// myBean 사용하는 코드 ~~~
```

이에 대한 자세한 내용은<br>
<a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/AnnotationConfigApplicationContext.html"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AnnotationConfigApplicationContext</code></a> 공식 문서를,<br>
``Servlet`` 컨테이너의 웹 설정 명령어들에 대해서는<br>
<a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/context/support/AnnotationConfigWebApplicationContext.html"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AnnotationConfigWebApplicationContext</code></a> 부분을 참고하면 된다.<br>
<!--------------->

<!-- 1.2 (h3) -->
<h3 id="via-spring-beans-xml-h3" data-heading-label=" 1.2. Via Spring 	&lt;beans&gt; XML을 통한 과정"> 1.2. 스프링&lt;beans&gt; XML을 통한 과정</h3>
<b style="font-size:1.2rem">Via Spring &lt;beans&gt; XML</b><br>

AnnotationConfigApplicationContext와는 반대로<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스를 직접 생성하는 것 대신에<br>
스프링 XML 파일에서 일반적으로 ``<bean>`` 정의를 이용하여<br>
다음과 같이 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스를 선언할 수도 있다.<br>

```xml
 <beans>
    <context:annotation-config/>
    <bean class="com.acme.AppConfig"/>
 </beans>
```

ConfigurationClassPostProcessor, 그리고<br>
다른 애너테이션 관련 post 프로세서를<br>
활성화하기 위해선<br>
``<context:annotation-config>``가 필수적이다.<br>
이 프로세서들이 있어야만<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스를 다룰 수 있다.<br>
<!--------------->
<!-- 1.3 (h3) -->
<h3 id="via-component-scanning-h3" data-heading-label=" 1.3. 컴포넌트 스캔을 통한 과정"> 1.3. 컴포넌트 스캔을 통한 과정</h3>
<b style="font-size:1.2rem">Via Component scanning</b><br>

<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code>에는<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Component</code> 애너테이션이 붙어있으므로<br>
컴포넌트 스캐닝 대상이 된다.<br>
(스프링 XML에선 ``<context:component-scan/> 요소)<br>
그렇기 때문에 다른 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Component</code>처럼<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Autowired</code>/<code class="language-java highlighter-rouge" style="color: #9E880D;">@Inject</code>를 쓰는 이점을 얻는다.<br>
특히, 단일 생성자가 존재할 경우에<br>
해당 생성자에 자동주입<span style="color: #808080;">autowireing</span>이<br>
이뤄지는 건 명백하다.<br>

```java
@Configuration
public class AppConfig {

    private final SomeBean someBean;

    public AppConfig(SomeBean someBean) {
        this.someBean = someBean;
    }

    // @Bean definition using "SomeBean"

}
```

<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스는<br>
컴포넌트 스캔을 통해서만<br>
초기화가 이뤄지는 건 아니다.<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@ComponentScan</code> 애너테이션을 이용하여<br>
다음과 같이 컴포넌트 스캔을 <i>설정<span style="color: #808080;">configure</span></i>할 수 있다.<br>

```java
@Configuration
@ComponentScan("com.acme.app.services")
public class AppConfig {
    // various @Bean definitions ...
}
```

자세한 내용은<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@ComponentScan</code> 문서를 참고하면 된다.<br>

<!--------------->
<!--------------->
<!-- 2 (h2) -->
<h2 id="working-with-externalized-values-h2">2. 외부의 값을 통한 방법</h2>
<b style="font-size:1.2rem">Bootstrapping <code class="language-java highlighter-rouge" style="color: #83060e;">@Configuration</code> classes</b><br>

<h3 id="using-the-environment-api-h3"> 2.1. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">Environment</code> API 사용</h3>

스프링 ``Environment``를 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code>에 주입하여<br>
외부의 값을 찾아올 수도 있다.<br>

```java
@Configuration
public class AppConfig {

    @Autowired Environment env;

    @Bean
    public MyBean myBean() {
        MyBean myBean = new MyBean();
        myBean.setName(env.getProperty("bean.name"));
        return myBean;
    }
}
```

하나 이상의 ``PropertySource`` 클래스 객체에 있는<br>
``Environment``를 통해 사용된 속성들과, 그리고<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스는<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@PropertySource</code> 애너테이션을 이용하는 ``Environment`` 객체에<br>
속성 소스들을 contribute 한다.<br>
다음 예제를 참고할 수 있다.<br>

```java
@Configuration
@PropertySource("classpath:/com/acme/app.properties")
public class AppConfig {

    @Inject Environment env;

    @Bean
    public MyBean myBean() {
        return new MyBean(env.getProperty("bean.name"));
    }
}
```

자세한 내용은<br>
``Environment``와 <code class="language-java highlighter-rouge" style="color: #9E880D;">@PropertySource</code> 문서를 참고하면 된다.<br>

<h3 id="using-the-value-annotation-h3"> 2.2. <code class="language-java highlighter-rouge" style="color: #9E880D;">@Value</code> 애너테이션 사용</h3>

<code class="language-java highlighter-rouge" style="color: #9E880D;">@Value</code> 애너테이션을 통하여<br>
외부의 값이 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스로 주입될 수 있다.<br>

```java
@Configuration
@PropertySource("classpath:/com/acme/app.properties")
public class AppConfig {

    @Value("${bean.name}") String beanName;

    @Bean
    public MyBean myBean() {
        return new MyBean(beanName);
    }
}
```

이러한 접근은<br>
스프링의 ``PropertySourcesPlaceholderConfigurer`` 클래스와<br>
결합할 때 자주 쓰이는데,<br>
이 클래스는 XML 설정에서<br>
``<context:property-placeholder>``나, 혹은<br>
관련된 ``static`` <code class="language-java highlighter-rouge" style="color: #9E880D;">@Bean</code> 메서드를 통해<br>
명시적으로 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스에서<br>
자동으로 활성화 된다.<br>

그러나, 주지해야 할 부분은<br>
그러한 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Bean</code> 메서드를 통해<br>
``PropertySourcesPlaceholderConfigurer`` 클래스를<br>
명시적으로 등록하는 것은<br>
placeholder 구분과 같은 설정을<br>
커스텀하고자 할 때에나 필요하단 점이다.<br>

특히, 빈 포스트-프로세서<span style="color: #808080;">post-processor</span>가<br>
(``PropertySourcesPlaceholderConfigurer`` 등이 있다.)<br>
``ApplicationContext``에 대한<br>
내장된 값<span style="color: #808080;">embedded</span> resolver를<br>
등록하지 않았다면,<br>
스프링이 기본 내장 값 resolver를 등록하고<br>
이는 ``Environment``에 등록된 속성 자원과는<br>
반대의 placeholder를 생성하게 될 것이다.<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@ImportResource</code>를 이용한 스프링 XML로<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Configuration</code> 클래스들을 합치는 것에 대해선<br>
아래의 섹션에서 다룬다.<br>
그리고 ``PropertySourcesPlaceholderConfigurer``와 같은<br>
``BeanFactoryPostProcessor`` 타입으로 다루는 것은<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Bean</code>의 공식 문서를 참고하면 된다.<br>

(추가 중)