# Scikit-learn을 사용하여 회귀 모델 구축: 회귀 네 가지 방법

## 초보자 참고사항

선형 회귀는 **숫자 값**(예: 주택 가격, 온도 또는 판매량)을 예측하려 할 때 사용됩니다.  
이는 입력 특성과 출력 간의 관계를 최적으로 나타내는 직선을 찾는 방식으로 작동합니다.

이 수업에서는 고급 회귀 기법을 다루기 전에 개념 이해에 집중합니다.  
![선형 회귀 vs 다항 회귀 인포그래픽](../../../../translated_images/ko/linear-polynomial.5523c7cb6576ccab.webp)  
> 인포그래픽: [Dasani Madipalli](https://twitter.com/dasani_decoded)  
## [사전 퀴즈](https://ff-quizzes.netlify.app/en/ml/)

> ### [이 수업은 R 버전으로도 제공됩니다!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)  
### 소개

지금까지 할로윈 호박 가격 데이터셋에서 샘플 데이터를 사용하며 회귀가 무엇인지 탐색했습니다. Matplotlib를 활용해 시각화도 했죠.

이제 머신러닝 회귀에 대해 더 깊이 들어갈 준비가 되었습니다. 시각화는 데이터를 이해하는 데 도움을 주지만, 머신러닝의 진정한 힘은 _모델 학습_에 있습니다. 모델은 역사적 데이터를 기반으로 학습하여 자동으로 데이터 의존성을 포착하고, 모델이 본 적 없는 새 데이터의 결과를 예측할 수 있도록 해줍니다.

이번 수업에서는 _기본 선형 회귀_와 _다항 회귀_ 두 가지 회귀 유형과 관련 수학을 배웁니다. 이 모델들은 다양한 입력 데이터에 따라 호박 가격을 예측할 수 있게 해줍니다.

[![초보자를 위한 ML - 선형 회귀 이해](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "초보자를 위한 ML - 선형 회귀 이해")

> 🎥 위 이미지 클릭 시 선형 회귀 짧은 동영상 개요를 볼 수 있습니다.

> 이 교육 과정 전반에 걸쳐 수학 지식을 최소화하고, 타 분야 학생도 이해하기 쉽게 만들고자 합니다. 노트, 🧮 계산 설명, 다이어그램 등 다양한 학습 도구를 참고하세요.

### 필수 준비 사항

지금까지 살펴본 할로윈 호박 데이터 구조에 익숙해졌을 것입니다. 본 수업의 _notebook.ipynb_ 파일에는 미리 불러오고 정제한 데이터가 있습니다. 여기서 호박 가격은 부셸 단위로 새 데이터프레임에 표시되어 있습니다. Visual Studio Code의 커널에서 이 노트북들을 실행할 수 있어야 합니다.

### 준비

데이터를 불러온 목적은 질문을 던지는 데 있습니다.  

- 언제가 호박을 사기에 가장 좋은 시기일까요?  
- 미니어처 호박 한 케이스 가격은 얼마일까요?  
- 반 부셸 바구니로 사야 할까요, 아니면 1 1/9 부셸 상자로 사야 할까요?  
더 깊이 탐색해 봅시다.

지난 수업에서는 Pandas 데이터프레임을 만들고 원본 데이터셋 일부로 채우며, 부셸 단위 가격을 표준화했습니다. 하지만 이렇게 하다 보니 가을 몇 개월에 대해서만 약 400개의 데이터 포인트만 얻을 수 있었습니다.

본 수업의 동봉된 노트북에 미리 불러온 데이터를 살펴보세요. 전처리가 완료되었고, 초기 산점도가 월별 데이터를 보여줍니다. 데이터를 더 정제하면 보다 상세한 통찰을 얻을 수 있을지도 모릅니다.

## 선형 회귀 직선

1장에서 배운 바와 같이 선형 회귀 목표는 다음을 할 수 있는 직선을 그리는 것입니다:

- **변수 간 관계 표시**: 변수 간 관계를 보여줍니다.  
- **예측 수행**: 새 데이터가 그 직선에서 어디에 위치할지 정확히 예측합니다.  

일반적으로 <strong>최소 제곱 회귀</strong>에서 이런 선을 그립니다. "최소 제곱"이란 모델에서 전체 오류를 최소화하는 과정을 의미합니다. 각 데이터 포인트마다 실제 점과 회귀선 사이의 수직 거리(잔차라고 함)를 측정합니다.

여기서 제곱하는 이유는 두 가지입니다:

1. **방향 무시, 크기만 고려:** -5와 +5의 오차를 동일하게 취급하기 위해 모든 값을 양수로 만듭니다.  
2. **이상치 패널티:** 큰 오차가 더 크게 반영되어 선이 멀리 떨어진 점에 더 가깝게 위치하도록 합니다.  

이렇게 제곱한 값들을 모두 더한 합을 최소화하는 선을 찾는 것이 목표입니다.

> **🧮 수학 공식 보여드리기**  
>  
> 최적 직선은 [다음 식](https://en.wikipedia.org/wiki/Simple_linear_regression)으로 나타낼 수 있습니다:  
>  
> ```
> Y = a + bX
> ```
>  
> `X`는 설명 변수, `Y`는 종속 변수입니다. 기울기는 `b`이고, y절편은 `a`로, `X=0`일 때 `Y` 값입니다.  
>  
>![기울기 계산](../../../../translated_images/ko/slope.f3c9d5910ddbfcf9.webp)  
>  
> 먼저 기울기 `b`를 계산합니다. 인포그래픽: [Jen Looper](https://twitter.com/jenlooper)  
>  
> 다시 말해, 본 호박 데이터 질문 "월별 부셸당 호박 가격 예측"에서 `X`는 가격, `Y`는 판매 월을 의미합니다.  
>  
>![방정식 완성](../../../../translated_images/ko/calculation.a209813050a1ddb1.webp)  
>  
> `Y` 값을 계산하세요. 약 $4라면 4월일 것입니다! 인포그래픽: [Jen Looper](https://twitter.com/jenlooper)  
>  
> 기울기뿐 아니라, `X=0`인 경우 `Y` 위치를 의미하는 절편도 계산식에 포함됩니다.  
>  
> 이 값 계산법은 [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) 사이트에서 상세히 볼 수 있습니다. [이 최소제곱 계산기](https://www.mathsisfun.com/data/least-squares-calculator.html)로 숫자 변화가 선에 미치는 영향도 확인하세요.

## 상관 관계

더 알아야 할 용어는 주어진 X와 Y 변수 간의 <strong>상관계수</strong>입니다. 산점도를 통해 쉽게 시각화할 수 있습니다. 데이터 포인트가 정렬된 직선에 가깝게 흩어져 있으면 강한 상관관계이고, 산만히 흩어져 있으면 약한 상관관계입니다.

좋은 선형 회귀 모델은 최소 제곱 회귀 방식으로 높은(0보다 1에 가까운) 상관계수를 갖습니다.

✅ 이번 수업 노트북을 실행하여 월별 가격 산점도를 봅시다. 호박 판매의 월별 가격 데이터가 산점도 시각판단상 상관관계가 높은가요, 아니면 낮은가요? `Month` 대신 연중 날짜(즉, 연도 시작부터의 일수) 같은 더 세분화된 변수를 이용하면 결과가 바뀔까요?

다음 코드는 데이터 정제 후 `new_pumpkins`라는 데이터프레임을 얻었다고 가정합니다:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  

> 데이터 정제 코드는 [`notebook.ipynb`](notebook.ipynb)에서 확인할 수 있습니다. 이전 수업과 같은 정제 단계를 수행했고, 아래 식으로 `DayOfYear` 열을 계산했습니다:  
>  
```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
선형 회귀의 수학적 이해를 마쳤으니, 어떤 호박 패키지가 최적의 가격을 가질지 예측하는 회귀 모델을 만들어 보겠습니다. 호박 밭을 위해 호박을 구매하는 사람은 최적의 구매를 위해 이 정보를 원할 것입니다.

## 상관 관계 찾아보기

[![초보자를 위한 ML - 상관관계 찾기: 선형 회귀의 핵심](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "초보자를 위한 ML - 상관관계 찾기: 선형 회귀의 핵심")

> 🎥 위 이미지 클릭 시 상관관계 짧은 동영상 개요 시청

이전 수업에서 월별 평균 가격이 다음과 같음을 보았을 것입니다:

<img alt="월별 평균 가격" src="../../../../translated_images/ko/barchart.a833ea9194346d76.webp" width="50%"/>

월별 가격 차이에서 상관 관계가 있어 보이고, `Month`와 `Price` 또는 `DayOfYear`와 `Price` 간의 관계를 예측하는 선형 회귀 모델을 훈련할 수 있겠습니다. 아래 그래프는 후자를 보여줍니다:

<img alt="가격 vs 연중 일수 산점도" src="../../../../translated_images/ko/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />

`corr` 함수를 이용해 상관관계가 있는지 확인해 봅시다:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
`Month` 상관계수는 -0.15, `DayOfMonth`는 -0.17로 낮은 편입니다. 하지만 호박 품종별로 가격 군집이 다른 관계가 있을 수도 있습니다. 이를 확인하기 위해 각 호박 종류를 다른 색깔로 표시해 봅시다. `scatter` 함수에 `ax` 매개변수를 주어 한 그래프에 모든 점을 표시할 수 있습니다:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="가격 vs 연중 일수 산점도 (색상별)" src="../../../../translated_images/ko/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" />

품종이 실제 판매일보다 가격에 더 큰 영향을 미치는 것 같습니다. 막대 그래프로도 볼 수 있습니다:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="품종에 따른 가격 막대그래프" src="../../../../translated_images/ko/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

현재는 'pie type' 품종 하나만 집중해, 날짜가 가격에 미치는 영향을 봅시다:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="가격 vs 연중 일수 산점도" src="../../../../translated_images/ko/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" />

`Price`와 `DayOfYear` 상관관계를 `corr` 함수로 계산하면 약 `-0.27`이 나옵니다. 이는 예측 모델 학습이 타당함을 의미합니다.

> 선형 회귀 모델을 훈련하기 전, 데이터 정리가 중요합니다. 선형 회귀는 결측치가 있으면 잘 작동하지 않으므로, 빈 셀을 제거하는 것이 좋습니다:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
결측치를 해당 열 평균값으로 채우는 방법도 있습니다.

## 단순 선형 회귀

[![초보자를 위한 ML - Scikit-learn을 사용한 선형 및 다항 회귀](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "초보자를 위한 ML - Scikit-learn을 사용한 선형 및 다항 회귀")

> 🎥 위 이미지 클릭 시 선형 및 다항 회귀 짧은 동영상 개요 시청

선형 회귀 모델 훈련에 **Scikit-learn** 라이브러리를 사용하겠습니다.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
입력값(특징)과 결과값(레이블)을 별개의 numpy 배열로 나눕니다:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Linear Regression 패키지가 데이터를 올바로 인식하려면 입력 데이터를 `reshape` 해야 합니다. Linear Regression은 입력을 2D 배열로 기대하며, 배열의 각 행이 입력 특징 벡터입니다. 여기선 입력이 하나뿐이므로, 크기 N×1 배열이어야 합니다(N은 데이터셋 크기).

그다음, 훈련 데이터와 테스트 데이터로 나누어 모델 검증에 사용합니다:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
마지막으로 Linear Regression 모델을 훈련하는 코드는 단 두 줄입니다. `LinearRegression` 객체를 만들고, `fit` 메서드로 데이터를 학습합니다:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`fit` 후의 `LinearRegression` 객체는 회귀의 모든 계수를 포함하며 `.coef_` 속성을 사용해 접근할 수 있습니다. 우리 경우에는 계수가 하나뿐이며, 약 `-0.017` 정도일 것입니다. 이는 가격이 시간이 지남에 따라 약간씩 떨어지는 경향이 있지만 하루에 약 2센트 정도로 크게 떨어지지는 않는다는 뜻입니다. 또한 회귀의 Y축과의 교차점은 `lin_reg.intercept_`로 접근할 수 있는데, 우리 경우에는 약 `21`이 되어 연초의 가격을 나타냅니다.

모델의 정확도를 확인하려면 테스트 데이터셋에 대해 가격을 예측하고, 예측값이 기대값과 얼마나 가까운지 측정하면 됩니다. 이는 예상값과 예측값 사이 모든 제곱 차이의 평균의 제곱근인 root mean square error(RMSE) 지표로 측정할 수 있습니다.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

오차는 약 2포인트, 즉 약 17% 정도로 보입니다. 그리 좋지 않군요. 모델 품질의 또 다른 지표는 <strong>결정 계수(coefficient of determination)</strong>로, 다음과 같이 얻을 수 있습니다:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
결정 계수가 0이라면 모델이 입력 데이터를 전혀 고려하지 않고 결과의 단순 평균값만을 예측하는 <em>최악의 선형 예측자</em>임을 의미합니다. 1이라면 모든 기대 출력값을 완벽하게 예측한다는 뜻입니다. 우리 경우 결정 계수는 약 0.06으로 꽤 낮습니다.

테스트 데이터와 회귀선을 함께 그리면 회귀가 어떻게 동작하는지 더 잘 알 수 있습니다:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/ko/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## 다항 회귀 (Polynomial Regression)

선형 회귀의 또 다른 유형은 다항 회귀입니다. 때때로 변수들 간에 선형 관계가 존재할 수 있지만 — 예를 들어 호박 부피가 크면 가격이 높아지는 것처럼 — 때로는 관계가 평면이나 직선으로 나타내기 어려울 때가 있습니다.

✅ 여기에 [다항 회귀에 적합한 데이터의 몇 가지 예](https://online.stat.psu.edu/stat501/lesson/9/9.8)가 있습니다.

다시 `Date`와 `Price` 관계를 살펴봅시다. 이 산점도가 반드시 직선으로 분석되어야 할까요? 가격이 변동할 수는 없을까요? 이런 경우에는 다항 회귀를 시도할 수 있습니다.

✅ 다항식은 하나 이상의 변수와 계수로 구성된 수학적 표현입니다.

다항 회귀는 비선형 데이터를 더 잘 맞추기 위해 곡선을 생성합니다. 우리 경우에 `DayOfYear`의 제곱 변수를 입력 데이터에 포함하면, 연중 특정 시점에 최소값이 있는 포물선 곡선으로 데이터를 맞출 수 있습니다.

Scikit-learn에는 여러 데이터 처리 단계를 결합하는 데 유용한 [파이프라인 API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline)가 포함되어 있습니다. <strong>파이프라인</strong>은 <strong>추정기(estimators)</strong>의 연결 고리입니다. 우리 경우 다항 특성을 먼저 추가하고 회귀를 학습하는 파이프라인을 생성할 것입니다:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

`PolynomialFeatures(2)`를 사용하면 입력 데이터의 모든 2차 다항식이 포함됩니다. 우리 경우는 `DayOfYear`<sup>2</sup>가 될 것이며, 만약 두 입력 변수 X, Y가 있다면 X<sup>2</sup>, XY, Y<sup>2</sup>가 추가됩니다. 필요하다면 더 높은 차수의 다항식도 사용할 수 있습니다.

파이프라인은 원래의 `LinearRegression` 객체처럼 사용할 수 있습니다. 즉, 파이프라인을 `fit`하고 `predict`를 사용해 예측 결과를 얻을 수 있습니다. 아래 그래프는 테스트 데이터와 근사 곡선을 보여줍니다:

<img alt="Polynomial regression" src="../../../../translated_images/ko/poly-results.ee587348f0f1f60b.webp" width="50%" />

다항 회귀를 사용하면 MSE가 약간 낮아지고 결정 계수가 높아지긴 하지만 크게 차이나진 않습니다. 더 정확한 예측을 위해서는 다른 피처도 고려해야 합니다!

> 할로윈 무렵 최소 호박 가격이 관찰된다는 점을 알 수 있습니다. 어떻게 설명할 수 있을까요?

🎃 축하합니다, 당신은 호박 가격을 예측하는 모델을 만들었습니다. 아마도 모든 호박 종류에 대해 같은 절차를 반복할 수 있겠지만 이는 매우 번거롭습니다. 이제 호박 품종을 모델에 반영하는 방법을 배우겠습니다!

## 범주형 특성 (Categorical Features)

이상적으로는 동일한 모델로 다양한 호박 품종의 가격을 예측할 수 있길 원합니다. 하지만 `Variety` 열은 `Month` 같은 열과 달리 수치 데이터가 아닌 값을 포함합니다. 이런 열을 **범주형(categorical)** 이라고 합니다.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 위 이미지를 클릭하면 범주형 특성 활용에 대한 간단한 동영상을 볼 수 있습니다.

다음은 품종별 평균 가격입니다:

<img alt="Average price by variety" src="../../../../translated_images/ko/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

품종을 고려하려면 먼저 품종을 숫자형으로 변환하거나 <strong>인코딩</strong>해야 합니다. 인코딩하는 방법은 여러 가지가 있습니다:

* 간단한 **숫자 인코딩(numeric encoding)** 은 다른 품종을 테이블로 만들고 품종명을 해당 인덱스로 대체하는 방법입니다. 이는 선형 회귀에는 적합하지 않은데, 선형 회귀는 인덱스의 수치값을 실제 값으로 받아들이고 계수를 곱해 결과에 더하기 때문입니다. 우리 경우 인덱스 번호와 가격의 관계는 명백히 비선형이므로 인덱스 순서가 선형 회귀에 적합하지 않습니다.
* **원-핫 인코딩(one-hot encoding)** 은 `Variety` 열을 각 품종마다 한 개씩 총 4개의 열로 분리합니다. 각 열은 해당 행이 그 품종이면 `1`, 아니면 `0`을 가집니다. 이로 인해 선형 회귀는 네 개의 결정 계수를 갖게 되어 각각 품종마다 "기본 가격"(또는 "추가 가격")을 나타내게 됩니다.

다음 코드는 품종을 원-핫 인코딩하는 방법을 보여줍니다:

```python
pd.get_dummies(new_pumpkins['Variety'])
```

 ID | FAIRYTALE | MINIATURE | MIXED HEIRLOOM VARIETIES | PIE TYPE
----|-----------|-----------|--------------------------|----------
70 | 0 | 0 | 0 | 1
71 | 0 | 0 | 0 | 1
... | ... | ... | ... | ...
1738 | 0 | 1 | 0 | 0
1739 | 0 | 1 | 0 | 0
1740 | 0 | 1 | 0 | 0
1741 | 0 | 1 | 0 | 0
1742 | 0 | 1 | 0 | 0

원-핫 인코딩된 품종을 입력으로 하여 선형 회귀를 학습시키려면, `X`와 `y` 데이터를 적절히 초기화하기만 하면 됩니다:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

나머지 코드는 위에서 선형 회귀를 학습할 때 사용한 것과 동일합니다. 시도해 보면 평균 제곱 오차는 비슷하지만 결정 계수가 훨씬 높아져 약 77%에 이릅니다. 더욱 정확한 예측을 위해서는 추가 범주형 특성과 `Month`, `DayOfYear` 같은 숫자 특성도 함께 고려할 수 있습니다. 모든 피처를 하나의 큰 배열로 합치려면 `join`을 사용할 수 있습니다:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

여기서는 `City`와 `Package` 타입도 포함하여 MSE 2.84 (10%), 결정 계수 0.94가 나옵니다!

## 모두 함께 합치기

최종 모델에는 위의 범주형 원-핫 인코딩 데이터와 숫자 데이터를 다항 회귀와 함께 사용합니다. 편의를 위해 전체 코드는 다음과 같습니다:

```python
# 학습 데이터 설정
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# 학습-테스트 분할 수행
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# 파이프라인 설정 및 학습
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# 테스트 데이터에 대한 결과 예측
pred = pipeline.predict(X_test)

# MSE 및 결정계수 계산
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

이렇게 하면 거의 97%의 최고 결정 계수와 MSE=2.23 (약 8% 예측 오차)를 얻을 수 있습니다.

| 모델 | MSE | 결정 계수 |
|-------|-----|---------------|
| `DayOfYear` 선형 | 2.77 (17.2%) | 0.07 |
| `DayOfYear` 다항 | 2.73 (17.0%) | 0.08 |
| `Variety` 선형 | 5.24 (19.7%) | 0.77 |
| 전체 특성 선형 | 2.84 (10.5%) | 0.94 |
| 전체 특성 다항 | 2.23 (8.25%) | 0.97 |

🏆 훌륭합니다! 한 수업에서 네 가지 회귀 모델을 만들고 모델 품질을 97%까지 향상시켰습니다. 마지막 회귀 섹션에서는 범주 분류를 위한 로지스틱 회귀에 대해 배울 것입니다.

---
## 🚀도전 과제

이 노트북에서 여러 변수를 시험하여 상관관계가 모델 정확도에 어떻게 대응하는지 확인해 보세요.

## [강의 후 퀴즈](https://ff-quizzes.netlify.app/en/ml/)

## 복습 및 자기 주도 학습

이번 수업에서는 선형 회귀에 대해 배웠습니다. 회귀에는 다른 중요한 유형도 있습니다. 단계별 회귀(Stepwise), 릿지(Ridge), 라쏘(Lasso), 엘라스틱넷(Elasticnet) 기법을 공부해 보세요. 더 자세히 배우고 싶다면 [스탠퍼드 통계학습 과정](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)이 좋은 코스입니다.

## 과제

[모델 만들기](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**면책 조항**:  
이 문서는 AI 번역 서비스 [Co-op Translator](https://github.com/Azure/co-op-translator)를 사용하여 번역되었습니다. 정확성을 위해 노력하고 있으나 자동 번역에는 오류나 부정확성이 포함될 수 있음을 유의해 주시기 바랍니다. 원본 문서는 해당 원어로 된 문서가 권위 있는 출처로 간주되어야 합니다. 중요한 정보의 경우 전문 인간 번역을 권장합니다. 이 번역 사용으로 인해 발생하는 오해나 잘못된 해석에 대해서는 당사가 책임지지 않습니다.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->