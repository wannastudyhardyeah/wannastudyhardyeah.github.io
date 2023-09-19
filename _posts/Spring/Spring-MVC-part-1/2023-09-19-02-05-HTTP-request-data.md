---
title: 섹션2 서블릿) HTTP 요청 데이터
author: wannastudyhardyeah
date: 2023-09-19 11:09:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. HTTP 요청 데이터 개요</h2>
HTTP 요청 메시지를 통해<br>
클라이언트에서 서버로 데이터 전달 방법 알아보기<br>
3가지가 있음.<br>

<h3>1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>GET</b></code> - 쿼리 패러미터</h3>

- ``/url?username=hello&age=20``<br>
- 메시지 바디 없이<br>
URL의 쿼리 패러미터에 데이터 포함해서 전달<br>
(검색, 필터, 페이징 등에서 많이 사용)<br>

<h3>1.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>POST</b></code> - HTML Form</h3>

- ``content-type``: ``application/x-www-form-urlencoded``<br>
- 메시지 바디에 쿼리 패러미터 형식으로 전달<br>
=> ``username=hello&age=20``<br>
(회원 가입, 상품 주문, HTML Form 사용)

<h3>1.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>HTTP message body</b></code>에 데이터 직접 담아서 요청</h3>

- HTTP API에서 주로 사용(REST API)<br>
(JSON, XML, TEXT)<br>
- 데이터 형식은 주로 JSON 사용<br>
- POST, PUT, PATCH<br>


