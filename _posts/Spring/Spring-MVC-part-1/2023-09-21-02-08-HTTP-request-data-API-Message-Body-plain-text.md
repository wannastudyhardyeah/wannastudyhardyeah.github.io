---
title: 섹션2 서블릿) HTTP 요청 데이터 - API 메시지 바디 - 단순 텍스트
author: wannastudyhardyeah
date: 2023-09-21 10:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. API 메시지 바디 - 단순 텍스트</h2>
&nbsp;&nbsp;``HTTP`` message body에<br>
데이터 직접 담아서 요청<br>
- HTTP API에서 주로 사용.<br>
(JSON, XML, TEXT)<br>
- 데이터 형식은 주로 JSON.<br>
- ``POST``, ``PUT``, ``PATCH``<br>

&nbsp;&nbsp;가장 단순한 텍스트 메시지를<br>
HTTP 메시지 바디에 담아 전송, 읽기 해보기!<br>

&nbsp;&nbsp;HTTP 메시지 바디 데이터를<br>
``InputStream`` 사용해서 직접 읽어보기!<br>

<h3>1.1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>RequestBodyStringServlet</b></code></h3>

```java
protected void service() throws ~ {
    ServletInputStream inputStream 
            = request.getInputStream();
    String messageBody 
            = StreamUtils.copyToString(inputStream, 
                            StandardCharsets.UTF_8);

    System.out.println("messageBody = " 
                        + messageBody);

    response.getWriter().write("ok");
}
```

이렇게 코드를 작성하고<br>
postman으로<br>
``http://localhost:8080/request-body-string``에<br>
``raw``의 ``text``로 "hello!"라고 전송하면,<br>
서버 로그에 아래와 같이 나온다.<br>

```powershell
Received 
[POST /request-body-string HTTP/1.1
Content-Type: text/plain
User-Agent: PostmanRuntime/7.32.3
Accept: */*
Postman-Token: 308b7c79-248b-40fb-966d-89d141f31715
Host: localhost:8080
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Length: 6

hello!]
```
```powershell
messageBody = hello!
```

정상적으로 출력된 걸 확인할 수 있다.<br>

```java
protected void service() throws ~ {
    ServletInputStream inputStream 
            = request.getInputStream();
    String messageBody 
            = StreamUtils.copyToString(inputStream, 
                            StandardCharsets.UTF_8);

    // System.out.println("messageBody = " 
    //                     + inputStream);
    System.out.println("messageBody = " 
                        + inputStream);

    response.getWriter().write("ok");
}
```

만약, 이렇게<br>
``inputStream``을 직접 찍는다면?<br>
<br>
서버 로그에 이렇게 나온다.<br>

```powershell
messageBody = org.apache.catalina.connector.CoyoteInputStream@52fc42ff
```