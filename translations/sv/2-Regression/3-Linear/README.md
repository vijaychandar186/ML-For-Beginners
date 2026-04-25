# Bygg en regressionsmodell med Scikit-learn: regression på fyra sätt

## Nybörjarnotering

Linjär regression används när vi vill förutsäga ett **numeriskt värde** (till exempel huspris, temperatur eller försäljning).
Det fungerar genom att hitta en rät linje som bäst representerar sambandet mellan inmatningsfunktionerna och utdata.

I denna lektion fokuserar vi på att förstå konceptet innan vi utforskar mer avancerade regressionstekniker.
![Linear vs polynomial regression infographic](../../../../translated_images/sv/linear-polynomial.5523c7cb6576ccab.webp)
> Informationsgrafik av [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [För-lectures quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Denna lektion finns tillgänglig på R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introduktion

Hittills har du utforskat vad regression är med exempeldata hämtad från pumpapriser datasetet som vi kommer att använda genom hela denna lektion. Du har också visualiserat det med hjälp av Matplotlib.

Nu är du redo att gå djupare in i regression för maskininlärning. Medan visualisering låter dig göra data begripligt, kommer den verkliga styrkan i maskininlärning från _träning av modeller_. Modeller tränas på historisk data för att automatiskt fånga databeroenden, och de låter dig förutsäga resultat för ny data som modellen inte har sett tidigare.

I denna lektion kommer du att lära dig mer om två typer av regression: _grundläggande linjär regression_ och _polynomregression_, tillsammans med något av matematiken bakom dessa tekniker. Dessa modeller kommer att göra det möjligt för oss att förutsäga pumpapris beroende på olika indata.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klicka på bilden ovan för en kort videoöversikt över linjär regression.

> Genom hela detta läroplan antar vi minimala matematiska förkunskaper, och strävar efter att göra det tillgängligt för studenter från andra fält, så håll utkik efter anteckningar, 🧮 utropstecken, diagram och andra lärverktyg som hjälper till vid förståelsen.

### Förkunskaper

Du bör nu vara bekant med strukturen på pumpadatan som vi undersöker. Du hittar den förladdad och förrensad i detta lektions _notebook.ipynb_-fil. I filen visas pumpapriset per skålpund i en ny dataframe. Se till att du kan köra dessa notebooks i kernels i Visual Studio Code.

### Förberedelse

Som en påminnelse, laddar du in denna data för att kunna ställa frågor om den. 

- När är den bästa tiden att köpa pumpor?
- Vilket pris kan jag förvänta mig för en låda miniature-pumpor?
- Ska jag köpa dem i halva skålpundskorgar eller per 1 1/9 skålpundslåda?
Låt oss fortsätta gräva i denna data.

I föregående lektion skapade du en Pandas dataframe och fyllde den med en del av originaldatasetet, och standardiserade prisningen efter skålpund. Genom att göra det kunde du dock bara samla ungefär 400 datapunkter och bara för höstmånaderna.

Titta på datan som vi förladdat i denna lektions tillhörande notebook. Datan är förladdad och en initial scatterplot plottad för att visa månadens data. Kanske kan vi få lite mer detaljer om datans natur genom att rengöra den mer.

## En linjär regressionslinje

Som du lärde dig i Lektion 1 är målet med en linjär regression att kunna rita en linje som:

- **Visar variabelrelationer**. Visar sambandet mellan variablerna
- **Gör förutsägelser**. Gör korrekta förutsägelser om var en ny datapunkt skulle falla i förhållande till den linjen.
 
Det är vanligt med **minsta kvadratmetoden (Least-Squares Regression)** att rita denna typ av linje. Begreppet "Least-Squares" hänvisar till processen att minimera den totala felet i vår modell. För varje datapunkt mäter vi det vertikala avståndet (kallat residual) mellan den verkliga punkten och vår regressionslinje.

Vi kvadrerar dessa avstånd av två huvudsakliga anledningar:

1. **Storlek över riktning:** Vi vill behandla ett fel på -5 lika som ett fel på +5. Kvadreringen gör alla värden positiva.

2. **Straffa avvikare:** Kvadrering ger högre vikt åt större fel, vilket tvingar linjen att hålla sig närmare punkter som ligger långt bort.

Vi adderar sedan alla dessa kvadrerade värden tillsammans. Vårt mål är att hitta den specifika linjen där denna summa är som minst (det minsta möjliga värdet)—därav namnet "Least-Squares".

> **🧮 Visa mig matematiken** 
> 
> Denna linje, kallad _bästa passande linje_ kan uttryckas med [en ekvation](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` är den 'förklarande variabeln'. `Y` är den 'beroende variabeln'. Lutningen av linjen är `b` och `a` är y-axelns skärningspunkt, som avser värdet på `Y` när `X = 0`.
>
>![räkna ut lutningen](../../../../translated_images/sv/slope.f3c9d5910ddbfcf9.webp)
>
> Först, räkna ut lutningen `b`. Informationsgrafik av [Jen Looper](https://twitter.com/jenlooper)
>
> Med andra ord, och med hänvisning till vår pumpadata ursprungliga fråga: "förutsäg priset på en pumpa per skålpund per månad", skulle `X` hänvisa till priset och `Y` till försäljningsmånaden.
>
>![komplettera ekvationen](../../../../translated_images/sv/calculation.a209813050a1ddb1.webp)
>
> Beräkna värdet på Y. Om du betalar runt 4 dollar måste det vara april! Informationsgrafik av [Jen Looper](https://twitter.com/jenlooper)
>
> Matematiken som räknar fram linjen måste visa lutningen på linjen, som också beror på interceptet, eller var `Y` är placerad när `X = 0`.
>
> Du kan observera metoden för beräkning av dessa värden på webbplatsen [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Besök även [denna Least-squares-kalkylator](https://www.mathsisfun.com/data/least-squares-calculator.html) för att se hur siffrornas värden påverkar linjen.

## Korrelation

En term till som är viktig att förstå är **korrelationskoefficienten** mellan givna X- och Y-variabler. Med hjälp av en scatterplot kan du snabbt visualisera denna koefficient. En plot med datapunkter utspridda i en tydlig linje har hög korrelation, men en plot med datapunkter utspridda överallt mellan X och Y har låg korrelation.

En bra linjär regressionsmodell är en som har hög (närmare 1 än 0) korrelationskoefficient med metoden minsta kvadrater och en regressionslinje.

✅ Kör notebook som hör till denna lektion och titta på spridningsdiagrammet Månad till Pris. Verkar datan som kopplar Månad till Pris för pumpaförsäljning ha hög eller låg korrelation, enligt din visuella tolkning av scatterploten? Förändras det om du använder ett finare mått istället för `Month`, t.ex. *dag på året* (dvs. antal dagar sedan årets början)?

I koden nedan antar vi att vi har rengjort datan och fått en dataframe kallad `new_pumpkins`, liknande följande:

ID | Månad | DagPåÅret | Sort | Stad | Förpackning | Lågt Pris | Högt Pris | Pris
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Koden för att rengöra datan finns tillgänglig i [`notebook.ipynb`](notebook.ipynb). Vi har utfört samma rengöringssteg som i föregående lektion, och har beräknat kolumnen `DayOfYear` med följande uttryck:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Nu när du har förstått matematiken bakom linjär regression, låt oss skapa en regressionsmodell för att se om vi kan förutsäga vilken pumpaförpackning som kommer ha de bästa pumpaprisen. Någon som köper pumpor för en höstpumpaplantering kanske vill ha denna information för att kunna optimera köp av pumpapaket till planteringen.

## Letar efter korrelation

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klicka på bilden ovan för en kort videoöversikt över korrelation.

Från föregående lektion har du förmodligen sett att medelpriset för olika månader ser ut så här:

<img alt="Average price by month" src="../../../../translated_images/sv/barchart.a833ea9194346d76.webp" width="50%"/>

Det antyder att det borde finnas någon korrelation, och vi kan försöka träna en linjär regressionsmodell för att förutsäga sambandet mellan `Month` och `Price`, eller mellan `DayOfYear` och `Price`. Här är ett scatterplot som visar det senare sambandet:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sv/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Låt oss se om det finns korrelation med funktionen `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Det ser ut som att korrelationen är ganska liten, -0.15 för `Month` och -0.17 för `DayOfMonth`, men det kan finnas ett annat viktigt samband. Det ser ut som om det finns olika kluster av priser som korrelerar med olika pumpasorter. För att bekräfta denna hypotes, låt oss plotta varje pumpakategori med en annan färg. Genom att skicka en `ax` parameter till `scatter`-plotfunktion kan vi plotta alla punkter på samma graf:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sv/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Vår undersökning antyder att sorten har större effekt på det totala priset än själva försäljningsdatumet. Vi kan se detta med ett stapeldiagram:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/sv/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Låt oss nu fokusera endast på en pumpasort, 'pie type', och se vilken effekt datumet har på priset:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sv/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Om vi nu beräknar korrelationen mellan `Price` och `DayOfYear` med `corr`-funktionen, får vi ungefär `-0.27` – vilket betyder att det är meningsfullt att träna en prediktiv modell.

> Innan du tränar en linjär regressionsmodell är det viktigt att säkerställa att vår data är ren. Linjär regression fungerar inte bra med saknade värden, så det är vettigt att ta bort alla tomma celler:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Ett annat tillvägagångssätt kan vara att fylla dessa tomma värden med medelvärden från motsvarande kolumn.

## Enkel linjär regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klicka på bilden ovan för en kort videoöversikt över linjär och polynomregression.

För att träna vår linjära regressionsmodell kommer vi att använda **Scikit-learn**-biblioteket.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Vi börjar med att separera indata (funktioner) och det förväntade resultatet (etikett) i separata numpy-arrayer:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Observera att vi var tvungna att använda `reshape` på indata för att linjär regressionspaketet ska förstå det korrekt. Linjär regression förväntar sig en 2D-array som indata, där varje rad i arrayen motsvarar en vektor av indatafunktioner. I vårt fall, eftersom vi bara har en indata, behöver vi en array med formen N×1, där N är datasetets storlek.

Därefter behöver vi dela data i tränings- och testdataset, så att vi kan validera vår modell efter träning:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Slutligen tar själva träningen av den linjära regressionsmodellen bara två kodrader. Vi definierar `LinearRegression`-objektet och anpassar det till vår data med metoden `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression`-objektet efter att ha `fit`ats innehåller alla regressionskoefficienter, som kan nås med `.coef_`-egenskapen. I vårt fall finns det bara en koefficient, som bör vara runt `-0.017`. Det betyder att priserna verkar sjunka lite med tiden, men inte för mycket, cirka 2 cent per dag. Vi kan också nå regressionsens skärningspunkt med Y-axeln med `lin_reg.intercept_` - den kommer att vara runt `21` i vårt fall, vilket indikerar priset i början av året.

För att se hur exakt vår modell är kan vi förutsäga priser på en testdatamängd och sedan mäta hur nära våra förutsägelser är de förväntade värdena. Detta kan göras med metrik som rotmedelkvadratfel (RMSE), som är roten ur medelvärdet av alla kvadrerade skillnader mellan förväntat och förutspått värde.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Vårt fel verkar vara runt 2 poäng, vilket är ~17%. Inte så bra. En annan indikator på modellens kvalitet är **bestämningskoefficienten**, som kan erhållas så här:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Om värdet är 0 betyder det att modellen inte tar hänsyn till indata och agerar som den *sämsta linjära förutsägaren*, vilket helt enkelt är ett medelvärde av resultatet. Värdet 1 innebär att vi perfekt kan förutsäga alla förväntade utdata. I vårt fall är koefficienten runt 0,06, vilket är ganska lågt.

Vi kan också plotta testdata tillsammans med regressionslinjen för att bättre se hur regression fungerar i vårt fall:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/sv/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomregression

En annan typ av linjär regression är polynomregression. Ibland finns det ett linjärt samband mellan variabler – ju större pumpa i volym, desto högre pris – men ibland kan dessa samband inte avbildas som ett plan eller en rät linje.

✅ Här är [några fler exempel](https://online.stat.psu.edu/stat501/lesson/9/9.8) på data som kan dra nytta av polynomregression

Titta igen på sambandet mellan datum och pris. Verkar denna scatterplot nödvändigtvis behöva analyseras med en rak linje? Kan inte priserna variera? I sådana fall kan du testa polynomregression.

✅ Polynom är matematiska uttryck som kan bestå av en eller flera variabler och koefficienter

Polynomregression skapar en kurvad linje för att bättre passa icke-linjära data. I vårt fall, om vi inkluderar en kvadrerad `DayOfYear`-variabel i indata, borde vi kunna anpassa vår data med en parabolisk kurva som har ett minimum vid en viss punkt under året.

Scikit-learn innehåller ett användbart [pipeline-API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) för att kombinera olika steg för databehandling. En **pipeline** är en kedja av **estimators**. I vårt fall skapar vi en pipeline som först lägger till polynomegenskaper till vår modell och sedan tränar regressionen:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Att använda `PolynomialFeatures(2)` innebär att vi tar med alla andragradspolynom från indata. I vårt fall kommer det bara innebära `DayOfYear`<sup>2</sup>, men med två indata X och Y skulle detta lägga till X<sup>2</sup>, XY och Y<sup>2</sup>. Man kan även använda polynom med högre grad om man vill.

Pipelines kan användas på samma sätt som det ursprungliga `LinearRegression`-objektet, dvs. vi kan `fit`a pipelinen och sedan använda `predict` för att få förutsägelserna. Här är grafen som visar testdata och approximationskurvan:

<img alt="Polynomial regression" src="../../../../translated_images/sv/poly-results.ee587348f0f1f60b.webp" width="50%" />

Med polynomregression kan vi få något lägre MSE och högre bestämning, men inte signifikant. Vi behöver ta hänsyn till fler funktioner!

> Du kan se att de lägsta pumpapriserna observeras någonstans runt Halloween. Hur kan du förklara detta? 

🎃 Grattis, du skapade just en modell som kan hjälpa till att förutsäga priset på pajpumpor. Du kan förmodligen upprepa samma procedur för alla pumpatyper, men det skulle vara tråkigt. Låt oss nu lära oss hur vi tar pumpasort i beaktande i vår modell!

## Kategoriska Funktioner

I en ideal värld vill vi kunna förutsäga priser för olika pumpasorter med samma modell. Men kolumnen `Variety` skiljer sig något från kolumner som `Month`, eftersom den innehåller icke-numeriska värden. Sådana kolumner kallas **kategoriska**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Klicka på bilden ovan för en kort videoöversikt om användning av kategoriska funktioner.

Här kan du se hur medelpriset beror på sort:

<img alt="Average price by variety" src="../../../../translated_images/sv/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

För att ta hänsyn till sort behöver vi först konvertera den till numerisk form, eller **koda** den. Det finns flera sätt att göra det:

* Enkel **numerisk kodning** bygger en tabell med olika sorter och ersätter sedan sortnamnet med ett index i tabellen. Detta är inte bästa metoden för linjär regression, för linjär regression tar det faktiska numeriska värdet på indexet och lägger till det i resultatet, multiplicerat med en koefficient. I vårt fall är sambandet mellan indexnummer och pris tydligt icke-linjärt, även om vi ser till att indexen är ordnade på ett specifikt sätt.
* **One-hot-kodning** ersätter `Variety`-kolumnen med 4 olika kolumner, en för varje sort. Varje kolumn innehåller `1` om motsvarande rad är av den givna sorten och `0` annars. Det innebär att det kommer finnas fyra koefficienter i linjär regression, en för varje pumpasort, ansvariga för "startpris" (eller snarare "tilläggspris") för just den sorten.

Koden nedan visar hur vi kan one-hot-koda en sort:

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

För att träna linjär regression med one-hot-kodad sort som indata behöver vi bara initiera `X` och `y` korrekt:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Resten av koden är densamma som vi använde tidigare för att träna linjär regression. Om du provar kommer du se att medelkvadratfelet är ungefär detsamma, men bestämningskoefficienten är mycket högre (~77%). För att få ännu mer exakta förutsägelser kan vi ta fler kategoriska funktioner i beaktande, samt numeriska funktioner som `Month` eller `DayOfYear`. För att få en stor matris med funktioner kan vi använda `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Här tar vi också med `City` och typ av `Package`, vilket ger oss MSE 2.84 (10%) och bestämning 0.94!

## Sammanfoga allt

För att göra bästa modell kan vi använda kombinerad (one-hot-kodad kategorisk + numerisk) data från ovanstående exempel tillsammans med polynomregression. Här är den kompletta koden för din bekvämlighet:

```python
# ställ in träningsdata
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# gör tåg-test delning
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# konfigurera och träna pipelinen
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# förutsäg resultat för testdata
pred = pipeline.predict(X_test)

# beräkna MSE och bestämning
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Detta bör ge oss bästa bestämningskoefficient på nästan 97%, och MSE=2.23 (~8% förutsägelsefel).

| Modell | MSE | Bestämning |
|-------|-----|-------------|
| `DayOfYear` Linjär | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynom | 2.73 (17.0%) | 0.08 |
| `Variety` Linjär | 5.24 (19.7%) | 0.77 |
| Alla funktioner Linjär | 2.84 (10.5%) | 0.94 |
| Alla funktioner Polynom | 2.23 (8.25%) | 0.97 |

🏆 Bra jobbat! Du skapade fyra regressionsmodeller i en lektion och förbättrade modellens kvalitet till 97%. I den sista delen om regression kommer du lära dig om logistisk regression för att bestämma kategorier.

---
## 🚀Utmaning

Testa flera olika variabler i denna notebook för att se hur korrelation korrelerar med modellens noggrannhet.

## [Quiz efter föreläsningen](https://ff-quizzes.netlify.app/en/ml/)

## Granskning & Självstudier

I denna lektion lärde vi oss om linjär regression. Det finns andra viktiga typer av regression. Läs om Stepwise, Ridge, Lasso och Elasticnet-tekniker. En bra kurs att studera för att lära sig mer är [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Uppgift 

[Bygg en modell](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Ansvarsfriskrivning**:
Detta dokument har översatts med hjälp av AI-översättningstjänsten [Co-op Translator](https://github.com/Azure/co-op-translator). Även om vi strävar efter noggrannhet, var vänlig observera att automatiska översättningar kan innehålla fel eller brister. Det ursprungliga dokumentet på dess modersmål bör anses vara den auktoritativa källan. För kritisk information rekommenderas professionell mänsklig översättning. Vi ansvarar inte för några missförstånd eller feltolkningar som uppstår från användningen av denna översättning.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->