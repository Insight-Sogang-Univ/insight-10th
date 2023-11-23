# 데이터 읽기, 전처리 정리

## 데이터 읽기

### 절대경로와 상대경로

절대경로
- 처음(파일의 root)부터 시작하여 목적지까지의 전체적인 경로(URL)를 의미
- 절대적이므로, 보통 다른 사람의 문서 or 파일을 이용할 때 사용
- 최상위 /를 포함

상대경로
- 현재 디렉터리를 기준으로 상위, 하위 디렉터리를 이동하며 표현되는 경로
- 최상위 /를 거치지 않고도 이동 가능

디렉터리 관련 함수 (os모듈)
1. os.getcwd() : 현재 사용하는 디렉터리 알기
2. os.chidr(path) : path로 디렉터리 변경
3. os.mkdir(path) : path 디렉터리 생성

### 데이터 입출력

파일 형식 별 데이터 읽기(read_) / 쓰기(to_)
- csv : read_csv / to_csv
- json : read_json / to_csv
- html : read_html / to_html
- ms excel : read_excel / to_excel
- sql : read_sql / to_sql


csv와 excel 파일은 pandas 이용하여 데이터프레임으로 읽기 가능
- pd.read_csv | pd.read_excel('파일경로/파일.xlsx', index_col=0)


utf-8 방식 인코딩 오류 발생 시, CP949 옵션 지정
- pd.read_csv('파일경로/파일.csv', index_col=0, encoding='CP949')

## 데이터 전처리

### 데이터 전처리

- 의미 : 데이터를 모델링에 필요한 변수로 만드는 과정
- 방법 : 데이터 정제 / 변환 / 필터링 / 통합

### 데이터 전처리 과정

- 과정 : 데이터 확인 -> 결측값 처리 -> 이상값 처리 -> 변수 가공

#1. 데이터 확인 
- 데이터 변수 확인 : 변수 정의 확인 / 변수 유형 확인 / 변수 데이터 형식 확인
- 로데이터 확인 : 데이터 분포를 보고 전처리 아이디어를 얻을 수 있음

#2. 결측값(=데이터 수집 및 입력 시 누락되는 값) 처리
- 처리 이유 : 시각적 표현에 문제 발생 / 변수 간 관계 왜곡
* 누락 데이터 확인하는법 : info(), value_counts(dropna=False), isnull(), notnull()
* 결측값 처리 방법 : 삭제 / 대체(1. 일괄대체, 2. 유사 유형 대체)

#3. 이상값(=기존 데이터들과 거리가 먼 데이터) 처리
- 이상값 확인 방법 3가지 : describe() / boxplot으로 시각화 / Z-score로 판단 / Turkey Fences(사분위범위 이용)
* 이상치 처리 방법 : 전체 삭제 / 다른 값으로 대체 / 변수화 / 리샘플링

#4. 변수 가공
- 의미 : 도메인 지식과 기존의 변수를 사용해서 기존의 데이터에 정보를 추가하는 일련의 과정
* 방법 : 구간화 / 더미 변수(명목변수) / 변환 / 스케일링(정규화)
