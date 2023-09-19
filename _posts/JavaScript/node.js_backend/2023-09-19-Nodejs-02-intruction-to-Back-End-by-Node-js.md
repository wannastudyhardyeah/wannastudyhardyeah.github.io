---
title: 02장 - Node.js로 백엔드 입문하기
author: wannastudyhardyeah
date: 2023-09-19 10:06:00 +0800
categories: [Node.js]
tags: [Javascript]

---
본 포스트는 <a href="https://goldenrabbit.co.kr/product/springboot3java/">『Node.js 백엔드 개발자 되기』(박승규, 골든래빗(주), 2023)</a>를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
<h2>1. Node.js 소개</h2>

<b style="font-size:1.2rem">Node.js</b><br>
서버 측 자바스크립트 런타임 환경.<br>
브라우저 밖에서 자바스크립트를 사용하는 V8 엔진 사용.<br>
이벤트 기반<span style="color: #808080;">Event-Driven</span> 비동기 환경<br>

<b style="font-size:1.2rem">npm</b><br>
패키지 매니저<br>

<br>
<h2>2. Node.js가 서버 - 자바스크립트 실행</h2>
Node.js는 V8 자바스크립트 엔진과 libuv 및 C/C++에 의존성을 가진 자바스크립트 런타임.<br>

<h3>2.1. Node.js의 구성요소</h3>
Node.js의 소스 코드는 C++, 자바스크립트, 파이썬 등으로 이뤄짐.<br>

각 계층이 각 하단에 있는 API 사용하는 계층의 집합으로 설계됨.<br>

<h3>2.2. 자바스크립트 실행 위한 V8 엔진</h3>
V8은 C++로 만든 오픈 소스 자바스크립트 엔진.<br>
이그니션(인터프리터 역할)과 터보팬(컴파일러) 사용해 컴파일.<br>

<h3>2.3. libuv</h3>
이벤트 루프와 운영체제 단 비동기 API 및 스레드 풀 지원.<br>
즉, HTTP, 파일, 소켓 통신 IO 기능 등을 이를 libuv 사용해 제공.<br>

다양한 플랫폼에서 사용 가능한 이벤트 루프 제공.<br>
(리눅스: epoll, 윈도우: IOCP,<br>
&nbsp;맥OS: kqueue, SunOS: 이벤트 포트)<br>

그리고, 네트워크, 파일 IO, DNS, 스레드 풀 기능 추가 제공.<br>

<h3>2.4. Node.js 아키텍처</h3>

Node.js의 프로세스는<br>
이벤트 루프에 사용하는 싱글 스레드 하나와<br>
비동기 처리 지원하는 스레드 풀로 구성됨.<br>

<br>
<h2>3. Node.js의 기술적 특징</h2>

<h3>3.1. 싱글 스레드</h3>
즉, 콜 스택이 하나만 있으므로<br>
한 번에 하나의 작업만 가능.<br>

<h3>3.2. 이벤트 기반 아키텍처</h3>
<b>어떻게 하면 요청을 하나의 스레드로 동시에 처리할까?</b><br>
<b>--></b> 이벤트 기반 아키텍처 적용.<br>
즉, 콜 스택에 쌓인 작업을 다른 곳에서 처리한 다음,<br>
처리 완료 시 알림 받음.<br>

Node.js는 오래 걸리는 일을 이벤트 루프에 맡김.<br>

<h3>3.3. 이벤트 루프</h3>
Node.js는 반응자 패턴<span style="color: #808080;">reactor pattern</span> 사용하여<br>
이벤트 기반 아키텍처 구축함.<br>


<b>반응자 패턴</b><br>
반응자 패턴은 이벤트 디멀티플렉서와 이벤트 큐로 구성.<br>

이벤트 추가 주체와 이벤트 실행 주체를 분리.<br>

반응자 패턴에서 이벤트 루프는 필수.<br>
(이벤트 루프는 libuv에 있음.)<br>


