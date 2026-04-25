# Build a regression model using Scikit-learn: regression four ways

## Beginner Note

Linear regression na wen we wan predict **numerical value** (for example, house price, temperature, or sales).
E dey work by finding straight line wey go best show di relationship between input features and di output.

For dis lesson, we go focus on understanding di concept before we go explore advance regression techniques.
![Linear vs polynomial regression infographic](../../../../translated_images/pcm/linear-polynomial.5523c7cb6576ccab.webp)
> Infographic by [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Pre-lecture quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [This lesson dey R too!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introduction 

So far, you don explore wetin regression mean with sample data we gather from di pumpkin pricing dataset wey we go dey use through dis lesson. You don also visualize am using Matplotlib.

Now, you ready to dive deeper into regression for ML. Visualizing dey help you understand data, but real power for Machine Learning come from _training models_. Models dem dey train on historic data to dey automatically capture data dependencies, and dem allow you predict outcomes for new data wey di model never see before.

For dis lesson, you go learn more about two types of regression: _basic linear regression_ and _polynomial regression_, plus some math wey dey under these techniques. Dem models go allow us predict pumpkin prices depending on different input data. 

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Click di image up top for small video overview of linear regression.

> Throughout dis curriculum, we assume say you get little knowledge of math, and we wan make am easy for students wey come from other fields, so lookout for notes, 🧮 callouts, diagrams, and other learning tools wey go help you understand.

### Prerequisite

By now, you suppose sabi di structure of di pumpkin data wey we dey look. You fit find am preloaded and pre-cleaned for dis lesson's _notebook.ipynb_ file. For di file, pumpkin price dey show per bushel for new data frame.  Make sure say you fit run these notebooks for kernels for Visual Studio Code.

### Preparation

Just reminder, you dey load dis data so you fit ask questions about am. 

- When bae time to buy pumpkins? 
- Wetin price I fit expect for one case of miniature pumpkins?
- Make I buy dem for half-bushel basket or for 1 1/9 bushel box?
Make we continue to dig into dis data.

For di previous lesson, you create Pandas data frame and put part of di original dataset inside, standardize di pricing by di bushel. But by doing that one, you only fit gather about 400 datapoints and only for fall months. 

Check di data wey we preload for dis lesson’s notebook. Di data dey preloaded and dem don chart initial scatterplot to show month data. Maybe we fit get small more detail about di nature of di data if we clean am more.

## A linear regression line

Like you learn for Lesson 1, di goal of linear regression exercise na to fit draw line to:

- **Show variable relationships**. Show d relationship between variables
- **Make predictions**. Make correct predictions how where new datapoint go land for di relationship to dat line. 
 
Na normal for **Least-Squares Regression** to draw dis kain line. Di "Least-Squares" term mean say you dey minimize total error for our model. For every data point, we measure di vertical distance (wey dem dey call _residual_) between di actual point and di regression line.  

We dey square these distances for two main reasons:  

1. **Magnitude over Direction:** We want treat -5 error same as +5 error. Squaring go make all values positive.  

2. **Penalizing Outliers:** Squaring dey give more weight to big errors, e go make line stay close to points wey far away.  

We go add all di squared values join. Our goal na to find di one exact line where di sum of dem less (smallest possible value)—na im cause di name "Least-Squares".  

> **🧮 Show me di math** 
> 
> Dis line, wey dem dey call _line of best fit_ fit express by [an equation](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` na di 'explanatory variable'. `Y` na di 'dependent variable'. Di slope of di line na `b` and `a` na di y-intercept, wey mean di value of `Y` when `X = 0`. 
>
>![calculate the slope](../../../../translated_images/pcm/slope.f3c9d5910ddbfcf9.webp)
>
> First, calculate slope `b`. Infographic by [Jen Looper](https://twitter.com/jenlooper)
>
> In oda words, and referring to di original question wey our pumpkin data get: "predict di price of pumpkin per bushel by month", `X` go mean di price and `Y` go mean di month of sale. 
>
>![complete the equation](../../../../translated_images/pcm/calculation.a209813050a1ddb1.webp)
>
> Calculate di value of Y. If you dey pay about $4, e suppose be April! Infographic by [Jen Looper](https://twitter.com/jenlooper)
>
> Di math wey dey calculate di line gats show di slope of di line, wey also depend on di intercept, or where `Y` dey when `X = 0`.
>
> You fit see how to calculate these values for [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) website. You fit also visit [dis Least-squares calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) to see how numbers values fit affect di line.

## Correlation

One more term wey you gats sabi na **Correlation Coefficient** between given X and Y variables. With scatterplot, you fit quickly see dis coefficient. Scatterplot wey get points for neat line get high correlation, but scatterplot wey get points scatter everywah for X and Y get low correlation.

Good linear regression model go get high (near 1 pass 0) Correlation Coefficient using Least-Squares Regression with regression line.

✅ Run di notebook for dis lesson and see di Month to Price scatterplot. Di data wey connect Month to Price for pumpkin sales get high or low correlation based on your visual check of di scatterplot? E fit change if you use fine-grained measure instead of `Month`, like *day of di year* (number of days since year start)?

For di code below, we go assume say we don clean di data, and dem get data frame wey dem call `new_pumpkins`, similar to dis one:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Di code to clean di data dey for [`notebook.ipynb`](notebook.ipynb). We don do same cleaning steps like for previous lesson, and we calculate `DayOfYear` column using dis expression: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Now wey you don understand di math behind linear regression, make we create Regression model to see if we fit predict which pumpkin package go get di best pumpkin prices. Anybody wey wan buy pumpkins for holiday pumpkin patch fit want this info to optimize dem pumpkin package purchases.

## Looking for Correlation

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Click di image up top for small video overview of correlation.

From previous lesson, you don probably see say average price for different months look like dis:

<img alt="Average price by month" src="../../../../translated_images/pcm/barchart.a833ea9194346d76.webp" width="50%"/>

Dis one suggest say e get correlation, and we fit try train linear regression model to predict di relationship between `Month` and `Price`, or between `DayOfYear` and `Price`. Here na di scatter plot wey show dis latter relationship:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/pcm/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Make we check if correlation dey using di `corr` function:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

E look like say di correlation small small, -0.15 by `Month` and -0.17 by `DayOfMonth`, but fit get another important relationship. E look like different price clusters dey correspond to different pumpkin varieties. To confirm dis guess, make we plot each pumpkin category with different color. By passing `ax` parameter to `scatter` plotting function, we fit plot all points for same graph:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/pcm/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Our investigation show say variety get more effect on price than di selling date. We fit see dis with bar graph:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/pcm/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Make we focus for now on one pumpkin variety, 'pie type', and see wetin di date dey do to price:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/pcm/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

If we calculate correlation between `Price` and `DayOfYear` with `corr` function, we go get something like `-0.27` - e mean say training predictive model make sense.

> Before you train linear regression model, e important say make sure say our data clean. Linear regression no dey work well if e get missing values, so e make sense to remove all empty cells:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Another way fit be to fill empty values with mean from di column wey get dem.

## Simple Linear Regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Click di image up top for short video overview of linear and polynomial regression.

To train our Linear Regression model, we go use **Scikit-learn** library.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

We dey start by separating input values (features) and expected output (label) into separate numpy arrays:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Note say we gats do `reshape` on input data make Linear Regression package fit understand am correct. Linear Regression dey expect 2D-array as input, wey each row get vector of input features inside. For our case, we get only one input, so we need array with shape N&times;1, where N na dataset size.

Next, we need split data into train and test datasets, so that we fit validate our model after training:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Finally, training di real Linear Regression model na just two lines code. We define `LinearRegression` object, then fit am to our data using `fit` method:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Di `LinearRegression` object afta `fit`-ting get all di coefficients of di regression, wey fit access wit `.coef_` property. For our case, e get only one coefficient, wey suppose be round `-0.017`. E mean say di prices dey drop small wit time, but no too much, around 2 cents per day. We fit still access di intersection point of di regression wit Y-axis wit `lin_reg.intercept_` - e go be around `21` for our case, wey mean di price for di beginning of di year.

To see how correct our model be, we fit predict prices for test dataset, then measure how near our predictions be to di expected values. Dis one fit do wit root mean square error (RMSE) metrics, wey be root of di mean of all squared differences between expected and predicted value.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Our error look like around 2 points, wey be ~17%. No too good. Another indicator of model quality na di **coefficient of determination**, wey fit get like dis:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
If di value na 0, e mean say di model no dey use input data, e just act as di *worst linear predictor*, wey be just mean value of di result. If e be 1, e mean say we fit predict all expected outputs perfectly. For our case, di coefficient na around 0.06, wey low small.

We fit still plot di test data with di regression line to betta see how di regression dey work for our case:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/pcm/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

Another kind of Linear Regression na Polynomial Regression. Sometimes, e dey get linear relationship between variables - like di bigger pumpkin in volume, di higher di price - but sometimes dis relationship no fit plot as plane or straight line.

✅ Here be [some more examples](https://online.stat.psu.edu/stat501/lesson/9/9.8) of data we fit use Polynomial Regression

Make you check di relationship between Date and Price again. Dis scatterplot look like e suppose necessarily analyze wit straight line? Prices no dey fluctuate abi? For dis kain case, you fit try polynomial regression.

✅ Polynomials na mathematical expressions wey fit get one or more variables plus coefficients

Polynomial regression dey create curved line to betta fit nonlinear data. For our case, if we put squared `DayOfYear` variable for input data, e suppose fit our data wit parabolic curve wey go get minimum for some point inside di year.

Scikit-learn get better [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) wey fit join different steps of data processing. **Pipeline** na chain of **estimators**. For our case, we go create pipeline wey first add polynomial features to our model, then go train di regression:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

If we use `PolynomialFeatures(2)`, e mean say we go include all second-degree polynomials from di input data. For our case, e go be just `DayOfYear`<sup>2</sup>, but if e get two input variables X and Y, e go add X<sup>2</sup>, XY and Y<sup>2</sup>. We fit still use higher degree polynomials if we want.

Pipelines fit use same way as di original `LinearRegression` object, we fit `fit` di pipeline, then use `predict` get prediction results. Dis na graph wey show test data with approximation curve:

<img alt="Polynomial regression" src="../../../../translated_images/pcm/poly-results.ee587348f0f1f60b.webp" width="50%" />

If we use Polynomial Regression, we fit get small lower MSE and higher determination, but no too much. We need take other features join!

> You fit see say minimum pumpkin prices dey happen around Halloween. How you fit explain dis? 

🎃 Congrats, you don create model wey fit help predict price of pie pumpkins. You fit fit do di same for all pumpkin types, but dat one go be tedious. Make we learn now how take pumpkin variety join our model!

## Categorical Features

For ideal world, we want fit predict prices for different pumpkin varieties wit one model. But di `Variety` column different small from `Month` column, because e get non-numeric values. Dis kin columns na **categorical**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Click di image for short video wey show how to use categorical features.

Here you fit see how average price dey depend on variety:

<img alt="Average price by variety" src="../../../../translated_images/pcm/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

To take variety join, we first need convert am to numeric form, wey be **encode** am. Several ways dey we fit do am:

* Simple **numeric encoding** go create table of different varieties, then go replace variety name wit index for dat table. Dis no be di best idea for linear regression because linear regression go take di actual numeric value of dat index and add am to di result, multiply by some coefficient. For our case, di relationship between di index number and di price no linear, even if we arrange di indices somehow.
* **One-hot encoding** go replace `Variety` column wit 4 different columns, one for every variety. Each column go get `1` if di row na dat variety, else `0`. Dis mean say di linear regression go get four coefficients, one for each pumpkin variety, wey go control "starting price" (or "additional price") for dat variety.

Code below show how to do one-hot encode for variety:

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

To train linear regression wit one-hot encoded variety as input, we just need initialize `X` and `y` data well:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Other code still be same wit how we train Linear Regression before. If you try am, you go see say mean squared error dey nearly di same, but coefficient of determination high pass (~77%). To get more correct predictions, we fit take more categorical features join, plus numeric features, like `Month` or `DayOfYear`. To get one big feature array, we fit use `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Here we still take `City` and `Package` type join, wey bring MSE 2.84 (10%) and determination 0.94!

## Putting it all together

To make di best model, we fit combine (one-hot encoded categorical + numeric) data from above example wit Polynomial Regression. Here be full code for you:

```python
# arrange training data
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# make train-test divide
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# setup and train di pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# predict results for test data
pred = pipeline.predict(X_test)

# calculate MSE and determination
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Dis one suppose give us di best determination coefficient nearly 97%, and MSE=2.23 (~8% prediction error).

| Model | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| All features Linear | 2.84 (10.5%) | 0.94 |
| All features Polynomial | 2.23 (8.25%) | 0.97 |

🏆 Well done! You don create four Regression models for one lesson, and improve model quality to 97%. For final section on Regression, you go learn about Logistic Regression to know categories. 

---
## 🚀Challenge

Try different variables for dis notebook to see how correlation dey relate to model accuracy.

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ml/)

## Review & Self Study

For dis lesson we learn about Linear Regression. Other important kinds of Regression dey. Read about Stepwise, Ridge, Lasso and Elasticnet techniques. Better course to learn more na [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Assignment 

[Build a Model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Disclaimer**:  
Dis document don translate wit AI translation service [Co-op Translator](https://github.com/Azure/co-op-translator). Even tho we dey try make am correct, abeg make you sabi say automated translations fit get errors or wahala for accuracy. Di original document for im own language na di correct source wey you suppose trust pass. For important tori dem, better make professional human translation dey used. We no go gree for any misunderstanding or wrong meaning wey fit happen because of this translation.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->