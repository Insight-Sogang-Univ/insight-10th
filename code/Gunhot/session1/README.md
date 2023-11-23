# 데이터 읽기 + 전처리
## <u> EDA 들어가기 전 과정</u>

### 참고 : EDA란...

<em> EDA(Exploratory Data Analysis, 탐색적 데이터 분석)</em>
<li>
EDA는 "탐색적 데이터 분석"의 약자로, 데이터를 이해하고 관찰하는 과정을 의미한다. EDA는 데이터 과학 및 데이터 분석 작업의 첫 번째 중요한 단계 중 하나이며, 주어진 데이터 세트의 특성, 구조, 패턴 등을 파악하는 데 사용됩니다. 다음은 EDA의 주요 요소와 목표다.
</li>

<ol>
<li>
데이터 이해: 데이터를 수집하고, 데이터의 특성 및 구조를 이해한다. 데이터가 어떤 형태인지, 어떤 변수가 있는지, 각 변수가 어떤 종류의 데이터를 포함하고 있는지 등을 파악한다.
</li>
<li>
데이터 시각화: 데이터를 시각화하여 그래프, 플롯, 차트 등을 통해 데이터 패턴을 시각적으로 파악한다. 이를 통해 데이터의 분포, 이상치, 상관 관계 등을 발견할 수 있다
</li>
<li>
통계 분석: 기술 통계량을 계산하고, 데이터의 중심 경향 및 분산을 파악한다. 평균, 중앙값, 표준 편차 등을 계산하여 데이터의 대략적인 특성을 이해한다.
</li>
<li>
상관 분석: 변수 간의 상관 관계를 파악하고, 이를 통해 변수 간의 연관성을 이해한다. 상관 분석은 두 변수 사이의 선형 관계를 측정한다.
</li>
<li>
이상치 탐지: 이상치(Outlier)를 식별하고 처리한다. 이상치는 데이터의 정상적인 패턴에서 벗어난 값을 의미하며, 분석 결과에 부정적인 영향을 미칠 수 있다
</li>
<li>
결측치 처리: 결측치(Missing Value)를 확인하고 적절한 처리 방법을 결정한다. 결측치는 데이터에 누락된 값이 있는 경우를 의미한다.
</li>
<li>
가설 검정: 데이터를 사용하여 가설을 검정하고 통계적 유의성을 확인한다. 예를 들어, 두 그룹 간의 차이가 통계적으로 유의미한지 확인할 수 있다
</li>
<li>
모델링 준비: EDA는 데이터 분석 및 머신 러닝 모델링을 위한 데이터의 전처리 및 준비를 포함한다. 이상치 처리, 변수 선택, 스케일링 등의 작업을 수행할 수 있다
</li>
<li>
EDA를 통해 데이터의 특성을 이해하고 데이터 과학 또는 머신 러닝 프로젝트를 진행하기 위한 기반을 마련한다. 데이터 분석가나 데이터 과학자는 EDA를 통해 데이터를 탐색하고 문제를 정의하며 모델링에 대한 초기 가정을 설정할 수 있다
</li>
</ol>




# 경로
<li> 전체 경로: 바닥부터</li>
<li> 상대 경로: 현재부터</li>

## 내 경로가 어디지? <u>-> os.getcwd()</u>

# (읽는 법, 쓰는 법)
<li>
CSV: (read_csv,	to_csv)
<ol>
예시 -> pandas.read_csv("파일경로(이름).csv")
</ol>
<ol>
<li>
<u>인덱스 설정</u> : pd.read_csv('./~~~~.csv',index_col=0).head()
</li>
<li>
<u>일부 인덱스만</u> : pd.read_csv('data/SeoulFloating.csv',usecols=['date','hour']).head()
</li>
<li>
<u>인코딩 설정</u> : df=pd.read_csv('경로/파일명.csv',encoding='CP949')
</li>
</ol>
</li>

<li>
JSON:	(read_json,	to_json)
</li>
<li>
HTML:	(read_html,	to_html)
</li>
<li>
MS EXCEL:	(read_excel,	to_excel)
<ol>
예시 -> pd.read_excel("파일경로.xlsx", engine = 'openpyxl')
</ol>
<ol>
예시 -> pd.read_excel('./지하철 승하차 인원 정보.xlsx',sheet_name='20년 2월')
</ol>
<ol>
예시 -> pd.read_excel('./지하철 승하차 인원 정보.xlsx',sheet_name=['Sheet 1', 'Sheet 2'])
</ol>
<li>
SQL:	(read_sql,	to_sql)
</li>

# 데이터 전처리
## 전처리란?
<ol>

**데이터 정제(Cleansing)**
<ol>
<li>
데이터에서 누락된 결측값을 보완하고 튀는 값을 이상값으로 제거
</li>
</ol>

**데이터 변환(Transformation)** 
<ol>
<li>데이터 분석을 보다 쉽게 하기 위해 데이터를 변환
</li>
<li>일관성을 확보하고 데이터의 중복을 최소화 -> 데이터 분석 시간을 절약
</li>
</ol>


**데이터 필터링(Filtering)** 
<ol>
<li> 
데이터의 오류를 발견하고 삭제 및 보정 -> 데이터의 품질 향상
</li>
</ol>

**데이터 통합(Integration)** 
<ol>
<li>
유사한 성질의 데이터를 연계(데이터를 통합) -> 데이터 분석을 수월 
</li>
</ol>
</ol>


## 데이터 세트 확인!
<ol>

**변수 정의 확인**
<ol>
<li>
어떤 정보를 가지는 변수인지 확인
</li>
</ol>

**변수 유형 확인** 
<ol>
<li>
질적·범주형(Categorical Data)과 양적·수치형(Numerical Data)으로 구분, 양적·수치형 데이터 중 트랜드가 보이면 연속형, 트렌드가 없다면 이산형으로 구분
</li>
</ol>

**변수 데이터 형식 확인**
<ol>
<li>
날짜, 수치, 텍스트, 이미지 등의 구분
</li>
</ol>
</ol>

## 결측값 확인
<ol>
<li>결측값이란? 데이터를 수집하고 입력하는 과정에서 누락되는 값</li>
<li>왜? 
<ol>
<li>
- 데이터의 시각적 표현에 문제 발생
</li>
<li>
- 변수 간 관계 왜곡 가능성
</li>
</ol></li>
<li>
누락데이터 확인
<ol>
<li>
info()
</li>
<li>
value_counts(dropna=False)
</li>
<li>
notnull()
isnull()
</li>
</ol>
</li>
<li>
삭제 및 대체
<ol>
<li>
df.dropna(axis=1, thresh=500)
</li>
<li>
df["열1"].fillna(a, inplace=True)
</li>
<li>
df['Value'] = df.groupby('Category')['Value'].apply(lambda x: x.fillna(x.mean()))
</li>
<li>
df["열2"].fillna(method="ffill", inplace=True)
</li>
<li>
df["열3"].fillna(method="bfill", inplace=True).
</li>
</ol>
</li>
</ol>














