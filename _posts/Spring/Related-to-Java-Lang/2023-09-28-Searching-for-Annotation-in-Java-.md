---
title: Java의 Annotation 알아보기
author: wannastudyhardyeah
date: 2023-09-28 14:59:00 +0800
categories: [Java]
tags: [Spring, Java]
math: true

---
<h2 id="what-is-annotation-h2">애너테이션(어노테이션)이란?</h2>

&nbsp;&nbsp;&nbsp;&nbsp;코드에서 ``@``으로 작성되는 요소.<br>
&nbsp;&nbsp;&nbsp;&nbsp;클래스 또는 인터페이스를 컴파일하거나 실행할 때,<br>
어떻게 처리해야 할 것인지를 알려주는<br>
설정 정보이다.<br>
(출처: 『이것이 자바다』)<br>

> <div style="color:black; font-size:1.15rem">Annotations, a form of metadata, provide data about a program that is not part of the program itself. Annotations have no direct effect on the operation of the code they annotate.</div>

애너테이션은 프로그램 자기 자신을<br>
포함하지 않는 데이터를 제공하는,<br>
메타데이터 형식으로 된 것이다.<br>
해당 애너테이션은 그 코드에 대해선<br>
직접적인 영향을 주진 않는다.<br>
<br>
> <div style="color:black; font-size:1.15rem"> Annotations have a number of uses, among them:<br>
><br>
> - Information for the compiler — Annotations can be used by the compiler to detect errors or suppress warnings.<br>
> - Compile-time and deployment-time processing — Software tools can process annotation information to generate code, XML files, and so forth.<br>
> - Runtime processing — Some annotations are available to be examined at runtime.</div>

애너테이션이 사용되는<br>
여러 용도들은 아래 세 가지 중 하나.<br>

- 컴파일러에 대한 정보<br>
\: 컴파일러가 에러를 탐지하거나<br>
경고를 숨기도록 하기 위해 사용됨.<br>
- 컴파일 타임과 deployment 타임 프로세싱<br>
\: 코드나 XML 파일과 같은 것들을 생성할 때<br>
SW 도구가 애너테이션을 이용함.<br>
- 런타임 프로세싱<br>
\: 런타임에 감지되어 쓰이는 것들도 있음.<br>
<br>
<hr width="50%">
<h2 id="alias-for-annotation-h2"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">AliasFor</code></h2>

<h3 id="usage-scenarios">사용 사례들</h3>

- <b>Explicit aliases within an annotation</b><br>
(단일 애너테이션에 대해 명시적인 여러 alias들)<br>
\: 단일 애너테이션 내에서,<br>
한 쌍의 속성에 대하여<br>
그 둘이 상호교환적인 alias임을 나타내기 위해<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@AliasFor</code>를 사용할 수 있다.<br>

- <b>Explicit alias for attribute in meta-annotation</b><br>
(메타-애너테이션 내의 속성에 대해 명시적인 alias)<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@AliasFor</code>의 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 0.95rem;">annotation()</code> 속성이,<br>
해당 애너테이션이 아닌<br>
다른 애너테이션에서 설정<span style="color: #808080;">set</span>될 경우,<br>
이때 ``attribute()``는<br>
메타 애너테이션의 속성에 대한 alias가 된다.<br>
(즉, 이것의 속성에 대한 명시적 오버라이드)<br>
<br>
이렇게 함으로써,<br>
애너테이션 계층 하에서<br>
어떤 속성을 오버라이드 할 지를<br>
문제없이 제어할 수 있다.<br>
<br>
사실, <code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@AliasFor</code>를 이용하여<br>
메타 애너테이션의 ``value`` 속성에 대한<br>
alis를 선언하는 것도 가능하다.<br>

- <b>Implicit aliases within an annotation</b><br>
(단일 애너테이션에 대해 암묵적인 alias들)<br>
\: 단일 애너테이션의 하나 이상의 속성들이<br>
동일한 메타 애너테이션 속성에 대한<br>
오버라이드로 선언될 경우<br>
(직접적이든, 간접적 변환이든),<br>
이러한 속성들은 서로에 대하여<br>
<i>암묵적인</i> alias들의 집합으로 간주된다.<br> 
그리고, 이 속성들은<br>
단일 애너테이션에 대한<br>
명시적인 경우와 유사하게 형성된다.<br>

<h3 id="explicit-alases-within-an-annotation-h3">예제 - 명시적 / 단일 애너테이션</h3>
Explicit Aliases within an Annotation<br>

<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>에서,<br>
``value``와 ``locations``는<br>
상호 명시적인 alias들이다.<br>

```java
 public @interface ContextConfiguration {

    @AliasFor("locations")
    String[] value() default {};

    @AliasFor("value")
    String[] locations() default {};

    // ...
 }
```

<h3 id="explicit-alas-for-attribute-in-meta-annotation-h3">예제 - 명시적 / 메타 애너테이션</h3>
Explicit Alias for Attribute in Meta-annotation<br>

<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@XmlTestConfig</code>에서, ``xmlFiles``는<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>의 ``locations``에 대한<br>
명시적 alias이다.<br>
달리 말하면, ``xmlFiles``이<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>의 ``locations`` 속성을<br>
상속한다고 할 수 있다.<br>

```java
 @ContextConfiguration
 public @interface XmlTestConfig {

    @AliasFor(annotation = ContextConfiguration.class, 
              attribute = "locations")
    String[] xmlFiles();
 }
 ```

<h3 id="implicit-aliases-within-an-annotation-h3">예제 - 단일 애너테이션 내의 암묵적 alias들</h3>
Example: Implicit Aliases within an Annotation

In <code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@MyTestConfig</code>에서,<br>
``value``, ``groovyScripts``, ``xmlFiles``는 모두<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>의<br>
``locations`` 속성에 대한,<br>
메타 애너테이션의 명시적 속성 오버라이드이다.<br>
또한, 이 세 속성들은 서로에 대하여<br>
암묵적인 alias가 된다.<br>

```java
 @ContextConfiguration
 public @interface MyTestConfig {

    @AliasFor(annotation = ContextConfiguration.class, 
              attribute = "locations")
    String[] value() default {};

    @AliasFor(annotation = ContextConfiguration.class, 
              attribute = "locations")
    String[] groovyScripts() default {};

    @AliasFor(annotation = ContextConfiguration.class, 
              attribute = "locations")
    String[] xmlFiles() default {};
 }
```
<!-- <h3 id="transitive-implicit-aliases-within-an-annotation-h3">예제 - 단일 애너테이션 내의 암묵적 변환 alias</h3>
Example: Transitive Implicit Aliases within an Annotation -->