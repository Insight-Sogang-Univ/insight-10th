# 1. EDA
- 수집한 데이터를 다양한 각도에서 관찰하고 이해하는 과정
-  데이터를 직관적으로 바라보기 위해 통계적인 방법과 데이터 시각화가 사용됨    
<br>

# 2. Feature 분석 및 시각화
## 2-1 Feature의 종류
- **범주형(Categorical)** : 몇 개의 범주로 나누어진 자료
  - **명목형(Nominal)** : 성별, 성공여부, 혈액형 등 순서 없이 단순히 분류된 자료
  - **순서형(Ordinal)** : 범주형 데이터 중 그들 사이에 순서 관계가 존재하는 자료 (ex. 만족도 조사 항목)
        
- **수치형(Numerical)** : 이산형과 연속형으로 이루어진 자료
  - **이산형(Descrete)** : 정수 단위로 떨어져 셀 수 있는 데이터
  - **연속형(Continuous)** : 연속적인 값을 갖는 데이터 (ex. 키)
  
<br>

## 2-2 Feature의 종류
|분류|플롯|
|:---:|:---:|
|명목형 자료|Bar plot(막대그래프), Count plot, Pie chart|
|자료의 개형|Histogram, Box plot, Stem and leaf plot(줄기 - 잎 그래프)|
|시계열 및 변수 간 관계|Time series plot(시계열 그래프), Scatter plot(산점도)|
<br>

## 2-3 사용하는 라이브러리
- **Matplotlib** : Python 프로그래밍 언어 및 수학적 확장 NumPy 라이브러리를 활용한 플로팅 라이브러리
- **Seaborn** : matplotlib을 기반으로 만들어져 통계 데이터 시각화에 최적화된 인기 라이브러리

→ Matplotlib에서 더 발전되어 추가된 것이 Seaborn이므로 둘 중 어떤 라이브러리를 사용해도 상관없음

<br>

# 3. 수치형 데이터 시각화
## 3-1. 히스토그램
- 수치형 데이터의 구간별 빈도수를 나타낸 그래프
```
sns.histplot(x='age', data=data)
``````
<br>

## 3-2. 커널밀도추정 함수 그래프
- 히스토그램을 매끄럽게 곡선으로 연결한 그래프

![Alt text](%EC%BB%A4%EB%84%90%EB%B0%80%EB%8F%84%EC%B6%94%EC%A0%95%ED%95%A8%EC%88%98.png)

<br>

## 3-3. 막대그래프, 포인트 플롯
**막대 그래프**
- 범주형 데이터 값에 따라 수치형 데이터 값이 어떻게 달라지는지 파악할 때 사용됨 
- 범주형 데이터인 class 피처를 x 파라미터에, 수치형 데이터인 fare을 y 파라미터에 전달하여 탑승자의 등급별 운임을 확인하면 왼쪽 아래와 같은 그래프가 출력됨 
  
**포인트플롯** 
- 막대 그래프와 모양만 다르고 동일한 정보를 제공

![Alt text](%ED%8F%AC%EC%9D%B8%ED%8A%B8%ED%94%8C%EB%A1%AF.png)

<br>

## 3-4. 박스 플롯
- 5가지 요약 수치를 제공하여 자료의 분포를 확인
 
![Alt text](%EB%B0%95%EC%8A%A4%ED%94%8C%EB%A1%AF.png)
  
<br>

## 3-5. 바이올린 플롯
- 박스 플롯과 커널밀도추정 함수 그래프를 합쳐 놓은 그래프

![Alt text](%EB%B0%94%EC%9D%B4%EC%98%AC%EB%A6%B0%ED%94%8C%EB%A1%AF.png)
```
sns.violinplot(x='class', y='age', data=data)
```
<br>

## 3-6. 카운트 플롯
- 각 카테고리 별로 데이터가 얼마나 있는지 수치를 표시

![Alt text](%EC%B9%B4%EC%9A%B4%ED%8A%B8%ED%94%8C%EB%A1%AF.png)
```
sns.countplot(x='class', data=data)
```

<br>

## 3-7. 파이 그래프
- 비율을 강조하기 위해 사용됨
- 모든 데이터가 합쳐서 전체를 이루는 경우에 효과적으로 활용할 수 있음
```
import matplotlib.pyplot as plt

x=[10,60,30]
labels=['A','B','C']

plt.pie(x, labels=labels, autopct='%.1f%%')
```
<br>

## 3-8. 라인 그래프
- 데이터 포인트를 연결하는 선으로 구성되어 시간, 순서 또는 다른 연속적인 변수의 변화를 시각적으로 보여줌 
- 주로 시계열 데이터나 연속적인 데이터의 변화를 분석하거나 비교할 때 사용됨

![Alt text](%EB%9D%BC%EC%9D%B8%EA%B7%B8%EB%9E%98%ED%94%84.png)

 ```
df.plot(marker='o', color=['r','b','g','y'])
 ``` 
<br>

## 3-9. 산점도
- 두 변수 간의 관계를 시각화하기 위해 사용되는 그래프 
```
sns.scatterplot(x='petal_length', y='petal_width', data=iris, color='purple', alpha=0.5)
plt.title('Scatter Plot of Petal size', fontsize=20)
plt.xlabel('petal_length', fontsize=14)
plt.ylabel('petal_width', fontsize=14)
plt.show()
```
<br>

## 3-10. 여러 변수 간 산점도
- 데이터셋 내의 모든 수치형 변수 간의 산점도와 히스토그램을 표시하여 변수들 간의 상관관계, 분포, 패턴 등을 살펴보는 데 유용함
```
import seaborn as sns
import matplotlib.pyplot as plt

sns.pairplot(iris)
```