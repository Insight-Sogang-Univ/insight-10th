# 1. 데이터 읽기
## 1)절대경로/상대경로
### - 절대 경로
처음부터 목적지까지의 전체 경로 - 절대적 <br>
**최상위 /** 포함
<br>
### - 상대 경로
현재 디렉터리 기준 상하위 디렉터리로 이동 시 사용
- 상위 : .. <br>
- 하위 : 이름<br>
- 현재 : .
<br>

### - 디렉 변경/확인/ 속성 함수
- os.getcwd() : **현재 사용 중인 디렉터리**
- os.chirdr(path) : **디렉터리 변경**
- os.mkdir(path) :**디렉터리 생성**

## 2)데이터 파일 형식에 따른 입출력
### [1] CSV - 쉼표로 구분하는 텍스트 파일
cf. TSV - 탭으로 구분되어 있는 데이터

```python
pandas.read_csv("파일경로(이름).csv")
```

### [2] EXCEL 파일 - 행과 열이 데이터프레임의 행, 열로 일대일 대응
- 시트 설정 가능 / list 이용해 여러 시트 입력 <br>
ex) sheet_name = ['시트1', '시트2'] <br>
    => dict 타입으로 반환 {'시트1' : df1 , '시트2' : df2}
    
```python
pd.read_excel("파일경로.xlsx", engine = 'openpyxl') # 확장자일 경우
pd.read_excel('./지하철 승하차 인원 정보.xlsx',sheet_name='20년 2월')
# sheet1 = 0 으로, sheet2 = 1로 표현 가능
```

### [3] Pandas를 통한 DF형식으로 읽기
- index_col : 하나의 칼럼을 인덱스로 <br>
pd.read_csv('경로/../파일명.csv', index_col = 0)
- usecols : 원하는 칼럼만 선별 <br>
pd.read_csv('경로/../파일명.csv', usecols=['col1','col2]) <br>
=> 메모리 절약 가능 

### +) 인코딩 시 오류 
**인코딩 방식 지정**해서 해결 <br>
df = pd.read_csv('경로/../파일명.csv', **encoding = 'CP949'**)




# 2. 데이터 전처리
## [1] 전처리?
- 데이터 정제 
누락된 결측값 보완, 이상값 제거

- 데이터 변환
데이터 일관성 확보 및 중복 최소화를 통한 분석 시간 절약

- 데이터 필터링
오류 발견 후 삭제 및 보정을 통한 품질 향상

- 데이터 통합 
유사 성질 데이터 연계 등의 데이터 기술 

## [2] 전처리 과정
데이터 세트 확인 > 결측값/이상값 처리 > 변수 가공(for 유용한 정보 추가)

## [3] 데이터 셋 확인
- 데이터 변수 확인
### 1) 변수 정의 확인 
어떤 정보를 갖는 변수인지
### 2) 변수 유형 확인
- 질적-범주형
- 양적-수치형 : 트렌드 O > 연속형 / 트렌드 X > 이산형
### 3) 변수 데이터 형식 확인 
날짜, 수치, 텍스트, 이미지 등의 구분
<br>
- 원시 RAW 데이터 확인
단변수 분석 : 원시 데이터의 평균값/최빈값/중간값 등 변수를 그래프를 통해 단변수 분포를 확인해 분석 가능 <br>
=> **전처리 아이디어** 얻을 수 있음 

    
## [4] 결측값 처리
### 1) 결측값?
- 데이터 수집/입력 과정에서 누락되는 값 <br>
**왜 결측값을 처리 하나요?**<br>
시각화 시 문제 및 변수 간 관계 왜곡 문제 방지

### 2) 누락 데이터 확인
- info()<br>
각 열의 유효한 값 개수 출력<br>
- value_counts(dropna=False)<br>
각 열의 결측값 포함 전체 데이터<br>
- isnull()<br>
누락 데이터 = True / 유효 데이터 = False <br>
- notnull()<br>
누락 데이터 = False / 유효 데이터 = True<br>
<br>
+) 결측값 NaN으로 표시 안 될 때 
df.replace('?', np.nan, inplace="True")
<br>
### 3) 결측값 처리 방법
#### 가. 삭제
- 전체 삭제 : 결측값 발생한 전체 관측치 삭제<br>
편리 but 관측치 감소로 인한 유효성 하락<br><br>

- 부분 삭제 : 모델에 포함할 변수 중 결측값 발생한 모든 관측치 삭제<br>
모델에 따라 달라지는 변수로 **Cost** 증가<br><br>

- 열 삭제 : 특성(변수) 삭제<br><br>
- 행 삭제 : 관측값(레코드) 삭제 <br><br>
cf. **임계점 설정** 가능 by **thresh** 옵션 <br>
```python
# thresh 옵션을 적용하여 임계값 설정이 가능!
# NaN 값이 500개 이상인 열을 모두 삭제
df.dropna(axis=1, thresh=500)
```
<br>
결측값이 무작위로 발생한 경우에만 **삭제**사용 for 왜곡된 모델 생성 방지
<br>

#### 나. 대체
**1.일괄 대체**<br>
모든 변수의 평균값 구해 일괄 대체<br>

```python
a = df["열1"].mean(axis=0)
df["열1"].fillna(a, inplace=True)
```
**2.유사 유형 대체**<br>
유사한 유형의 평균값으로 대체
```python
# 범주별로 그룹화하여 평균값 계산
category_means = df.groupby('Category')['Value'].mean()

# 결측값을 범주의 평균값으로 대체
df['Value'] = df.groupby('Category')['Value'].apply(lambda x: x.fillna(x.mean()))
```
<br>
+) 이웃값으로 치환 가능
<br>

- NaN이 있는 바로 직전 행에 있는 값 <br>
df["열2"].fillna(method="ffill", inplace=True)<br>
- NaN이 있는 바로 다음 행에 있는 값<br>
df["열3"].fillna(method="bfill", inplace=True).<br>

<br>

<br>


## [5] 이상값 처리

### 1) 이상치?
기존 데이터와 거리가 먼 데이터
### 2) 이상치 확인
- df.describe()<br>
- 시각화 (BoxPlot) : 직관적 but 자의적 판단 반영 가능성 및 수치 확인 번거로움<br>
- Z-score ; 표준 편차만큼 벗어나있는 정도로 처리<br>
- Tukey Fences : 사분위 범위(IQR)기준 두 가지 경우 이상치 판단
    1. Q1 - (1.5 * IQR) 미만<br>
    2. Q3 + (1.5 * IQR) 초과<br>
<br>
### 3) 이상치 처리
### 가. 전체 삭제
- humon error에 의한 경우<br>
- 단순 오타, 비현실적 응답, 처리 과정 중 오류 <br>
### 나. 다른 값으로 대체
- 절대적 관측치의 숫자가 작은 경우 -> 단순 삭제 시 절대량 감소로 인한 신뢰서 문제 발생<br>
- 다른 값으로 **대체**하거나 예측 모델을 통한 **예측값**으로 대체<br>
### 다. 변수화 
- 이상 값이 **자연 발생**한 경우<br>
    > 삭제/대체의 방법은 설명/예측하고자 하는 현상 설명 어려움<br>
- 즉각적 삭제보단, 이상값에 대한 **파악**이 중요<br>    
### 라. 리샘플링
- 해당 이상값을 **분리**하여 모델 생성
- 이상값 제외 모델과 포함 모델 생성 후 각 모델에 대한 설명 제시
*특이점을 발견하지 못했다면 **케이스 분리 후 분석**

## [6] 변수 가공
- 도메인 지식 + 기존 변수 > 기존 데이터에 정보 추가 과정<br>
추가적인 데이터 및 변수 추가 없이 기존 데이터 유용성▲<br>

### 1) 구간화 
- 일정 구간으로 나누어 분석<br>
but 원칙/규칙 없으므로 분석 목적에 따른 도메인 지식 활용<br>

### 2) 더미 변수
- 범주형을 **연속형 변수**로 변환 <br>
= 더미 변수(숫자 0 or 1) 사용, 단순 특성의 유무 보여줌<br>

### 3) 변환
- 기존 데이터 특성 및 다른 정보 활용을 통한 다 데이터로의 변환 및 분석<br>
데이터 특성 이해도에 따라 다양한 데이터 생성 가능

### 4) 스케일링
- for 상대적 크기 차이로 인한 결과 왜곡 방지를 위한 정규화<br>
- 변수 단위 변경 / 분포 편향 + 변수 간 관계 파악 어려움 > 변수 변환 방법 사용<br>
- 주로 log 함수 / Square root 사용<br>
- 라이브러리 임포트<br>
**from sklearn, preprocessing import StandardScaler, MinMaxScaler, QuantileTransformer, RobustScaler**<br>

#### 가. StandardScaler
feature의 **평균 = 0, 분산 = 1로 변경** > 모든 특성이 **같은 스케일**가짐<br>
=> **정규분포**를 따른다고 가정하는 기술<br>


```python
standard_scaler = StandardScaler()
scaled_data['열1'] = standard_scaler.fit_transform(scaled_data[['열1']])
```

#### 나.MinMaxScaler
모든 feature가 **0과 1사이에 위치**하게 함<br>
2차원 데이터셋 > 각 x, y축의 0과 1사이에 위치 <br>
=> **서로 다른 비율 속성**으로 구성된 걸 **같은 비율 속성**으로<br>
=> **연산 속도 향상** 및 알고리즘 **최적화**


```python
scaler = MinMaxScaler(feature_range=(0,1))
```

#### 다. RobustScaler
모든 특성이 **같은 크기** but 평균/분산 대신 **median과 quartile(사분위수)** 사용<br>
**이상치에 영향 X**

