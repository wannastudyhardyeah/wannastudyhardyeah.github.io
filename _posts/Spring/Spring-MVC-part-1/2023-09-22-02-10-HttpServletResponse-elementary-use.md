---
title: 섹션2 서블릿) HTTP 요청 데이터 - API 메시지 바디 - JSON
author: wannastudyhardyeah
date: 2023-09-22 13:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">


&nbsp;&nbsp;HTTP API에서 주로 사용하는 JSON 형식으로<br>
데이터를 전달해보자.<br>

<h2>1. <code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">HttpServletResponse</code></h2>

<b style="font-size:1.2rem">HTTP 응답 메시지 생성</b><br>
- HTTP 응답코드 지정<br>
(``404``, ``200`` 등)<br>
- 헤더 생성
- 바디 생성

<b style="font-size:1.2rem">편의 기능 제공</b><br>
- content-type
- cookie
- redirect

<h3>1.1. HttpServletResponse 기본 사용법</h3>

``/main/~/hello.servlet/basic``에서<br>
``response`` 패키지 생성,<br>
그리고<br>
``ResponseHeaderServlet.java`` 클래스 생성.<br>


