---
title: 섹션2 서블릿) HttpServletRequest 개요
author: wannastudyhardyeah
date: 2023-09-19 11:07:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. <<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">HttpServletRequest</code></h2>
서블릿은 개발자가 HTTP 요청 메시지 편리하게 사용하도록<br>
개발자 대신에 HTTP 요청 메시지 파싱하고,<br>
그 결과를 ``HttpServletRequest`` 객체에 담아서 제공함.<br>

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



<h3>1.1. 서블릿 등록하기</h3><br>
``~src/main/~/hello/servlet/ServletApplication.java``에서<br>
``@ServletComponentScan`` 애너테이션으로 서블릿 사용 가능.<br>

그리고<br>

``~/src/main/~/hello/servlet/~/HelloServlet.java``에서<br>
@WebServlet(name = "서블릿_이름", urlPatterns = "/URL_매핑")<br>.


```java
System.out.println("request = " + request);
System.out.println("resp = " + response);
```

```powershell
request = org.apache.catalina.connector.RequestFacade@1e09573
resp = org.apache.catalina.connector.ResponseFacade@c6ea04
```

WAS가 서블릿 표준스펙(``HttpServletRequest``)을 구현하는데,<br>
그 구현체가 찍힌 게 바로 위의 결과.<br>


``URL?username=~~`` 여기서 ``?``로 붙은 걸<br>
쿼리 파라미터<span style="color: #808080;">Query Parameter</span>라고 함.<br>

```powershell
http://localhost:8080/hello?username=kim
```
이렇게 보내면<br>

```powershell
username = kim
```
이렇게 찍힌다.<br>

HTTP 요청으로 매핑된 URL이 호출되면,<br>
서블릿 컨테이너는 ``service`` 메서드 실행함.<br>
``service(HttpServletRequest, HttpServletResponse)``<br>

<h3>1.2. HTTP 요청 메시지를 로그로 확인하기</h3>

``/src/main/resources/application.properties``에서<br>
아래와 같이 입력.<br>

```plaintext
logging.level.org.apache.coyote.http11=debug
```

<h3>1.3. 서블릿 컨테이너 동작 방식 설명<br>