# session5 과제
📌 필수과제: 코드 돌려보고 새롭게 알게된 점, 느낀점 마크다운으로 정리

##  House Sales in King Country, USA: 집값 예측 과정

### 1. 전반적인 데이터 파악 및 전처리
- 결측치 확인
    * df.is_null().sum
- 각 column의 data 확인
    * df.info
- 기본적인 기술 통계값 확인
    * df.describe()
    * np.log(df['...']).hist() -> 자연 로그를 활용한 분포 조정
- 컬럼 삭제 및 생성

### 2. 시각화
- 히스토그램
    * df.hist(figsize=(22,18), density=True)
- 산점도 그래프
    * df_pairplot = df[columns]
    * sns.pairplot(df_pairplot)
- 히트맵
    * ns.heatmap(df.corr(), annot=True, mask=mask, cmap=cmap, linewidths=.5, fmt='.2f', annot_kws={"size":10})

### 3. 다중공산성 확인
### 4. fit() 함수를 통한 선형 모델 적합

## 다중 선형 회귀
: 연속형 반응변수 하나에 "설명 변수가 둘 이상"인 모형
- 다중공선성(multicollinearlity) 문제: 명 변수 정보 중첩으로 발생
-  차원의 저주 문제: , 너무 많은 설명 변수를 포함해 발생

## 회귀 모형의 가정 진단
◼️ 선형 모형의 전제
-  반응 변수와 설명 변수의 선형 관계
- 오차에 대한 독립성, 정규성, 등분산성

-> 앞서 확인한 모형의 유의성과 계수의 유의성이 확보되었다고 해도, 오차에 대한 가정을 만족하지 않으면 다른 대안을 찾아야 함.
