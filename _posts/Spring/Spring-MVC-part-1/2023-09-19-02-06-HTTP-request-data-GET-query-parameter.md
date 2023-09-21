---
title: 섹션2 서블릿) HTTP 요청 데이터 - GET 쿼리 파라미터
author: wannastudyhardyeah
date: 2023-09-19 11:10:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. HTTP 요청 데이터 - GET 쿼리 패러미터</h2>
아래 데이터를<br>
클라이언트에서 서버로 전송해보기<br>

- ``username=hello``<br>
- ``age=20``<br>

메시지 바디 없이,<br>
URL의 쿼리 패러미터 이용하여 데이터 전달!<br>
(검색, 필터, 페이징 등에서 많이 사용됨.)<br>

<h3>1.1. 쿼리 패러미터 조회 메서드</h3>

```java
// 단일 패러미터 조회
String username = request.getParameter("username");
// 패러미트 이름들 모두 조회
Enumeration<String> parameterNames
                    = request.getParameterNames();
// 패러미터를 Map으로 조회
Map<String, String[]> parameterMap
                    = request.getParameterMap();
// 복수 패러미터 조회
String[] usernames = request.getParameterValues("username");
```

<b><code class="language-java highlighter-rouge" style="color: #83060e; font-size: 1.25rem;">RequestParamServlet</code></b><br>

```java
@WebServlet(name="RequestParamServlet",
            urlPatterns="/request-param")
public class RequestParamServlet 
                    extends HttpServlet {
    @Override
    protected void service(~~ request, ~~ response)
                    throws ServletException, IOException {
        // 전체 패러미터 조회
        request.getParameterNames().asIterator()
                .forEachRemaining(paramName
                        -> Sout(paramName + " = "
                        request.getParameter(paramName)));
        
        // 이름이 같은 복수 패러미터 조회
        String[] usernames
                = request.getParameterValues("username");
        for (String name : usernames) {
            Sout("username=" + name);
        }
    }
}
```