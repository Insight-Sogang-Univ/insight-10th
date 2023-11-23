EDA = 탐색적 데이터 분석

Feature
- 범주형
    - 명목형(명목척도)
    - 순서형(서열척도)
- 수치형
    - 이산형
    - 연속형
    
명목형 자료 => Bar plot, Count plot, Pie chart
자료 개형 => Histogram, Box plot, Stem and leaf plot
시계열, 변수 관계 => Time series plot, Scatter plot

Seaborn = 맥플러리 상위호환

sns.histplot(x 축, data=?)
hue -> 범주 구분

막대그래프 => 범주형 데이터에 따라 수치형 데이터 표현

violinplot => box plot + 커널밀도
sns.violinplot(x=범주, y=수치, data=자료)
countplot => 각 범주 별 데이터 수

파이차트, 라인 그래프, 산점도
scatterplot(x, y, data= , hue=범주, palette=[, , ])

pairplot => 종합 산점도
