---
title: 섹션2 서블릿) HttpServletRequest 개요
author: wannastudyhardyeah
date: 2023-09-19 11:07:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">HttpServletRequest</code></h2>
서블릿은 개발자가 HTTP 요청 메시지 편리하게 사용하도록<br>
개발자 대신에 HTTP 요청 메시지 파싱하고,<br>
그 결과를 ``HttpServletRequest`` 객체에 담아서 제공함.<br>

<h3>1.1. HTTP 요청 메시지</h3>

```plaintext
POST /save HTTP/1.1
Host: ~~~
Content-Type: ~~

username=~~&age=~~
```

- Start Line
    - HTTP 메서드
    - URL
    - 쿼리 스트링
    - 스키마, 프로토콜

- 헤더
    - 헤더 조회

- 바디
    - form 파라미터 형식 조회
    - message body 데이터 직접 조회

<h3>``HttpServletRequest`` 객체의 추가 부가기능</h3>

- 임시 저장소 기능<br>
\: 해당 HTTP 요청 시작~끝날 때까지 유지됨<br>
    - 저장<br>
    ``request.setAttribute(name, value)``<br>
    - 조회<br>
    ``request.getAttribute(name)``<br>

- 세션 관리 기능<br>
\: ``request.getSession(create: true);``

- <span style="color:red"><b>중요한 점</b></span><br>
``HttpServletRequest``, ``HttpServletResponse`` 사용 시<br>
이 기능에 대해 깊이있게 이해 하려면<br>
<b>HTTP 스펙의 제공 요청, 응답 메시지 자체를 이해!!!</b><br>
