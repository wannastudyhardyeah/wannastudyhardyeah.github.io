---
title: 섹션2 서블릿) HTTP 요청 데이터 - POST HTML Form
author: wannastudyhardyeah
date: 2023-09-20 10:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>POST</b></code> HTML Form</h2>
HTML의 Form을 이용하여<br>
클라이언트에서 서버로<br>
데이터를 전송해보기<br>
(주로 회원가입, 상품 주문 등)<br>

<b style="font-size:1.2rem">특징</b><br>
- Content-Type<br>
\: ``application/x-www-form-urlencoded``<br>
- ``username=hello&age=20''
메시지 바디에<br>
쿼리 패러미터 형식으로 데이터 전달<br>

<h3>1.1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>src/~/hello-form.html</b></code> 생성</h3>

```html
(생략)
<form action="/request-param" method="post">
    username: <input type="text" name="username" />
    age:      <input type="text" name="age" />
    <button type="submit">전송</button>
(생략)
```

이 form에<br>
``username=hello``, ``age=20`` 입력 시<br>

```powershell
username = hello
age = 20
```
서버 로그에 이렇게 기록된다.<br>

클라이언트(브라우저) 입장에서는<br>
``GET``, ``POST``<br>
이 두 방식에 있어서 차이가 있지만,<br>
서버의 입장에서는 둘의 형식이 동일하여<br>
구분없이 조회 가능하다.<br>


<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;"><b style="color:red">Cf)</b> content-type은<br>&nbsp;&nbsp;&nbsp;&nbsp;HTTP 메시지 바디의 데이터 형식을 지정.<br>
<br>
<b>-</b> GET URL 쿼리 패러미터 형식으로 전달 시,<br>
&nbsp;&nbsp;&nbsp;&nbsp;HTTP 메시지 바디 미사용하므로 없음.<br>
<b>-</b> POST HTML Form 형식으로 전달 시,<br>
&nbsp;&nbsp;&nbsp;&nbsp;HTTP 메시지 바디에 해당 데이터 포함해 보내므로<br>
바디에 포함된 데이터의 형식을 꼭 지정!!!<br>
</div>

<h3>1.1.2. Postman 사용한 테스트</h3>
HTML Form 사용 안 하고<br>
Postman을 이용해도 됨.<br>

- <b>Body</b><br>
``x-www-form-urlencoded`` 선택<br>
- 헤더의 ``Content-Type``<br>
``application/x-www-form-urlencoded``<br>
