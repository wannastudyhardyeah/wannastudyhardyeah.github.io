---
title: Java의 Annotation 알아보기 - &#64;AliasFor
author: wannastudyhardyeah
date: 2023-09-28 14:59:00 +0800
categories: [Java]
tags: [Spring, Java]
math: true

---
<div class="toc-multiple-posts">
<h2>스프링 애너테이션<span style="color: #808080;">Annotation</span> 시리즈</h2>
<ol class="sc-fmciRz gyCSrP"><li><a href="/posts/Searching-for-Annotation-in-Java/">Java의 Annotation 알아보기</a></li>
<li><a href="/posts/Searching-for-Annotation-AliasFor-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - &#64;AliasFor</a></li>
<li><a href="/posts/Searching-for-Annotation-Component-in-Java/">Java의 Annotation 알아보기 - &#64;Component</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">2/3</div>
</div></div>
</div>
<br>
<hr width="50%">
<h2 id="alias-for-annotation-h2"><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.5rem;">AliasFor</code></h2>

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
<h3 id="transitive-implicit-aliases-within-an-annotation-h3">예제 - 단일 애너테이션 내의 암묵적 변환 alias</h3>
Example: Transitive Implicit Aliases within an Annotation<br>

<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@GroovyOrXmlTestConfig</code>에서, ``groovy``는<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@MyTestConfig</code>의 ``groovyScripts``를 명시적으로 오버라이드한 것이다.<br>
그런 반면, ``xml``은 마찬가지로<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>의 ``locations`` 속성에 대하여<br>
명시적으로 오버라이드한 것이다.<br>
<br>
이에 따라,<br>
``groovy``와 ``xml``은 둘 모두<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@ContextConfiguration</code>의 ``locations``를<br>
오버라이드한 것의 효과를 지니므로<br>
이 둘은 서로에 대하여 암묵적 변환 alias이다.<br>
서로에 대하여<br>

```java
@MyTestConfig
 public @interface GroovyOrXmlTestConfig {

    @AliasFor(annotation = MyTestConfig.class,
              attribute = "groovyScripts")
    String[] groovy() default {};

    @AliasFor(annotation 
                  = ContextConfiguration.class,      
              attribute = "locations")
    String[] xml() default {};
 }
```

<h3 id="spring-annotations-supporting-attribute-aliases-h3">스프링 애너테이션 중 속성 Alias들을 지원하는 것</h3>

스프링 프레임워크 4.2 기준으로,<br>
스프링에서 핵심이 되는 몇몇 애너테이션은<br>
<code class="language-java highlighter-rouge" style="color: #9E880D; font-size: 0.95rem;">@AliasFor</code>를 사용함으로써<br>
내부 속성 alias들을 설정하는 것으로 업데이트 되었다.<br>
세부 사항은 javadoc의 개별 애너테이션 부분과<br>
레퍼런스 매뉴얼을 참조하면 된다.<br>