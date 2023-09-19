---
title: 06 - 데이터 타입
author: wannastudyhardyeah
date: 2023-08-03 00:03:00 +0800
categories: [Javascript]
tags: [Javascript]

---
<h1>데이터 타입<span style="color: #808080;">data type</span></h1>
&nbsp;\: 값의 종류.<br>JS에서 모든 값은 데이터 타입을 가짐.<br>ES6 기준 7개의 데이터 타입 제공.<br>
<br>
<table bordercolor="black" align="left">
    <tr style="background: #ccffff" align="center">
        <td><b>구분</b></td>
        <td><b>데이터 타입</b></td>
        <td><b>설명</b></td>
    </tr>
    <tr>
        <td rowspan="6">원시 타입</td>
        <td>숫자<span style="color: #808080;">number</span> 타입</td>
        <td>숫자</td>
    </tr>
    <tr>
        <td>문자열<span style="color: #808080;">string</span> 타입</td>
        <td>문자열</td>
    </tr>
    <tr>
        <td>hihi</td>
        <td>hihihi</td>
    </tr>
    <tr>
        <td>hihi</td>
        <td>hihihi</td>
    </tr>
    <tr>
        <td>hihi</td>
        <td>hihihi</td>
    </tr>
    <tr>
        <td>hihi</td>
        <td>hihihi</td>
    </tr>
    <tr>
        <td colspan="2">객체 타입</td>
        <td>객체, 함수, 배열 등</td>
    </tr>    
</table>
<br>

<h2>1. 숫자 타입</h2>
JS에선 하나의 숫자 타입만 존재.<br>
숫자 타입의 값은 배정밀도 64비트 부동소수점 형식<span style="color: #808080;">double-precision 64-bit format</span>.<br>
즉, 모든 수를 실수로 처리.<br>
```js
var binary = 0b10010010;
var octal = 0o134;
var hex = 0x92;

console.log("10진수 92의");
console.log(" 2진수는 ", binary);
console.log(" 8진수는 ", octal);
console.log(" 16진수는 ", hex);
console.log("2진수와 8진수는 서로 같다? \n => ", binary === octal);
console.log("8진수와 16진수는 서로 같다? \n => ", octal === hex);
```
```
10진수 92의
declaring_values.js:5
 2진수는  146
declaring_values.js:6
 8진수는  92
declaring_values.js:7
 16진수는  146
declaring_values.js:8
2진수와 8진수는 서로 같다? 
 =>  false
declaring_values.js:9
8진수와 16진수는 서로 같다? 
 =>  false
```

모든 수를 실수로 처리하므로,<br>
정수로 표시되는 수끼리 나누어도 실수가 나올 수 있음.<br>
```js
console.log("1 and 1.0 is... same?\n => ", 1 === 1.0);
```

```
1 and 1.0 is... same?
 =>  true
```

<h2>2. 문자열 타입</h2>
0개 이상의 16비트 유니코드 문자(UTF-8)의 집합.<br>

문자열은 작은따옴표<span style="color: #808080;">single quote</span>(`` '' ``), 큰따옴표<span style="color: #808080;">double quotes</span>(`` "" ``), 백틱<span style="color: #808080;">backtick</span>(`` ` ` ``)으로 감싼다.<br>
(JS에선 작은따옴표가 일반적)<br>


<h2>3. 템플릿 리터럴<span style="color: #808080;">template literal</span></h2>
``ES6``부터 도입된 새로운 문자열 표기법.<br>
멀티라인 문자열<span style="color: #808080;">multi-line string</span>, 표현식 삽입<span style="color: #808080;">expression interpolation</span>, 태그드 템플릿<span style="color: #808080;">tagged template</span> 등의 문자열 처리 기능 제공.<br>
<br>
템플릿 리터럴은 백틱(`` ` ` ``)을 사용하여 표현.<br>

<h3>&nbsp;&nbsp;3.1. 멀티라인 문자열</h3>
★비교<br>
&nbsp;&nbsp;&nbsp;&nbsp;일반 문자열 내에선 <span style="color:red">개행 허용 X</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;대신에, <b>이스케이프 시퀀스</b><span style="color: #808080;">escape sequence</span> 사용해야 함.<br>
<span style="color: red;"><b>BUT</b></span>,<br>
&nbsp;&nbsp;&nbsp;&nbsp;템플릿 리터럴에선<br>
&nbsp;&nbsp;&nbsp;&nbsp;이스케이프 시퀀스 <b>없이도 줄바꿈 허용</b>, 모든 <b>공백도 그대로</b> 적용.<br>

<h3>3.2. 표현식 삽입</h3>
문자열은 문자열 연산자 ``+``로 연결 가능.<br>
(<b>피연산자 中 하나 이상이 문자열</b>이면 문자열 연결 연산자로 동작)<br>

```js
var first = 'Thurs';

var last = 'day';

console.log('Today is ' + first + last);
```
```
Today is Thursday
```

템플릿 리터럴에선 <b>표현식 삽입</b><span style="color: #808080;">expression interpolation</span>으로 간단히 문자열 삽입 가능.<br>
```js
var first = 'Thurs';
var last = 'day';

console.log(`Today is ${first}${last}`);
```
```
Today is Thursday
```
표현식 삽입하기 위해선 ``${ }``으로 해당 표현식을 감싸기.<br>
이때, 문자열이 아니더라도 문자열로 타입이 강제로 변환됨.<br>

<h2>4. 불리언 타입</h2>
``true``{: .js}, ``false``{: .js}<br>

<h2>5. <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">undefined</code> 타입</h2>
``undefined``{: .js}가 유일.<br>

``var`` 키워드로 선언한 변수는 암묵적으로 ``undefined``로 초기화됨.<br>즉, 변수 선언 이후에 값 할당하지 않은 변수 참조 시 ``undefined`` 반환됨.<br>

<span style="color: red;">★ <b>변수에 값 없다는 걸 명시할 때는?</b></span><br>
=> ``null`` 할당.<br>

<h2>6. null 타입</h2>

``null``이 유일<br>

<span style="color: red;">★ <b><code class="language-plaintext highlighter-rouge" style="font-size: 1rem; color: red !important;">null</code>, <code class="language-plaintext highlighter-rouge" style="font-size: 1rem; color: red !important;">Null</code>, <code class="language-plaintext highlighter-rouge" style="font-size: 1rem; color: red !important;">NULL</code></b></span><br>

JS에서는 대소문자 구별하므로 셋은 서로 다르다.<br>
``null``은 변수에 값 없다는 걸 의도적으로 명시(의도적 부재<span style="color: #808080;">intentional absence</span>)할 때 사용.<br>


<h2>7. 심벌 타입<span style="color: #808080;">symbol</span></h2>
``ES6``에서 추가된 7번째 타입.<br>
변경 불가능한 원시 타입의 값.<br>
<br>
심벌 값은 다른 값과 중복 않는 유일무이한 값이므로,<br>
주로 이름 충돌 위험이 없는 객체의 유일한 프로퍼티 키 만들기 위해 사용됨.<br>

<h2>8. 객체 타입</h2>
원시 타입과 객체 타입은 근본적으로 다르다.<br>
<br>

<h2>9. 데이터 타입의 필요성</h2>
데이터 타입은 값의 종류를 말함.<br>

<b>필요한 이유</b><br>
&nbsp;\- 값 저장할 때 확보해야 하는 <b>메모리 공간의 크기</b> 결정하기 위해<br>
&nbsp;\- 값 참조할 때 한 번에 읽어들어야 할 <b>메모리 공간의 크기</b> 결정하기 위해<br>
&nbsp;\- 메모리에서 읽어들인 <b>2진수를 어떻게 해석</b>할지 결정하기 위해<br>

<h2>10. 동적 타이핑</h2>
JS의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론<span style="color: #808080;">type inference</span>)됨.<br>
또한, 변수의 타입은 재할당에 의해 언제든지 동적으로 변할 수 있음.(동적 타이핑<span style="color: #808080;">dynamic typing</span>)<br>

동적 타입 언어<span style="color: #808080;">dynamic/weak type</span>인 JS에선<br>
어떤 데이터 타입의 값이라도 자유롭게 할당 가능.<br>
=> 유연성<span style="color: #808080;">flexibility</span>은 높지만, 신뢰성<span style="color: #808080;">reliability</span>은 떨어짐.<br>

<span style="color: red;"><b>★ 주의사항</b></span><br>
&nbsp;\- 변수는 꼭 필요한 경우에 한해 제한적 사용하기.<br>
&nbsp;&nbsp;&nbsp;&nbsp;필요한 만큼 최소한으로 유지하기.<br>

&nbsp;\- 변수의 유효 범위(스코프)는 최대한 좁게 만들기.(=> 부작용 억제)<br>

&nbsp;\- 전역 변수는 최대한 사용하지 않기<br>

&nbsp;\- 변수보다는 상수 사용하여 값 변경 억제하기<br>

&nbsp;\- 변수 이름은 변수 목적이나 의미 파악 가능하도록 네이밍하기. 식별자도 마찬가지.<br>