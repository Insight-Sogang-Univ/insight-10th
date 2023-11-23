"2주차 세션 예습"

-절대경로:

최초의 시작점부터 해당파일까지의 전체경로
보통 다른 사람의 문서나 파일을 이용할 때 사용. 

장점) 어느 곳에서든 경로에 접근 가능
단점) 경로가 변경되면 일일히 수정해야 됨.

-상대경로:

현재파일의 위치를 기준으로 연결하려는 파일의 상대적인 경로를 적는 것.
(특정 경로를 기준으로 다른 경로를 표시하는 방법)

장점) 수정없이 그대로 사용가능
단점) 자기 자신이 기준이기 때문에 자기 자신의 위치가 바뀐다는 점 
분실가능성이 높을 수 있음


데이터 전처리 매우 중요!
데이터 오류의 원인은 1) 결측값 2) 노이즈 3) 이상값으로 구분가능

데이터 세분화
1) 계층적 방법 : 군집수 정하지 않고 단계적으로 군집결과 산출
    a.응집분석법
    b.분할분석법
2) 비계층적방법 : 소집단의 개수를 정해놓고 하나의 소집단으로 배정
    a.인공신경망 모델
    b.k-평균 군집화
    
데이터 결측값 처리 방법
1) 단순대치법: 결측값을 그런 듯한 값으로 대체
    a. 완전분석법
    b. 평균대치법
    c. 단순확률대치법
2) 다중대치법: 단순 대치법을 한 번 하지 않고 가상적 완전한 자료 만들어 분석
    a 대치 -> 분석 -> 결합
    
데이터이상값은 개별데이터를 관찰하거나 통계를 이용하거나
시각화를 이용하거나 머신러닝기법을 이용하여 찾아낼 수 있음!
마할라노비스 거리 활용, LOF, iForest도 활용할 수 있음. (이건 공부 더 필요)

데이터이상값을 찾아냈으면 어떻게 처리하는가?
삭제하거나 대체법을 쓰거나 변환한다.

**분석변수처리 - 공부 더 필요
변수선택기법 (변수= 예측을 수행하는데 사용되는 입력변수)
1) 필터기법 (통계적 측정 방법 사용, ex. 카이제곱 검정)
2) 래퍼기법 (예측 정확도 측면에서 가장 좋은 성능을 보이는 하위 집합 선택)
(ex. SVM, 유전알고리즘...)
3) DLAQPELEM RLQJQ

차원축소: 변수의 정보 최대한 유지하되 데이터세트 변수의 개수를 줄임
1) 주성분분석
2)특이값분해
3)요인분석
4)독립성분분석
5)다차원척도법

변수변환:
1) 단순기능변환
2) 비닝
3) 정규화
4) 표준화

불균형데이터처리:
1) 언더샘플링 - 데이터 소실 가능
2) 오버샘플링 - 과적합 초래 가능..
3) 임곗값 이동
4) 앙상블



**df.iloc['행번호']=원하는 행 출력
df.loc['인덱스']=원하는 인덱스값 출력

행번호는 iloc, loc은 인덱스!!


```python

```