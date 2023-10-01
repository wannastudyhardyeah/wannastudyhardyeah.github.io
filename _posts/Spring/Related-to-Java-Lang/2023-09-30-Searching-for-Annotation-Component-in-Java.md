---
title: Java의 Annotation 알아보기 - &#64;Component
author: wannastudyhardyeah
date: 2023-09-30 01:58:00 +0800
categories: [Java]
tags: [Spring, Java, Annotation]
math: true

---
<div class="toc-multiple-posts">
<h2>스프링 애너테이션<span style="color: #808080;">Annotation</span> 시리즈</h2>
<ol class="sc-fmciRz gyCSrP"><li><a href="/posts/Searching-for-Annotation-in-Java/">Java의 Annotation 알아보기 - 애너테이션</a></li>
<li><a href="/posts/Searching-for-Annotation-AliasFor-in-Java/">Java의 Annotation 알아보기 - &#64;AliasFor</a></li>
<li><a href="/posts/Searching-for-Annotation-Component-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - &#64;Component</a></li>
<li><a href="/posts/Searching-for-Annotation-Configuration-in-Java/">Java의 Annotation 알아보기 - &#64;Configuration</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">3/4</div>
</div></div>
</div>

출처: <a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/annotation/AliasFor.html">Package org.springframework.core.annotation / Annotation Interface AliasFor</a>
<hr width="50%">
<h2 id="what-is-annotation-h2"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">@Component</code></h2>

```java
@Target(TYPE)
@Retention(RUNTIME)
@Documented
@Indexed
public @interface Component
```

> <div style="color:black; font-size:1.15rem">Indicates that an annotated class is a "component". Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning.
Other class-level annotations may be considered as identifying a component as well, typically a special kind of component: e.g. the <code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 1.0rem;">@Repository</code> annotation or AspectJ's <code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 1.0rem;">@Aspect</code> annotation.</div>

``@Component`` 애너테이션이 붙은 클래스를<br>
"컴포넌트"임을 알려주고, 즉, 해당 클래스는<br>
애너테이션 기반 설정과 클래스패스<span style="color: #808080;">classpath</span> 스캔 시에<br>
자동 감지되는 대상이 된다.<br>
클래스에 붙은 다른 애너테이션들 역시도<br>
컴포넌트로 인식된다.<br>
특히 컴포넌트의 특별한 경우로,<br>
``@Repository``나<br>
AspectJ의 ``Aspect`` 애너테이션 등이 있다.<br>
<br>
<hr width="50%">
<h2 id="optional-element-summary-h2">선택적 요소 - 요약</h2>
<b style="font-size:1.2rem"><i>Optional Element Summary</i></b><br>

- 제어자<span style="color: #808080;">Modifier</span>, 타입<span style="color: #808080;">Type</span><br>
\: ``String``<br>
- 선택적 요소<span style="color: #808080;">Optinal element</span><br>
\: ``value``<br>
- 설명<br>
\: 해당 값<span style="color: #808080;">value</span>은<br>
컴포넌트 이름에 대한 암시를 나타내는데,<br>
이 값은 컴포넌트가 자동 감지되는 경우에<br>
스프링 <b>빈</b><span style="color: #808080;">bean</span>으로 변환된다.<br>
<br>
<hr width="50%">
<h2 id="element-details-h2">요소에 대한 설명</h2>
<b style="font-size:1.2rem"><i>Element Details</i></b><br>

<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>value</b></code><br>
``String``&nbsp;&nbsp;&nbsp;&nbsp;``value``<br>

해당 값<span style="color: #808080;">value</span>은<br>
컴포넌트 이름에 대한 암시를 나타내는데,<br>
이 값은 컴포넌트가 자동 감지되는 경우에<br>
스프링 <b>빈</b><span style="color: #808080;">bean</span>으로 변환된다.<br> 

- 반환 값<br>
암시로 나타내어진 컴포넌트 이름<br>
(없을 시에는 ``empty`` ``String`` 값)<br>