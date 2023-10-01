## 선형회귀 학습
---
중간값, 결측치, 왜도, 철도
```
median_results = []
skew_results = []
kurtosis_results = []
null_results = []

for idx, val in enumerate(df_stats.index):
    median_results.append(df[val].median())
    skew_results.append(df[val].skew())
    kurtosis_results.append(df[val].kurtosis())
    null_results.append(df[val].isnull().sum())
```

이때 특정 변수의 왜도가 치우쳐져 있으면 자연로그를 통하여 분포를 조정할 수 있다.
np.log(df['price']).hist()
np.log(df['price']).skew()
---
### 새로운 변수를 추가하는 방법
df['새로운 변수'] = df.apply(lambda x:((x['기준 변수1']) - (x['기준 변수2'])), axis=1)

이렇게 하면 두 가지 변수를 조합하여 새로운 변수를 생성할 수 있다!

## 관계를 파악하는 방법
1. 산점도를 이용하는 방법 (Scatter Plot)
문자열 변수는 제외해야한다.

```
df_pairplot = df[columns]
sns.pairplot(df_pairplot)
plt.show()
```

이러한 산점도를 그리게 되면 종속 변수와 독립 변수들 사이의 선형 관계를 대략적으로 알 수 있다.

2. HeatMap을 이용하는 방법
```
df_corr = df.corr()
cmap = sns.diverging_palette(240, 10, n=9, as_cmap=True)

mask = np.zeros_like(df_corr, dtype=bool)
mask[np.triu_indices_from(mask)] = True

plt.figure(figsize=(16,12))

sns.heatmap(df.corr(), annot=True, mask=mask, cmap=cmap, linewidths=.5, fmt='.2f', annot_kws={"size":10})
```

3. 독립 변수들 간의 상관관계를 확인하는 방법

```
columns = ['sqft_living', 'sqft_living15', 'sqft_above']
colors = ['blue','green','red']

living = df[columns]

plt.figure(figsize=(12,6))

for i in range(3):
    ax = sns.distplot(df[columns[i]], hist=True, norm_hist=False, kde=False, label=columns[i], color=colors[i])
ax.set(xlabel="sqft_living / sqft_living15 / sqft_above")

plt.legend()
plt.show()
```

## 중간 느낀점
- 과제나 인사이콘을 진행할 때 무작정 히트맵을 그려서 상관관계를 파악하려고 했는데, 상관관계를 파악할 때에도 범주형 변수도 넣었었다. 하지만 이러한 선형관계를 확인하는 과정을 하나씩 뜯어보니 어떤 변수들을 비교해야할지 단순히 전체 변수를 넣고 코드를 돌리는 과정을 진행하기 전에 예측할 수 있게 되었다.


## 다중 선형 회귀

다중 선형 회귀 모형은 단순 선형 회귀모형의 확장으로, 연속형 반응변수 하나에 "설명 변수가 둘 이상"인 모형을 말합니다. 설명 변수가 늘어나므로 추가 검토해야 할 문제는 설명 변수 정보 중첩으로 발생하는 다중공선성(multicollinearlity) 문제와, 너무 많은 설명 변수를 포함해 발생하는 차원의 저주 문제 등이 있다.
```
원래 뭐든 다 때려보고, 그 중 괜찮은 걸 고르는 것이 가장 속이 편합니다.
```
이 말을 기억해두어야할 것 같다. 직관적으로 상관관계가 없을 것 같은 변수들이 실제로 상관관계가 있던 경험이 있고, 상관관계가 있을 것 같았던 변수들이 없던 경우도 있었다. 또한 인과관계과 상관관계의 혼동도 충분히 발생할 수 있기 때문에 여러 가지 변수들을 모두 비교해보고 분석하는 태도가 중요하다고 생각한다.

### 독립성 검정은 아직 미숙하기 때문에 추가적으로 공부를 하려고 합니다.