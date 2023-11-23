경사하강법
실제값과 예측값의 차이를 뜻하는 손실함수를 최소화시키는 방법
(근데 왜 손실함수는 무조건 2차함수 모양이지)
원리만 보면 점하나를 찍어놓고 기울기값이 0이 되는 점까지 찾아가도록 값을 더하거나 빼는거 같은데... 사실 자세히 이해가 안간다.

문제점
- Local Minima 문제
- step size 찾지 못함

해결법
- Adaptivve Gradient Descent
- 모멘텀

규제선형모델 => 과적합 막는 방법
- 릿지 회귀(계수 제곱 기준)
- 리쏘 회귀(계수 절대값 기준)
- 엘라스틱넷 회귀

스케일링
- StandardScaler
- MinMaxScaler
- MaxAbsScaler => 데이터가 -1과 1 사이 위치하도록 스케일링
- RobustScaler => 중앙값이 0, IQE=1이 되도록 스케일링
- Normalize => 각 행의 크기를 1로 만드는 스케일링

차원축소
- PCA
- LDA
- SVD
- NMF
