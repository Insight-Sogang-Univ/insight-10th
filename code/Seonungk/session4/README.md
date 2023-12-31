# 회귀, 분류, 군집화란?
1. 회귀: 둘 이상의 변수 간의 관계를 보여주는 통계적 기법
- 지도학습이며, 집값 예측, 주식 가격 예측 등 연속적인 숫자를 다룸.
2. 분류: 기존 데이터들의 관계를 학습하여 새롭게 관측된 데이터에 대한 결과 판별
- 지도 학습이며 범주형 변수에 대해 예측할 때 사용
3. 군집화: 주어진 데이터들을 특성을 분류하여 같은 그룹으로 묶어줌
- 구분하려고 하는 데이터에 대한 정보가 없기 때문에 비지도
# 선형회귀란?
***잔차를 최소화하는 직선형 회귀식 최적화***
## 선형회귀의 목적
- 데이터의 이해: 종속변수의 원인이 되는 독립변수 파악
- 예측: 과거의 데이터를 기반으로 모델을 형성하여 미래의 값을 예측
- 인과관계 증명: 다른 요인을 통제했을때 원인으로 반복해서 결과로 나오는지 검증
# 다중공선성이란?
***다중선형회귀:연속형 종속 변수 하나에 독립 변수가 둘 이상인 회귀 모형***
<span style='color:red'>주의: 독립변수들 간 높은 상관관계를 가질 경우 정보 중첩 발생</span>
- 분산팽창계수(VIF)가 10이 넘으면 다중공선성이 있다고 봄.
## 대처 방법
1. 변수 제거: 가설에 영향을 줄 수 있어 가급적 자제
2. 변수 변환: 변수를 병합하거나 분리하여 새로운 변수 생성
3. 규제 선형 모델 활용
4. PCA

# 최소제곱법이란?
- 최소 자승법이라고 함. 잔차를 최소화하는 방법 사용
*최소 자승법은 노이즈에 취약하다는 한계가 있다.*

