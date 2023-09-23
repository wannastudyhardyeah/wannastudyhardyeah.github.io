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

<h2>1. JSON 형식 전송</h2>
- POST 방식<br>
<b>=></b> ``http://localhost:8080/request-body-json``<br>
- content-type<br>
<b>``application/json``</b><br>
- message body<br>
``{"username": "hello", "age": 20}``<br>
<br>
- <b style="font-size:1.2rem">결과</b><br>
<b>``{"username": "hello", "age": 20}``</b><br>
<br>
<h2>2. JSON 형식 파싱 추가</h2>
&nbsp;&nbsp;JSON 형식으로 파싱 되도록<br>
객체를 하나 생성하기!<br>

``/main/~/hello.servlet/basic/``에서<br>
``HelloData.java``를 다음과 같이 작성.<br>
```java
@Getter @Setter
public class HelloData {

    private String username;
    private int age;
}
```
<br>

``/main/~/hello.servlet/basic/request``에서<br>
``RequestBodyJsonServlet.java``를<br>
다음과 같이 작성.<br>

```java
@WebServlet(name = "requestBodyJsonServlet", 
            urlPatterns = "/request-body-json")
public class RequestBodyJsonServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request, 
                           HttpServletResponse response) 
                throws ServletException, IOException {
        ServletInputStream inputStream 
                                = request.getInputStream();
        String messageBody 
                = StreamUtils
                        .copyToString(inputStream, 
                                      StandardCharsets.UTF_8);

        System.out.println("messageBody = " 
                          + messageBody);
    }
}
```
<br>

그런 뒤에 postman에서<br>
POST 메서드로<br>
``http://localhost:8080/request-body-json`` 주소로<br>
``body``에는 다음과 같이 입력.<br>
```json
{"username": "hello", "age": 20}
```
``raw`` 체크, ``JSON`` 선택!<br>

그런 뒤 "Send"로 전송을 하면<br>
서버 로그에 아래와 같이 찍힌다.<br>
```powershell
messageBody = {"username": "hello", "age": 20}
```

<h3>&nbsp;&nbsp;2.1. 스프링에서 JSON 파싱하기</h3>
&nbsp;&nbsp;JSON을 사용가능한 자바 객체로 변환하려면<br>
--> Jackson, Gson 등의 JSON 변환 라이브러리 사용.<br>
스프링 부트에서는 Jackson 라이브러리 제공함.<br>
(``ObjectMapper``)<br>

이 라이브러리를 이용해서<br>
다음과 같이 코드 작성.<br>

```java
protected void service(~~){
        ~~~~
        HelloData helloData 
                = objectMapper.readValue(messageBody, 
                                         HelloData.class);
        System.out.println("helloData.getUsername = " 
                          + helloData.getUsername());
        System.out.println("helloData.getAge = " 
                          + helloData.getAge());
        ~~~~
}
```
그리고 실행한 뒤에<br>
postman으로 똑같이 전송하면<br>
서버 로그에 아래와 같이 찍힌다.<br>

```powershell
helloData.getUsername = hello
helloData.getAge = 20
```
