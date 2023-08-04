---
title: 제1절 - 1. 데이터 모델의 이해
author: wannastudyhardyeah
date: 2023-08-03 00:01:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---
<h2>1. 모델링의 정의</h2>
<b>다양한 정의</b><br>
&nbsp;\- 웹스터 사전<br>
&nbsp;&nbsp; • 가설적 또는 일정 양식에 맞춘 표현<br>
&nbsp;&nbsp; • 어떤 것에 대한 예비표현으로 그로부터 최종 대상이 구축되도록 하는 계획으로서 기여하는 것<br><br>
&nbsp;\- 복잡한 '현실세계'를 단순화해 표현하는 것.<br><br>
&nbsp;\- 모델이란 사물 또는 사건에 관한 양상<span style="color: #808080;">aspect</span>이나 관점<span style="color: #808080;">perspective</span>을 연관된 사람이나 그룹을 위하여 명확하게 하는 것.<br><br>
&nbsp;\- 모델이란 현실세계를 추상화한 반영<br><br>

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