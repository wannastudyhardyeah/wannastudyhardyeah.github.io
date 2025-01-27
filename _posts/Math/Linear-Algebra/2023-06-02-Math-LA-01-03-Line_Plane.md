---
title: 1.3. 직선과 평면
author: wannastudyhardyeah
date: 2023-06-02 01:02:00 +0800
categories: [Linear Algebra]
tags: [Linear Algebra, Mathematics]
math: true

---
<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">R2에서의 직선</h2>
(scalar/dot product)
길이, 거리, 각의 벡터 형식은 두 벡터의 스칼라곱의 표현을 사용하여 나타낼 수 있다.<br><br>
<b><span style="font-size: 1.34rem;">Def.</span></b><br>
\\( \overrightarrow{u} = \begin{bmatrix} u_1 \\\ u_2 \\\ \vdots \\\ u_n \end{bmatrix} \\), \\( \ \ \overrightarrow{v} = \begin{bmatrix} v_1 \\\ v_2 \\\ \vdots \\\ v_n \end{bmatrix} \ \\)이면,<br>
\\( \overrightarrow{u} \ \\)와 \\( \ \overrightarrow{v} \ \\)의 스칼라곱(스칼라적) \\( \ \overrightarrow{u} \ \cdot \ \overrightarrow{v} \ \\)는<br>
\\( \overrightarrow{u} \ \cdot \ \overrightarrow{v} = u_1 v_1 + u_2 v_2 + \cdots + u_n v_n \\)으로 정의한다.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">Thm 1.1</h2>
\\( \overrightarrow{u}, \ \overrightarrow{v}, \ \overrightarrow{w} \ \\)가 \\( \ \mathbb{R}^n \\)의 벡터이고 \\( \ c \\)가 스칼라이면,<br>
- (a) &nbsp; \\( \overrightarrow{u} \ \cdot \ \overrightarrow{v} = \overrightarrow{v} \ \cdot \ \overrightarrow{u} \\)<br>
&nbsp; &nbsp; (교환법칙)
- (b) &nbsp; \\( \overrightarrow{u} \ \cdot \( \ \overrightarrow{v} + \overrightarrow{w} \ \) = \overrightarrow{u} \ \cdot \ \overrightarrow{v} + \overrightarrow{u} \ \cdot \ \overrightarrow{w} \\)<br>
&nbsp; &nbsp; (분배법칙)
- (c) &nbsp; \\( \( c \ \overrightarrow{u} \ \) \cdot \ \overrightarrow{v} = c \ \( \ \overrightarrow{u} \ \cdot \ \overrightarrow{v} \ \) \\)<br>
- (d) &nbsp; \\( \overrightarrow{u} \ \cdot \ \overrightarrow{u} \ge 0 \\)이고, &nbsp; \\( \overrightarrow{u} \ \cdot \ \overrightarrow{u} = 0 \\)<br>
\\( \quad \quad \quad \quad \quad \Longleftrightarrow \\)<br>
\\( \quad \quad \quad \quad \quad \overrightarrow{u} = \overrightarrow{0} \\)<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">길이</h2>
\\( \mathbb{R}^n \\)의 벡터 &nbsp; \\( \overrightarrow{v} = \begin{bmatrix} v_1 \\\ \vdots \\\ v_n \end{bmatrix} \\)의 길이 또는 크기는<br>
\\( \left| \left| \ \overrightarrow{v} \ \right| \right| = \sqrt{ \ \ \overrightarrow{v} \ \cdot \ \overrightarrow{v} \ \ } = \sqrt{ {v_1}^2 + \cdots + {v_n}^n } \\)으로<br>
정의된 음이 아닌 스칼라이다.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">Thm 1.3</h2>
\\( \overrightarrow{v} \ \\)가 \\( \ \mathbb{R}^n \\)의 벡터이고 &nbsp; \\( c \\)가 스칼라이면,<br>
&nbsp; (a) &nbsp; \\( \lVert \overrightarrow{v} \rVert = 0 \\)<br>
&nbsp; (b) &nbsp; \\( \left\vert c \ \overrightarrow{v} \right\vert = \left\vert c \right\vert \ \lVert \overrightarrow{v} \rVert \\)<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">단위벡터<span style="color: #808080;">unit vector</span></h2>
: 길이가 1인 벡터<br>

&nbsp; &nbsp; <b><span style="font-size: 1.35rem;">Thm. 코시-슈바르츠 부등식</span></b><br>
\\( \mathbb{R}^n \ \\)의 임의의 벡터 &nbsp; \\( \overrightarrow{u}, \ \overrightarrow{v} \\)에 대하여<br>
\\( \left\vert \ \overrightarrow{u} \cdot \overrightarrow{v} \ \right\vert  \le \lVert \overrightarrow{u} \rVert \ \lVert \overrightarrow{v} \rVert \\)이다.<br>
&nbsp; &nbsp; <b><span style="font-size: 1.35rem;">Thm. 삼각 부등식</span></b><br>
\\( \lVert \ \overrightarrow{u} + \overrightarrow{v} \ \rVert  \le \lVert \overrightarrow{u} \rVert + \lVert \overrightarrow{v} \rVert \\)이다.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">두 벡터 사이의 거리</h2>
두 벡터 \\( \overrightarrow{u}, \ \overrightarrow{v} \\)에 대하여,<br>
\\( d(\overrightarrow{u}, \ \overrightarrow{v}) = \lVert \overrightarrow{u} - \overrightarrow{v} \rVert \\)로 정의.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">두 벡터 사이의 각 &#952;</h2>
\\( \cos \theta = \dfrac{ \overrightarrow{u} \cdot \overrightarrow{v} }{ \lVert \overrightarrow{u} \rVert \lVert \overrightarrow{v} \rVert } \\)를 만족하는 &nbsp; \\( 0 \le \theta \le \pi \\)로 정의.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">직교/수직</h2>
\\( \mathbb{R}^n \\)의 벡터 &nbsp; \\( \overrightarrow{u}, \ \overrightarrow{v} \\)는<br>
\\( \overrightarrow{u} \cdot \overrightarrow{v} = 0 \\)일 때,<br>
서로 수직(또는 직교)이라고 한다.<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">피타고라스 정리</h2>
\\( \mathbb{R}^n \\)에 있는 임의의 벡터 &nbsp; \\( \overrightarrow{u}, \ \overrightarrow{v} \\)에 대하여<br>
\\( { \lVert \overrightarrow{u} + \overrightarrow{v} \rVert }^2 = { \lVert \overrightarrow{u} \rVert }^2 + { \lVert \overrightarrow{v} \rVert }^2 \\)<br>
\\( \quad \quad \quad \quad \Longleftrightarrow \\)<br>
\\( \quad \quad \overrightarrow{u} \\)와 &nbsp; \\( \overrightarrow{v} \\)가 직교<br>

<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">사영</h2>
&nbsp; &nbsp; <b><span style="font-size: 1.35rem;">목표</span></b><br>
&nbsp; &nbsp; &#58; 한 점( \\( B \\) )에서 직선( \\( l \\) )까지의 최단거리를 기하학적으로 이해해보기.<br>
&nbsp; &nbsp; <b><span style="font-size: 1.35rem; border-bottom: 3px solid;">Def.</span></b><br>
&nbsp; &nbsp; \\( \overrightarrow{v} \\)&nbsp;의 종점에서 &nbsp; \\( \overrightarrow{u} \\) 위로 수직으로 내려 얻어지는 벡터를<br>
&nbsp; \\( \overrightarrow{u} \\) 위로의 &nbsp; \\( \overrightarrow{v} \ \\)의 사영&nbsp;이라 정의한다.<br>
&nbsp; 이를 \\( \text{proj}_{ \overrightarrow{u} } \ ( \ \overrightarrow{v} \ ) \\)라고 표기하면,<br>
<span style="line-height: 2;">&nbsp; \\( \text{proj}_{ \overrightarrow{u} } \ ( \ \overrightarrow{v} \ ) = \dfrac{ \overrightarrow{u} \cdot \overrightarrow{v} }{ \overrightarrow{u} \cdot \overrightarrow{u} } \\)를 만족한다.</span><br>
<hr width="5%">
&nbsp; &nbsp; <span style="font-size: 1.35rem;">\\( \overrightarrow{p} = \text{proj}_\overrightarrow{v} \\)&nbsp;<b>를 구하기</b></span><br>

&nbsp; \\( \text{sol)} \ \ \overrightarrow{p} = a \ \overrightarrow{u} \ \\)라고 하고 &nbsp; \\( a \\)를 구하기.<br><br>
피타고라스의 정리에 의해서<br>
\\( \begin{matrix} { \lVert \overrightarrow{v} \rVert }^2 &=& { \lVert a \ \overrightarrow{u} \rVert }^2 + { \lVert \overrightarrow{v} - a \ \overrightarrow{u} \rVert }^2 \quad \quad \quad \quad \quad \quad \\\ &=& a^2 \ { \lVert \overrightarrow{u} \rVert }^2 + { \lVert \overrightarrow{v} \rVert }^2 + a^2 \ { \lVert \overrightarrow{u} \rVert }^2 - 2 a \ \overrightarrow{u} \cdot \overrightarrow{v} \end{matrix} \\) <br>
&nbsp; <span style="line-height: 1.85">\\( \Longrightarrow 2a^2 \ { \lVert \overrightarrow{u} \rVert }^2 = 2a \ \overrightarrow{u} \cdot \overrightarrow{v} \\) </span><br>
\\( \therefore a = \dfrac{ \overrightarrow{u} \cdot \overrightarrow{v} }{ { \lVert \overrightarrow{u} \rVert }^2 } \overrightarrow{u} \\)이므로,<br>
&nbsp; \\( \overrightarrow{p} = \text{proj}_{ \overrightarrow{u} } \ ( \ \overrightarrow{v} \ ) = \dfrac{ \overrightarrow{u} \cdot \overrightarrow{v} }{ { \lVert \overrightarrow{u} \rVert }^2 } \overrightarrow{u} \\)<br>