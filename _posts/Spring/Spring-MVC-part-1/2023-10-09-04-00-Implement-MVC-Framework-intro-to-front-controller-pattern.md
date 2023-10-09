---
title: 섹션4) MVC 프레임워크 - 프론트 컨트롤러 패턴 소개
author: wannastudyhardyeah
date: 2023-10-09 07:20:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2 id="intro-to-front-controller-pattern">1. 프론트 컨트롤러<span style="color: #808080;">FrontController</span> 패턴 소개</h2>

<h3 id="feature-h3">1.1. 특징</h3>
- 프론트 컨트롤러 서블릿 하나로<br>
클라이언트의 요청을 받음.<br>
- 프론트 컨트롤러가<br>
요청에 맞는 컨트롤러 찾아서 호출.<br>
- 입구를 하나로!!!<br>
- 공통 처리 가능<br>
- 프론트 컨트롤러 제외한<br>
나머지 컨트롤러는 서블릿 사용 안 해도 됨.<br>

&nbsp;&nbsp;&nbsp;&nbsp;스프링 웹 MVC의 핵심은<br>
바로 ``FrontController``!<br>
<b>==></b> ``DispatcherServlet``이 프론트 컨트롤러 패턴임.<br>