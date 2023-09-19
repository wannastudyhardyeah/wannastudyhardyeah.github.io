---
title: 섹션2 서블릿) HttpServletRequest 기본 사용법
author: wannastudyhardyeah
date: 2023-09-19 11:08:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 <a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/">스프링 MVC 1편(김영한, 인프런)</a> 강의를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">

<h2>1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">HttpServletRequest</code> - 기본 사용법</h2>

<h3>1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;"><b>~~.request.RequestHeaderServlet</b></code></h3>

<b>Start-Line 정보</b><br>

```powershell
--- REQUEST-LINE - start ---
request.getMethod() = GET
request.getProtocol() = HTTP/1.1
request.getScheme() = http
request.getRequestURL() = http://localhost:8080/request-header
request.getRequestURI() = /request-header
request.getQueryString() = null
request.isSecure() = false
--- REQUEST-LINE - end ---
```

<b>모든 헤더 정보</b><br>

```powershell
--- Headers - start ---
host: localhost:8080
connection: keep-alive
cache-control: max-age=0
sec-ch-ua: "Whale";v="3", "Not-A.Brand";v="8", "Chromium";v="116"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
upgrade-insecure-requests: 1
user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Whale/3.22.205.18 Safari/537.36
accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
sec-fetch-site: none
sec-fetch-mode: navigate
sec-fetch-user: ?1
sec-fetch-dest: document
accept-encoding: gzip, deflate, br
accept-language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
--- Headers - end ---
```
