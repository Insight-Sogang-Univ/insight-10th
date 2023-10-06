# Session2 사전 과제 - 국필호
## 키워드
- 절대경로, 상대경로, 
- read file in python
- preprocessing in data science
--------
### 절대경로와 상대경로

1. 절대경로와 상대 경로
   - 데이터 입출력을 이해하는데 필요한 개념이다.

2. 배경지식

    파일은 경로(Dir name)와 파일 이름(Base name)으로 구성되어 저장된다.

        ex) text file
         C:/Users/UserID/...../text.txt

    이때,C:/Users/UserID/..... 는 경로이고, text.txt 는 파일의 이름이다. 

3. 절대 경로
   
   절대경로는 정적인 문자열로 특정 컴퓨터의 파일 위치를 정확히 알려준다. 다시 말해, 처음 (파일의 root)로부터 목적지(위의 예시라면 text.txt일 것이다)까지의 전체적인 경로(URL)를 의미한다.

         C:/Users/UserID/...../
    
4. 상대경로

    현재 디렉토리를 기준으로 상위, 하위 디렉토리를 이동하며 표현되는 경로이다.

    즉, 절대경로의 특징 중 하나인 최상위 / 를 거쳐야하는 번거로움에서 벗어날 수 있다.

    - . : 현재 디렉터리
    - .. : 상위 디렉터리
    - 이름 : 하위 디렉터리

        ex) 현재 작업 디렉터리가 /content/drive/MyDrive/MyPythonFiles/TextFiles/A 인 경우

            절대경로 : /content/drive/MyDrive/MyPythonFiles/

            상대경로 : '../../../MyPythonFiles/

---
### Read file in python

1. File Format 에 따른 Reader 함수

        CSV :       read_csv
        JSON :      read_json
        HTML :      read_html
        MS EXCEL :  read_excel
        SQL :       read_sql

2. File 들의 특징

* **CSV**
  - 데이터 값을 쉼표(,)로 구분하고 있는 텍스트 파일

  - 데이터의 크기가 작고 압축이 용이하기 때문에 가장 널리 사용되는 데이터 형식

        약자 : Comma Separated Value
        메모장과 엑셀로 열 수 있음
        참고 : tsv : tab separated value, tab 으로 구분되어 있는 data

* **EXCEL**
  -  행과 열이 데이터프레임의 행, 열로 일대일 대응
  -  
        여러 개의 시트로 구성데이터 불러올 때 불러올 시트 설정 가능 (이때 list로 받으면 된다)
        Ex) sheet_name=['Sheet 1', 'Sheet 2']{'Sheet 1' : 데이터프레임1, 'Sheet 2' : 데이터프레임2}인 dictionary 타입으로 return 

* CSV 와 EXCEL 모두 pandas 를 통해서 DataFrame 형식으로 Read 가능

        index_col : 불러온 data 중 하나의 column = 인덱스

        useclos : data 중 원하는 column만 선별하여 불러온다.
        - 메모리 절약 이점

---
### Preprocessing in data science


**Definition**

- **데이터 정제(leansing)**
  
  : 데이터에서 누락된 결측값을 보완하고 튀는 값을 이상값으로 제거해 데이터를 깨끗하게 만드는 기술

- **데이터 변환(Transformation)** 

    : 데이터 분석을 보다 쉽게 하기 위해 데이터를 변환해 일관성을 확보하고 데이터의 중복을 최소화해 데이터 분석 시간을 절약하는 기술

- **데이터 필터링(Filtering)** 

    : 데이터의 오류를 발견하고 삭제 및 보정을 통해 데이터의 품질 향상시키는 기술

- **데이터 통합(Integration)** 

    : 데이터 분석을 수월하게 하기 위해 유사한 성질의 데이터를 연계하는 등 데이터를 통합하는 기술



**Processing**
- 데이터 확인 -> 결측값 처리 -> 이상값 처리 -> 변수 가공

---

1. 데이터 확인
- 분석하고자하는 데이터를 확인하여 변수를 정의하는 과정이다.
- 이때 변수는 양적 수치형, 질적 범주형 변수가 있다.

2. 결측값 처리
- 데이터를 수집하고 입력하는 과정에서 누락되는 값을 의미한다.
- 필요한 이유
    - 데이터의 시각적 표현에 문제 발생
    - 변수 간 관계 왜곡의 가능성

3. 이상값 처리
- 이상치(Outlier)란 기존 데이터들과 거리가 먼 데이터
- 방법
    - 전체 삭제
    - 다른 값으로의 대체
    - 변수화
    - 리샘플링

4. 변수 가공
- 변수 가공이란 도메인 지식 + 기존의 변수 -> 기존 데이터에 정보를 추가하는 일련의 과정
- 데이터 전처리의 마지막 단계로서 기존의 데이터를 보다 유용하게 만드는 방법이다.

- 특징
    - 구간화 : 연속된 데이터를 의도적으로 구간을 나누어 분석한다
    - 더미 변수 : 범주형 변수를 연속형 변수로 변환하고 인식 가능한 입력값으로 변환하는 과정이다.
    - 변환 : 기존의 데이터를 다른 정보를 이용해 다른 데이터로 변환 및 분석하기 위한 과정
    - 스케일링 : 숫자의 상대적 크기로 인한 결과의 왜곡 방지를 위한 과정(StandardScaler, MinMaxScaler, RobustScaler)