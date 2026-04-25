# Gumawa ng regression model gamit ang Scikit-learn: apat na paraan ng regression

## Tala para sa Baguhan

Ginagamit ang linear regression kapag nais nating mahulaan ang isang **numerikal na halaga** (halimbawa, presyo ng bahay, temperatura, o benta).
Ito ay gumagana sa pamamagitan ng paghahanap ng tuwid na linya na pinakamainam na kumakatawan sa relasyon sa pagitan ng mga input na katangian at ng output.

Sa araling ito, tututok tayo sa pag-unawa sa konsepto bago tuklasin ang mas advanced na mga teknik sa regression.
![Linear vs polynomial regression infographic](../../../../translated_images/tl/linear-polynomial.5523c7cb6576ccab.webp)
> Infographic mula kay [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Pre-lecture quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Available din ang araling ito sa R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Panimula

Sa ngayon ay na-explore mo na kung ano ang regression gamit ang sample data mula sa pumpkin pricing dataset na gagamitin natin sa buong araling ito. Na-visualize mo rin ito gamit ang Matplotlib.

Ngayon, handa ka nang sumisid ng mas malalim sa regression para sa ML. Habang ang visualization ay nagpapahintulot sa iyo na maunawaan ang data, ang totoong kapangyarihan ng Machine Learning ay nagmumula sa _pagsasanay ng mga modelo_. Ang mga modelo ay sinasanay gamit ang makasaysayang data upang awtomatikong makuha ang mga dependency ng data, at pinapayagan kang mahulaan ang mga resulta para sa bagong data na hindi pa nakita ng modelo.

Sa araling ito, matututuhan mo pa ang tungkol sa dalawang uri ng regression: _basic linear regression_ at _polynomial regression_, kasama ang ilan sa matematika sa likod ng mga teknik na ito. Papayagan tayo ng mga modelong ito na mahulaan ang presyo ng kalabasa depende sa iba't ibang input na datos.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 I-click ang larawan sa itaas para sa maikling video overview ng linear regression.

> Sa buong kurikulum na ito, ipinapalagay namin ang minimal na kaalaman sa matematika, at layuning gawing accessible ito para sa mga estudyanteng galing sa ibang larangan, kaya panoorin ang mga tala, 🧮 callouts, diagram, at iba pang mga kagamitan sa pagkatuto upang makatulong sa pag-unawa.

### Paunang Kaalaman

Dapat pamilyar ka na ngayon sa estruktura ng pumpkin data na sinusuri natin. Maaari mo itong makita na naka-preload at malinis na sa _notebook.ipynb_ file ng araling ito. Sa file, ipinapakita ang presyo ng kalabasa kada bushel sa isang bagong data frame. Siguraduhing kaya mong patakbuhin ang mga notebook na ito sa kernels ng Visual Studio Code.

### Paghahanda

Paalala, ini-load mo ang datos na ito upang makapagtanong tungkol dito.

- Kailan ang pinakamainam na oras para bumili ng kalabasa?
- Anong presyo ang aasahan ko para sa isang kahon ng miniature pumpkins?
- Dapat ba akong bumili sa mga half-bushel baskets o sa 1 1/9 bushel na kahon?
Patuloy nating tuklasin ang datos na ito.

Sa nakaraang aralin, gumawa ka ng Pandas data frame at pinunan ito gamit ang bahagi ng orihinal na dataset, na na-standardize ang pagpepresyo base sa bushel. Sa paggawa noon, nakalikom ka lang ng humigit-kumulang 400 datapoints at para lamang sa mga buwan ng taglagas.

Tingnan ang data na preloaded sa kasamang notebook ng araling ito. Ang data ay naka-preload at unang scatterplot ang ginawa upang ipakita ang data ng buwan. Marahil, makakakuha tayo ng mas detalyadong impormasyon tungkol sa kalikasan ng data sa pamamagitan ng masusing paglilinis nito.

## Isang linya ng linear regression

Gaya ng iyong natutunan sa Lesson 1, ang layunin ng linear regression exercise ay maging kaya mong iguhit ang isang linya upang:

- **Ipakita ang relasyon ng mga variable**. Ipakita ang relasyon sa pagitan ng mga variable
- **Gumawa ng prediksyon**. Gumawa ng tumpak na prediksyon kung saan mahuhulog ang isang bagong datapoint kaugnay ng linyang iyon. 

Karaniwan sa **Least-Squares Regression** na gumuhit ng ganitong uri ng linya. Ang terminong "Least-Squares" ay tumutukoy sa proseso ng pagbabawas ng kabuuang error sa ating modelo. Para sa bawat data point, sinusukat natin ang patayong distansya (tinatawag na residual) sa pagitan ng aktwal na punto at ng ating regression line.

Pinapangkat natin ang mga distansyang ito sa pamamagitan ng pag-square ng mga ito para sa dalawang pangunahing dahilan:

1. **Magnitude higit sa Direksyon:** Gusto nating tratuhin ang error na -5 nang pareho sa error na +5. Ang pag-square ay nagpapabago ng lahat ng halaga upang maging positibo.

2. **Pagpaparusa sa Outliers:** Ang pag-square ay nagbibigay ng mas malaking timbang sa malalaking errors, na pinipilit ang linya na manatili na mas malapit sa mga puntong malayo.

Pagkatapos ay pinag-samasama natin ang lahat ng squared na halaga. Ang layunin natin ay hanapin ang partikular na linya kung saan ang huling kabuuan ay pinakamaiksi (pinakamaliit na posibleng halaga)—kaya tinawag itong "Least-Squares".

> **🧮 Ipakita sa akin ang matematika**  
> 
> Ang linyang ito, na tinatawag na _line of best fit_ ay maaaring ipahayag gamit ang [isang ekwasyon](https://en.wikipedia.org/wiki/Simple_linear_regression):  
> 
> ```
> Y = a + bX
> ```
>
> `X` ay ang 'explanatory variable'. `Y` ay ang 'dependent variable'. Ang slope ng linya ay `b` at `a` ang y-intercept, na tumutukoy sa halaga ng `Y` kapag `X = 0`.
>
>![calculate the slope](../../../../translated_images/tl/slope.f3c9d5910ddbfcf9.webp)
>
> Una, kalkulahin ang slope `b`. Infographic mula kay [Jen Looper](https://twitter.com/jenlooper)
>
> Sa ibang salita, at ayon sa orihinal na tanong sa data ng kalabasa: "hulaan ang presyo ng kalabasa kada bushel ayon sa buwan", ang `X` ay tumutukoy sa presyo at ang `Y` ay tumutukoy sa buwan ng pagbebenta.
>
>![complete the equation](../../../../translated_images/tl/calculation.a209813050a1ddb1.webp)
>
> Kalkulahin ang halaga ng Y. Kung nagbabayad ka ng nasa halagang $4, siguradong Abril iyon! Infographic mula kay [Jen Looper](https://twitter.com/jenlooper)
>
> Kinakailangang ipakita ng matematika na kumukuwenta sa linya ang slope nito, na nakabase rin sa intercept, o kung saan matatagpuan ang `Y` kapag `X = 0`.
>
> Maaari mong obserbahan ang paraan ng pagkalkula ng mga halagang ito sa website ng [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Bisitahin din ang [Least-squares calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) upang makita kung paano naaapektuhan ng halaga ng mga numero ang linya.

## Korelasyon

Isa pang term na kailangang maunawaan ay ang **Correlation Coefficient** sa pagitan ng mga variable na X at Y. Sa pamamagitan ng scatterplot, madali mong ma-visualize ang coefficient na ito. Ang plot na may mga datapoints na nakaayos sa isang maayos na linya ay may mataas na korelasyon, ngunit ang isang plot na may datapoints na kalat-kalat sa pagitan ng X at Y ay may mababang korelasyon.

Ang isang magandang linear regression model ay yaong may mataas (mas malapit sa 1 kaysa 0) na Correlation Coefficient gamit ang Least-Squares Regression method na may regression line.

✅ Patakbuhin ang notebook na kasama sa araling ito at tingnan ang scatterplot ng Month to Price. Mukhang mataas ba o mababa ang korelasyon ng data sa pagitan ng Month at Price para sa benta ng kalabasa, ayon sa iyong visual na interpretasyon ng scatterplot? Nagbabago ba ito kung gagamit ka ng mas detalyadong sukat sa halip na `Month`, hal. *araw ng taon* (ibig sabihin bilang ng mga araw mula simula ng taon)?

Sa code sa ibaba, ipapalagay natin na malinis na ang data, at nakuha natin ang data frame na tinatawag na `new_pumpkins`, katulad ng sumusunod:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Ang code para linisin ang data ay makikita sa [`notebook.ipynb`](notebook.ipynb). Ginawa namin ang parehong mga hakbang sa paglilinis gaya ng sa nakaraang aralin, at nakalkula ang kolum na `DayOfYear` gamit ang sumusunod na expression:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Ngayon na naiintindihan mo na ang matematika sa likod ng linear regression, gumawa tayo ng Regression model upang makita kung kaya nating hulaan kung aling pakete ng kalabasa ang may pinakamagandang presyo. Ang sinumang bibili ng mga kalabasa para sa holiday pumpkin patch ay maaaring gusto ang impormasyong ito upang ma-optimize ang kanilang pagbili ng mga pakete ng kalabasa.

## Paghahanap ng Korelasyon

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 I-click ang larawan sa itaas para sa maikling video overview ng korelasyon.

Mula sa nakaraang aralin, marahil ay nakita mo na ang karaniwang presyo para sa iba't ibang buwan ay ganito:

<img alt="Average price by month" src="../../../../translated_images/tl/barchart.a833ea9194346d76.webp" width="50%"/>

Ipinapahiwatig nito na dapat may korelasyon, at maaari nating subukan ang pagsasanay ng linear regression model upang mahulaan ang relasyon sa pagitan ng `Month` at `Price`, o sa pagitan ng `DayOfYear` at `Price`. Narito ang scatter plot na nagpapakita ng huling relasyon:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/tl/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Tingnan natin kung may korelasyon gamit ang `corr` function:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Mukhang maliit ang korelasyon, -0.15 base sa `Month` at -0.17 base sa `DayOfMonth`, ngunit maaaring may isa pang mahalagang relasyon. Mukhang may iba't ibang cluster ng mga presyo na tumutugma sa iba't ibang varieties ng kalabasa. Upang kumpirmahin ito, ipapakita natin bawat kategorya ng kalabasa gamit ang iba't ibang kulay. Sa pamamagitan ng pagpasa ng `ax` parameter sa `scatter` na plotting function, mapapakita natin lahat ng puntos sa iisang graph:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/tl/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Sinasabi ng imbestigasyon natin na mas malaki ang epekto ng variety sa kabuoang presyo kaysa sa aktwal na petsa ng pagbebenta. Makikita natin ito sa isang bar graph:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/tl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Magtuon muna tayo sa isang uri ng kalabasa, ang 'pie type', at tingnan kung ano ang epekto ng petsa sa presyo:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/tl/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Kung kakalkulahin natin ngayon ang korelasyon sa pagitan ng `Price` at `DayOfYear` gamit ang `corr` function, makakakuha tayo ng mga tulad ng `-0.27` - ibig sabihin ay may saysay ang pagsasanay ng predictive model.

> Bago magsanay ng linear regression model, mahalagang tiyakin na malinis ang ating data. Hindi maganda ang linear regression kapag may mga missing values, kaya nararapat na alisin ang lahat ng walang lamang cells:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Isa pang paraan ay punan ang mga walang laman na halaga gamit ang mean values mula sa katugmang kolum.

## Simple Linear Regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 I-click ang larawan sa itaas para sa maikling video overview ng linear at polynomial regression.

Para sanayin ang Linear Regression model natin, gagamitin natin ang **Scikit-learn** library.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Sinisimulan natin sa paghihiwalay ng mga input values (features) at ang inaasahang output (label) sa magkahiwalay na numpy arrays:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Tandaan na kinailangan nating gawin ang `reshape` sa input na data upang maintindihan ito ng Linear Regression package nang tama. Ang Linear Regression ay inaasahan ang 2D-array bilang input, kung saan bawat hilera ng array ay tumutukoy sa isang vector ng input na mga katangian. Sa ating kaso, dahil isa lang ang input, kailangan natin ng array na may hugis na N&times;1, kung saan ang N ay ang laki ng dataset.

Pagkatapos, kailangan nating hatiin ang data sa train at test datasets, upang ma-validate natin ang model pagkatapos ng training:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Sa wakas, ang pagsasanay ng aktwal na Linear Regression model ay ginagawa lamang sa dalawang linya ng code. Idefine natin ang `LinearRegression` object, at i-fit ito sa ating data gamit ang `fit` method:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Ang `LinearRegression` na object pagkatapos mag-`fit` ay naglalaman ng lahat ng coefficients ng regression, na maaaring ma-access gamit ang `.coef_` na property. Sa ating kaso, may isa lamang coefficient, na dapat ay nasa paligid ng `-0.017`. Ibig sabihin nito, tila bumababa ang mga presyo kasabay ng paglipas ng panahon, ngunit hindi masyadong malaki, mga 2 sentimo bawat araw. Maaari rin nating i-access ang punto ng intersection ng regression sa Y-axis gamit ang `lin_reg.intercept_` - ito ay magiging mga `21` sa ating kaso, na nagpapahiwatig ng presyo sa simula ng taon.

Para makita kung gaano kasaktong ang ating modelo, maaari nating i-predict ang mga presyo sa test dataset, at pagkatapos ay sukatin kung gaano kalapit ang ating mga prediction sa inaasahang mga halaga. Maaari itong gawin gamit ang root mean square error (RMSE) metrics, na siyang root ng mean ng lahat ng squared differences sa pagitan ng inaasahan at predicted na halaga.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Ang ating error ay tila nasa paligid ng 2 puntos, na mga ~17%. Hindi masyadong maganda. Isa pang tagapagpahiwatig ng kalidad ng modelo ay ang **coefficient of determination**, na maaaring makuha nang ganito:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```

Kung ang halaga ay 0, ibig sabihin ay hindi isinasaalang-alang ng modelo ang input data, at kumikilos bilang *pinakapangit na linear predictor*, na simpleng mean value ng resulta. Ang halaga na 1 ay nangangahulugang maaari nating perpektong mahulaan ang lahat ng inaasahang output. Sa ating kaso, ang coefficient ay mga 0.06, na medyo mababa.

Maaari rin nating i-plot ang test data kasama ang regression line upang mas makita nang mabuti kung paano gumagana ang regression sa ating kaso:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/tl/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

Isa pang uri ng Linear Regression ay Polynomial Regression. Habang minsan ay may linear na relasyon sa pagitan ng mga variable - mas malaki ang kalabasa sa volume, mas mataas ang presyo - minsan hindi maaaring i-plot ang mga relasyong ito bilang isang patag o tuwid na linya.

✅ Narito ang [ilang karagdagang halimbawa](https://online.stat.psu.edu/stat501/lesson/9/9.8) ng data na maaaring gumamit ng Polynomial Regression

Tingnan pang muli ang relasyon sa pagitan ng Date at Price. Para bang ang scatterplot ba ay dapat talagang suriin gamit ang tuwid na linya? Hindi ba maaaring mag-fluctuate ang mga presyo? Sa kasong ito, maaari mong subukan ang polynomial regression.

✅ Ang mga polynomial ay mga matematikal na ekspresyon na maaaring binubuo ng isa o higit pang mga variable at coefficients

Ang polynomial regression ay lumilikha ng kurbadang linya upang mas maiangkop ang nonlinear na data. Sa ating kaso, kung isasama natin ang squared `DayOfYear` na variable sa input data, dapat nating magawang i-fit ang ating data gamit ang parabolic curve, na magkakaroon ng minimum sa isang tiyak na punto sa loob ng taon.

Kasama sa Scikit-learn ang kapaki-pakinabang na [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) upang pagsamahin ang iba't ibang mga hakbang ng data processing. Ang **pipeline** ay isang chain ng **estimators**. Sa ating kaso, gagawa tayo ng pipeline na unang nagdaragdag ng polynomial features sa ating modelo, at pagkatapos ay nagtetrain ng regression:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Ang paggamit ng `PolynomialFeatures(2)` ay nangangahulugan na isasama natin ang lahat ng second-degree polynomials mula sa input data. Sa ating kaso, ito ay nangangahulugang `DayOfYear`<sup>2</sup> lamang, ngunit kung merong dalawang input na variable na X at Y, ito ay magdaragdag ng X<sup>2</sup>, XY at Y<sup>2</sup>. Maaari din nating gamitin ang mga polynomial ng mas mataas na degree kung nais natin.

Maaaring gamitin ang mga pipelines sa parehong paraan tulad ng orihinal na `LinearRegression` object, ibig sabihin maaari nating `fit` ang pipeline, at pagkatapos ay gamitin ang `predict` upang makuha ang mga resulta ng prediction. Narito ang graph na nagpapakita ng test data, at ang approximation curve:

<img alt="Polynomial regression" src="../../../../translated_images/tl/poly-results.ee587348f0f1f60b.webp" width="50%" />

Gamit ang Polynomial Regression, makakakuha tayo ng bahagyang mas mababang MSE at mas mataas na coefficient of determination, ngunit hindi gaanong malaki ang kaibahan. Kailangan nating isaalang-alang ang ibang mga features!

> Makikita mo na ang pinakamababang presyo ng kalabasa ay naobserbahan sa paligid ng Halloween. Paano mo ito maipapaliwanag?

🎃 Congratulations, kakagawa mo lang ng isang modelo na makakatulong mag-predict ng presyo ng pie pumpkins. Maaari mong ulitin ang parehong proseso para sa lahat ng uri ng kalabasa, ngunit ito ay magiging mahirap. Alamin natin ngayon kung paano isaalang-alang ang iba't ibang uri ng kalabasa sa ating modelo!

## Categorical Features

Sa perpektong mundo, gusto nating makapag-predict ng presyo para sa iba't ibang variety ng kalabasa gamit ang parehong modelo. Ngunit, ang column na `Variety` ay medyo iba sa mga column tulad ng `Month`, dahil naglalaman ito ng mga non-numeric na halaga. Ang mga ganitong uri ng column ay tinatawag na **categorical**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 I-click ang larawan sa itaas para sa isang maikling video overview ng paggamit ng categorical features.

Dito makikita mo kung paano ang average price ay nakasalalay sa variety:

<img alt="Average price by variety" src="../../../../translated_images/tl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Para isaalang-alang ang variety, kailangan muna natin itong i-convert sa numeric na anyo, o **i-encode** ito. May ilang paraan kung paano natin ito magagawa:

* Ang simpleng **numeric encoding** ay gagawa ng talaan ng iba't ibang variety, at pagkatapos ay papalitan ang pangalan ng variety ng isang index sa talaang iyon. Hindi ito pinakamagandang ideya para sa linear regression, dahil ang linear regression ay kumukuha ng aktwal na numeric value ng index, at ina-add ito sa resulta, na minamultiply ng isang coefficient. Sa ating kaso, ang relasyon sa pagitan ng bilang ng index at presyo ay malinaw na hindi linear, kahit na siguraduhin natin na ang mga index ay nakaayos sa isang tiyak na paraan.
* Ang **one-hot encoding** ay papalitan ang `Variety` column ng 4 na magkakaibang columns, isa para sa bawat variety. Bawat column ay magkakaroon ng `1` kung ang katumbas na row ay nasa isang partikular na variety, at `0` kung hindi. Ibig sabihin nito ay magkakaroon ng apat na coefficients sa linear regression, isa para sa bawat variety ng kalabasa, na responsable para sa "starting price" (o mas tama "karagdagang presyo") para sa partikular na variety na iyon.

Ipinapakita ng code sa ibaba kung paano natin mae-one-hot encode ang variety:

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

Para mag-train ng linear regression gamit ang one-hot encoded na variety bilang input, kailangan lang nating i-initialize ang `X` at `y` na data nang tama:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Ang natitirang bahagi ng code ay pareho sa ginamit natin sa itaas para mag-train ng Linear Regression. Kung susubukan mo ito, makikita mo na halos pareho ang mean squared error, ngunit makakakuha tayo ng mas mataas na coefficient of determination (~77%). Para makakuha pa ng mas tumpak na predictions, maaari nating isaalang-alang ang mas maraming categorical na features, pati na rin ang numeric na features, tulad ng `Month` o `DayOfYear`. Para makuha ang isang malaking array ng features, maaari nating gamitin ang `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Dito isinaalang-alang din natin ang `City` at uri ng `Package`, na nagbigay sa atin ng MSE 2.84 (10%), at determination na 0.94!

## Pagsasama-sama ng lahat

Para makagawa ng pinakamahusay na modelo, maaari nating gamitin ang pinagsamang (one-hot encoded categorical + numeric) data mula sa halimbawa sa itaas kasabay ng Polynomial Regression. Narito ang buong code para sa iyong kaginhawaan:

```python
# ayusin ang data para sa pagsasanay
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# gawin ang hati ng pagsasanay-pagsubok
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# ayusin at sanayin ang pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# hulaan ang mga resulta para sa test data
pred = pipeline.predict(X_test)

# kalkulahin ang MSE at determinasyon
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Dapat magbigay ito sa atin ng pinakamagandang coefficient of determination na halos 97%, at MSE=2.23 (~8% na prediction error).

| Model | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| All features Linear | 2.84 (10.5%) | 0.94 |
| All features Polynomial | 2.23 (8.25%) | 0.97 |

🏆 Magaling! Nakagawa ka ng apat na Regression models sa isang aralin, at napabuti ang kalidad ng modelo hanggang 97%. Sa huling bahagi tungkol sa Regression, matututuhan mo ang tungkol sa Logistic Regression para tukuyin ang mga kategorya.

---
## 🚀Challenge

Subukan ang ilang iba't ibang mga variable sa notebook na ito upang makita kung paano ang korelasyon ay tumutugma sa katumpakan ng modelo.

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ml/)

## Review & Self Study

Sa araling ito natutunan natin ang tungkol sa Linear Regression. May iba pang mahahalagang uri ng Regression. Basahin tungkol sa Stepwise, Ridge, Lasso at Elasticnet techniques. Isang magandang kurso para pag-aralan upang matuto nang higit pa ay ang [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Assignment 

[Build a Model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Paunawa**:  
Ang dokumentong ito ay isinalin gamit ang AI translation service na [Co-op Translator](https://github.com/Azure/co-op-translator). Bagamat aming nilalayon ang katumpakan, pakatandaan na ang mga awtomatikong pagsasalin ay maaaring maglaman ng mga pagkakamali o di-katumpakan. Ang orihinal na dokumento sa orihinal nitong wika ang dapat ituring na pangunahing sanggunian. Para sa mahahalagang impormasyon, inirerekomenda ang propesyonal na pagsasaling-tao. Hindi kami mananagot sa anumang hindi pagkakaunawaan o maling interpretasyon na maaaring magmula sa paggamit ng pagsasaling ito.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->