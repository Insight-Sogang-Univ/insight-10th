중심위치척도
평균 - mean()
중앙값 - median()
최빈값 - mode()

변동성 척도
quantiles(data, method = 'inclusive or exclusive')
np.quantile(data, [-0.25,0.5,0.75])
inclusive 하고 exclusive 차이는 자료 개수가 짝수일 때 고려하는거 같은데...

IQR
직접 계산
q = np.quantile(x, ~)
하면 q[0], q[1] 등 값 배정됨

분산 - variance(data)
표준편차 - stdev(data)
변동 계수 - stdev(x) / mean(x) * 100

공분산표 - .cov()
특정 열 공분산 - .cov().iloc[:2,:2]
=> .cov(df[a], df[b]) 하면 안되려나?
상관계수표 - corr()
data1.corr(data2) -> 두 데이터 간의 상관계수

정규분포
x = np.linspace(a,b,c) => a, b x의 최소최대, 101은 샘플 개수인가?
stats.norm(0,1).pdf(x) => 평균 0 , 분산 1^2 인 정규분포를 따르는 pdf 

T분포
t = np.linspace(~) -> 위랑 동일
stats.t(n).pdf(t) => n은 자유도인듯

chi-square
chi2 = np.linspace(a,b,c)
stats.chi2(n).pdf(chi2) => n은 마찬가지로 자유도 일거 같음

F분포
x= ~ 동일
y1 = stats.f(n1, n2).pdf(x) => f는 자유도 두개

이항분포
bimon(n,p).pmf(x)
푸아송분포
poission(l), l=람다

random.randrange(a, b) => a~b 사이의 값 중 랜덤 값 반환

검정들은 읽어보긴 했는데 직접 시연해봐야 이해할거 같다...


