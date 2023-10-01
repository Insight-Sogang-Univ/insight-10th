느낀 점 및 새롭게 알게 된 점을 선형회귀분석을 진행하는 순서대로 작성하였습니다.

1) 데이터 변수 파악
- 본격적인 데이터 분석에 앞서 변수 파악은 필수불가결한 단계이다.
- 이 단계에서 주로 확인하는 세 가지는 '결측치, 각 변수의 data type, 기본적인 기술 통계값'이다.

1-1) 결측치 확인
- df.isnull().sum()을 통해 각 변수별 결측치를 확인

1-2) 변수의 data type 확인
- df.info()를 통해 Dtype을 확인

1-3) 기본적인 기술 통계값
- df.describe()으로 기본적인 통계값을 확인할 수 있지만, 본 과제에서는 왜도, 첨도 등 더 다양한 통계값도 보기 위해 아래와 같이 코딩

df_stats = df.describe().T #.T는 행과 열을 바꿔주는 전치
#각각 중앙값, 왜도 등의 정보를 입력할 빈 열을 생성
median_results = []
skew_results = []
kurtosis_results = []
null_results = []

#for반복문을 통해 각 행 별로 중앙값 등의 정보를 계산하여 해당 열에 추가
for idx, val in enumerate(df_stats.index):
    median_results.append(df[val].median())
    skew_results.append(df[val].skew())
    kurtosis_results.append(df[val].kurtosis())
    null_results.append(df[val].isnull().sum())

df_stats['median'] = median_results
df_stats['missing'] = null_results
df_stats['skewness'] = skew_results
df_stats['kurtosis'] = kurtosis_results
df_stats

- 이 단계에서 단순히 describe함수만을 사용해서 기술 통계값을 파악하는 것보다 보다 다양한 기술 통계값을 확인하는 방법을 새로 배울 수 있었습니다.
- 이와 같은 방법으로 다양한 기술 통계량을 확인한 덕분에 종속 변수인 price가 왜도가 4.02로 분포가 왼쪽으로 치우쳐 있음을 확인할 수 있었고 자연로그를 통해 분포를 조정할 수 있었다.

1-4) 기타 데이터 전처리
- 문자열 형식으로 저장된 date 변수에서 앞 4자리만 추출하여 집이 매각된 '연도' 정보만을 취하는 전처리 과정을 거침
- yr_built(집이 지어진 연도)와 date2(집이 매각된 연도)의 기간 차이를 계산하여 집이 지어진 이후 매각되기 까지 걸린 기간을 나타내는 새로운 변수 'sold-built_years'를 생성

1-5) 시각화
- df.hist(figsize=(22,18), density=True)라는 코드를 통해 각 독립 변수의 데이터 분포를 히스토그램 형식으로 관찰할 수 있다는 것을 새롭게 알 수 있었다. 이 히스토그램을 통해 선형 관계가 의심되는 독립변수를 선정하여 산점도 그래프를 그려볼 수 있었다.
- # 변수 선정
columns = ['price','bedrooms','sqft_living','waterfront','view','yr_built','sold-built_years','date2']

df_pairplot = df[columns]
sns.pairplot(df_pairplot)
위와 같은 코딩을 통해 price와 sqft_living 두 독립 변수의 선형 관계를 확인할 수 있었다. 
- 산점도뿐만 아니라 히트맵으로 상관계수를 파악한 뒤, 정렬하여 price와 상관계수가 높은 변수들을 확인할 수 있었다. 그리하여 파악된 변수는 sqft_living, sqft_above, sqft_living15였다.
- 해당 세 변수들을 분포를 찍어본 결과, 비슷한 분포를 가진다는 것을 확인할 수 있었다. 이후에 다중회귀분석에서 다중공선성이 발견된다면 이 세 변수 중 가장 상관관계가 높은 sqft_living 변수로 분석하기로 할 것을 결정할 수 있었다.


2) 단순선형회귀 - price와 sqtf_living
2-1) 선형 회귀 찍어보기
sns.jointplot(x='sqft_living', y='price', data=df, kind='reg')

2-2) 상수항 추가하기 (add_constant 함수 사용)
X = df[['sqft_living']]
y = df[['price']]
X = sm.add_constant(X, has_constant="add")
X.head()

2-3) 선형 모델에 적용해보기 (fit 함수 사용)
model = sm.OLS(y, X)
result_model = model.fit()
result_model.summary()
-> 이 결과, P값이 유의수준 0.05보다 훨씬 작은 것으로 나와 유의 수준 0.05 이하에서 귀무가설은 기각된다. 즉, 해당 모형은 통계학적으로 유의미하다고 봐도 된다는 뜻이다.

2-4) 잔차 확인하기 (resid 함수 사용)
result_model.resid.plot()
plt.show()
-> '잔차 = 실제 값 - 모델 추정을 통해 산출한 값'

3) 다중선형회귀 - (price와 다른 변수들)
3-0) 독립 변수로 넣을 수 없는 변수들은 사전에 제거하기
# date의 경우 전처리를 한 column이 존재하기 때문에 제외
columns = list(df.columns)
not_used = ['id','date']
for item in not_used:
    if item in columns:
        columns.remove(item)
columns

3-1) 모든 변수들을 독립 변수로 넣어보고 다중선형회귀모형 만들기
# 위의 columns 만 선택한 df 선언
df_reg = df[columns]
# constant 더하고 feature columns 뽑아내기
df_kc_reg = sm.add_constant(df_reg, has_constant='add')
feature_columns = list(df_kc_reg.columns.difference(['price']))
# 변수 선택
X = df_kc_reg[feature_columns]
y = df_kc_reg.price
# 회귀 모형
multi_linear_model = sm.OLS(y, X)
result_model_1 = multi_linear_model.fit()
# 결과
result_model_1.summary()
-> summary를 통해 관찰한 결과는 다음과 같다. 우선 p값이 유의 수준 0.05보다 훨씬 작아서 모형 통계학적 유의성이 확인된다. R-squared 값 또한 0.701로 약 70%가 해당 모형에 의해 설명된다는 것을 확인할 수 있다. 

3-2) 다중공선성 확인하기
from statsmodels.stats.outliers_influence import variance_inflation_factor
df_vif = pd.DataFrame()
df_vif["VIF"] = np.round([variance_inflation_factor(df_reg.values, i) for i in range(df_reg.shape[1])], 2)
df_vif["features"] = df_reg.columns
df_vif.sort_values(by='VIF', ascending=False)
-> VIF 값이 큰 변수들이 존재한다는 것을 확인할 수 있다. 그렇다면 몇몇 독립변수를 선정하여 다시 다중선형회귀분석을 실시한다.

3-3) 독립변수 선정 후 다중선형회귀분석 재실시
df_reg = df[['bedrooms','sqft_living','waterfront','view','sold-built_years','price']]
df_kc_reg = sm.add_constant(df_reg, has_constant='add')
feature_columns = list(df_kc_reg.columns.difference(['price']))
X = df_kc_reg[feature_columns]
y = np.log(df_kc_reg.price)
# 회귀 모형
multi_linear_model = sm.OLS(y, X)
result_model_2 = multi_linear_model.fit()
result_model_2.summary()
-> P값은 유의수준 0.05보다 작아서 모형의 통계학적 유의성은 확인되었다. 다시 다중공선성을 검사한다. -> 확실히 이전보다 감소하였음을 확인할 수 있었다.


4) 회귀모형의 오차에 대한 가정 진단
4-1) 정규성 검정
# Q-Q 도표
qqplot = sm.qqplot(result_model_2.resid, line="s")

# 잔차 패턴 확인
fitted = result_model_2.predict()
resid = result_model_2.resid
pred = result_model_2.predict(X)
fig = plt.scatter(pred, resid, s=3)
# plt.xlim(2)
# plt.xlim(20, 140)
# plt.xlim(0.5)
plt.xlabel('Fitted values')
plt.ylabel('Residual')

# 샤피로 - 월크 검정
result_shapiro = stats.shapiro(result_model_2.resid)
print(f"F value : {result_shapiro[0]:.4f} / p-value : {result_shapiro[1]:.4f}")
if result_shapiro[1] < 0.05:
    print("p-value < 0.05 입니다.")
    
-> 위와 같이 Q-Q 도표, 잔차 패턴, 샤피로-윌크 검정을 통해 정규성을 만족한다는 것을 확인할 수 있다.


4-2) 독립성 검정
# 잔차 그래프
result_model_2.resid.plot()
plt.show()
# ACF (Auto-Correlation Function)
sm.graphics.tsa.plot_acf(result_model_2.resid)
plt.show()
-> 위와 같이 잔차 그래프와 ACF를 통해 독립성을 확인할 수 있다. ACF 그래프에서 0시차 이후에 파란색 구간을 이탈하는 시차가 존재하지 않다면 독립성을 만족한다고 봐도 된다는 것을 배울 수 있었다.

4-3) 등분산성 검정
# displot
sns.distplot(result_model_2.resid)
plt.show()
# 잔차 그래프
result_model_2.resid.plot()
plt.show()
-> 잔차 그래프를 통해 오차의 등분산성 가정 만족 여부를 확인할 수 있다는 것도 배울 수 있었다.
