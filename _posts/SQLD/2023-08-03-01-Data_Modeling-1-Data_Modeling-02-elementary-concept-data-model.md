---
title: 제1장 - 제2절&#58; 데이터 모델의 기본 개념 이해
author: wannastudyhardyeah
date: 2023-08-03 00:02:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---
<h2>1. 데이터 모델링의 정의</h2>
<b>다양한 정의</b><br>
&nbsp;\- 정보시스템을 구축하기 위해,<br>
&nbsp;&nbsp;&nbsp;&nbsp;해당 업무에 어떤 데이터가 존재하는지 OR 업무가 필요로 하는 정보는 무엇인지를 분석하는 방법<br><br>
&nbsp;\- 기업 업무에 대한 종합적 이해를 바탕으로 데이터에 존재하는 업무 규칙<span style="color: #808080;">Business Rule</span>에 대하여<br>
&nbsp;&nbsp;&nbsp;&nbsp;참<span style="color: #808080;">True</span> 또는 거짓<span style="color: #808080;"></span>을 판별할 수 있는 사실(사실명제)을 데이터에 접근하는 방법(How), 사람(Who), 전산화와 별개의(독립적) 관점에서 이를 명확하게 표현하는 추상화 기법<br><br>

<b>실무적으로</b><br>
업무에서 필요로 하는 데이터를 시스템 구축 방법론에 따라 분석하고 설계하여 정보시스템을 구축하는 과정.<br>
<br>
<b>목적</b><br>
&nbsp;\- 업무 정보 구성하는 기초가 되는 정보들을 일정한 표기법에 따라 표현함으로써, 정보시스템 구축 대상이 되는 업무 내용을 정확하게 분석하는 것<br>
&nbsp;\- 분석한 모델을 가지고 실제 데이터베이스를 생성하여 개발 및 데이터 관리에 사용하기 위함<br>

<h2>2. 모델링의 특징</h2>
&nbsp;\- <b>추상화</b>(모형화, 가설적)<br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 현실세계를 일정한 형식에 맞추어 표현.<br>
&nbsp;&nbsp;&nbsp;&nbsp;다양한 현상을 일정한 양식인 표기법에 따라 표현.<br><br>
&nbsp;\- <b>단순화</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 복잡한 현실세계를 약속된 규약에 의해 제한된 표기법이나 언어로 표현하여 쉽게 이해할 수 있도록 하는 개념<br><br>
&nbsp;\- <b>명확화</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 누구나 이해하기 쉽게 하기 위해 대상에 대한 애매모호함을 제거하고 정확하게 현상을 기술하는 것.<br><br>

<h2>3. 모델링의 세 가지 관점</h2>
<i>'시스템의 대상이 되는 업무 분석하여 정보시스템으로 구성 과정에서<br>
업무 내용과 정보시스템의 모습을 적절한 표기법으로 표현하는 것'</i>&nbsp;을 <b>모델링</b>이라고 한다면,<br>
모델링을 크게 아래 세 가지 관점으로 구분 가능<br><br>
&nbsp;\- <b>데이터 관점</b> <br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 업무가 어떤 데이터와 관련이 있는지 OR 데이터 간의 관계는 무엇인지에 대해 모델링하는 방법<br>(What, Data)<br><br>
&nbsp;\- <b>프로세스 관점</b> <br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 실제로 하는 업무는 무엇인지 OR 무엇을 해야 하는지를 모델링하는 방법<br>(How, Process)<br><br>
&nbsp;\- <b>데이터와 프로세스의 상관 관점</b> <br>
&nbsp;&nbsp;&nbsp;&nbsp;\: 업무가 처리하는 일의 방법에 따라 데이터는 어떻게 영향 받고 있는지를 모델링하는 방법<br>(Interaction)<br><br>