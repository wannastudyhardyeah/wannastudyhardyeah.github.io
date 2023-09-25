---
title: 섹션3) 회원 관리 웹 애플리케이션 요구사항
author: wannastudyhardyeah
date: 2023-09-25 10:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

&nbsp;&nbsp;기본적인 "회원 관리 웹 애플리케이션"을 통해<br>
서블릿, JSP, MVC 패턴의 순서대로<br>
각각 적용하여 개발해본다!<br>

<h2 id="member-app-needs">1. 회원 관리 웹 애플리케이션 요구사항</h2>

<b style="font-size:1.2rem">회원 정보</b><br>
- 이름<br>
\: ``username``<br>
- 나이<br>
\: ``age``<br>

<b style="font-size:1.2rem">기능 요구사항</b><br>
- 회원 저장<br>

- 회원 목록 조회<br>

<h3 id="member-domain-model-h3">1.1. 회원 도메인 모델</h3>

``/main/~/hello/servlet/domain/member``에서<br>
``Member.java`` 생성하여 아래와 같이 작성.<br>

