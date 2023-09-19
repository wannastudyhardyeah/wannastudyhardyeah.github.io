---
title: 07 - 연산자
author: wannastudyhardyeah
date: 2023-08-03 00:04:00 +0800
categories: [Javascript]
tags: [Javascript]

---
<h1>연산자<span style="color: #808080;">operator</span></h1>
하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다.<br>
이때 연산의 대상을 <b>피연산자</b><span style="color: #808080;">operand</span>라고 함.

<h2>1. 산술<span style="color: #808080;">arithmetic</span> 연산자</h2>
<h3>&nbsp;&nbsp;1.1. 이항<span style="color: #808080;">binary</span> 산술 연산자</h3>
<h3>&nbsp;&nbsp;1.2. 단항<span style="color: #808080;">unary</span> 산술 연산자</h3>
<h3>&nbsp;&nbsp;1.3. 문자열 연결 연산자</h3>
```js
console.log(1 + true);
console.log(1 + null);
console.log(+undefined);
```
```
2
1
NaN
```
이러한 걸 <b>암묵적 타입 변환</b><span style="color: #808080;">implicit coercion</span>/<b>타입 강제 변환</b><span style="color: #808080;">type coercion</span>이라 함.<br>
<br>
<h2>2. 할당 연산자</h2>
할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가됨.<br>

<b>연쇄 할당 가능</b>

```js
var a, b, c;

a = b = c = 0;

console.log(a, ,b, c);
```
```
0 0 0 
```
<br>
<h2>3. 비교<span style="color: #808080;">comparison</span> 연산자</h2>
<h3>&nbsp;&nbsp;3.1. 동등<span style="color: #808080;">loose equality</span>/일치<span style="color: #808080;">strict equality</span> 비교 연산자<br></h3>
이 둘은 비교하는 엄격성의 정도가 다름.<br>
<table bordercolor="black" align="left">
    <tr style="background: #ccffff" align="center">
        <td><b>비교<br> 연산자</b></td>
        <td><b>의미</b></td>
        <td><b>사례</b></td>
        <td><b>설명</b></td>
        <td><b>부수 효과</b></td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">==</code></td>
        <td>동등 비교</td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x == y</code></td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x</code>와 <code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">y</code>의<br> 값이 같음</td>
        <td align="center">X</td>    
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">===</code></td>
        <td>일치 비교</td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x === y</code></td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x</code>와 <code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">y</code>의<br> 값과 타입이 같음</td>
        <td align="center">X</td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">!=</code></td>
        <td>부동등 비교</td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x != y</code></td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x</code>와 <code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">y</code>의<br> 값이 다름</td>
        <td align="center">X</td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">!==</code></td>
        <td>불일치 비교</td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x !== y</code></td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">x</code>와 <code class="language-plaintext highlighter-rouge" style="font-size: 1rem;">y</code>의<br> 값과 타입이 다름</td>
        <td align="center">X</td>
    </tr>
</table>

<b>동등 비교 연산자</b><br>
\: 좌항과 우항의 피연산자 비교 시,<br>
&nbsp;먼저 암묵적 타입 변환 통해 타입 일치시킨 후 같은 값인지 비교<br>

<b>일치 비교 연산자</b><br>
\: 좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한하여<br>
&nbsp;``true``를 반환.<br>
<br>

<span style="color: red;"><b>★ 주의 사항</b></span><br>

```js
NaN === NaN;
```
```powershell
false
```
``NaN``은 자신과 일치하지 않는 유일한 값.<br>

<h3>&nbsp;&nbsp;3.2. 대소 관계 비교 연산자</h3>
<br>
<h2>4. 삼항<span style="color: #808080;">termary</span> 조건 연산자</h2>
조건식의 평가 결과에 따라 반환할 값 결정.
```js
var result = score >= 60 ? 'pass' : 'fail';
```
<br>
<h2>5. 논리<span style="color: #808080;">logical</span> 연산자</h2>

<br>

<h2>6. 쉼표 연산자</h2>

<br>

<h2>7. 그룹 연산자</h2>
<b>연산자 우선순위</b>가 가장 높다!<br>

<br>

<h2>8. <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">typeof</code> 연산자</h2>
"``string``", "``number``", "``boolean``", "``undefined``", "``symbol``", "``object``", "``function``"<br>
中 하나를 반환.<br>
"``null``" 반환하는 경우 없음.<br>
함수는 "``function``" 반환.<br>

<b>미수정 버그인 부분</b><br>
``typeof``로 ``null`` 연산하면 ``object`` 반환함.<br>

<span style="color: red;"><b>★주의</b></span><br>
선언하지 않은 식별자를 ``typeof``로 연산하면 ``undefined`` 반환함.<br>

<br>

<h2>9. 지수 연산자</h2>
좌항 => 밑<span style="color: #808080;">base</span><br>
우항 => 지수<span style="color: #808080;">exponent</span><br>

<br>

<h2>10. 그 외 연산자</h2>
<table bordercolor="black" align="left">
    <tr style="background: #ccffff" align="center">
        <td><b>연산자</b></td>
        <td><b>개요</b></td>
        <td><b>참고</b></td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">?.</code></td>
        <td>옵셔널 체이닝 연산자</td>
        <td> </td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">??</code></td>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">null</code> 병합 연산자</td>
        <td> </td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">delete</code></td>
        <td>프로퍼티 삭제</td>
        <td> </td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">new</code></td>
        <td>생성자 함수 호출 시<br>사용하여 인스턴스 생성</td>
        <td> </td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">instanceof</code></td>
        <td>좌변 객체가<br>우변 생성자 함수와<br> 연결된 인스턴스인지 판별</td>
        <td> </td>
    </tr>
    <tr>
        <td><code class="language-plaintext highlighter-rouge" style="font-size: 1.0rem;">in</code></td>
        <td>프로퍼티 존재 확인</td>
        <td> </td>
    </tr>    
</table>

<br>

<h2>11. 연산자의 부수 효과</h2>
<b>부수 효과가 있는 연산자</b><br>
할당 연산자(``=``), 증가/감소 연산자(``++``/``--``), ``delete`` 연산자.<br>

<br>

<h2>12. 연산자 우선순위</h2>

<br>

<h2>13. 연산자 결합 순서</h2>