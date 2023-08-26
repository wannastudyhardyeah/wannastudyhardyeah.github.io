---
title: 제1장 - 제2절&#58; FK(외래키) 무결성 제약 옵션
author: wannastudyhardyeah
date: 2023-08-07 13:01:55 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true
plugins:
  - jekyll-plantuml

---
<h2 id="constraint">1. FK(외래키) 참조 무결성 제약 옵션</h2>

<h3 id="delete-modify-h3">1.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">DELETE</code> ACTION</h3>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASCADE</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 Child 테이블 데이터도 함께 삭제.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET NULL</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 Child 테이블 데이터가 ``NULL``로 변경됨.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET DEFAULT</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 child 테이블 데이터가 ``DEFAULT``값으로 변경.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RESTRICT</code><br>
&nbsp;&nbsp;\: Child 테이블에 PK값 없는 경우만 Parent 테이블에서 데이터 삭제 허용<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NO ACTION</code><br>
&nbsp;&nbsp;\: 참조무결성 위반하는 삭제/수정 action 취하지 않음.<br>


<h3 id="insert-h3">1.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">INSERT</code> ACTION</h3>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AUTOMATIC</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;PK 값 생성 후 Child 테이블 데이터 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET NULL</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블 외부키를 ``NULL`` 값으로 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET DEFAULT</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블 외부키를 지정된 기본값으로 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DEPENDENT</code><br>
&nbsp;&nbsp;\: Parent 테이블 데이터에 PK 있을 때만,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블에서 데이터 입력 허용<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NO ACTION</code><br>
&nbsp;&nbsp;\: 참조무결성 위반하는 입력 action 취하지 않음.<br>