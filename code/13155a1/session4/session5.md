# INSIGHT 4주차 교육 세션: 회귀 이론, 실습

## 📌 목차
- 회귀, 분류, 군집화 구분
- 선형회귀
- 다중공선성
- 최소제곱법

## 회귀, 분류, 군집화 구분
- 회귀: 둘 이상의 변수 간의 관계를 보여주는 통계적 기법 (지도학습)
- 분류: 기존에 존재하는 데이터의 관계를 학습하여 새롭게 관특한 데이터에 대한 결과를 스스로 판별하는 과정 (지도학습)
- 군집화: 주어진 데이터들의 특성을 고려해 같은 그룹을 정의하고 그룹화하여 그룹의 대표성을 찾아내는 방법 (비지도 학습)

💡 지도학습과 비지도학습
- 지도학습: 정답값(label)이 있는 데이터셋으로 학습하는 방식
- 비지도학습: 정답값(label)이 없는 데이터셋으로 학습하는 방식

## 선형회귀
실제 값과 예측값의 차이(오류의 제곱값)를 최소화하는 직선형 회귀선을 최적화하는 방식
- 단순선형회귀
- 다중선형회귀

## 다중공선성
설명 변수들 간의 선형 종속이 심한 경우

= 설명 변수들 간 정보의 중첩이 발생한 것으로 설명변수들 간에 높은 상관관계를 갖는 경우

## 최소제곱법(OLS, 최소자승법)
- 회귀계수를 추정하는 방식 중 하나
- 오차를 최소화시킴
