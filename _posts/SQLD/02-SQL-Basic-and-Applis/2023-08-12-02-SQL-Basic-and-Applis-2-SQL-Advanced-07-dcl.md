---
title: 제2장 - 제7절&#58; DCL
author: wannastudyhardyeah
date: 2023-08-12 13:09:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="dcl-intro"><b>1. DCL 개요</b></h2>
&nbsp;&nbsp;유저를 생성하고 권한 제어할 수 있는 명령어.<br>

<br>
<hr width="50%">
<h2 id="prmt-for-user"><b>2. 유저와 권한</b></h2>

<b>권한 부여</b><br>
```sql
GRANT CREATE USER TO [유저명];
```

<b>유저 접속</b><br>
```sql
CONN [유저명]/[패스워드];
```

<b>유저 생성</b><br>
```sql
CREATE USER [유저명] IDENTIFIED BY [패스워드];
```

<b>유저의 로그인 위한 권한 부여</b><br>
```sql
GRANT   CREATE SESSION  TO  [유저명];
```

<b>유저에게 테이블 생성 권한 부여</b><br>
```sql
GRANT   CREATE TABLE TO [유저명];
```

<b>테이블 생성</b><br>
```sql
CREATE TABLE MENU (
    MENU_SEQ    NUMBER_NOT_NULL;
    TITLE       VARCHAR2(10)
);
```

<br>
<hr width="50%">
<h2 id="grntng-by-role"><b>3. Role을 이용한 권한 부여</b></h2>
&nbsp;&nbsp;유저 생성 시 많은 권한 부여해야 하는데,<br>
ROLE을 생성하여 ROLE에 각종 권한 부여 후<br>
이를 다른 ROLE이나 유저에게 부여 가능.<br>
<br>
&nbsp;&nbsp;Oracle에서 제공하는 기본적 ROLE들 중 가장 많이 사용되는 것은<br>
``CONNENT``와 ``RESOURCE``.<br>
일반적으로 이 둘을 사용하여 권한 부여.<br>

<table align="left">
    <tr style="text-align: left; text-align: center; font-weight:bold; background: #e0e0e0;">
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">CONNECT</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">RESOURCE</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ALTER SESSION</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE CLUSTER</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE CLUSTER</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE INDEXTYPE</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE DATABASE LINK</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE OPERATOR</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE MENU_SEQUENCE</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE PROCEDURE</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE SESSION</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE MENU_SEQUENCE</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE SYNONYM</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE TABLE</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE TABLE</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE TRIGGER</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE VIEW</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE</code></td>
    </tr>
</table>

<b>유저 삭제 명령어</b><br>
```
DROP USER [유저명] CASCADE
```
``CASCADE`` 옵션은<br>
해당 유저가 생성한 오브젝트 먼저 삭제 후 유저 삭제함.<br>