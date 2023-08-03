---
title: 3.2. 행렬 대수
author: wannastudyhardyeah
date: 2023-06-10 01:06:00 +0800
categories: [Linear Algebra]
tags: [Linear Algebra, Mathematics]
math: true

---
<h2 style="position: relative; display: inline-block; text-align: center; padding: 5px; height: 100%; border: 1px dotted black;">행렬과 사다리꼴</h2>
<b><span style="font-size: 1.34rem;">Def.</span></b><br>
- 계수행렬
    : 연립일차방정식의 미지수들의 계수로 이뤄진 행렬
- 첨가계수행렬
    : 상수항을 계수행렬에 첨가한 행렬
<br>
    
    ex)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  $$
    \begin{align*}
    \begin{cases} \phantom{-}2x+\phantom{0}y -\phantom{0}z &= 3 \\ \phantom{-0}x \phantom{-0y} \phantom{0}+ 5z &= 1 \\ \phantom{}-x +3y -2z &= 0 \\ \end{cases} 
    \end{align*}
$$ &nbsp; 의 <br><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;계수행렬: $ \begin{bmatrix} \phantom{-}2 & \phantom{-}1 & -1 \\\ \phantom{-}1 & \phantom{-}0 & \phantom{-}5 \\\ -1 & \phantom{-}3 & -2 \end{bmatrix} $<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;$( = A )$<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;첨가계수행렬: 
$ \left[ \begin{array}{cc|c} \phantom{-}2 & \phantom{-}1 & -1 \\\ \phantom{-}1 & \phantom{-}0 & \phantom{-}5 \\\ -1 & \phantom{-}3 & -2 \end{array} \right] $<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;$( = \left[ \ A | \overrightarrow{b} \ \right] )$<br>

<b><span style="font-size: 1.34rem;">Def.</span></b><br>
다음 성질을 만족하는 행렬을 <b>행사다리꼴</b>이라 한다.<br>
1. 모든 성분이 $ 0 $인 항은 아래 쪽에 있다.<br>
2. 적어도 한 성분이 $ 0 $인 행에서,<br>
    처음으로 $ 0 $이 아닌 성분,<br>
    즉, 선행선분<span style="color: #808080;">leading entry</span>은 아래 행에 있는 선행선분의 왼쪽 열에 위치한다.<br>

일차방정식<span style="color: #808080;">linear equation</span>이라 한다.<br>
여기서 계수 &nbsp; \\( a_1, \ ..., \ a_n \\)과 상수항 \\( b \\)는 상수이다.<br>
일차방정식의 해<span style="color: #808080;">solution</span>는 \\( x_1 = s_1, \ ..., \ x_n = s_n \\)을 대입할 때<br>
방정식을 만족하는 벡터 &nbsp; \\( \left[ s_1 , \ ..., \ s_n \right] \\)이다.<br><br>

<b><span style="font-size: 1.34rem;">연립일차방정식의 해법</span></b><br>
- 두 연립일차방정식이 같은 해집합을 가질 때<br>
동치<span style="color: #808080;">equivalent</span>라고 한다.<br>
    ex) 

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  $$
    \begin{align*}
    \begin{cases} x-y &= 1 \\ x+y &= 3 \end{cases} 
    \end{align*}
$$
<br><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; $$
    \begin{align*}
    \begin{cases} x-y &= 1 \\ y &= 1 \end{cases} 
    \end{align*}
$$
<br><br>
$ \quad \quad \Rightarrow $ 해: $ \left[ 2, \ 1 \right] $

- 주어진 연립방정식을<br>
풀기 쉬운 동치인 연립방정식으로 바꿔서 해를 구한다.<br>
    ex)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; $$
    \begin{align*}
    \begin{cases} x-y - \ \ z &= 2 \\ \ \ \ \ \ \ \ y + 3z &= 5 \\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ 5z &= 10 \end{cases} 
    \end{align*}
$$
<br>
&nbsp; &nbsp; &nbsp; &nbsp; (후진 대입법 이용)
<br>
$ \quad \quad \Rightarrow $
$$ 
    \begin{align*} 
    z &= 2, \\ y &= 5 - 3 \times 2 = -1, \\ x &= 2 + (-1) + 2 = 3 \\
    \end{align*} 
$$
<br>
&nbsp; &nbsp; &nbsp; &nbsp; $ \therefore \ \ $ 해: $ \left[ 3, \ -1, \ 2 \right] $
