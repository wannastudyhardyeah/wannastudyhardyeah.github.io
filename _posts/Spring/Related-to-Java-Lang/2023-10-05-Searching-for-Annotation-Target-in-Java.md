---
title: Java의 Annotation 알아보기 - &#64;Target
author: wannastudyhardyeah
date: 2023-10-05 01:06:00 +0800
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
<li><a href="/posts/Searching-for-Annotation-Indexed-in-Java/">Java의 Annotation 알아보기 - &#64;Indexed</a></li>
<li><a href="/posts/Searching-for-Annotation-Target-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - &#64;Target</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">6/6</div>
</div></div>
</div>

출처: <a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Target.html">Package org.springframework.core.annotation / Annotation Interface Target</a>
<hr width="50%">
<h2 id="what-is-Indexed-annotation-h2"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.35rem;">@Target</code></h2>


> <div style="color:black; font-size:1.15rem">An annotation of type <code class="language-java highlighter-rouge" style="color: #9E880D;">java.lang.annotation.Target</code> is used on the declaration of an annotation interface A to specify the contexts in which A is applicable. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">java.lang.annotation.Target</code> has a single element, <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">value</code>, of type <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">java.lang.annotation.ElementType[]</code>, to specify contexts.</div>

&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-java highlighter-rouge" style="color: #9E880D;">java.lang.annotation.Target</code> 타입인 애너테이션은<br>
애너테이션 인터페이스 A 선언이<br>
<i>적용가능하다는</i> 문맥을<br>
명시하는 데에 사용된다.<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">java.lang.annotation.Target</code>은<br>
<code class="language-java highlighter-rouge" style="color: #9E880D;">java.lang.annotation.ElementType[]</code> 중<br>
단일 요소, ``value``를 가지며<br>
이를 통해 문맥을 명시한다.<br>

<hr width="30%">

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target {

    ElementType[] value();
}
```

&nbsp;&nbsp;&nbsp;&nbsp;이 애너테이션은,<br>
해당 애너테이션 인터페이스가<br>
적용 가능<span style="color: #808080;">applicable</span>한 문맥에 있음을 알려준다.<br>
애너테이션 인터페이스가 적용가능한<br>
선언 문맥과 타입 문맥이란 것은<br>
JSL 9.6.4.1에 명시되어 있다.<br>

<code class="language-java highlighter-rouge" style="color: #9E880D;">@Taget</code> 메타 애너테이션이<br>
``T``라는 애너테이션 인터페이스에<br>
붙어있지 않다면,<br>
``T`` 타입의 애너테이션은<br>
어느 선언에서든<br>
제어자<span style="color: #808080;">modifier</span>로 작성될 것이다.<br>

반대로, ``T``에 붙어있다면,<br>
컴파일러는 열거형 상수 중에서<br>
``ElementType``을 이용하여<br>
사용 제한 설정을 강제할 것이다.<br>
이는 JLS 9.7.4에 나와있다.<br>

예를 들어,<br>
아래의 <code class="language-java highlighter-rouge" style="color: #9E880D;">@Taget</code> 메타 애너테이션은<br>
선언된 인터페이스 스스로가<br>
메타 애너테이션 인터페이스임을 나타낸다.<br>
이는 오직<br>
애너테이션 인터페이스 선언에만 쓰인다.<br>

```java
@Target(ElementType.ANNOTATION_TYPE)
public @interface MetaAnnotationType {
    ...
}
```
