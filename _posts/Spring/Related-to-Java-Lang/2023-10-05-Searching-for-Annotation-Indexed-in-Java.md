---
title: Java의 Annotation 알아보기 - &#64;Indexed
author: wannastudyhardyeah
date: 2023-10-05 01:05:00 +0800
categories: [Java]
tags: [Spring, Java, Annotation]
math: true

---
<div class="toc-multiple-posts">
<h2>스프링 애너테이션<span style="color: #808080;">Annotation</span> 시리즈</h2>
<ol class="sc-fmciRz gyCSrP"><li><a href="/posts/Searching-for-Annotation-in-Java/">Java의 Annotation 알아보기 - 애너테이션</a></li>
<li><a href="/posts/Searching-for-Annotation-AliasFor-in-Java/">Java의 Annotation 알아보기 - &#64;AliasFor</a></li>
<li><a href="/posts/Searching-for-Annotation-Component-in-Java/">Java의 Annotation 알아보기 - &#64;Component</a></li>
<li><a href="/posts/Searching-for-Annotation-Configuration-in-Java/">Java의 Annotation 알아보기 - &#64;Configuration</a></li>
<li><a href="/posts/Searching-for-Annotation-Indexed-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - &#64;Indexed</a></li>
<li><a href="/posts/Searching-for-Annotation-Target-in-Java/">Java의 Annotation 알아보기 - &#64;Target</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">5/6</div>
</div></div>
</div>

출처: <a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Configuration.html">Package org.springframework.core.annotation / Annotation Interface AliasFor</a>
<hr width="50%">
<h2 id="what-is-Indexed-annotation-h2"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">@Configuration</code></h2>

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Indexed {
}
```

> <div style="color:black; font-size:1.15rem">Indicate that the annotated element represents a stereotype for the index.
</div>

&nbsp;&nbsp;&nbsp;&nbsp;이 애너테이션이 붙은 요소는 해당 인덱스에 대하여 스테레오타입<span style="color: #808080;">stereotype</span>임을 나타낸다.<br>

(생략)<br>

메타 애너테이션인 이 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Indexed</code>가<br>
붙어있기도 한 기본 애너테이션인 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Component</code>를<br>
생각해보자.<br>
어떤 컴포넌트에 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Component</code>가 붙어있다면,<br>
이 컴포넌트에 대한 공간은<br>
``org.springframework.stereotype.Component``라는<br>
스테레오타입을 사용하는<br>
인덱스에 추가될 것이다.<br>

이 애너테이션은<br>
메타 애너테이션이기도 하다.<br>
그래서 다음과 같이<br>
커스텀 애너테이션을 만들 수도 있다.<br>

```java
package com.example;

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Indexed
@Service
public @interface PrivilegedService { ... }
```

위의 애너테이션에서는<br>
타입(``TYPE``)으로 나타나고 있는데,<br>
이 경우에는 두 개의 스테레오타입이<br>
인덱스에 추가된다.<br>
즉, ``org.springframework.stereotype.Component``와<br>
``com.example.PrivilegedService``이다.<br>

<code class="language-java highlighter-rouge" style="color: #9E880D;">@Service</code>에는 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Indexed</code>가<br>
직접적으로 붙어있지는 않지만,<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">@Component</code>를 통하여<br>
메타 애너테이션이 붙어있다.<br>

