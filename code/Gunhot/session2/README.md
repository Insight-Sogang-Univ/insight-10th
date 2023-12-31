# EDA란
<li>데이터 분석의 초기 단계</li>
<li>주어진 데이터셋을 탐색하고 이해 <- 다양한 분석 기법과 시각화 도구를 활용</li>
<li>데이터의 특성, 분포, 이상치, 상관 관계 등을 파악</li>
<li>이러한 정보는 데이터 분석 및 모델링 과정에서 중요한 기반을 제공</li>
<li>EDA를 통해 데이터의 패턴을 발견</li>
<li>데이터에 대한 가설을 세우고 검증</li>
<ol>

<li>데이터 이해</li>
- 데이터의 구조, 변수, 및 특성을 이해
<li>데이터 시각화</li>
- 그래프와 차트를 통해 데이터를 시각화 -> 패턴 및 관계를 파악
<li>이상치 탐지</li>
- 데이터 내의 이상치나 오류를 감지하고 처리
<li>변수 간 관계 파악</li>
- 변수들 간의 상관 관계 및 영향을 조사
<li>가설 설정</li>
- 데이터를 통해 가설을 설정하고 검증하기 위한 방향을 제시
</ol>
<u>EDA를 통해 데이터를 더 잘 이해하고, 후속 분석 및 의사 결정에 도움을 줌</u>



# Feature 분석 및 시각화
### 2.1 Feature의 종류

**범주형(Categorical)**
    <li>몇 개의 범주로 나누어진 자료를 의미(ex. 만족도 조사 항목)</li>
    <li>어떤 항목이 어떤 범주에 속하는지를 표현</li>
<ol>
    <li>명목형(Nominal)</li>
    <ol>
        <li>순서 없이 단순히 분류된 자료</li> 
        <li> ex) 성별, 성공여부, 혈액형 </li>
    </ol>
    <li>순서형(Ordinal)</li>
    <ol>
        <li>범주형 데이터 중 그들 사이에 순서 관계가 존재하는 자료</li>
    </ol>
</ol>

        
**수치형(Numerical)** 
    - 이산형과 연속형으로 이루어진 자료를 의미 (ex. 오늘 내가 먹은 아이스크림의 개수)

<ol>
    <li>이산형(Descrete)</li> 
    <ol>
        <li>이산적인 값</li>
        <li>정수 단위로 떨어져 셀 수 있는 데이터</li>
    </ol>
    <li>연속형(Continuous)</li>
    <ol>
        <li>연속적인 값을 갖는 데이터</li>
        <li>신장, 체중 등을 의미</li>
    </ol>

<u>'키'라는 값은 170cm와 171cm사이에 170.1, 170.2, 170.9999 등 무한히 많은 값이 있으므로 연속형이다.</u>

<u>만약 키가 Tall, Medium, Short라는 범주로 표현되어 있으면 이 경우는 범주형 데이터 중 순서형이다</u>
</ol>

## Feature의 유형에 따른 시각화

- 사용 라이브러리 :
    - Matplotlib
    - Seaborn

**명목형**
<li>막대그래프</li>
<li>Count plot</li>
<li>Pie Chart</li>

**자료의 개형**
<li>Histogram</li>
<li>Box plot</li>
<li>Stem and leaf plot</li>

**시계열 및 변수 간 관계**
<li>Time Series Plot</li>
<li>Scatter Plot</li>

### 히스토그램
- 수치형 데이터의 구간별 빈도수를 나타냄

### 커널밀도추정 함수 그래프
- 히스토그램을 매끄럽게 연결

### 막대그래프, 포인트 플롯
- 범주형 데이터 값에 따른 수치형 데이터 값의 변화 파악

### 박스 플롯
- 데이터의 분포와 중앙값 이상치의 시각화

### 바이올린 플롯
- 박스플롯 + 커널밀도추정함수 그래프

### 카운트 플롯
- 카테고리 별 데이터의 수치화

### 파이 그래프
- 데이터의 부분과 전체 간의 비율 표현 -> 비율 강조

### 라인 그래프
- 데이터의 시각화 기본적인 차트

### 산점도
- 두 변수 간의 관계 시각화

## 여러 변수 간 산점도
- 데이터셋 내의 여러 변수 간의 관계를 한번에 시각화


