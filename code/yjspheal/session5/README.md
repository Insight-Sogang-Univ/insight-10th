<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#경사-하강법(Gradient-Descent)" data-toc-modified-id="경사-하강법(Gradient-Descent)-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>경사 하강법(Gradient Descent)</a></span><ul class="toc-item"><li><span><a href="#학습률(Learning-Rate)" data-toc-modified-id="학습률(Learning-Rate)-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>학습률(Learning Rate)</a></span></li><li><span><a href="#문제점" data-toc-modified-id="문제점-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>문제점</a></span><ul class="toc-item"><li><span><a href="#Local-Minima" data-toc-modified-id="Local-Minima-1.2.1"><span class="toc-item-num">1.2.1&nbsp;&nbsp;</span>Local Minima</a></span></li><li><span><a href="#적절한-step-size를-찾지-못하는-경우" data-toc-modified-id="적절한-step-size를-찾지-못하는-경우-1.2.2"><span class="toc-item-num">1.2.2&nbsp;&nbsp;</span>적절한 step size를 찾지 못하는 경우</a></span></li></ul></li></ul></li><li><span><a href="#규제선형모델" data-toc-modified-id="규제선형모델-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>규제선형모델</a></span><ul class="toc-item"><li><span><a href="#종류" data-toc-modified-id="종류-2.1"><span class="toc-item-num">2.1&nbsp;&nbsp;</span>종류</a></span><ul class="toc-item"><li><span><a href="#릿지-회귀" data-toc-modified-id="릿지-회귀-2.1.1"><span class="toc-item-num">2.1.1&nbsp;&nbsp;</span>릿지 회귀</a></span></li><li><span><a href="#라쏘-회귀" data-toc-modified-id="라쏘-회귀-2.1.2"><span class="toc-item-num">2.1.2&nbsp;&nbsp;</span>라쏘 회귀</a></span></li><li><span><a href="#엘라스틱넷회귀" data-toc-modified-id="엘라스틱넷회귀-2.1.3"><span class="toc-item-num">2.1.3&nbsp;&nbsp;</span>엘라스틱넷회귀</a></span></li></ul></li></ul></li><li><span><a href="#Scaling" data-toc-modified-id="Scaling-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>Scaling</a></span><ul class="toc-item"><li><span><a href="#표준화(Standardization)" data-toc-modified-id="표준화(Standardization)-3.1"><span class="toc-item-num">3.1&nbsp;&nbsp;</span>표준화(Standardization)</a></span></li><li><span><a href="#정규화(Normalization)" data-toc-modified-id="정규화(Normalization)-3.2"><span class="toc-item-num">3.2&nbsp;&nbsp;</span>정규화(Normalization)</a></span></li><li><span><a href="#스케일링-종류" data-toc-modified-id="스케일링-종류-3.3"><span class="toc-item-num">3.3&nbsp;&nbsp;</span>스케일링 종류</a></span><ul class="toc-item"><li><span><a href="#StandardScaler()" data-toc-modified-id="StandardScaler()-3.3.1"><span class="toc-item-num">3.3.1&nbsp;&nbsp;</span>StandardScaler()</a></span></li><li><span><a href="#MinMaxScaler()" data-toc-modified-id="MinMaxScaler()-3.3.2"><span class="toc-item-num">3.3.2&nbsp;&nbsp;</span>MinMaxScaler()</a></span></li><li><span><a href="#MaxAbsScaler()" data-toc-modified-id="MaxAbsScaler()-3.3.3"><span class="toc-item-num">3.3.3&nbsp;&nbsp;</span>MaxAbsScaler()</a></span></li><li><span><a href="#RobustScaler()" data-toc-modified-id="RobustScaler()-3.3.4"><span class="toc-item-num">3.3.4&nbsp;&nbsp;</span>RobustScaler()</a></span></li><li><span><a href="#Normalizer()" data-toc-modified-id="Normalizer()-3.3.5"><span class="toc-item-num">3.3.5&nbsp;&nbsp;</span>Normalizer()</a></span></li></ul></li></ul></li><li><span><a href="#차원-축소" data-toc-modified-id="차원-축소-4"><span class="toc-item-num">4&nbsp;&nbsp;</span>차원 축소</a></span><ul class="toc-item"><li><span><a href="#차원-축소-알고리즘" data-toc-modified-id="차원-축소-알고리즘-4.1"><span class="toc-item-num">4.1&nbsp;&nbsp;</span>차원 축소 알고리즘</a></span><ul class="toc-item"><li><span><a href="#PCA(주성분-분석,-Principal-Component-Analysis)" data-toc-modified-id="PCA(주성분-분석,-Principal-Component-Analysis)-4.1.1"><span class="toc-item-num">4.1.1&nbsp;&nbsp;</span>PCA(주성분 분석, Principal Component Analysis)</a></span></li><li><span><a href="#LDA(선형-판별-분석,-Linear-Discriminant-Analysis)" data-toc-modified-id="LDA(선형-판별-분석,-Linear-Discriminant-Analysis)-4.1.2"><span class="toc-item-num">4.1.2&nbsp;&nbsp;</span>LDA(선형 판별 분석, Linear Discriminant Analysis)</a></span></li><li><span><a href="#SVD(특이값-분해,-Singular&nbsp;Value-Decomposition)" data-toc-modified-id="SVD(특이값-분해,-Singular&nbsp;Value-Decomposition)-4.1.3"><span class="toc-item-num">4.1.3&nbsp;&nbsp;</span>SVD(특이값 분해, Singular&nbsp;Value Decomposition)</a></span></li><li><span><a href="#NMF(비음수-행렬-분해,-Non-negative-Matrix-Factorization)" data-toc-modified-id="NMF(비음수-행렬-분해,-Non-negative-Matrix-Factorization)-4.1.4"><span class="toc-item-num">4.1.4&nbsp;&nbsp;</span>NMF(비음수 행렬 분해, Non-negative Matrix Factorization)</a></span></li></ul></li><li><span><a href="#차원-축소가-필요한-이유" data-toc-modified-id="차원-축소가-필요한-이유-4.2"><span class="toc-item-num">4.2&nbsp;&nbsp;</span>차원 축소가 필요한 이유</a></span><ul class="toc-item"><li><span><a href="#차원의-저주" data-toc-modified-id="차원의-저주-4.2.1"><span class="toc-item-num">4.2.1&nbsp;&nbsp;</span>차원의 저주</a></span></li><li><span><a href="#과적합(Overfit)-문제" data-toc-modified-id="과적합(Overfit)-문제-4.2.2"><span class="toc-item-num">4.2.2&nbsp;&nbsp;</span>과적합(Overfit) 문제</a></span></li><li><span><a href="#분석-및-시각화-용이" data-toc-modified-id="분석-및-시각화-용이-4.2.3"><span class="toc-item-num">4.2.3&nbsp;&nbsp;</span>분석 및 시각화 용이</a></span></li></ul></li></ul></li></ul></div>

## 경사 하강법(Gradient Descent)
: 현재 값 - 미분한 값 을 계산하여, 현재 손실함수 그래프가 상승중인지 하강중인지 파악한다. 이후 반대 방향으로 이동하여 미분값이 0인 곳을 찾아낸다.

### 학습률(Learning Rate)
하지만 **얼마나 이동하는지**에 따라 오히려 손실 최소값에서 멀어질 수 있음. 이를 막기 위해 얼마나 움직일지를 학습률이 결정함.

* Learning Rate가 크면 모델이 수렴하지 못하고 오히려 발산하게 됨.
* Learning Rate가 작으면 모델이 수렴하기까지 오랜 시간이 걸리게 됨
<br> -> 적당한 학습률이 가장 좋음

### 문제점
#### Local Minima
* 모든 손실 함수가 하나의 최소값을 가지는 2차함수 형태가 아님. global minima가 아닌 local minima에 도달하게 됨.
* 딥러닝의 경우 손실함수가 어떤 모양인지 예측할 수 없으므로 극소점을 찾게 되는 경우를 주의해야 함.

#### 적절한 step size를 찾지 못하는 경우
* 학습률을 너무 높거나 낮게 설정하여 생기는 문제.
* 해결법
1. 학습 도중에 학습률을 지속적으로 바꾸는 Adaptive Gradient Descent 사용
2. 모멘텀 사용(기울기에 관성을 부여)

## 규제선형모델
* overfitting을 막기 위해 규제를 가하고자 등장한 모델
### 종류
#### 릿지 회귀
‘계수를 제곱한 기준’으로 규제를 적용 (L2 규제)
* alpha 매개변수 값을 통하여 규제 정도 조절
    * 높은 alpha -> 규제 정도 상승, 계수를 줄여 과소적합을 유도
    * 낮은 alpha -> 과대적합을 유도
    

#### 라쏘 회귀
‘계수의 절댓값 기준’으로 규제를 적용 (L1 규제)
* 릿지와 라쏘 모두 계수의 크기를 줄이지만, 라쏘는 0으로 만들 수 있음.
* alpha 매개변수 값을 통하여 규제 정도 조절
    * 높은 alpha -> 규제 정도 상승, 계수를 줄여 과소적합을 유도
    * 낮은 alpha -> 과대적합을 유도

#### 엘라스틱넷회귀
: L2와 L1을 결합한 회귀

## Scaling
:모든 feature들의 데이터 분포나 범위를 동일하게 조정하는 과정
### 표준화(Standardization)
:입력된 값들을 표준정규분포에 맞게 변환. 특정 범위를 벗어난 데이터는 outlier로 간주하고 제거함.

### 정규화(Normalization)
: 입력된 값들을 모두 0과 1 사이의 값으로 변환하여 서로 다른 feature의 크기를 통일함. 가장 큰 값이 1, 가장 작은 값이 0이다.

### 스케일링 종류
#### StandardScaler()
특성(feature)의 평균을 0, 분산을 1로 맞추는 표준화(Standardization)를 수행
#### MinMaxScaler()
모든 feature들이 0과 1 사이의 데이터 값을 갖도록 변환
#### MaxAbsScaler()
데이터가 -1과 1 사이에 위치하도록 변환
#### RobustScaler()
데이터의 중앙값이 0, IQE(Q3 - Q1) = 1이 되도록 변환
#### Normalizer()
각 데이터포인트(행)의 norm(크기)를 1로 만들어주는 변환


## 차원 축소
차원이란? 공간 내에 있는 점의 위치를 나타내기 위해 필요한 축의 갯수
* 데이터에서 차원이란 변수의 수와 같다.
* 차원이 크면 분석이 어려워지고 시각화도 어렵다. -> 줄이는 것이 좋다.

### 차원 축소 알고리즘
#### PCA(주성분 분석, Principal Component Analysis)
n개의 변수만으로 **전체 변수의 분산**에 대해 설명할 수 있다면, n개의 변수만 사용하면 되지 않을까?라는 생각에서 기인한 분석
* 주성분 분석 PCA: 고차원 데이터를 기존의 분산을 최대한 보존하는 선형 독립의 새로운 변수들로 변환: 여러 변수 간에 존재하는 상관관계를 이용해 이를 대표하는 주성분을 추출해 차원 축소
* PCA의 핵심은 데이터를 축에 사영했을 때 가장 높은 분산을 가지는 데이터의 축을 찾는것-> 그 축(고유벡터)으로 차원을 축소

#### LDA(선형 판별 분석, Linear Discriminant Analysis)
* PCA처럼 입력 데이터 세트를 저차원 공간에 투영해 차원을 축소하는 기법으로 PCA와 매우 유사
* PCA는 입력 데이터의 변동성의 가장 큰 축을 찾았지만, LDA는 입력 데이터의 결정값 클래스를 최대한 분리할 수 있는 축을 찾음
#### SVD(특이값 분해, Singular Value Decomposition)
* SVD는 정사각행렬이 아닌 m\*n 형태의 다양한 행렬을 분해하며, 이를 특이값 분해라고 함
#### NMF(비음수 행렬 분해, Non-negative Matrix Factorization)
* 하나의 객체정보를 음수를 포함하지 않은 두 개의 부분 정보로 인수분해하는 방법
* NMF는 대량의 정보를 의미 특징과 의미 변수로 나누어 효율적으로 표현할 수 있음

### 차원 축소가 필요한 이유
#### 차원의 저주
: 차원이 커짐에 따라 공간의 범위가 기하급수적으로 증가하여 많은 샘플이 필요해지는 현상.
* 차원이 커지면서 두 데이터간의 거리가 멀어지고 밀도가 급격히 줄어든다

#### 과적합(Overfit) 문제
* 고차원 문제를 풀다보면 너무 정교해서 일반화 결과를 도출할 수 없는 상황이 올 수 있다

#### 분석 및 시각화 용이
* 복잡한 형태의 데이터 구조를 낮은 차원에서 분석하게 되면 구조를 파악하기 쉽거나 시각화하기 쉬워짐



```python

```
