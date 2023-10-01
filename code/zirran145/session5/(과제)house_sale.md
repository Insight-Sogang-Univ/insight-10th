# House Sales in King Country, USA

선형 회귀분석을 학습해 봅시다.
선형 회귀분석을 사용하여 집값(price)을 예측해 봅시다.

**어떤 데이터 분석을 하더라도 가장 먼저 변수들을 살펴보고 시작해야 합니다.**

데이터셋에서 추출할 수 있는 변수는 다음과 같습니다.

독립 변수
- id : 고유한 id 값
- date : 집이 매각된 날자
- bedrooms : 침실 수
- bathrooms : 욕실 수
- sqft_living : 집의 평방 피트
- sqft_lot : 부지의 평방 피트
- floors : 집의 총 층수
- waterfront : 물가가 보이는 집
- condition : 상태가 얼마나 좋은지 여부
- grade : 주택에 부여되는 등급
- sqft_above : 지하실을 제외한 집의 평방 피트
- sqft_basement : 지하실의 평방 피트
- yr_built : 지어진 연도
- yr_renovated : 리모델링된 연도
- lat : 위도 좌표
- long : 경도 좌표
- sqft_living15 : 2015년 당시 거실 면적 (일부 개조를 의미하고, 부지 면적에 영향을 미칠 수도 있고 아닐 수도 있음)
- sqft_lot15 : 2015년 당시 부지 면적(일부 개조를 의미함)

종속 변수(y)
- price : 주택 가격

Details
https://info.kingcounty.gov/assessor/esales/Glossary.aspx


```python
import numpy as np
import pandas as pd

# 통계학습을 위한 패키지입니다
from scipy import stats
import statsmodels.api as sm
from statsmodels.formula.api import ols

# 기계학습을 위한 패키지입니다
import sklearn.linear_model
from sklearn.model_selection import train_test_split

# 시각화를 위한 패키지입니다
from matplotlib import pyplot as plt
import seaborn as sns

# 그래프를 실제로 그리기 위한 설정입니다
%matplotlib inline

# 경고 메시지를 무시합니다
import warnings
warnings.filterwarnings('ignore')
```


```python
# csv 파일을 불러와서 DataFrame 에 담습니다.
df = pd.read_csv('kc_house_data.csv')

# index 를 1로 시작하도록 수정합니다.
df.index += 1
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>date</th>
      <th>price</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>sqft_living</th>
      <th>sqft_lot</th>
      <th>floors</th>
      <th>waterfront</th>
      <th>view</th>
      <th>...</th>
      <th>grade</th>
      <th>sqft_above</th>
      <th>sqft_basement</th>
      <th>yr_built</th>
      <th>yr_renovated</th>
      <th>zipcode</th>
      <th>lat</th>
      <th>long</th>
      <th>sqft_living15</th>
      <th>sqft_lot15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>7129300520</td>
      <td>20141013T000000</td>
      <td>221900.0</td>
      <td>3</td>
      <td>1.00</td>
      <td>1180</td>
      <td>5650</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>7</td>
      <td>1180</td>
      <td>0</td>
      <td>1955</td>
      <td>0</td>
      <td>98178</td>
      <td>47.5112</td>
      <td>-122.257</td>
      <td>1340</td>
      <td>5650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6414100192</td>
      <td>20141209T000000</td>
      <td>538000.0</td>
      <td>3</td>
      <td>2.25</td>
      <td>2570</td>
      <td>7242</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>7</td>
      <td>2170</td>
      <td>400</td>
      <td>1951</td>
      <td>1991</td>
      <td>98125</td>
      <td>47.7210</td>
      <td>-122.319</td>
      <td>1690</td>
      <td>7639</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5631500400</td>
      <td>20150225T000000</td>
      <td>180000.0</td>
      <td>2</td>
      <td>1.00</td>
      <td>770</td>
      <td>10000</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>6</td>
      <td>770</td>
      <td>0</td>
      <td>1933</td>
      <td>0</td>
      <td>98028</td>
      <td>47.7379</td>
      <td>-122.233</td>
      <td>2720</td>
      <td>8062</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2487200875</td>
      <td>20141209T000000</td>
      <td>604000.0</td>
      <td>4</td>
      <td>3.00</td>
      <td>1960</td>
      <td>5000</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>7</td>
      <td>1050</td>
      <td>910</td>
      <td>1965</td>
      <td>0</td>
      <td>98136</td>
      <td>47.5208</td>
      <td>-122.393</td>
      <td>1360</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1954400510</td>
      <td>20150218T000000</td>
      <td>510000.0</td>
      <td>3</td>
      <td>2.00</td>
      <td>1680</td>
      <td>8080</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>8</td>
      <td>1680</td>
      <td>0</td>
      <td>1987</td>
      <td>0</td>
      <td>98074</td>
      <td>47.6168</td>
      <td>-122.045</td>
      <td>1800</td>
      <td>7503</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>21609</th>
      <td>263000018</td>
      <td>20140521T000000</td>
      <td>360000.0</td>
      <td>3</td>
      <td>2.50</td>
      <td>1530</td>
      <td>1131</td>
      <td>3.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>8</td>
      <td>1530</td>
      <td>0</td>
      <td>2009</td>
      <td>0</td>
      <td>98103</td>
      <td>47.6993</td>
      <td>-122.346</td>
      <td>1530</td>
      <td>1509</td>
    </tr>
    <tr>
      <th>21610</th>
      <td>6600060120</td>
      <td>20150223T000000</td>
      <td>400000.0</td>
      <td>4</td>
      <td>2.50</td>
      <td>2310</td>
      <td>5813</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>8</td>
      <td>2310</td>
      <td>0</td>
      <td>2014</td>
      <td>0</td>
      <td>98146</td>
      <td>47.5107</td>
      <td>-122.362</td>
      <td>1830</td>
      <td>7200</td>
    </tr>
    <tr>
      <th>21611</th>
      <td>1523300141</td>
      <td>20140623T000000</td>
      <td>402101.0</td>
      <td>2</td>
      <td>0.75</td>
      <td>1020</td>
      <td>1350</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>7</td>
      <td>1020</td>
      <td>0</td>
      <td>2009</td>
      <td>0</td>
      <td>98144</td>
      <td>47.5944</td>
      <td>-122.299</td>
      <td>1020</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>21612</th>
      <td>291310100</td>
      <td>20150116T000000</td>
      <td>400000.0</td>
      <td>3</td>
      <td>2.50</td>
      <td>1600</td>
      <td>2388</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>8</td>
      <td>1600</td>
      <td>0</td>
      <td>2004</td>
      <td>0</td>
      <td>98027</td>
      <td>47.5345</td>
      <td>-122.069</td>
      <td>1410</td>
      <td>1287</td>
    </tr>
    <tr>
      <th>21613</th>
      <td>1523300157</td>
      <td>20141015T000000</td>
      <td>325000.0</td>
      <td>2</td>
      <td>0.75</td>
      <td>1020</td>
      <td>1076</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>7</td>
      <td>1020</td>
      <td>0</td>
      <td>2008</td>
      <td>0</td>
      <td>98144</td>
      <td>47.5941</td>
      <td>-122.299</td>
      <td>1020</td>
      <td>1357</td>
    </tr>
  </tbody>
</table>
<p>21613 rows × 21 columns</p>
</div>



기본적으로 다음 세 가지를 해 주시면 좋습니다.

1. 결측치 확인
2. 각 column(변수)의 data type 학인
3. 기본적인 기술 통계값 확인


```python
# 결측치 확인
df.isnull().sum()
```




    id               0
    date             0
    price            0
    bedrooms         0
    bathrooms        0
    sqft_living      0
    sqft_lot         0
    floors           0
    waterfront       0
    view             0
    condition        0
    grade            0
    sqft_above       0
    sqft_basement    0
    yr_built         0
    yr_renovated     0
    zipcode          0
    lat              0
    long             0
    sqft_living15    0
    sqft_lot15       0
    dtype: int64




```python
# type 확인
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 21613 entries, 1 to 21613
    Data columns (total 21 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   id             21613 non-null  int64  
     1   date           21613 non-null  object 
     2   price          21613 non-null  float64
     3   bedrooms       21613 non-null  int64  
     4   bathrooms      21613 non-null  float64
     5   sqft_living    21613 non-null  int64  
     6   sqft_lot       21613 non-null  int64  
     7   floors         21613 non-null  float64
     8   waterfront     21613 non-null  int64  
     9   view           21613 non-null  int64  
     10  condition      21613 non-null  int64  
     11  grade          21613 non-null  int64  
     12  sqft_above     21613 non-null  int64  
     13  sqft_basement  21613 non-null  int64  
     14  yr_built       21613 non-null  int64  
     15  yr_renovated   21613 non-null  int64  
     16  zipcode        21613 non-null  int64  
     17  lat            21613 non-null  float64
     18  long           21613 non-null  float64
     19  sqft_living15  21613 non-null  int64  
     20  sqft_lot15     21613 non-null  int64  
    dtypes: float64(5), int64(15), object(1)
    memory usage: 3.5+ MB
    

보통 `describe()` 를 통해 기본적인 기술 통계값을 확인할 수 있습니다.<br/>
여기서는 중간값, 결측치, 왜도, 첨도까지 보기 위해 다음과 같이 코드를 작성하겠습니다.


```python
# 중간값, 결측치, 왜도, 첨도를 표시합니다.
df_stats = df.describe().T

median_results = []
skew_results = []
kurtosis_results = []
null_results = []

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
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>median</th>
      <th>missing</th>
      <th>skewness</th>
      <th>kurtosis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>id</th>
      <td>21613.0</td>
      <td>4.580302e+09</td>
      <td>2.876566e+09</td>
      <td>1.000102e+06</td>
      <td>2.123049e+09</td>
      <td>3.904930e+09</td>
      <td>7.308900e+09</td>
      <td>9.900000e+09</td>
      <td>3.904930e+09</td>
      <td>0</td>
      <td>0.243329</td>
      <td>-1.260542</td>
    </tr>
    <tr>
      <th>price</th>
      <td>21613.0</td>
      <td>5.400881e+05</td>
      <td>3.671272e+05</td>
      <td>7.500000e+04</td>
      <td>3.219500e+05</td>
      <td>4.500000e+05</td>
      <td>6.450000e+05</td>
      <td>7.700000e+06</td>
      <td>4.500000e+05</td>
      <td>0</td>
      <td>4.024069</td>
      <td>34.585540</td>
    </tr>
    <tr>
      <th>bedrooms</th>
      <td>21613.0</td>
      <td>3.370842e+00</td>
      <td>9.300618e-01</td>
      <td>0.000000e+00</td>
      <td>3.000000e+00</td>
      <td>3.000000e+00</td>
      <td>4.000000e+00</td>
      <td>3.300000e+01</td>
      <td>3.000000e+00</td>
      <td>0</td>
      <td>1.974300</td>
      <td>49.063653</td>
    </tr>
    <tr>
      <th>bathrooms</th>
      <td>21613.0</td>
      <td>2.114757e+00</td>
      <td>7.701632e-01</td>
      <td>0.000000e+00</td>
      <td>1.750000e+00</td>
      <td>2.250000e+00</td>
      <td>2.500000e+00</td>
      <td>8.000000e+00</td>
      <td>2.250000e+00</td>
      <td>0</td>
      <td>0.511108</td>
      <td>1.279902</td>
    </tr>
    <tr>
      <th>sqft_living</th>
      <td>21613.0</td>
      <td>2.079900e+03</td>
      <td>9.184409e+02</td>
      <td>2.900000e+02</td>
      <td>1.427000e+03</td>
      <td>1.910000e+03</td>
      <td>2.550000e+03</td>
      <td>1.354000e+04</td>
      <td>1.910000e+03</td>
      <td>0</td>
      <td>1.471555</td>
      <td>5.243093</td>
    </tr>
    <tr>
      <th>sqft_lot</th>
      <td>21613.0</td>
      <td>1.510697e+04</td>
      <td>4.142051e+04</td>
      <td>5.200000e+02</td>
      <td>5.040000e+03</td>
      <td>7.618000e+03</td>
      <td>1.068800e+04</td>
      <td>1.651359e+06</td>
      <td>7.618000e+03</td>
      <td>0</td>
      <td>13.060019</td>
      <td>285.077820</td>
    </tr>
    <tr>
      <th>floors</th>
      <td>21613.0</td>
      <td>1.494309e+00</td>
      <td>5.399889e-01</td>
      <td>1.000000e+00</td>
      <td>1.000000e+00</td>
      <td>1.500000e+00</td>
      <td>2.000000e+00</td>
      <td>3.500000e+00</td>
      <td>1.500000e+00</td>
      <td>0</td>
      <td>0.616177</td>
      <td>-0.484723</td>
    </tr>
    <tr>
      <th>waterfront</th>
      <td>21613.0</td>
      <td>7.541757e-03</td>
      <td>8.651720e-02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>1.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0</td>
      <td>11.385108</td>
      <td>127.632494</td>
    </tr>
    <tr>
      <th>view</th>
      <td>21613.0</td>
      <td>2.343034e-01</td>
      <td>7.663176e-01</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>4.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0</td>
      <td>3.395750</td>
      <td>10.893022</td>
    </tr>
    <tr>
      <th>condition</th>
      <td>21613.0</td>
      <td>3.409430e+00</td>
      <td>6.507430e-01</td>
      <td>1.000000e+00</td>
      <td>3.000000e+00</td>
      <td>3.000000e+00</td>
      <td>4.000000e+00</td>
      <td>5.000000e+00</td>
      <td>3.000000e+00</td>
      <td>0</td>
      <td>1.032805</td>
      <td>0.525764</td>
    </tr>
    <tr>
      <th>grade</th>
      <td>21613.0</td>
      <td>7.656873e+00</td>
      <td>1.175459e+00</td>
      <td>1.000000e+00</td>
      <td>7.000000e+00</td>
      <td>7.000000e+00</td>
      <td>8.000000e+00</td>
      <td>1.300000e+01</td>
      <td>7.000000e+00</td>
      <td>0</td>
      <td>0.771103</td>
      <td>1.190932</td>
    </tr>
    <tr>
      <th>sqft_above</th>
      <td>21613.0</td>
      <td>1.788391e+03</td>
      <td>8.280910e+02</td>
      <td>2.900000e+02</td>
      <td>1.190000e+03</td>
      <td>1.560000e+03</td>
      <td>2.210000e+03</td>
      <td>9.410000e+03</td>
      <td>1.560000e+03</td>
      <td>0</td>
      <td>1.446664</td>
      <td>3.402304</td>
    </tr>
    <tr>
      <th>sqft_basement</th>
      <td>21613.0</td>
      <td>2.915090e+02</td>
      <td>4.425750e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>5.600000e+02</td>
      <td>4.820000e+03</td>
      <td>0.000000e+00</td>
      <td>0</td>
      <td>1.577965</td>
      <td>2.715574</td>
    </tr>
    <tr>
      <th>yr_built</th>
      <td>21613.0</td>
      <td>1.971005e+03</td>
      <td>2.937341e+01</td>
      <td>1.900000e+03</td>
      <td>1.951000e+03</td>
      <td>1.975000e+03</td>
      <td>1.997000e+03</td>
      <td>2.015000e+03</td>
      <td>1.975000e+03</td>
      <td>0</td>
      <td>-0.469805</td>
      <td>-0.657408</td>
    </tr>
    <tr>
      <th>yr_renovated</th>
      <td>21613.0</td>
      <td>8.440226e+01</td>
      <td>4.016792e+02</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>2.015000e+03</td>
      <td>0.000000e+00</td>
      <td>0</td>
      <td>4.549493</td>
      <td>18.701152</td>
    </tr>
    <tr>
      <th>zipcode</th>
      <td>21613.0</td>
      <td>9.807794e+04</td>
      <td>5.350503e+01</td>
      <td>9.800100e+04</td>
      <td>9.803300e+04</td>
      <td>9.806500e+04</td>
      <td>9.811800e+04</td>
      <td>9.819900e+04</td>
      <td>9.806500e+04</td>
      <td>0</td>
      <td>0.405661</td>
      <td>-0.853479</td>
    </tr>
    <tr>
      <th>lat</th>
      <td>21613.0</td>
      <td>4.756005e+01</td>
      <td>1.385637e-01</td>
      <td>4.715590e+01</td>
      <td>4.747100e+01</td>
      <td>4.757180e+01</td>
      <td>4.767800e+01</td>
      <td>4.777760e+01</td>
      <td>4.757180e+01</td>
      <td>0</td>
      <td>-0.485270</td>
      <td>-0.676313</td>
    </tr>
    <tr>
      <th>long</th>
      <td>21613.0</td>
      <td>-1.222139e+02</td>
      <td>1.408283e-01</td>
      <td>-1.225190e+02</td>
      <td>-1.223280e+02</td>
      <td>-1.222300e+02</td>
      <td>-1.221250e+02</td>
      <td>-1.213150e+02</td>
      <td>-1.222300e+02</td>
      <td>0</td>
      <td>0.885053</td>
      <td>1.049501</td>
    </tr>
    <tr>
      <th>sqft_living15</th>
      <td>21613.0</td>
      <td>1.986552e+03</td>
      <td>6.853913e+02</td>
      <td>3.990000e+02</td>
      <td>1.490000e+03</td>
      <td>1.840000e+03</td>
      <td>2.360000e+03</td>
      <td>6.210000e+03</td>
      <td>1.840000e+03</td>
      <td>0</td>
      <td>1.108181</td>
      <td>1.597096</td>
    </tr>
    <tr>
      <th>sqft_lot15</th>
      <td>21613.0</td>
      <td>1.276846e+04</td>
      <td>2.730418e+04</td>
      <td>6.510000e+02</td>
      <td>5.100000e+03</td>
      <td>7.620000e+03</td>
      <td>1.008300e+04</td>
      <td>8.712000e+05</td>
      <td>7.620000e+03</td>
      <td>0</td>
      <td>9.506743</td>
      <td>150.763110</td>
    </tr>
  </tbody>
</table>
</div>



해당 결과값에서 종속 변수(타겟)인 price의 왜도 (skewness)가 4.02로 왼쪽으로 치우쳐 있는 것을 확인할 수 있다.</br>
자연로그를 활용하여 분포를 조정할 필요가 있다.


```python
df['price'].hist()
```




    <Axes: >




    
![png](output_10_1.png)
    



```python
np.log(df['price']).hist()
```




    <Axes: >




    
![png](output_11_1.png)
    



```python
np.log(df['price']).skew()
```




    0.42807247557592526



자연로그를 취해서 종속 변수(price)의 분포가 정규분포 형태를 띄는 것을 확인할 수 있다.(선형 회귀분석 시 자연로그를 적용할 계획이다.)

다음 함수를 통해 object 타입과 int64, float64 타입을 분류해서 데이터를 살펴보자.</br>
df_obj.head() 함수를 통해서 확인해보면 date의 전처리가 필요한 것을 알 수 있다.


```python
def separate_dtype(DataFrame:df):
    df_obj = df.select_dtypes(include=['object'])
    df_numr = df.select_dtypes(include=['int64','float64'])
    return [df_obj, df_numr]

(df_obj, df_numr) = separate_dtype(df)
```


```python
df_numr.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>price</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>sqft_living</th>
      <th>sqft_lot</th>
      <th>floors</th>
      <th>waterfront</th>
      <th>view</th>
      <th>condition</th>
      <th>grade</th>
      <th>sqft_above</th>
      <th>sqft_basement</th>
      <th>yr_built</th>
      <th>yr_renovated</th>
      <th>zipcode</th>
      <th>lat</th>
      <th>long</th>
      <th>sqft_living15</th>
      <th>sqft_lot15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>7129300520</td>
      <td>221900.0</td>
      <td>3</td>
      <td>1.00</td>
      <td>1180</td>
      <td>5650</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>7</td>
      <td>1180</td>
      <td>0</td>
      <td>1955</td>
      <td>0</td>
      <td>98178</td>
      <td>47.5112</td>
      <td>-122.257</td>
      <td>1340</td>
      <td>5650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6414100192</td>
      <td>538000.0</td>
      <td>3</td>
      <td>2.25</td>
      <td>2570</td>
      <td>7242</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>7</td>
      <td>2170</td>
      <td>400</td>
      <td>1951</td>
      <td>1991</td>
      <td>98125</td>
      <td>47.7210</td>
      <td>-122.319</td>
      <td>1690</td>
      <td>7639</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5631500400</td>
      <td>180000.0</td>
      <td>2</td>
      <td>1.00</td>
      <td>770</td>
      <td>10000</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>6</td>
      <td>770</td>
      <td>0</td>
      <td>1933</td>
      <td>0</td>
      <td>98028</td>
      <td>47.7379</td>
      <td>-122.233</td>
      <td>2720</td>
      <td>8062</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2487200875</td>
      <td>604000.0</td>
      <td>4</td>
      <td>3.00</td>
      <td>1960</td>
      <td>5000</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>7</td>
      <td>1050</td>
      <td>910</td>
      <td>1965</td>
      <td>0</td>
      <td>98136</td>
      <td>47.5208</td>
      <td>-122.393</td>
      <td>1360</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1954400510</td>
      <td>510000.0</td>
      <td>3</td>
      <td>2.00</td>
      <td>1680</td>
      <td>8080</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>8</td>
      <td>1680</td>
      <td>0</td>
      <td>1987</td>
      <td>0</td>
      <td>98074</td>
      <td>47.6168</td>
      <td>-122.045</td>
      <td>1800</td>
      <td>7503</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_obj.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>20141013T000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20141209T000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20150225T000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20141209T000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20150218T000000</td>
    </tr>
  </tbody>
</table>
</div>



date column을 앞에서 4자리만 추출하고 type을 int64로 변경하고 column명을 date2로 저장하자.


```python
df_obj['date2'] = df_obj['date'].apply(lambda x: x[0:4])
df['date2'] = df_obj['date2'].astype('int64')
df['date2']
```




    1        2014
    2        2014
    3        2015
    4        2014
    5        2015
             ... 
    21609    2014
    21610    2015
    21611    2014
    21612    2015
    21613    2014
    Name: date2, Length: 21613, dtype: int64



date2(집이 매각된 연도)와 yr_built(집이 지어진 연도)의 기간 차이를 비교해서 sold-built_years 라는 새로운 변수를 추가하자.


```python
df['sold-built_years'] = df.apply(lambda x:((x['date2']) - (x['yr_built'])), axis=1)
df['sold-built_years']
```




    1        59
    2        63
    3        82
    4        49
    5        28
             ..
    21609     5
    21610     1
    21611     5
    21612    11
    21613     6
    Name: sold-built_years, Length: 21613, dtype: int64



지금까지 데이터의 전체적인 파악 및 전처리를 했다.</br>
이제 시작화를 통해 데이터의 특징을 살펴보자.

히스토그램을 통해 각각의 독립 변수 데이터의 분포를 확인할 수 있다.


```python
df.hist(figsize=(22,18), density=True)
plt.show()
```


    
![png](output_22_0.png)
    


종속 변수(price)와 선형 관계가 있을 것 같은 독립 변수들을 선정하여 산점도(Scatter plot) 그래프를 그려보자.


```python
# 변수 선정
columns = ['price','bedrooms','sqft_living','waterfront','view','yr_built','sold-built_years','date2']


df_pairplot = df[columns]
sns.pairplot(df_pairplot)
plt.show()
```


    
![png](output_24_0.png)
    


산점도를 통해서 종속 변수(price)와 독립 변수들 사이의 선형 관계를 대략적으로 파악할 수 있다.</br>
특히, 다른 변수들과는 달리 price와 sqft_living 간의 선형 관계를 볼 수 있다.

히트맵(Heatmap)을 통해 종속 변수(price)와 상관관계가 높은 독립 변수들은 무엇인지 확인해보자.

또한, 독립 변수들 간에 상관관계가 높은 것들은 어떤 것인지 살펴본다.


```python
# 반대쪽 삼각형은 안 보이게 설정합니다.
# fmt -> 실제 값 표시, .2f -> 소수점 둘째 자리까지 표현

df_corr = df.corr()
cmap = sns.diverging_palette(240, 10, n=9, as_cmap=True)

mask = np.zeros_like(df_corr, dtype=bool)
mask[np.triu_indices_from(mask)] = True

plt.figure(figsize=(16,12))

sns.heatmap(df.corr(), annot=True, mask=mask, cmap=cmap, linewidths=.5, fmt='.2f', annot_kws={"size":10})
```




    <Axes: >




    
![png](output_26_1.png)
    


price와 상관관계가 높은 변수들만 추려서 확인합니다. </br>
정렬을 이용하면 편리합니다.


```python
df_corr.sort_values(by='price', ascending=False)[['price']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>price</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>sqft_living</th>
      <td>0.702035</td>
    </tr>
    <tr>
      <th>grade</th>
      <td>0.667434</td>
    </tr>
    <tr>
      <th>sqft_above</th>
      <td>0.605567</td>
    </tr>
    <tr>
      <th>sqft_living15</th>
      <td>0.585379</td>
    </tr>
    <tr>
      <th>bathrooms</th>
      <td>0.525138</td>
    </tr>
    <tr>
      <th>view</th>
      <td>0.397293</td>
    </tr>
    <tr>
      <th>sqft_basement</th>
      <td>0.323816</td>
    </tr>
    <tr>
      <th>bedrooms</th>
      <td>0.308350</td>
    </tr>
    <tr>
      <th>lat</th>
      <td>0.307003</td>
    </tr>
    <tr>
      <th>waterfront</th>
      <td>0.266369</td>
    </tr>
    <tr>
      <th>floors</th>
      <td>0.256794</td>
    </tr>
    <tr>
      <th>yr_renovated</th>
      <td>0.126434</td>
    </tr>
    <tr>
      <th>sqft_lot</th>
      <td>0.089661</td>
    </tr>
    <tr>
      <th>sqft_lot15</th>
      <td>0.082447</td>
    </tr>
    <tr>
      <th>yr_built</th>
      <td>0.054012</td>
    </tr>
    <tr>
      <th>condition</th>
      <td>0.036362</td>
    </tr>
    <tr>
      <th>long</th>
      <td>0.021626</td>
    </tr>
    <tr>
      <th>date2</th>
      <td>0.003576</td>
    </tr>
    <tr>
      <th>id</th>
      <td>-0.016762</td>
    </tr>
    <tr>
      <th>zipcode</th>
      <td>-0.053203</td>
    </tr>
    <tr>
      <th>sold-built_years</th>
      <td>-0.053951</td>
    </tr>
  </tbody>
</table>
</div>



독립 변수들 간의 상관관계를 확인해본 결과 </br>
`sqft_living`, `sqft_above`, `sqft_living15`
세 변수들이 상관관계가 높게 나왔다.

세 변수들의 데이터 분포를 살펴보자.

*grade의 경우 최종 결정되는 '등급' 값이라 등급으로 가격을 예측하는 것은 무의미하다고 판단*


```python
# column 선택
columns = ['sqft_living', 'sqft_living15', 'sqft_above']
colors = ['blue','green','red']

living = df[columns]

# 한 번에 보기
plt.figure(figsize=(12,6))

for i in range(3):
    ax = sns.distplot(df[columns[i]], hist=True, norm_hist=False, kde=False, label=columns[i], color=colors[i])
ax.set(xlabel="sqft_living / sqft_living15 / sqft_above")

plt.legend()
plt.show()
```


    
![png](output_30_0.png)
    


그림에서 볼 수 있듯이 세 변수들의 분포가 비슷하다는 것을 알 수 있습니다.</br>
따라서 다중공선성이 존재할 경우 이 중 price와 상관관계가 가장 높은 sqft_living 으로 분석합니다.

설명 변수(X) 1개, 반응 변수(y) 1개일 때 사용하는 대표적인 방법론으로 단순 선형 회귀분석이 있습니다.</br>
종속 변수(price)와 가장 상관관계가 높은 sqft_living 변수를 독립 변수로 단순 선형 회귀 분석을 실시합니다.

설명 변수(X)를 sqft_living으로 하고 반응 변수(y)로 price를 했을 때 두 변수 간의 선형관계를 확인해보자.


```python
sns.jointplot(x='sqft_living', y='price', data=df, kind='reg')
plt.show()
```


    
![png](output_32_0.png)
    


회귀분석을 할 때는 항상 상수항을 추가해야 합니다.</br>
add_constant 함수를 사용해서 상수항을 추가해 봅시다.


```python
X = df[['sqft_living']]
y = df[['price']]

# 상수항을 추가합니다
X = sm.add_constant(X, has_constant="add")
X.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>const</th>
      <th>sqft_living</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>1180</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2570</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>770</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
      <td>1960</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.0</td>
      <td>1680</td>
    </tr>
  </tbody>
</table>
</div>



fit() 함수를 통해 선형 모델에 적합시켜봅시다.

해당 결과를 result_model에 저장하고 summary() 함수를 통해서 결과를 확인합니다.


```python
# 모델 fit
model = sm.OLS(y, X)
result_model = model.fit()
result_model.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>price</td>      <th>  R-squared:         </th>  <td>   0.493</td>  
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th>  <td>   0.493</td>  
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th>  <td>2.100e+04</td> 
</tr>
<tr>
  <th>Date:</th>             <td>Sun, 01 Oct 2023</td> <th>  Prob (F-statistic):</th>   <td>  0.00</td>   
</tr>
<tr>
  <th>Time:</th>                 <td>20:26:49</td>     <th>  Log-Likelihood:    </th> <td>-3.0027e+05</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td> 21613</td>      <th>  AIC:               </th>  <td>6.005e+05</td> 
</tr>
<tr>
  <th>Df Residuals:</th>          <td> 21611</td>      <th>  BIC:               </th>  <td>6.006e+05</td> 
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>      <td> </td>     
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>      <td> </td>     
</tr>
</table>
<table class="simpletable">
<tr>
       <td></td>          <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>       <td>-4.358e+04</td> <td> 4402.690</td> <td>   -9.899</td> <td> 0.000</td> <td>-5.22e+04</td> <td> -3.5e+04</td>
</tr>
<tr>
  <th>sqft_living</th> <td>  280.6236</td> <td>    1.936</td> <td>  144.920</td> <td> 0.000</td> <td>  276.828</td> <td>  284.419</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>14832.490</td> <th>  Durbin-Watson:     </th>  <td>   1.983</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th>  <td> 0.000</td>   <th>  Jarque-Bera (JB):  </th> <td>546444.713</td>
</tr>
<tr>
  <th>Skew:</th>           <td> 2.824</td>   <th>  Prob(JB):          </th>  <td>    0.00</td> 
</tr>
<tr>
  <th>Kurtosis:</th>       <td>26.977</td>   <th>  Cond. No.          </th>  <td>5.63e+03</td> 
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 5.63e+03. This might indicate that there are<br/>strong multicollinearity or other numerical problems.



주요 항목별 세부 내용은 다음과 같습니다.

- Dep. Variable : 종속 변수, 타겟값.
- Model : 학습 모델 / OLS(Ordinary Least Squares), 잔차 제곱합(손실)을 최소로 하는 파라미터를 선택하는 방법
- Method : Least Squares / 잔차 제곱합(손실)을 최소로 하는 파라미터를 선택하는 방법
- No. Observation : 데이터셋 크기
- Df Residuals : 데이터셋 크기 - 추정된 파라미터 수를 뺀 것
- Df Model : 독립 변수의 숫자
- Covariance Type : 공분산 종류(default: nonrobust)
- R-squared : 결정계수, 모델의 설명력(0~1 사이 값), 1에 가까울수록 모델의 설명력이 높음
- Adj. R-squared : 조정된 결정계수, 조정된 모델의 설명력
- Std. error : 계수의 표준 오차
- F-statistic : F value
- Prob (F-statistic): p-value
- Log-Likelihood : 최대 로그 우도
- 아카이케 정보 기준(Akaike's Information Criterion; AIC) : 모델의 성능지표로 작을수록 좋은 모델
- Coef : 계수값
- P>|t| : p-value

P>|t|(p-value) 항목의 유의 확률이 유의 수준 0.05보다 훨씬 작아 유의 수준 0.05 이하에서 귀무 가설은 기각됩니다.

즉, 모형 통계학적 유의성이 확보됩니다.

시각화를 통해 실제 타겟값과 모델을 통해 추정한 값, 잔차(residual)를 확인해 봅시다.


```python
# 잔차를 확인합니다
result_model.resid.plot()
plt.show()
```


    
![png](output_39_0.png)
    


# 다중 선형 회귀


앞에서는 단순히 변수 하나만 가지고 단순 선형 회귀 모형을 돌렸습니다.

다중 선형 회귀 모형은 단순 선형 회귀모형의 확장으로, 연속형 반응변수 하나에 "설명 변수가 둘 이상"인 모형을 말합니다.
설명 변수가 늘어나므로 추가 검토해야 할 문제는 설명 변수 정보 중첩으로 발생하는 다중공선성(multicollinearlity) 문제와,
너무 많은 설명 변수를 포함해 발생하는 차원의 저주 문제 등이 있습니다.

이번에는 범주형 변수를 설명 변수로 포함한 회귀모형에 대해서도 논의할 것입니다.

id를 제외한 모든 독립 변수를 사용해서 다중 선형 회귀분석을 합니다.

그 후 선별한 독립 변수들로 다시 다중 선형 회귀분석을 해 봅시다.

>원래 뭐든 다 때려보고, 그 중 괜찮은 걸 고르는 것이 가장 속이 편합니다.


```python
# date의 경우 전처리를 한 column이 존재하기 때문에 제외
columns = list(df.columns)
not_used = ['id','date']

for item in not_used:
    columns.remove(item)
columns

```




    ['price',
     'bedrooms',
     'bathrooms',
     'sqft_living',
     'sqft_lot',
     'floors',
     'waterfront',
     'view',
     'condition',
     'grade',
     'sqft_above',
     'sqft_basement',
     'yr_built',
     'yr_renovated',
     'zipcode',
     'lat',
     'long',
     'sqft_living15',
     'sqft_lot15',
     'date2',
     'sold-built_years']




```python
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
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>price</td>      <th>  R-squared:         </th>  <td>   0.701</td>  
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th>  <td>   0.701</td>  
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th>  <td>   2816.</td>  
</tr>
<tr>
  <th>Date:</th>             <td>Sun, 01 Oct 2023</td> <th>  Prob (F-statistic):</th>   <td>  0.00</td>   
</tr>
<tr>
  <th>Time:</th>                 <td>20:27:24</td>     <th>  Log-Likelihood:    </th> <td>-2.9455e+05</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td> 21613</td>      <th>  AIC:               </th>  <td>5.891e+05</td> 
</tr>
<tr>
  <th>Df Residuals:</th>          <td> 21594</td>      <th>  BIC:               </th>  <td>5.893e+05</td> 
</tr>
<tr>
  <th>Df Model:</th>              <td>    18</td>      <th>                     </th>      <td> </td>     
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>      <td> </td>     
</tr>
</table>
<table class="simpletable">
<tr>
          <td></td>            <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>bathrooms</th>        <td> 4.125e+04</td> <td> 3245.693</td> <td>   12.710</td> <td> 0.000</td> <td> 3.49e+04</td> <td> 4.76e+04</td>
</tr>
<tr>
  <th>bedrooms</th>         <td>-3.598e+04</td> <td> 1887.302</td> <td>  -19.064</td> <td> 0.000</td> <td>-3.97e+04</td> <td>-3.23e+04</td>
</tr>
<tr>
  <th>condition</th>        <td> 2.767e+04</td> <td> 2348.964</td> <td>   11.781</td> <td> 0.000</td> <td> 2.31e+04</td> <td> 3.23e+04</td>
</tr>
<tr>
  <th>const</th>            <td> -5.46e+07</td> <td> 6.59e+06</td> <td>   -8.282</td> <td> 0.000</td> <td>-6.75e+07</td> <td>-4.17e+07</td>
</tr>
<tr>
  <th>date2</th>            <td> 1.938e+04</td> <td> 1952.650</td> <td>    9.926</td> <td> 0.000</td> <td> 1.56e+04</td> <td> 2.32e+04</td>
</tr>
<tr>
  <th>floors</th>           <td> 7322.7479</td> <td> 3587.535</td> <td>    2.041</td> <td> 0.041</td> <td>  290.915</td> <td> 1.44e+04</td>
</tr>
<tr>
  <th>grade</th>            <td>  9.61e+04</td> <td> 2147.594</td> <td>   44.750</td> <td> 0.000</td> <td> 9.19e+04</td> <td>    1e+05</td>
</tr>
<tr>
  <th>lat</th>              <td> 6.053e+05</td> <td> 1.07e+04</td> <td>   56.511</td> <td> 0.000</td> <td> 5.84e+05</td> <td> 6.26e+05</td>
</tr>
<tr>
  <th>long</th>             <td>-2.147e+05</td> <td> 1.31e+04</td> <td>  -16.387</td> <td> 0.000</td> <td> -2.4e+05</td> <td>-1.89e+05</td>
</tr>
<tr>
  <th>sold-built_years</th> <td>   1.1e+04</td> <td>  976.501</td> <td>   11.265</td> <td> 0.000</td> <td> 9086.329</td> <td> 1.29e+04</td>
</tr>
<tr>
  <th>sqft_above</th>       <td>   70.7647</td> <td>    2.248</td> <td>   31.481</td> <td> 0.000</td> <td>   66.359</td> <td>   75.171</td>
</tr>
<tr>
  <th>sqft_basement</th>    <td>   39.8440</td> <td>    2.640</td> <td>   15.092</td> <td> 0.000</td> <td>   34.669</td> <td>   45.019</td>
</tr>
<tr>
  <th>sqft_living</th>      <td>  110.6171</td> <td>    2.264</td> <td>   48.857</td> <td> 0.000</td> <td>  106.179</td> <td>  115.055</td>
</tr>
<tr>
  <th>sqft_living15</th>    <td>   21.7694</td> <td>    3.439</td> <td>    6.330</td> <td> 0.000</td> <td>   15.028</td> <td>   28.511</td>
</tr>
<tr>
  <th>sqft_lot</th>         <td>    0.1249</td> <td>    0.048</td> <td>    2.612</td> <td> 0.009</td> <td>    0.031</td> <td>    0.219</td>
</tr>
<tr>
  <th>sqft_lot15</th>       <td>   -0.3794</td> <td>    0.073</td> <td>   -5.191</td> <td> 0.000</td> <td>   -0.523</td> <td>   -0.236</td>
</tr>
<tr>
  <th>view</th>             <td> 5.251e+04</td> <td> 2135.068</td> <td>   24.596</td> <td> 0.000</td> <td> 4.83e+04</td> <td> 5.67e+04</td>
</tr>
<tr>
  <th>waterfront</th>       <td> 5.837e+05</td> <td> 1.73e+04</td> <td>   33.705</td> <td> 0.000</td> <td>  5.5e+05</td> <td> 6.18e+05</td>
</tr>
<tr>
  <th>yr_built</th>         <td> 8381.0850</td> <td>  977.490</td> <td>    8.574</td> <td> 0.000</td> <td> 6465.132</td> <td> 1.03e+04</td>
</tr>
<tr>
  <th>yr_renovated</th>     <td>   20.7777</td> <td>    3.648</td> <td>    5.696</td> <td> 0.000</td> <td>   13.628</td> <td>   27.928</td>
</tr>
<tr>
  <th>zipcode</th>          <td> -582.8028</td> <td>   32.905</td> <td>  -17.712</td> <td> 0.000</td> <td> -647.298</td> <td> -518.307</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>18432.447</td> <th>  Durbin-Watson:     </th>  <td>   1.992</td>  
</tr>
<tr>
  <th>Prob(Omnibus):</th>  <td> 0.000</td>   <th>  Jarque-Bera (JB):  </th> <td>1903378.131</td>
</tr>
<tr>
  <th>Skew:</th>           <td> 3.576</td>   <th>  Prob(JB):          </th>  <td>    0.00</td>  
</tr>
<tr>
  <th>Kurtosis:</th>       <td>48.414</td>   <th>  Cond. No.          </th>  <td>5.29e+17</td>  
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The smallest eigenvalue is 7.82e-22. This might indicate that there are<br/>strong multicollinearity problems or that the design matrix is singular.



결과를 보면 모든 독립 변수들의 p>|t| (p-value) 유의 확률이 유의 수준 0.05보다 훨씬 작아 모형 통계학적 유의성이 확인된다.</br>
R-squared 값이 0.701 로써 약 70%가 모형에 의해 설명된다는 것을 의미한다.

단순 선형 회귀와 달리 다중 선형 회귀분석에서는 모든 변수의 경우 **다중공선성(multicollinearlity)** 문제를 확인해야 한다.


```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

df_vif = pd.DataFrame()
df_vif["VIF"] = np.round([variance_inflation_factor(df_reg.values, i) for i in range(df_reg.shape[1])], 2)

df_vif["features"] = df_reg.columns
df_vif.sort_values(by='VIF', ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VIF</th>
      <th>features</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>inf</td>
      <td>sqft_above</td>
    </tr>
    <tr>
      <th>11</th>
      <td>inf</td>
      <td>sqft_basement</td>
    </tr>
    <tr>
      <th>19</th>
      <td>inf</td>
      <td>date2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>inf</td>
      <td>yr_built</td>
    </tr>
    <tr>
      <th>20</th>
      <td>inf</td>
      <td>sold-built_years</td>
    </tr>
    <tr>
      <th>3</th>
      <td>inf</td>
      <td>sqft_living</td>
    </tr>
    <tr>
      <th>14</th>
      <td>4922845.94</td>
      <td>zipcode</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1388182.32</td>
      <td>long</td>
    </tr>
    <tr>
      <th>15</th>
      <td>159610.79</td>
      <td>lat</td>
    </tr>
    <tr>
      <th>9</th>
      <td>162.17</td>
      <td>grade</td>
    </tr>
    <tr>
      <th>8</th>
      <td>35.37</td>
      <td>condition</td>
    </tr>
    <tr>
      <th>2</th>
      <td>28.83</td>
      <td>bathrooms</td>
    </tr>
    <tr>
      <th>17</th>
      <td>27.87</td>
      <td>sqft_living15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>23.75</td>
      <td>bedrooms</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17.36</td>
      <td>floors</td>
    </tr>
    <tr>
      <th>0</th>
      <td>10.56</td>
      <td>price</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2.61</td>
      <td>sqft_lot15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.38</td>
      <td>sqft_lot</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.61</td>
      <td>view</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.28</td>
      <td>waterfront</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1.20</td>
      <td>yr_renovated</td>
    </tr>
  </tbody>
</table>
</div>



설명 변수가 다수이기 때문에 모형에 포함된 설명 변수의 정보가 중첩(상관관계를 가짐)으로,

**다중공선성 문제가 발생하는 것을 확인할 수 있다.**

다음 독립 변수들을 선택해서 다중 선형 회귀분석을 실시해보자.

또한, 반응 변수(price)에 자연로그를 취해 비대칭인 데이터의 분포를 완화한 상태에서 회귀분석을 한다.

- bedrooms(연속형)
- sqrt_living(연속형)
- waterfront(범주형)
- view(범주형)
- sold-built_years : date - yr_built (연속형)


```python
df_reg = df[['bedrooms','sqft_living','waterfront','view','sold-built_years','price']]

df_kc_reg = sm.add_constant(df_reg, has_constant='add')
feature_columns = list(df_kc_reg.columns.difference(['price']))

X = df_kc_reg[feature_columns]
y = np.log(df_kc_reg.price)

# 회귀 모형
multi_linear_model = sm.OLS(y, X)
result_model_2 = multi_linear_model.fit()
result_model_2.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>price</td>      <th>  R-squared:         </th> <td>   0.529</td> 
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.529</td> 
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   4852.</td> 
</tr>
<tr>
  <th>Date:</th>             <td>Sun, 01 Oct 2023</td> <th>  Prob (F-statistic):</th>  <td>  0.00</td>  
</tr>
<tr>
  <th>Time:</th>                 <td>20:27:33</td>     <th>  Log-Likelihood:    </th> <td> -8675.5</td> 
</tr>
<tr>
  <th>No. Observations:</th>      <td> 21613</td>      <th>  AIC:               </th> <td>1.736e+04</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td> 21607</td>      <th>  BIC:               </th> <td>1.741e+04</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     5</td>      <th>                     </th>     <td> </td>    
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>    
</tr>
</table>
<table class="simpletable">
<tr>
          <td></td>            <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>bedrooms</th>         <td>   -0.0413</td> <td>    0.003</td> <td>  -12.647</td> <td> 0.000</td> <td>   -0.048</td> <td>   -0.035</td>
</tr>
<tr>
  <th>const</th>            <td>   12.1722</td> <td>    0.011</td> <td> 1128.098</td> <td> 0.000</td> <td>   12.151</td> <td>   12.193</td>
</tr>
<tr>
  <th>sold-built_years</th> <td>    0.0025</td> <td> 8.96e-05</td> <td>   27.564</td> <td> 0.000</td> <td>    0.002</td> <td>    0.003</td>
</tr>
<tr>
  <th>sqft_living</th>      <td>    0.0004</td> <td> 3.62e-06</td> <td>  117.929</td> <td> 0.000</td> <td>    0.000</td> <td>    0.000</td>
</tr>
<tr>
  <th>view</th>             <td>    0.0785</td> <td>    0.004</td> <td>   21.269</td> <td> 0.000</td> <td>    0.071</td> <td>    0.086</td>
</tr>
<tr>
  <th>waterfront</th>       <td>    0.2885</td> <td>    0.031</td> <td>    9.285</td> <td> 0.000</td> <td>    0.228</td> <td>    0.349</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>190.066</td> <th>  Durbin-Watson:     </th> <td>   1.956</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td> 215.753</td>
</tr>
<tr>
  <th>Skew:</th>          <td>-0.183</td>  <th>  Prob(JB):          </th> <td>1.41e-47</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 3.325</td>  <th>  Cond. No.          </th> <td>2.88e+04</td>
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 2.88e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.



결과를 보면 모든 독립 변수들의 P >|t| (p-value) 유의 확률이 유의 수준 0.05보다 훨씬 작아 모형 통계학적 유의성이 확인된다.

이제 다중공선성을 살펴보자.


```python
df_vif = pd.DataFrame()
df_vif["VIF"] = np.round([variance_inflation_factor(df_reg.values, i) for i in range(df_reg.shape[1])], 2)

df_vif["features"] = df_reg.columns
df_vif.sort_values(by='VIF', ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VIF</th>
      <th>features</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>19.32</td>
      <td>sqft_living</td>
    </tr>
    <tr>
      <th>0</th>
      <td>14.17</td>
      <td>bedrooms</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.56</td>
      <td>price</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.85</td>
      <td>sold-built_years</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.48</td>
      <td>view</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.24</td>
      <td>waterfront</td>
    </tr>
  </tbody>
</table>
</div>



다중공선성 문제가 확실히 줄어들었음을 알 수 있다.

# 회귀모형의 가정 진단

회귀모형은 반응 변수와 설명 변수의 선형 관계를 전제로 한다.</br>
또한 오차에 대한 독립성, 정규성, 등분산성 가정을 전제로 한다.

앞서 확인한 모형의 유의성과 계수의 유의성이 확보되었다고 해도, **오차에 대한 가정을 만족하지 않으면** 다른 대안을 찾아야 한다.

## 정규성 검정


```python
# 1. 정규성 검정

# Q-Q 도표
qqplot = sm.qqplot(result_model_2.resid, line="s")
```


    
![png](output_56_0.png)
    



```python
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
```




    Text(0, 0.5, 'Residual')




    
![png](output_57_1.png)
    



```python
# 샤피로 - 월크 검정
result_shapiro = stats.shapiro(result_model_2.resid)

print(f"F value : {result_shapiro[0]:.4f} / p-value : {result_shapiro[1]:.4f}")

if result_shapiro[1] < 0.05:
    print("p-value < 0.05 입니다.")
```

    F value : 0.9959 / p-value : 0.0000
    p-value < 0.05 입니다.
    

Q-Q 플롯, 잔차 패턴, 샤피로-윌크 검정을 통해 정규성을 만족하는 것을 확인할 수 있다.

샤피로-윌크 검정은 p-value < 0.05 이기 때문에 정규성을 만족한다고 할 수 있다.

## 독립성 검정


```python
# 잔차 그래프
result_model_2.resid.plot()
plt.show()
```


    
![png](output_61_0.png)
    



```python
# ACF (Auto-Correlation Function)
sm.graphics.tsa.plot_acf(result_model_2.resid)
plt.show()
```


    
![png](output_62_0.png)
    


잔차 그래프와 ACF를 이용해 독립성 만족 여부를 확인할 수 있다.

ACF 그래프에서 0시차 이후에 파란색 구간을 벗어나는 시차가 존재하지 않다고 보이기 때문에 독립성을 만족한다고 볼 수 있다.

## 등분산성


```python
sns.distplot(result_model_2.resid)
plt.show()
```


    
![png](output_65_0.png)
    



```python
result_model_2.resid.plot()
plt.show()
```


    
![png](output_66_0.png)
    


잔차 그래프를 통해서 오차의 등분산성 가정을 만족하는 것을 확인할 수 있다.

<새롭게 알게된 점>
다중회귀모델의 설명력, p값, 다중공선성 문제를 해결하면
자연스레 잔차의 정규성, 등분산성, 독립성 문제가 해결된다고 알고 있었는데
이와는 별개로 확인을 해봐야 한다는 사실을 알게 되었다.

코드를 다 돌려보긴 했지만, 확실히 암기하고 손에 익으려면 다른 데이터를 가지고 클론 코딩을 한번 해봐야겠다고 느꼈다.



```python

```
