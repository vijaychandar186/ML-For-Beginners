# Jenga mfano wa regression kwa kutumia Scikit-learn: namna nne za regression

## Kumbusho kwa Waanzaji

Linear regression hutumika tunapotaka kutabiri **thamani ya nambari** (kwa mfano, bei ya nyumba, joto, au mauzo).
Inafanya kazi kwa kupata mstari wa moja kwa moja unaowakilisha vizuri uhusiano kati ya vipengele vya ingizo na matokeo.

Katika somo hili, tunazingatia kuelewa dhana kabla ya kuchunguza mbinu za regression zilizo juu zaidi.
![Linear vs polynomial regression infographic](../../../../translated_images/sw/linear-polynomial.5523c7cb6576ccab.webp)
> Infographic na [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Jaribio la awali](https://ff-quizzes.netlify.app/en/ml/)

> ### [Somo hili lipo pia kwa R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Utangulizi

Hadi sasa umechunguza ni regression ni nini kwa data mfano iliyokusanywa kutoka kwenye dataset ya bei ya malenge ambayo tutaitumia kwa somo hili lote. Pia umeionyesha kwa kutumia Matplotlib.

Sasa uko tayari kuingia zaidi katika regression kwa ML. Wakati uoneshaji (visualization) unakuwezesha kuelewa data, nguvu halisi ya Machine Learning hutokana na _kujifunza kwa mifano_. Mifano hujifunza kwa data ya kihistoria ili kunasa uhusiano wa data kiotomatiki, na hukuwezesha kutabiri matokeo kwa data mpya, ambayo mfano haujawahi kuona kabla.

Katika somo hili, utajifunza zaidi kuhusu aina mbili za regression: _linear regression msingi_ na _polynomial regression_, pamoja na baadhi ya hesabu zilizo nyuma ya mbinu hizi. Mifano hiyo itatuwezesha kutabiri bei za malenge kulingana na data tofauti za ingizo.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Bonyeza picha hapo juu kwa video fupi ya muhtasari wa linear regression.

> Katika mtaala huu mzima, tunadhani ujuzi mdogo wa hesabu, na tunalenga kuufanya uwe rahisi kwa wanafunzi kutoka nyanja nyingine, hivyo angalia vidokezo, 🧮 maelezo, michoro, na zana nyingine za kujifunzia kusaidia kuelewa.

### Mahitaji ya awali

Unapaswa kuwa unafahamu sasa muundo wa data ya malenge ambayo tunaiangalia. Unaweza kuipata tayari imepakizwa na kusafishwa kwenye faili _notebook.ipynb_ ya somo hili. Katika faili hiyo, bei ya malenge inaonyeshwa kwa kila bakuli katika fremu mpya ya data. Hakikisha unaweza kuendesha vitabu hivi kwenye kernels za Visual Studio Code.

### Maandalizi

Kama kumbusho, unapopakua data hii ili kuweza kuuliza maswali juu yake.

- Ni lini ni wakati bora wa kununua malenge?
- Bei gani ninaweza kutarajia kwa sanduku la malenge madogo?
- Je, nipate kwa nusu-bushel katika vikapu au kwa sanduku la 1 1/9 bushel?
Tuendelee kuchunguza data hii.

Katika somo lililopita, uliunda fremu ya data ya Pandas na kuijaza kwa sehemu ya dataset ya awali, ukipatanisha bei kwa bakuli. Kwa kufanya hivyo, ulifanikiwa kukusanya takriban pointi 400 za data na kwa miezi ya vuli tu.

Tazama data tuliyoipakia tayari katika daftari la somo hili. Data imesababishwa na mchoro wa kunyeshea kuonyesha data ya mwezi. Labda tunaweza kupata maelezo zaidi kuhusu asili ya data kwa kusafisha zaidi.

## Mstari wa regression wa moja kwa moja (linear regression)

Kama ulivyojifunza katika Somo la 1, lengo la zoezi la linear regression ni kuwezesha kutoa mchoro wa mstari ili:

- **Onyesha uhusiano wa vigezo**. Onyesha uhusiano kati ya vigezo
- **Fanya utabiri**. Fanya utabiri sahihi wa mahali ambapo pointi mpya ya data itakuwa kuhusiana na mstari huo.
 
Ni kawaida kwa **Least-Squares Regression** kuchora mstari wa aina hii. Neno "Least-Squares" linarejelea mchakato wa kupunguza jumla ya makosa katika mfano wetu. Kwa kila pointi ya data, tunaepima umbali wima (unaoitwa residual) kati ya pointi halisi na mstari wa regression.

Tunazidisha umbali huu kwa mraba kwa sababu kuu mbili:

1. **Ukubwa kuliko Mwelekeo:** Tunataka kushughulikia kosa la -5 kama vile kosa la +5. Kupindisha mraba kunafanya thamani zote kuwa chanya.

2. **Kuwadhibiti Wasiokuwa Na Kawaida:** Kupindisha mraba kunazidisha uzito wa makosa makubwa, na kulazimisha mstari kuwa karibu zaidi na pointi zilizoko mbali.

Kisha tunajumlisha thamani zote hizi za mraba. Lengo letu ni kupata mstari maalum ambapo jumla hii ya mwisho ni ndogo zaidi (thamani ndogo kabisa) — ndiyo maana inaitwa "Least-Squares".

> **🧮 Nionyeshe hesabu**  
> 
> Mstari huu, unaoitwa _mstari wa kufaa vizuri_, unaweza kuelezwa na [sawia](https://en.wikipedia.org/wiki/Simple_linear_regression):  
> 
> ```
> Y = a + bX
> ```
>
> `X` ni 'kigezo kinachoelezea'. `Y` ni 'kigezo kinategemea'. Mwinuko wa mstari ni `b` na `a` ni kiingilio kwenye y-mhimili (y-intercept), kinachorejelea thamani ya `Y` wakati `X = 0`.
>
>![hesabu ya mwinuko](../../../../translated_images/sw/slope.f3c9d5910ddbfcf9.webp)
>
> Kwanza, hesabu mwinuko `b`. Infographic na [Jen Looper](https://twitter.com/jenlooper)
>
> Kwa maneno mengine, na kurejelea swali la data ya malenge: "tabiri bei ya malenge kwa bakuli kwa mwezi", `X` itaonyesha bei na `Y` itaonyesha mwezi wa mauzo.
>
>![kamilisha sawia](../../../../translated_images/sw/calculation.a209813050a1ddb1.webp)
>
> Hesabu thamani ya Y. Ikiwa unalipa karibu $4, lazima iwe Aprili! Infographic na [Jen Looper](https://twitter.com/jenlooper)
>
> Hesabu inayopima mstari lazima ionyeshe mwinuko wa mstari, pia inategemea intercept, au mahali `Y` wanapopatikana wakati `X = 0`.
>
> Unaweza kuangalia njia ya hesabu hizi kwenye tovuti ya [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Pia tembelea [kalkuleta hii ya Least-squares](https://www.mathsisfun.com/data/least-squares-calculator.html) kuona jinsi thamani za namba zinavyoathiri mstari.

## Uhusiano (Correlation)

Neno moja zaidi la kuelewa ni **Uwiano wa Uhusiano** kati ya vigezo vya X na Y vilivyotolewa. Kutumia mchoro wa pointi za kufyatua (scatterplot), unaweza haraka kuona uwiano huu. Mchoro wenye pointi zinazopangwa kwa mstari mzuri unaonyesha uhusiano mkubwa, lakini mchoro wenye pointi zilizotawanyika kila mahali kati ya X na Y unaonyesha uhusiano mdogo.

Mfano mzuri wa linear regression utakuwa ule unaoonyesha Uwiano wa Juu (karibu na 1 kuliko 0) kwa kutumia mbinu ya Least-Squares Regression na mstari wa regression.

✅ Endesha daftari la somo hili na angalia mchoro wa Mwezi dhidi ya Bei. Je, data inayohusisha Mwezi na Bei kwa mauzo ya malenge inaonekana kuwa na uhusiano mkubwa au mdogo, kulingana na tafsiri yako ya picha ya scatterplot? Je, hiyo inabadilika ikiwa unatumia kipimo kidogo zaidi badala ya `Mwezi`, kwa mfano, *siku ya mwaka* (yaani, idadi ya siku tangu mwanzo wa mwaka)?

Katika msimbo hapa chini, tutaidhinisha kwamba tumesafisha data, na kupata fremu ya data inayoitwa `new_pumpkins`, kama ifuatavyo:

ID | Mwezi | DayOfYear | Aina | Jiji | Mfuko | Bei ya Chini | Bei ya Juu | Bei
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Msimbo wa kusafisha data upo kwenye [`notebook.ipynb`](notebook.ipynb). Tumeifanya hatua sawa za usafi kama katika somo lililopita, na tumekokotoa safu ya `DayOfYear` kwa kutumia kaulimbiu ifuatayo:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Sasa baada ya kuwa na ufahamu wa hesabu za nyuma ya linear regression, hebu tujenge mtindo wa Regression kuona kama tunaweza kutabiri ni mfuko gani wa malenge utakuwa na bei bora zaidi. Mtu anayenunua malenge kwa sherehe anaweza kutaka habari hii ili kuboresha ununuzi wa pakiti za malenge kwa sherehe.

## Kutafuta Uhusiano

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Bonyeza picha hapo juu kwa video fupi ya muhtasari wa uhusiano.

Kutoka somo lililopita huenda umeona kuwa bei ya wastani kwa miezi mbalimbali inaonekana hivi:

<img alt="Average price by month" src="../../../../translated_images/sw/barchart.a833ea9194346d76.webp" width="50%"/>

Hii inaonyesha kuwa kunapaswa kuwepo na uhusiano, na tunaweza kujaribu kufundisha mfano wa linear regression kutabiri uhusiano kati ya `Mwezi` na `Bei`, au kati ya `DayOfYear` na `Bei`. Hapa kuna mchoro wa kina unaoonyesha uhusiano wa mwisho:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sw/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Tuchukulie kama kuna uhusiano kwa kutumia kazi ya `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Inaonekana uwiano ni mdogo kidogo, -0.15 kwa `Mwezi` na -0.17 kwa `DayOfMonth`, lakini kunaweza kuwepo na uhusiano mwingine muhimu. Inaonekana kama kunao makundi tofauti ya bei kulingana na aina tofauti za malenge. Ili kuthibitisha nadharia hii, tuchore kila kundi la malenge kwa rangi tofauti. Kwa kupitisha parameta `ax` kwa kazi ya scatterplot tunaweza kuchora pointi zote kwenye mchoro mmoja:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sw/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Uchunguzi wetu unaonyesha kuwa aina inaathiri zaidi bei kuliko tarehe halisi ya mauzo. Tunaweza kuona hili kwa mchoro wa mihimili (bar graph):

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/sw/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Tujizomee kwa muda kwa aina moja tu ya malenge, 'aina ya pie type', na tuelewe athari ya tarehe kwenye bei:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sw/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Sasa tukihesabu uwiano kati ya `Bei` na `DayOfYear` kwa kutumia kazi ya `corr`, tutapata kitu kama `-0.27` - ambayo ina maana kuwa kufundisha mfano wa utabiri kunaeleweka.

> Kabla ya kufundisha mfano wa linear regression, ni muhimu kuhakikisha data yetu ni safi. Linear regression haiendani vizuri na vipengele vilivyokosa (missing values), hivyo inafaa kuondoa seli zote tupu:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Njia nyingine ni kujaza thamani tupu kwa thamani za wastani kutoka kwenye safu husika.

## Linear Regression Rahisi

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Bonyeza picha hapo juu kwa video fupi ya muhtasari wa linear na polynomial regression.

Ili kufundisha mfano wetu wa Linear Regression, tutatumia maktaba ya **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Tunaanza kwa kutenganisha vitu vya ingizo (features) na matokeo yanayotarajiwa (label) katika matrekta tofauti ya numpy:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Kumbuka tulilazimika kufanya `reshape` kwa data ya ingizo ili kifurushi cha Linear Regression kiielewe vyema. Linear Regression inatarajia array ya 2D kama ingizo, ambapo kila safu ni vekta ya vipengele vya ingizo. Kwa kuwa tunayo ingizo moja tu, tunahitaji array yenye umbo la N&times;1, ambapo N ni ukubwa wa dataset.

Kisha, tunahitaji kugawanya data kuwa datasets za mafunzo na majaribio, ili tuweze kuthibitisha mfano baada ya mafunzo:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Mwishowe, kufundisha mfano halisi wa Linear Regression kunachukua mistari miwili tu ya msimbo. Tunaelezea kitu cha `LinearRegression`, na kukiambatanisha na data yetu kwa kutumia njia `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Kitu cha `LinearRegression` baada ya kufanywa `fit` kina coefficients zote za regression, ambazo zinaweza kupatikana kwa kutumia mali ya `.coef_`. Katika kesi yetu, kuna coefficient moja tu, ambayo inapaswa kuwa karibu na `-0.017`. Hii ina maana bei zinaonekana kushuka kidogo kwa muda, lakini si nyingi sana, takriban senti 2 kwa siku. Tunaweza pia kupata sehemu ya kukutana ya regression na mhimili wa Y kwa kutumia `lin_reg.intercept_` - itakuwa karibu na `21` katika kesi yetu, ikionyesha bei mwanzoni mwa mwaka.

Ili kuona usahihi wa mfano wetu, tunaweza kutabiri bei kwenye seti ya data ya mtihani, kisha kupima jinsi makisio yetu yalivyo karibu na maadili yanayotarajiwa. Hii inaweza kufanyika kwa kutumia metrics ya root mean square error (RMSE), ambayo ni mizizi ya wastani wa tofauti zote zilizochukuliwa mraba kati ya thamani inayotarajiwa na inayotabiriwa.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Kosa letu linaonekana kuwa takriban pointi 2, ambayo ni ~17%. Si nzuri sana. Kiashiria kingine cha ubora wa mfano ni **coefficient of determination**, ambayo inaweza kupatikana kama hii:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Ikiwa thamani ni 0, ina maana mfano hauzingatii data ya ingizo, na hufanya kama *mtabiri mbaya zaidi wa mstari*, ambao ni wastani tu wa matokeo. Thamani ya 1 ina maana tunaweza kutabiri kwa usahihi zote matokeo yote yanayotarajiwa. Katika kesi yetu, coefficient ni takriban 0.06, ambayo ni ya chini sana.

Tunaweza pia kuchora data ya mtihani pamoja na mstari wa regression kuona vizuri jinsi regression inavyofanya kazi katika kesi yetu:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/sw/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

Aina nyingine ya Linear Regression ni Polynomial Regression. Wakati mwingine kuna uhusiano wa mstari kati ya vigezo - vile vile ukubwa wa loti huongezeka, ndivyo bei inavyoongezeka - wakati mwingine uhusiano huu hauwezi kuchorwa kama usawa au mstari wa moja kwa moja.

✅ Hapa kuna [mifano mingine zaidi](https://online.stat.psu.edu/stat501/lesson/9/9.8) ya data ambayo inaweza kutumia Polynomial Regression

Tazama tena uhusiano kati ya Tarehe na Bei. Je, mchoro huu wa mchanganyiko unaonekana kwamba lazima uchunguzwe kwa mstari wa moja kwa moja? Je, bei haziwezi kubadilika? Katika kesi hii, unaweza kujaribu polynomial regression.

✅ Polynomials ni misemo ya hisabati ambayo inaweza kuwa na vigezo moja au zaidi pamoja na coefficients

Polynomial regression huunda mstari wa mviringo ili kuendana vizuri zaidi na data isiyo mstari. Katika kesi yetu, ikiwa tutajumuisha kigezo chenye kiwango cha mraba `DayOfYear` katika data ya ingizo, tunapaswa kuwa na uwezo wa kulinganisha data yetu na curve ya parabolic, ambayo itakuwa na kiwango cha chini mahali fulani ndani ya mwaka.

Scikit-learn inajumuisha API ya [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) inayosaidia kuunganisha hatua tofauti za usindikaji wa data pamoja. **pipeline** ni mnyororo wa **estimators**. Katika kesi yetu, tutaunda pipeline ambayo kwanza inaongeza sifa za polynomial kwenye mfano wetu, kisha kuandaa regression:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Kutumia `PolynomialFeatures(2)` ina maana kwamba tutajumuisha polynomials zote za daraja la pili kutoka kwa data ya ingizo. Katika kesi yetu itamaanisha tu `DayOfYear`<sup>2</sup>, lakini ikizingatiwa vigezo viwili vya ingizo X na Y, hii itaongeza X<sup>2</sup>, XY na Y<sup>2</sup>. Tunaweza pia kutumia polynomials za daraja kubwa zaidi ikiwa tunataka.

Pipelines zinaweza kutumiwa kwa njia ile ile kama kitu cha asili cha `LinearRegression`, yaani tunaweza `fit` pipeline, kisha tumia `predict` kupata matokeo ya utabiri. Hii ni grafu inayoonyesha data ya mtihani, na curve ya makadirio:

<img alt="Polynomial regression" src="../../../../translated_images/sw/poly-results.ee587348f0f1f60b.webp" width="50%" />

Kwa kutumia Polynomial Regression, tunaweza kupata MSE kidogo chini na coefficient ya determination kubwa zaidi, lakini si kwa kiwango kikubwa. Tunahitaji kuzingatia sifa zingine!

> Unaweza kuona kuwa bei za chini kabisa za loti zinapatikana karibu na Sikukuu ya Halloween. Unawezaje kueleza hili? 

🎃 Hongera, umeunda mfano ambao unaweza kusaidia kutabiri bei ya maloti ya pie. Labda unaweza kurudia utaratibu huo kwa aina zote za maloti, lakini hiyo itakuwa ya kuchosha. Sasa tufurahie kujifunza jinsi ya kuzingatia aina ya loti katika mfano wetu!

## Vipengele vya Kikategoria

Katika ulimwengu wa kawaida, tunataka kuweza kutabiri bei kwa aina tofauti za loti kwa kutumia mfano mmoja. Hata hivyo, safu ya `Variety` ni tofauti kidogo na safu kama `Month`, kwa sababu ina maadili yasiyo nambari. Safu kama hizi huitwa **kategoria**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Bonyeza picha hapo juu kwa video fupi ya matumizi ya vipengele vya kategoria.

Hapa unaweza kuona jinsi bei ya wastani inavyotegemea aina:

<img alt="Average price by variety" src="../../../../translated_images/sw/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Ili kuzingatia aina, kwanza tunahitaji kuibadilisha kuwa muundo wa nambari, au **kuandika**. Kuna njia kadhaa tunazoweza kuifanya:

* **Kudhibiti mduara wa nambari rahisi** kutatengeneza jedwali la aina tofauti, kisha kubadilisha jina la aina kwa nambari ya index katika jedwali hili. Hii si wazo bora kwa regression ya mstari, kwa sababu regression ya mstari huchukua nambari halisi ya index, na kuongeza kwenye matokeo, ikizidisha na coefficient fulani. Katika kesi yetu, uhusiano kati ya nambari ya index na bei ni wazi kuwa si mstari, hata tukihakikisha kuwa maindex yamepangwa kwa njia fulani maalum.
* **One-hot encoding** itabadilisha safu ya `Variety` kuwa safu 4 tofauti, moja kwa kila aina. Kila safu itakuwa na `1` ikiwa mstari husika ni wa aina fulani, na `0` vinginevyo. Hii ina maana kutakuwa na coefficients nne katika regression ya mstari, moja kwa kila aina ya loti, inayohusika na "bei ya mwanzo" (au badala yake "bei ya ziada") kwa aina husika.

Nambari hapa chini inaonyesha jinsi ya kufanya one-hot encode kwa aina:

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

Ili kufundisha regression ya mstari kwa kutumia aina zilizohifadhiwa kama one-hot encoded, tunahitaji tu kuanzisha data za `X` na `y` kwa usahihi:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Mengine ya msimbo ni sawa na tuliotumia hapo juu kufundisha Linear Regression. Ukijaribu, utaona kuwa mean squared error ni takriban ile ile, lakini tunapata coefficient kubwa zaidi ya determination (~77%). Ili kupata utabiri sahihi zaidi, tunaweza kuzingatia vipengele vya kategoria vingi zaidi, pamoja na vipengele vya nambari, kama `Month` au `DayOfYear`. Ili kupata safu kubwa ya vipengele, tunaweza kutumia `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Hapa pia tunazingatia `City` na aina ya `Package`, ambayo inatupa MSE 2.84 (10%), na coefficient ya determination 0.94!

## Kuunganisha yote pamoja

Ili kutengeneza mfano bora zaidi, tunaweza kutumia data mchanganyiko (ya one-hot encoded kategoria + nambari) kutoka mfano wa juu pamoja na Polynomial Regression. Huu ndio msimbo kamili kwa urahisi wako:

```python
# weka data ya mafunzo
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# tengeneza mgawanyo wa mafunzo-na-majaribio
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# weka na faya mfumo wa mafunzo
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# tabiri matokeo kwa data ya majaribio
pred = pipeline.predict(X_test)

# hesabu MSE na uamuzi
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Hii inapaswa kutupatia coefficient bora zaidi ya determination ya karibu 97%, na MSE=2.23 (~8% kosa la utabiri).

| Mfano | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| Vipengele vyote Linear | 2.84 (10.5%) | 0.94 |
| Vipengele vyote Polynomial | 2.23 (8.25%) | 0.97 |

🏆 Hongera! Umeunda mifano minne ya Regression katika somo moja, na kuboresha ubora wa mfano hadi 97%. Katika sehemu ya mwisho kuhusu Regression, utajifunza kuhusu Logistic Regression kutambua makundi.

---
## 🚀Changamoto

Jaribu vigezo tofauti kadhaa katika daftari hili kuona jinsi uhusiano unavyolingana na usahihi wa mfano.

## [Mtihani baada ya somo](https://ff-quizzes.netlify.app/en/ml/)

## Mapitio & Kujifunza Binafsi

Katika somo hili tulijifunza kuhusu Linear Regression. Kuna aina zingine muhimu za Regression. Soma kuhusu mbinu za Stepwise, Ridge, Lasso na Elasticnet. Kozi nzuri ya kujifunza zaidi ni [kozi ya Stanford ya Kujifunza Takwimu](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Kazi ya Nyumbani

[Jenga Mfano](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Hekweti**:  
Hati hii imetatuliwa kwa kutumia huduma ya kutafsiri AI [Co-op Translator](https://github.com/Azure/co-op-translator). Ingawa tunajitahidi kwa usahihi, tafadhali fahamu kuwa tafsiri za kiotomatiki zinaweza kuwa na makosa au ukosefu wa usahihi. Hati ya awali katika lugha yake asili inapaswa kuchukuliwa kama chanzo cha mamlaka. Kwa taarifa muhimu, tafsiri ya mtaalamu wa binadamu inashauriwa. Hatubebwi dhamana kwa kutoelewana au tafsiri potofu zinazotokana na kutumia tafsiri hii.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->