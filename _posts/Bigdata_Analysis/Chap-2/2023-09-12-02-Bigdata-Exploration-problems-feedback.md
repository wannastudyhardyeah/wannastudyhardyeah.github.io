---
title: 과목 2 - 빅데이터 탐색 문제 피드백 정리
author: wannastudyhardyeah
date: 2023-09-11 23:00:20 +0800
categories: [Bigdata_cert]
tags: [Bigdata, Bigdata_cert]
math: true

---
<h2 id="data-cleansing-1"><b>1. 데이터 정제<span style="color: #808080;">Data Cleansing</span> 관한 설명</b></h2>
    
<h3 id="reason-for-wrong-1st-1-h3">&nbsp;①번 틀린 이유</h3>
노이즈와 이상값은 정형 데이터보다는<br>
반정형, 비정형 데이터에서 더 많이 발생함.<br>

<h3 id="reason-for-wrong-2nd-1-h3">&nbsp;②번 틀린 이유</h3>
데이터 정제 과정은<br>
데이터 분석 과정에서 반드시 수행!!<br>

<h3 id="reason-for-wrong-4th-1-h3">&nbsp;④번 틀린 이유</h3>
모든 데이터를 대상으로 정제 활동 해야함!<br>

<br>
<hr width="50%">
<h2 id="outlier-2"><b>2. 이상값<span style="color: #808080;">Outlier</span> 관한 설명</b></h2>
<h3 id="reason-for-wrong-1st-2-h3">&nbsp;①번 틀린 이유</h3>
이상값의 발생 원인 중 하나에는<br>
데이터 분석 및 처리 과정에서 발생하는 것이다.<br>

<br>
<hr width="50%">
<h2 id="representative-value-3"><b>3. 대푯값 관한 설명, 특징</b></h2>
<h3 id="reason-for-wrong-1st-3-h3">&nbsp;①번 틀린 이유</h3>
중앙값은 이상값에 민감하지 않음!<br>
(이상값 영향 적게 받음.)<br>

<h3 id="outlier-category-3-h3">&nbsp;관련 개념 - 이상값 영향 기준</h3>

<h4 id="big-3-h4">&nbsp;&nbsp;영향 많이 받는 것</h4>
- 평균<span style="color: #808080;">Mean</span>, 분산, 표준편차, 범위
- 앙상블 中 부스팅<span style="color: #808080;">Boosting</span>
- (비지도 & 군집 & 비계층적) k-Means

<h4 id="small-3-h4">&nbsp;&nbsp;영향 적게 받는 것</h4>
- 중앙값<span style="color: #808080;">Median</span>
- (지도 & 분류/회귀) kNN
- (비지도 & 군집 & 비계층적) DBSCAN

<br>
<hr width="50%">
<h2 id="outlier-5"><b>5. 이상치 정의</b></h2>
통계적 자료 분석의 결과 왜곡시키거나<br>
자료 분석의 적절성 해치며<br>
분포의 집중경향치를 왜곡시키는 변숫값.<br>

<br>
<hr width="50%">
<h2 id="methods-find-outlier-6"><b>6. 이상치 판별 방법</b></h2>

<h3 id="esd-6-h3">&nbsp;ESD</h3>
<b>Extreme Studentized Deviation</b><br>

$$ \mu - 3\delta <$$ 정상데이터 $$< \mu + 3\delta$$<br>
즉, 평균에서 3*(표준편차)를 벗어나면<br>
&nbsp;&nbsp;--> 이상치로 판단

<h3 id="iqr-6-h3">&nbsp;사분위수</h3>
$$ \text{IQR} = Q_3 - Q_1 $$<br>
( 즉, $$\text{IQR}$$은 데이터의 가운데 50% 의미 )<br>
&nbsp;==> $$Q_1 - 1.5 \times \text{IQR} <$$ 정상데이터 $$< Q_3 + 1.5 \times \text{IQR}$$<br>

<h3 id="visualization-6-h3">&nbsp;데이터 시각화</h3>
- 히스토그램<span style="color: #808080;">Histogram</span>
- 밀도차트<span style="color: #808080;">Density Chart</span>
- 상자그림<span style="color: #808080;">BoxPlot</span>
&nbsp;&nbsp;\: 수염 밖으로 이상값이 표시됨.
- 잔차도<span style="color: #808080;">Residuals</span>

<br>
<hr width="50%">
<h2 id="method-features-11"><b>11. 변수 선택 기법</b></h2>

<h3 id="filter-11-h3">필터<span style="color: #808080;">Filter</span> 기법</h3>
- 래퍼 기법 사용 전 전처리로 사용
- 통계적 측정 방법 사용
- 정보 소득, $\chi^2$ 검정, 피셔 스코어, 상관계수

<h3 id="wrapper-11-h3">래퍼<span style="color: #808080;">Wrapper</span>기법</h3>
- 변수의 일부로 모델링 한 뒤,<br>
그 결과 확인 작업 반복하여<br>
가장 성능 좋은 변수 조합 찾음.<br>

- 전진 선택법 / 후진 제거법 / 단계적 선택법<br>

- 필터 방법보다 예측 정확도 높음.<br>

<h3 id="embedded-11-h3">임베디드<span style="color: #808080;">Embedded</span>기법</h3>
- 모델 자체에 포함된 변수 선택 기법
- 모델의 학습, 생성 과정에서 최적 변수 선택
- 릿지<span style="color: #808080;">Ridge</span>, 라쏘<span style="color: #808080;">Lasso</span>, 엘라스틱넷<span style="color: #808080;">ElasticNet</span>,<br>
의사결정나무<br>

<br>
<hr width="50%">
<h2 id="backward-12"><b>12. 독립변수 선택 기법</b></h2>
(Wrapper 기법 中)<br>
<br>
<b style="font-size:1.25rem">기준</b><br>
AIC, BIC의 기준으로 가장 적합한 회귀 모형 선택<br>
&nbsp;==> $R^2$와 비슷한 역할 but $R^2$은 클수록 좋으나<br>
&nbsp;&nbsp;AIC, BIC는 작은 값이 좋음.<br>

- 전진선택법<span style="color: #808080;">Forward Selection</span>
절편만 있는 모델에서 출발.<br>
기준 통계치 가장 많이 개선하는 변수를 차례로 추가.<br>

- 후진제거법<span style="color: #808080;">Backward Elimination</span>
모든 독립변수 포함한 모형에서 출발.<br>
제곱합 기준으로 가장 적은 영향 주는 변수를 하나씩 제거.<br>

- 단계별 선택법<span style="color: #808080;">Stepwise Method</span>
모든 독립변수 포함한 모델에서 출발.<br>
기준 통계치에 가장 도움 안 되는 변수 삭제<br>
&nbsp;&nbsp;또는<br>
모델에서 빠져있는 변수 중 기준 통계치 가장 개선하는 변수 추가<br>

<br>
<hr width="50%">
<h2 id="Dimension-curse"><b>13. 차원의 저주</b></h2>
- 차원 증가하면서<br>
개별 차원 내의 학습 데이터 수가 차원 수보다 적어지면서<br>
성능이 저하되는 현상.<br>

- 데이터 차원 증가할수록<br>
데이터 표현가능 공간은 기하급수적 증가<br>
But, 데이터 수는 변하지 않기 때문에 발생.<br>

- 모델링 과정에서<br>
저장공간과 처리시간 불필요하게 증가<br>
&nbsp;==> 성능 저하<br>

- 표본 수 적을 때 더욱 심화됨<br>

<br>
<hr width="50%">
<h2 id="object-and-charact-of-dimesion-reduct-11"><b>14. 차원 축소의 목적과 특징</b></h2>

&nbsp;&nbsp;변수의 정보를 최대한 유지하면서<br>
변수 개수를 줄이는 통계 기법.<br>

&nbsp;&nbsp;차원의 축소 and 다중 공선성과 관련.<br>

<b>목적</b><br>
데이터 분석의 효율성 측면에서<br>
복잡도 축소, 과적합 방지, 해석력 확보<br>

<b>기법</b><br>
- 주성분 분석<br>
- 요인 분석<br>
- 특이값 분해<br>
- 다차원 척도법<br>

<br>
<hr width="50%">
<h2 id="multicollinearity"><b>15. 다중공선성</b></h2>
- 모형의 일부가<br>
다른 설명변수와 높은 상관관계 있을 때 발생<br>

- 다중공선성 클수록<br>
회귀계수의 분산 증가<br>
&nbsp;<b>==></b> 모델 불안정, 해석 어렵게 함.<br>

- VIF 값이 10 넘으면<br>
&nbsp;<b>==></b> 다중공선성 존재로 간주.<br>


<b style="font-size:1.25rem">대책</b><br>
- 높은 상관관계 있는 설명변수를 모형에서 제거<br>
- 다양한 변수 선택, 차원 축소 방법<br>
- 설명변수 제거 시 $R^2$가 감소<br>

<b style="font-size:1.25rem">방법</b><br>
- 변수축소<br>
&nbsp;\: 주성분 분석, 요인분석, 다차원 척도법 등의 변수축소<br>
- 변수제거<br>
&nbsp;\: 상관관계 분석 후<br>
&nbsp;&nbsp; 높은 상관계수 갖는 독립변수 중 일부를 제거<br>
- 릿지<span style="color: #808080;">Ridge</span>, 라쏘<span style="color: #808080;">Lasso</span>, 엘라스틱넷<span style="color: #808080;">ElasticNet</span> 회귀분석<br>
(과대적합 해결)<br>

- Mean Centering<br>
&nbsp;\: 모든 변수를 각 변수의 평균값으로 뺀 후 회귀분석.<br>

<br>
<hr width="50%">
<h2 id="object-and-charact-of-dimesion-reduct-11"><b>14. 차원 축소의 목적과 특징</b></h2>