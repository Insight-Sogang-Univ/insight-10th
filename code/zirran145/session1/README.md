os.getcwd() => 현재 저장 위치 확인
pd.read_csv => csv 파일 불러오기
sep => entry 분류하는 기준
pd.read_excel => 엑셀 파일 불러오기

usecol 이 뭐지??

with
w=>파일 새로 쓰기
r=>파일 읽기
a=>새로운 내용 추가

read=>파일 내용 전체 문자열 반환
readline=>한줄씩 천천히
readlines=>그걸 다 리스트로 반환

.to_csv => 저장하는거
(utf8 인가 16인가 설정 안하면 한글이 깨지던데,,, 이건 왜 멀쩡하지)

json => 파이썬의 dic 같은거
dump => json 파일 저장(=to_csv)
load => 읽어오는거(= read_csv)

pickle => 설명만 봐서는 잘 이해가 안간다, 리스트 자체를 저장하는거 같긴 하다
추가로 행렬도 저장 가능한거 같음


info()=>기본적인 결측치 확인, column 별로 결측치 개수(null) 확인 가능 + data type까지
더 간단하게 => isnull().sum()
unique => column 에서 어떤 값들이 있는지 확인
value_counts => 그 값들이 몇 개씩 있는지 확인

replace(object, to_what, agg~) => 객체를 대체하는
비슷하게 dropna 를 사용해서 결측치 제거
.dropna(axis= , how='any'/'all', subset=[], inplace=)
axis => 행 or 열 선택
any => or
all => and
subset => 어떤 열만 할거야?

fillna()=>결측치 대체 (주로 평균 사용, 사용 전 해당 열의 데이터 타입 확인)

describe => count, mean, std, 분위, max, min 보여줌
boxplot()

data 자체에 boxplot() 을 사용하는 것과, 직접 IQR 계산해서 boxplot 뽑는 것은 무슨 차이가 있지? => 확인해보기
