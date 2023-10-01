---
title: Java의 Annotation 알아보기 - 애너테이션
author: wannastudyhardyeah
date: 2023-09-28 14:58:00 +0800
categories: [Java]
tags: [Spring, Java, Annotation]
math: true

---
<div class="toc-multiple-posts">
<h2>스프링 애너테이션<span style="color: #808080;">Annotation</span> 시리즈</h2>
<ol class="sc-fmciRz gyCSrP"><li><a href="/posts/Searching-for-Annotation-in-Java/" aria-current="page" class="active">Java의 Annotation 알아보기 - 애너테이션</a></li>
<li><a href="/posts/Searching-for-Annotation-AliasFor-in-Java/">Java의 Annotation 알아보기 - &#64;AliasFor</a></li>
<li><a href="/posts/Searching-for-Annotation-Component-in-Java/">Java의 Annotation 알아보기 - &#64;Component</a></li>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">1/3</div>
</div></div>
</div>

출처: <a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/annotation/AliasFor.html">Package org.springframework.core.annotation / Annotation Interface AliasFor</a>
<hr width="50%">
<h2 id="what-is-annotation-h2">애너테이션(어노테이션)이란?</h2>

&nbsp;&nbsp;&nbsp;&nbsp;코드에서 ``@``으로 작성되는 요소.<br>
&nbsp;&nbsp;&nbsp;&nbsp;클래스 또는 인터페이스를 컴파일하거나 실행할 때,<br>
어떻게 처리해야 할 것인지를 알려주는<br>
설정 정보이다.<br>
(출처: 『이것이 자바다』)<br>

> <div style="color:black; font-size:1.15rem">Annotations, a form of metadata, provide data about a program that is not part of the program itself. Annotations have no direct effect on the operation of the code they annotate.</div>

애너테이션은 프로그램 자기 자신을<br>
포함하지 않는 데이터를 제공하며<br>
메타데이터 형식으로 된 것이다.<br>
해당 애너테이션은 그 코드에 대해선<br>
직접적인 영향을 주진 않는다.<br>
(출처: <a href="https://docs.oracle.com/javase/tutorial/java/annotations/">오라클 - 자바 튜토리얼의 애너테이션 부분 中</b>)<br>
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