---
title: 스프링 프레임워크 - 1. 개요
author: wannastudyhardyeah
date: 2023-10-02 14:59:00 +0800
categories: [Spring-Doc]
tags: [Spring, Java]
math: true
---
<div class="toc-multiple-posts">
<h2>스프링 프레임워크 문서 읽기</h2>
<ol class="sc-fmciRz gyCSrP"><a href="/posts/Spring-Chap-01-Frame-Work-Overview/" aria-current="page" class="active">챕터 1. 개요</a><br>
<a href="/posts/Spring-Chap-02-Core-Technologies/">챕터 2. 핵심 기술</a>
</ol><div class="sc-fIosxK hRRhWV"><div class="sc-gUQvok eBShCz">
<div class="series-number" align="right">1/2</div>
</div></div>
</div>
<br>
<hr width="80%">
<h2 id="what-we-mean-by-spring-h2">1. "스프링"이 뜻하는 바</h2>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 프레임워크<span style="color: #808080;">Spring Framework</span>는 여러 모듈로 구성되어 있다. 그중 중심이 되는 모듈은 설정 모델<span style="color: #808080;">configuration model</span>과 의존관계 주입<span style="color: #808080;">dependency injection mechanism</span>이 포함된 컨테이너이다.<br>
<br>
<hr width="50%">
<h2 id="history-of-spring-and-the-spring-framework-h2">2. 스프링과 스프링 프레임워크의 변천사</h2>

&nbsp;&nbsp;&nbsp;&nbsp;스프링은 2003년 J2EE 기술 명세 복합체에 대응된 것으로 시작되었다.
스프링 프로그래밍 모델은 단순히 자카르타(자바) EE 플랫폼 기술 명세에만 방점을 두는 것이 아니라, 그보다는, 세심한 선택에 의한 전통적 EE 범주의 개별 기술명세를 통합하는 데에 있다.

- 서블릿<span style="color: #808080;">Servlet</span> API (JSR 340)<br>
- 웹소켓<span style="color: #808080;">WebSocket</span> API (JSR 356)<br>
- 동시성<span style="color: #808080;">Concurrency</span> 유틸리티 (JSR 236)<br>
- JSON 바인딩<span style="color: #808080;">Biding</span> API (JSR 367)<br>
- 빈 검증<span style="color: #808080;">Bean Validation</span> (JSR 303)<br>
- JPA (JSR 338)<br>
- JMS (JSR 914)<br>

그리고, 스프링 프레임워크는 의존관계 주입 (JSR 330), 그리고 공통 애너테이션 (JSR 250) 기술 명세 또한 지원하고 있다.<br> 이것은 ``javax`` 패키지 기반이었으나, 본래 스프링 프레임워크에서 제공했던 스프링에 특화된 메커니즘을 대신하여 개발자들에게 선택받게 되었다.

<br>
<hr width="50%">
<h2 id="design-philosophy-h2">3. 설계에 관한 철학</h2>
- 모든 레벨에서 선택할 수 있도록 한다.<br>
스프링을 이용하면, 설계에 관련된 사항을 최대한 늦게 결정할 수 있습니다. 가령, 객체 저장<span style="color: #808080;">persistence</span> 솔루션을 변경하고자 할 때 코드를 수정하지 않고 이러한 설정이 가능해집니다. 이는 서드파티 API들을 통합하여 아우르는 다른 인프라스트럭처에 대해서도 마찬가지입니다.<br>

- 다양한 관점을 수용한다.<br>

- 호환성을 바탕으로 지속적인 유지보수를 제공한다.<br>

- API 설계를 신경 쓴다.<br>
스프링 개발 팀은 오랜 기간, 여러 버전에 걸쳐서도 유지되고 직관적인 API를 만들 수 있도록 많은 시간을 들여 고려합니다.<br>

- 코드 품질에 대해 높은 기준을 가진다.<br>
스프링 프레임워크는 현재의 유효하고 정확한 javadoc에 만전을 기합니다. 이는 패키지 사이의 순환 의존관계를 확실하게 방지할 수 있는 코드 설계구조 프로젝트 중 하나이기 때문입니다.<br>

<br>
<hr width="50%">
<h2 id="feedback-and-contributions-h2">4. 피드백과 기여에 대해</h2>

<br>
<hr width="50%">
<h2 id="getting-started-h2">5. 시작하기</h2>