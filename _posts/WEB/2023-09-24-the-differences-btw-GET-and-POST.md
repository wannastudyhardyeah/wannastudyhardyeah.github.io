---
title: 메서드 방식 - GET과 POST 차이점
author: wannastudyhardyeah
date: 2023-09-24 23:00:20 +0800
categories: [WEB]
tags: [HTTP, Network]
math: true

---
<h2 id="get-method-h2"><code class="language-javascript highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GET</code> 메서드</h2>
&nbsp;&nbsp;``GET`` 요청 보낼 때<br>
본문<span style="color: #808080;">body</span>이나 페이로드<span style="color: #808080;">payload</span>를 보내게 되면,<br>
요청 거부당할 수도 있음.<br>
따라서, ``GET`` 요청에는 본문, 페이로드 담지 않는 게 바람직함.<br>

- 요청<span style="color: #808080;">request</span>에 본문 존재<br>
\: <b style="color:red">X</b><br>
- 성공 응답<span style="color: #808080;">response</span>에 본문 존재<br>
\: <b style="color:red">O</b><br>
- 안전함<br>
\: <b style="color:red">O</b><br>
<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;">cf) <b style="color:red">"안전하다"의 정의</b><br>
&nbsp;&nbsp;HTTP 메서드가 서버의 상태<span style="color: #808080;">state</span>를 바꾸지 않을 시에!<br>
달리 말하면, 읽기 작업만<span style="color: #808080;">read-only</span> 수행하면!<br>
<br>
&nbsp;&nbsp;모든 안전한 HTTP 메서드는 멱등성도 갖는다.<br>
But, 그 역<span style="color: #808080;">reverse</span>은 성립 X</div>
- 멱등성<span style="color: #808080;">idempotent</span><br>
\: <b style="color:red">O</b><br>
<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;">cf) <b style="color:red">"멱등"의 정의</b><br>
&nbsp;&nbsp;HTTP 메서드가<br>
- &nbsp;동일 요청 한 번 보내는 것과 여러 번 보내는 것이<br>
&nbsp;&nbsp;&nbsp;같은 효과를 지니고,<br>
- &nbsp;서버의 상태도 동일하게 남을 때.<br>
==> <i>"해당 HTTP 메서드가 멱등성을 지닌다."</i><br></div>
- 캐시<span style="color: #808080;">cache</span> 가능<br>
\: <b style="color:red">O</b><br>
- HTML 양식<span style="color: #808080;">forms</span>에서 사용 가능<br>
\: <b style="color:red">O</b><br>

<hr width="50%">
<h2 id="post-method-h2"><code class="language-javascript highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">POST</code> 메서드</h2>
&nbsp;&nbsp;보통 HTML 양식<span style="color: #808080;">forms</span>을 통해 전송.<br> 이로써 서버에 변경사항 만듦.<br>
<br>
&nbsp;&nbsp;``<form>`` 요소<span style="color: #808080;">element</span>의 ``enctype`` 특성<span style="color: #808080;">attribute</span>이나<br>
``<input>`` 요소의 ``formenctype``,<br>
혹은, ``button`` 요소의 ``formenctype``에<br>
담긴 문자열로 결정됨.<br>
<br>
&nbsp;&nbsp;<b>예시)</b><br>
1. 기존 리소스에 주석달기<br>
2. 게시판, 메일링 리스트 등에 글 게재<br>
3. 회원가입 모달<span style="color: #808080;">modal</span>로 새 사용자 추가<br>
4. 양식 전송 결과 등을<br>
데이터 처리 프로세스에 전송<br>
5. 이어붙이기<span style="color: #808080;">append</span> 연산 통한 DB 확장<br>

- 요청<span style="color: #808080;">request</span>에 본문 존재<br>
\: <b style="color:red">O</b><br>
- 성공 응답<span style="color: #808080;">response</span>에 본문 존재<br>
\: <b style="color:red">O</b><br>
- 안전함<br>
\: <b style="color:red">X</b><br>
- 멱등성<span style="color: #808080;">idempotent</span><br>
\: <b style="color:red">X</b><br>
(즉, 한 번 보내는 것과 여러 번 보내는 것이<br>
그 효과가 다르다.)<br>
- 캐시<span style="color: #808080;">cache</span> 가능 여부<br>
\: <b style="color:red">fresh</b>한 응답이 담겼을 때만!!<br>
[참조](https://httpwg.org/specs/rfc7234.html#expiration.model)<br>
- HTML 양식<span style="color: #808080;">forms</span>에서 사용 가능<br>
\: <b style="color:red">O</b><br>