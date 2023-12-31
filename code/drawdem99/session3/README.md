# 통계

## 1. 통계란?

- 데이터를 수집, 분석, 해석하는 과정을 통해 패턴, 관계, 변동 등을 이해하고 결론을 도출하는 학문 및 방법론
    1. 기술 통계학 (Descriptive Statistics) : 데이터를 요약하고 기술하는 기법을 다루는 분야. 평균, 중앙값, 표준편차, 분포 등의 개념.
        - 수치 기술 통계 : 숫자 형태로 데이터를 요약하는 방법
        - 표와 그래프 기술 통계 : 표와 그래프 형태로 정보를 시각화하는 방법
    2. 추론 통계학 (Inferential Statistics) : 주어진 데이터를 기반으로 미래의 정보를 추론하고 결론을 도출하는 분야.


## 2. 수치 기술 통계 (기술 통계)

### 2.1 중심 위치 척도

- 평균(mean) / 중앙값(median) / 최빈값(mode)
- 이러한 값을 통해 자료의 개형(skewness 등)을 확인할 수 있다.
    - Positive Skewness
    - Negative Skewness
    - Normal Distribution


### 2.2 변동성 척도

- 사분위수(quartile) : 데이터의 표본을 네 개의 동일한 부분으로 나눈 값
- 사분위간 범위 (IQR) : Q3에서 Q1값을 제외한 범위
- 범위(range) : 데이터의 최대값과 최소값의 차이
- 분산(variance) : 데이터 값들이 평균으로부터 얼마나 퍼져있는지 나타내는 지표
- 표준편차(standard deviation) : 분산의 제곱근
- 변동계수 (coefficient of variation) : 데이터의 상대적인 변동성을 나타내는 통계적 지표. 표준편차를 평균으로 나눈 값.


### 2.3 연관성 척도

- 공분산(covariance) : 두 변수가 각자의 평균으로부터 떨어진 값을 곱한 후 평균한 값. 두 변수가 함께 어떤 방향으로 변화하는지와 크기를 표현.
    - Cov (x, y) > 0 --> x와 y는 양의 상관관계
- 상관계수(correlation) : 두 변수 간의 선형적인 관계를 나타내는 지표. 
    - 상관계수는 -1과 1 사이의 값을 가지며, 상관관계와 인과관계는 다르다.
    - 공분산을 -1과 1 사이로 표준화 한 것이다.


## 3. 추론 통계 (모집단 분포 추정)

- 예시) 우리나라 성인 평균 키를 구하고자 할때 :
    - 모집단 = 우리나라 성인 전체
    - 모집단으로부터 일부를 추출하여 조사된 집단을 표본집단이라고 한다.
- 대수의 법칙 : 표본의 크기가 커질수록 표본 평균의 모평균에 근사하는 현상. 표본의 수가 많을수록 통계적 정확도는 올라간다.
- 중심극한정리 : 표본의 크기가 크면 표본 평균의 분포가 모집단의 분포와 상관없이 정규분포에 가까워진다.


###  3.1 확률분포

- 확률분포(Probability Distribution) : 확률변수가 특정한 값을 가질 확률을 나타내는 함수.
    - 이산확률분포 : 확률 변수가 이산적인 값을 가지는 경우
    - 연속확률분포 : 확률 변수가 연속적인 값을 가지는 경우


### 3.2 확률분포 예시

- 정규분포(Normal Distribution)
    - 종 모양, 좌우 대칭
    - 위치가 평균에 의해 정해지고, 그 모양은 표준편차의 크기에 의해 결정.
- T분포 : 표본 평균이 어떤 분포를 가지는가
    - 0을 중심으로 종형의 모습
    - '자유도' n의 값에 따라 모습이 변하며, 그 값이 커짐에 따라 표준정규분포 N(0, 1)에 수렴함.
- 카이제곱분포(Chi-Square Distribution)
    - 범주형 데이터의 분석이나 카이제곱 검정과 같은 통계적 검정.
    - 정규분포의 제곱은 카이스퀘어 분포
    - 자유도가 커질수록 평균과 분산이 증가
- F분포
    - 두 개의 카이제곱분포의 비율에 관련된 확률분포
    - 주로 분산 분석과 회귀 분석
    - 자유도가 증가할수록 F분포의 확률밀도 함수의 모양이 정규분포 모양에 가까워짐.
- 이항분포(Binomial Distribution) + 베르누이분포(Bernoulli Distribution)
    - 이항분포 : 연속된 독립시행에서 각 시행이 성공활 확률 p를 가질 때 만들어지는 이산 확률 분포. 예시) 동전던지기
- 포아송분포(Poisson Distribution)
    - 단위 시간 안에 어떤 사건이 몇 번 일어날 것인지를 표현하는 이산 확률 분포
    - 시행 횟수가 증가할수록 분포가 대칭적으로 변함


## 4. 가설 검정

### 4.1 가설 검정의 절차

1. 가설 설정
    - 귀무가설 H0과 대립가설 H1을 설정
    - 귀무가설은 주로 확인하기 용이하거나 기각하고자 하는 명제로 설정
2. 유의 수준 설정
    - 얼마나 정해진 수치를 벗어나면 귀무가설이 오류라고 인정할 것인가를 판단하는 기준
    - 기호 : (α)
    - 이 값이 커지면 대립가설이 채택될 가능성이 높아지며, 작아지면 대립가설이 기각될 가능성이 높아진다.
3. 검정통계량 산출
    - 검정통계량은 가설 검정의 결과를 판단하는데 사용
    - 데이터가 분포나 특징에 따라 Z통계량, T통계량 등 어떤 검정통계량을 사용할지 정해야 함.
4. 가설 기각 / 채택 판단
    - 검정통계량이 확률분포 어디에 위치하느냐에 따라 기각 및 채택 여부가 결정됨.
    - 검정통계량이 신뢰기간에 위치해 있을 경우 귀무가설 채택(대립가설 기각), 벗어날 시에는 귀무가설을 채택(대립가설 기각)
    - 유의확률(p-value) : 검정통계량에서 유도된 값으로 유의 확률 p-value가 유의 수준보다 클 시에 귀무가설을 채택.


### 4.2 1종, 2종 오류

1. 1종 오류(α) : 귀무가설이 실제로 참이었는데 기각할 확률
2. 2종 오류(β) : 귀무가설이 실제로 거짓인데 채택할 확률


## 5. 조건부확률과 베이즈 정리

- 조건부 확률(Conditional Probability)
    - 어떤 사건이 일어났을 때, 그와 연관된 다른 사건이 일어날 확률
    - 보통 P(B|A)로 표시하며, 이는 사건 A가 일어났을 때 B가 일어날 확률
- 베이즈 정리(Bayes' Theorem)
    - 의학, 인공지능, 경제학 등 다양한 분야에서 활용되며, 조건부 확률을 통해 사전정보가 주어진 상태에서 새로운 정보를 추론.
