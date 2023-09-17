# 절대경로, 상대경로란?

 : 파일 및 디렉토리 위치를 참조하는 데에 사용되는 두 경로 지정 방법

### 절대경로
* 파일, 디렉토리의 위치를 __최상위 디렉토리__ 부터 정확하게 나타내는 경로
</br>=> 항상 고정되어 있음
* ex) C:\Users\Username\Documents\file.txt

### 상대경로
* 파일, 디렉토리의 위치를 __현재 작업 디렉토리__ 를 기준으로 나타내는 경로
</br>=> 현재 위치에 따라 달라짐
* ex) 현재 작업 디렉토리가 C:\Users\Username\Documents 라면,
</br>file.txt는 ./file.txt로 표현됨

# read file in python이란?
 : python에서 파일을 읽는 작업

### open()으로 파일 열기
file = open('경로', '읽어들일 방식')

이 때 읽어들일 방식은 아래와 같이 지정할 수 있음
* 'r' (읽기 모드 - Read): 읽기 전용. 파일이 없으면 오류 발생

* 'w' (쓰기 모드 - Write): 쓰기 전용. 파일이 이미 존재하면 내용이 지워지고, 파일이 없으면 새로 생성됨

* 'x' (새로고침 모드 - Exclusive creation): 쓰기 전용. 파일이 이미 존재하면 FileExistsError 발생

* 'a' (추가 모드 - Append): 쓰기 전용. 파일이 이미 존재하면 내용이 유지되고, 파일의 끝에 내용을 추가할 수 있음.

* 'b' (바이너리 모드 - Binary): 바이너리 모드. 텍스트 파일 대신 이진 파일을 다룰 수 있음. 예: 'rb' 또는 'wb'.

* 't' (텍스트 모드 - Text): 텍스트 모드. 이 모드가 기본값이며 텍스트 파일을 다룰 때 사용. 예: 'rt' 또는 'wt'.

* '+' (읽기 및 쓰기 모드 - Read and Write): 파일을 읽기 및 쓰기 모드로 오픈. 예: 'r+', 'w+', 'a+'.(모두 읽고 쓸 수 있는 모드이나, r+는 파일이 없으면 오류를 내는 등 약간의 차이가 있음)

### read()로 파일 읽기
file_contents = file.read()

### close()로 파일 닫기
file.close()

# preprocessing in datascience란?
: 데이터 전처리, 현실의 raw data를 분석에 적합한 형식으로 만들어주는 과정

<br>데이터 정제, 결측값 처리, 이상값 처리, 분석변수 처리 순서로 진행

## 데이터 정제
: 결측값을 채우거나 이상값을 제거하는 과정. 데이터의 신뢰도를 높임

## 데이터 결측값 처리
: 결측값이란? 입력이 누락된 값. NA, 999999, Null 등으로 표현함
* 완전 무작위 결측(다른 변수와 아무 상관이 없는 경우), 무작위 결측(특정 변수와 관련되어 일어나나 결과는 관계가 없는 경우), 비 무작위 결측(누락이 다른 변수와 연관이 있는 경우) 로 나뉨
* 단순 대치, 다중 대치(여러 번의 대치를 통해 완전한 자료를 만들어서 분석하는 방법) 등의 방법을 이용하여 처리

## 데이터 이상값 처리
: 이상값이란? 관측된 데이터 범위에서 크게 벗어난, 아주 작은 또는 큰 값.
* 데이터 입력 과정의 오류, 측정 과정의 오류, 실험 오류, 고의적인 이상값, 표본 추출 과정에서의 오류 등으로 발생함.
* 이상치로 판단하는 기준은 표준편차와 사분위수, z-값 등의 수치나 카이제곱 등의 검정 결과를 사용할 수 있음.
* 삭제, 대체, 변환, 분류 등의 방법으로 처리.

## 분석 변수 처리
: 변수란? 데이터 모델에서 사용하는, 예측을 수행하는 데에 사용되는 입력 변수


```python

```