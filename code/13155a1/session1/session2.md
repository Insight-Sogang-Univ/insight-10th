# INSIGHT 2주차 교육 세션: 읽기, 전처리
📌 키워드: 절대경로/상대경로, read file in python, preprocessing in data science

## 절대경로 / 상대 경로
### ◼️ 절대경로
: root부터 시작하여 목적지까지의 전체적인 경로

예시) C:\Program Files\Git

### ◼️ 상대 경로
: 현재 디렉터리를 기준으로 표현되는 경로
- . : 현재 디렉터리
- .. : 상위 디렉터리
- 이름 : 하위 디렉터리

예시) ../test.py -> 현재 디렉터리의 상위 폴더의 test.py라는 파일을 가리킴

### ◼️ 디렉터리 변경/ 확인 및 파일 속성 관련 함수
- os.getcwd(): 현재 작업 디렉터리
- os.chidr(path): 디렉터리 변경
- os.mkdir(path): 디렉터리 생성

## Read file in python
| File Format | Reader | Writer |
| --- | --- | --- |
| CSV | read_csv | to_csv |
| JSON | read_json | to_json |
| HTML | read_html | to_html |
| MS EXCEL | read_excel | to_excel |
| SQL | read_sql | to_sql |

## Preprocessing in data science
:데이터를 분석 및 처리에 적합한 형태로 만드는 과정

### 🎈 데이터 전처리 과정
1. 데이터 세트 확인
2. 결측값 처리
3. 이상값 처리
4. 변수 가공

### 1. 데이터 세트 확인
- 데이터 변수 확인 (변수 정의, 변수 유형, 변수 데이터 형식)
- 원시(RAW) 데이터 확인

### 2. 결측값 처리
- 결측값: 데이터를 수집하고 입력하는 과정에서 누락되는 값
- 결측값 확인: info(), value_counts(dropna=False), df.isnull().sum(), notnull()
- 결측값 처리: 삭제, 대체

### 3. 이상값 처리
- 이상치: 기존 데이터들과 거리가 먼 데이터
- 이상치 확인: df.describe(), 시각화(BoxPlot), Z-score, Tukey Fences
- 이상치 처리: 전체 삭제, 대체, 변수화, 리샘플링

### 4. 변수 가공
: 새로운 데이터 또는 변수의 추가 없이 기존의 데이터를 보다 유용하게 만드는 방법

- 구간화(binning)
- 더미 변수
- 변환
- 스케일링(StandardScaler, MinMaxScaler, RobustScaler)