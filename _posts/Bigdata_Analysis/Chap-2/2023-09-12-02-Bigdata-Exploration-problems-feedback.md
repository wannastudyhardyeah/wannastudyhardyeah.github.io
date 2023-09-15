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
<h2 id="pca-16"><b>16. 주성분 분석</b></h2>
<b>차원 축소 기법 중 하나</b><br>

- 여러 차원의 변수를 대표하는<br>
새로운 차원의 주성분을 생성하여<br>
전체 변동의 대부분을 설명하는 게 목적.<br>

- 주성분은 <b>변수들의 선형결합</b>.<br>

- 변수들의 공분산 행렬 or 상관행렬 사용<br>
(이때 행렬은 정방행렬만!)<br>
    - 공분산 행렬<br>
    \: 측정단위 그대로 반영함<br>
    &nbsp;변수들 측정 단위에 민감함.<br>
    &nbsp;=> 단위가 같은 수준일 때 사용<br>
    $-\infty$부터 $\infty$사이의 값.<br>
    - 상관 행렬<br>
    \: 모든 변수의 측정단위를 표준화함.<br>
    &nbsp;변수 단위가 서로 많이 다를 때.<br>
    $-1$부터 $1$ 사이의 값.<br>

- 주성분 결정 기준
    - 분산의 비율<br>
    \: 누적분산 비율이 70~90% 사이가 되는<br>
    &nbsp;주성분 개수 선택.<br>
    - 고윳값<span style="color: #808080;">Eigenvalue</span><br>
    \: 분산의 크기 나타냄.<br>
    &nbsp;고윳값이 1보다 큰 주성분만 사용.<br>
    - Scree Plot<br>
    \: 고윳값을 내림차순으로 보여줌.<br>

<br>
<hr width="50%">
<h2 id="factor-analysis-18"><b>18. 요인 분석</b></h2>

<h3 id="types-of-factor-h3">변수의 구성</h3>
- 공통요인<br>
\: 변수와 다른 변수가 공유하고 있는 것.<br>
- 고유요인<br>
\: 그 변수만이 가지고 있는 것.<br>

<h3 id="suppose-18-h3">가정</h3>
&nbsp;&nbsp;데이터 내부에 관찰할 수 없는<br>
잠재적 요인(변수) 가정<br>

- 모형 세운 뒤,<br>
관찰 가능 데이터 이용하여<br>
해당 잠재 요인 도출, 데이터 안의 구조 해석<br>

- 독립변수, 종속변수 구분 X<br>
주로 기술통계 방법 사용<br>

- 유사한 변수끼리 묶음.<br>

<br>
<hr width="50%">
<h2 id="mds-19"><b>19. 다차원 척도법</b></h2>

- 객체 사이의 근접성 시각화 기법.<br>

- 개체들 사이의 유사성, 비유사성을<br>
2차원 or 3차원 공간산에 점으로 표현<br>
<b>==></b> 개체 사이 군집 시각적 표현.<br>

- 개체들의 거리<br>
\: 유클리드 거리 & 유사도<br>

- 적합 정도를<br>
스트레스 값<span style="color: #808080;">Stress Value</span>으로 나타냄.<br>
<b>==></b> 관측 대상의 상대적 거리의 정확도 높임.<br>
&nbsp;&nbsp;$0$에 가까울수록 적합도 좋음.<br>

<br>
<hr width="50%">
<h2 id="derived-variables-21"><b>21. 파생 변수</b></h2>
- 상관관계 있는 변수들끼리 결합하여<br>
분산을 극대화하는 변수로 만들어<br>
변수 축약하여 희생되는 정보 최소화 함.<br>

- 생성 방법
    - 단위 변환
    - 요약 통계량 변환
    - 변수 분해
    - 변수 결합

<br>
<hr width="50%">
<h2 id="transform-22-and-24"><b>22 ~ 27. 변수 변환</b></h2>

<h3 id="scailing-h3">스케일링</h3>

<h4 id="min-max-normal-h4" data-heading-label="- Min-Max Normalization">&nbsp;&nbsp;- Min-Max Normalization</h4>

&nbsp;&nbsp;데이터를 특정 구간($0$ ~ $1$ 범위)으로 바꿈.<br>

$X' = \dfrac{X - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}}$

<h4 id="z-score-h4" data-heading-label="- Z-Score(표준화)">&nbsp;&nbsp;- Z-Score(표준화)</h4>
&nbsp;&nbsp;데이터를 평균 $0$, 표준편차 $1$의<br>
표준정규분포로 변환.<br>
$Z = \dfrac{X - \mu}{\sigma}$

<h4 id="robust-scaler-h4" data-heading-label="- Robust Scaler">&nbsp;&nbsp;- Robust Scaler</h4>
&nbsp;&nbsp;중앙값과 IQR 사용.<br>
&nbsp;&nbsp;이상값의 영향이 최소화 됨.<br>

<h4 id="max-absolute-scaler-h4" data-heading-label="- Max Absolute Scaler">&nbsp;&nbsp;- Max Absolute Scaler</h4>
&nbsp;&nbsp;최대 절댓값이 $1$, $0$은 $0$이 되도록 스케일링<br>

<h3 id="simple-trans-h3">단순 함수 변환</h3>
&nbsp;&nbsp;한쪽으로 치우쳐진 분포를<br>
분석 모형에 적합하게 변형<br>
(즉, 비선형 <b>--></b> 선형)<br>

- 오른쪽 꼬리 길 때<br>
=> 로그, 제곱근, 역수<br>

- 왼쪽 꼬리 길 때<br>
=> 제곱, 지수 변환<br>

<h3 id="box-cox-trans-h3">Box Cox 변환</h3>

- 상대적 특성 반영된 데이터로 변환.<br>
(데이터가 가진 스케일이 크게 차이 날 때 사용)<br>

- 정규성 만족 X인 데이터에 대해,<br>
데이터를 정규분포 가깝게 만들거나<br>
데이터 분산을 안정화 하는 것.<br>

- 데이터 전처리 기법임.<br>
(정규성 가정하는 분석법 사용 전 활용)<br>

<br>
<hr width="50%">
<h2 id="imbalanced-data-28"><b>28 ~ 30. 불균형 데이터 처리</b></h2>

<h3 id="imbalanced-data-28-h3">불균형 데이터</h3>

- 분포가 더 높은 클래스 예측하려 함<br>
<b>==></b> 정확도는 높아짐<br>
&nbsp;&nbsp;&nbsp;But, 분포 낮은 클래스의 재현율(Recall) 낮아짐.<br>

- 불균형 상태 그대로 예측하면<br>
과적합 문제 발생 가능<br>
<b>==></b> 테스트 데이터에선 예측 성능 낮게 나올 가능성<br>

<h3 id="overfitting-h3">과대적합</h3>
&nbsp;&nbsp;주어진 표본의 설명변수와 종속변수의 관계를<br>
필요이상으로 너무 자세하고 복잡하게 분석함<br>

<b>해결방법</b><br>
- 변수(Feature) 개수 줄이기
- 규제<span style="color: #808080;">Regularization</span>
- 드랍아웃<span style="color: #808080;">Dropout</span>

<h3 id="address-imbalanced-data-h3">불균형 데이터 처리 방법</h3>
- 전처리 단계
    - <b>언더 샘플링</b><br>
    \: 다수 클래스의 데이터를 샘플링해 사용<br>
    &nbsp;데이터 손실 매우 큼.<br>
    중요한 정상적 데이터 읽을 가능성.<br>
    - <b>오버 샘플링</b><br>
    \: 소수 클래스의 데이터 샘플링해 사용<br>
    정보 손실 없음.<br>
    새로운 테스터 데이터 추가되면 모델 결과 나빠짐.<br>
    과대적합 가능성.<br>
- 학습 단계
    - <b>앙상블</b>
    - <b>Weight Balancing</b>
- 평가 단계
    - <b>임계값 이동</b><span style="color: #808080;">Threshold-moving</span>

<br>
<hr width="50%">
<h2 id="eda-31-h2"><b>31 ~ 32. 탐색적 데이터 분석</b></h2>

- 데이터 통계량과 분포 등을 통해<br>
데이터 형태 확인하고,<br>
데이터 이해하며 의미 있는 관계 찾아내는 과정.<br>

- 분석 이전에<br>
그래프나 통계적 방법으로<br>
자료를 직관적으로 바라보는 과정.<br>

- 수집한 데이터를<br>
다양한 관점에서 관찰, 이해하는 과정.<br>

<b style="font-size:1.2rem">4가지 특징</b><br>
- 저항성<br>
- 잔차 해석<br>
- 자료 재표현<br>
- 현시성<br>

<br>
<hr width="50%">
<h2 id="correlation-analysis-33-h2"><b>33 ~ 35. 상관 관계 분석</b></h2>

- 두 개 이상 변수 사이에 존재하는<br>
상호 연관성 여부 및 강도 측정<br>

- 선형적으로 관련된 정도<br>

- 상관관계 있다고 해서<br>
인과관계 있는 건 아님.<br>

<h3 id="classes-33-h3">종류</h3>

- 변수 개수
    - 단순 상관 분석
    - 다중/다변량 상관 분석
- 변수 속성
    - 범주형->명목<br>
    \: 데이터 순서 의미 X.<br>
    변수 연산 불가능.<br>
    $\chi^2$ 검정(교차분석)<br>
    - 범주형->순서<br>
    \: 데이터 순서에 의미 O.<br>
    변수 연산 불가능.<br>
    스피어만 순위 상관계수<br>
    - 수치<br>
    \: 변수 연산 가능<br>
    피어슨 상관계수<br>

<h3 id="classes-33-h3">상관계수</h3>

- 피어슨 상관계수
    - $x$, $y$의 공분산을<br>
    $x$, $y$의 표준편차의 곱으로 나눈 값<br>
    즉, $corr(x, y) = \dfrac{cov(x, y)}{\sigma_x \sigma_y}$<br>
    - 대상자료<br>
    \: 등간척도, 비율척도<br>
    &nbsp;두 변수 사이의 선형적 크기만 측정가능<br>

- 스피어만 상관계수
    - 두 데이터의 실제 값 대신에<br>
    <b style="color:red">두 값의 순위에 기반</b>함.<br>
    - 완전 일치 => $1$ / 완전 반대 => $-1$<br>
    - 대상자료<br>
    \: 서열척도<br>
    &nbsp;두 변수 사이의 비선형적 관계 나타내기 가능.<br>

- 공분산<span style="color: #808080;">Covariance</span>
    - 2개 확률변수의 선형 관계 나타내는 값<br>
    - $cov(x, y) = \dfrac{\sum^n_{i=1} (x-\bar{x})(y-\bar{y})}{n-1}$
    - $0$인 경우, 선형 관계 없음 나타냄.
    - 측정 단위에 대한 표준화 <b style="color:red">안 돼있음</b>.<br>
    &nbsp;&nbsp;&nbsp;&nbsp;==> 선형관계 강도 나타내지 못함.<br>
    - $x$, $y$가 독립 $\longrightarrow$ 공분산 $cov(x, y) = 0$<br>
    <b>But</b>, 그 반대는 성립 X.<br>

<br>
<hr width="50%">
<h2 id="visualization-36-h2"><b>36 ~ 48. 시각적 데이터 탐색</b></h2>

<h3 id="types-of-visualiz-36-h3">종류</h3>

- 범주형<br>
\: Bar 차트, Pie 차트<br>
- 수치형<br>
\: 히스토그램, Boxplot<br>
- 범주형-범주형<br>
\: Bar 차트, Heatmap<br>
- 범주형-수치형<br>
\: Boxplot<br>
&nbsp;(범주를 그룹으로 사용)<br>
- 수치형-수치형<br>
\: Scatter plot, Scatter matrix plot<br>

<h3 id="progress-of-visualiz-36-h3">시각화 과정</h3>

1. <b>정보 구조화</b>
    - 유사 데이터 묶거나<br>
    재배열, 정리 및 변환<br>
    ==> 데이터 패턴 찾거나 추출<br>
    - 수집 및 탐색 -> 분류 -> 배열 -> 재배치<br>

2. <b>정보 시각화</b>
    - 시각화 도구 사용해<br>
    그래프 만들어 효과적 정보 표현<br>
    - 시간, 관계, 비교, 공간, 분포<br>

3. <b>정보 시각표현</b>
    - 시각화 완성단계,<br>
    그래픽 요소 활용해 완성<br>
    - 인포그래픽<br>
    \: 복잡한 대규모 빅데이터 분석결과를<br>
    명료하고 이해 쉽게 표현<br>

<h3 id="classes-36-h3">시각화 분류</h3>

- <b>시간 시각화</b><br>
\: 시간 흐름 따른 변화 표현<br>
    - 선/막대/계단식 그래프
    - 영역 차트
    - 산점도

- <b>공간 시각화</b><br>
\: 지도 활용해 데이터 표현<br>
   - 코로프레스 맵
   - 카토그램
   - 버블 플롯 맵
   - 등치선도
   - 등치지역도

- <b>관계 시각화</b><br>
\: 다변량 데이터에 대해<br>
변수 간의 연관성 및 패턴을<br>
색상, 농도 등 사용해 표현, 분석<br>
    - 산점도
    - 산점도 행렬
    - 버블차트
    - 히트맵

- <b>비교 시각화</b><br>
\: 다변량 데이터 대해<br>
유사 및 차이에 대하여<br>
점, 선, 막대, 색 등을 사용해 표현<br>

- <b>구성 시각화</b><br>
\: 범주형 데이터의 구성을<br>
크기로 표현<br>
    - 파이 차트
    - 도넛 차트
    - 트리 맵 차트

- <b>분포 시각화</b><br>
\: 연속형 데이터 분포를 시각적 표현<br>
    - 1개 변수<br>
    \: 히스토그램, 박스플롯<br>
    - 2개 변수<br>
    \: 산점도<br>

<br>
<hr width="50%">
<h2 id="mean-median-mode-49-h2"><b>49. 평균, 중앙값, 최빈값</b></h2>

왜도<span style="color: #808080;">Skewed</span><br>
- 양수일 때<br>
오른쪽으로 긴 꼬리<br>
<b>==></b> $\text{Mode} < \text{Median} < \text{Mean} $

- 음수일 때<br>
왼쪽으로 긴 꼬리<br>
<b>==></b> $\text{Mean} < \text{Median} < \text{Mode} $

<br>
<hr width="50%">
<h2 id="proper-median-50-h2"><b>50. 중앙값</b></h2>

선수의 연봉이 <b style="color:red">매우 높은 상위권</b>에 분포<br>
<b>==></b> 중앙값이 적절.<br>

<br>
<hr width="50%">
<h2 id="descriptive-51-h2"><b>51. 기술 통계</b></h2>

- 중심 경향 통계량
    - 평균
    - 중위수
    - 최빈값

- 산포도 통계량
    - 범위
    - 분산
    - 표준편차
    - 평균의 표준오차

- 분포 통계량
    - 첨도
    - 왜도

<br>
<hr width="50%">
<h2 id="outlier-for-mean-and-median-53-h2"><b>53. 평균과 중앙값 - 이상값 / 변동계수</b></h2>

- 평균<br>
\: (전체 합) / (개수) 이므로<br>
<b>==></b> 이상값에 민감<br>

- 중앙값<br>
\: 가운데 위치하는 값<br>
<b>==></b> 이상값에 민감 <b>X</b><br>

- 변동계수<br>
\: 표준편차를 산술평균을 기준으로 표준화시킨 것<br>
<b>==></b> $\text{\bf CV} = \dfrac{s}{\bar{x}} $

<br>
<hr width="50%">
<h2 id="sampling-types-56-h2"><b>56. (확률적)표본추출</b></h2>

- <b>단순 무작위</b><span style="color: #808080;">Simple random</span> <b>추출</b><br>
    - 모집단의 각 개체가 표본으로 선택될 확률이<br>
    동일하게 추출되는 것<br>
    - 개별 개체 선택 확률<br>
    <b>==></b> $\dfrac{n}{N}$<br>
    ($N$: 모집단 개체 수, $n$: 표본 수)<br>

- <b>계통</b><span style="color: #808080;">Systematic</span> <b>추출</b><br>
    - 모집단 개체에 일련번호 부여 후,<br>
    첫 번째 표본을 임의 선택 후<br>
    일정한 간격으로 다음 표본 선택<br>

- <b>층화</b><span style="color: #808080;">Stratified</span> <b>추출</b><br>
    - 이질적 원소들로 구성된 모집단에서<br>
    각 계층 고루 대표되도록 표본 추출함.<br>
    - 모집단을 서로 겹치치 않는 층들로 나누고,<br>
    각 층에서 단순확률표본 추출.<br>
    (<b style="color:red">집단 간 이질적, 집단 내 동질적</b>)<br>
    - 층: 성별, 나이대, 지역 등 차이 존재하는 그룹<br>

- <b>군집</b><span style="color: #808080;">Cluster</span> <b>추출</b><br>
    - <b style="color:red">집단 내 서로 이질적, 집단 간 서로 동질적</b><br>
    - 집단 중 몇 개 선택 후,<br>
    선택 집단 내에서 필요한 만큼을 임의 선택<br>

<br>
<hr width="50%">
<h2 id="sampling-error-h2"><b>59. 표본오차</b></h2>

- 표본(추출) 오차<br>
    - 모집단 대표 못하는 표본 추출하여<br>
    발생하는 오차<br>
    - 전수조사가 아니라<br>
    표본 추출하므로 발생하는 오차.<br>
    - <b style="color:red">표본오차를 표본 크기 커지면 작아짐!!</b><br>
    <b>==></b> 전수조사에선 $0$임.<br>

- 비표본 추출 오차<br>
    - 표본오차 제외한,<br>
    집계, 조사, 분석 과정에서 발생가능한 모든 오차.<br>
    - 표본 크기에 비례하여 커짐.<br>

- 표본 편의<span style="color: #808080;">bias</span><br>
    - 표본추출 과정에서<br>
    발생하는 편의(bias)<br>
    (편의: 추정값의 기댓값과, 모수의 차이)<br>
    - 확률화에 의해 최소화 or 제거 가능<br>

<!-- <br>
<hr width="50%">
<h2 id="sampling-error-h2"><b>60. </b></h2> -->