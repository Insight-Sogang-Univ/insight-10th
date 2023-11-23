# 데이터 전처리
<ol>df_obj['date2'] = df_obj['date'].apply(lambda x: x[0:4])</ol>
<ol>df['date2'] = df_obj['date2'].astype('int64')</ol>
<ol>df['date2']</ol>
<ol>df['sold-built_years'] = df.apply(lambda x: ((x['date2']) - (x['yr_built'])), axis=1)</ol>
<ol>df['sold-built_years']</ol>
<li>위와 같은 처리로 인해 date의 전처리는 물론 매각 연도와 지은 연도를</li>

# 선형 관계가 있는 것은 어떤 것??
<ol>columns = ['price','bedrooms','sqft_living','waterfront','view','yr_built','sold-built_years','date2']</ol>
<li>막대모양이 특정 값에만 몰려있는 경우 변수로 선정하는 것을 배웠다.</li>

# 선형 관계
<ol>price와 sqft_living </ol>
<li>price와 sqft_living은 분산되어있지 않고 선형적으로 분포되어있는 것을 확인했다.</li>

# 상관관계 파악
<ol>price</ol>
<ol>price	1.000000</ol>
<ol>sqft_living	0.702035</ol>
<ol>view	0.397293</ol>
<ol>bedrooms	0.308350</ol>
<ol>waterfront	0.266369</ol>
<ol>yr_built	0.054012</ol>
<ol>date2	0.003576</ol>
<ol>sold-built_years	-0.053951</ol>
<li>상관관계를 오름차순 정렬해서 보여주는 것은 나중에 유용하게 사용할 수 있을 것 같다.</li>

</br>
<ol>columns = ['sqft_living', 'sqft_living15', 'sqft_above']</ol>
<ol>colors = ['blue','green','red']</ol>
<ol>living = df[columns]</ol>
<ol>for i in range(3):
    ax = sns.distplot(df[columns[i]], hist=True, norm_hist=False, kde=False, label=columns[i], color=colors[i])</ol>
<ol>ax.set(xlabel="sqft_living / sqft_living15 / sqft_above")</ol>
<ol>plt.figure(figsize=(12,6))</ol>
<ol>plt.legend()</ol>
<ol>plt.show()</ol>
<li>다중 공산성을 피해서 상관관계 높은 변수만 사용한 것을 기억하고 나중에 유용하게 사용해야겠다.</li>

</br>
<ol>result_model.summary()</ol>
<li>summary함수를 유용하게 사용할 수 있겠다.</li>

</br>
<ol>원래 뭐든 다 때려보고, 그 중 괜찮은 걸 고르는 것이 가장 속이 편합니다.</ol>
<li>명언이다.</li>

</br>
<ol>다중 선형 회귀분석에서는 모든 변수의 경우 다중공선성(multicollinearlity) 문제를 확인해야 한다.</ol>
<li>잊지말자.</li>

</br>
<ol>반응 변수(price)에 자연로그를 취해 비대칭인 데이터의 분포를 완화한 상태에서 회귀분석을 한다.</ol>
<li>자연로그를 취하는 것은 생각보다 더 자주 쓰이는 좋은 방법 같다.</li>

</br>
<ol>다중공선성 문제가 확실히 줄어들었음을 알 수 있다.</ol>
<li>위의 방법들로 인해 다중공선성을 해결하는 것을 확인할 수 있었다.</li>


