# Byg en regressionsmodel ved brug af Scikit-learn: regression på fire måder

## Begynder Note

Lineær regression bruges, når vi vil forudsige en **numerisk værdi** (for eksempel huspris, temperatur eller salg).
Den fungerer ved at finde en lige linje, der bedst repræsenterer forholdet mellem inputfunktioner og output.

I denne lektion fokuserer vi på at forstå konceptet, før vi udforsker mere avancerede regressionsteknikker.
![Linear vs polynomial regression infographic](../../../../translated_images/da/linear-polynomial.5523c7cb6576ccab.webp)
> Infografik af [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [For-forelæsning quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Denne lektion findes også i R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introduktion

Indtil nu har du undersøgt, hvad regression er med prøve data indsamlet fra græskarprisdatasetet, som vi vil bruge igennem denne lektion. Du har også visualiseret det ved hjælp af Matplotlib.

Nu er du klar til at dykke dybere ned i regression for ML. Mens visualisering giver dig mulighed for at forstå data, kommer den virkelige styrke ved Maskinlæring fra _at træne modeller_. Modeller trænes på historiske data for automatisk at fange dataafhængigheder, og de giver dig mulighed for at forudsige resultater for nye data, som modellen ikke har set før.

I denne lektion vil du lære mere om to typer regression: _basis lineær regression_ og _polynomiel regression_, sammen med noget af den matematik, der ligger til grund for disse teknikker. Disse modeller vil gøre det muligt for os at forudsige græskarpriser afhængigt af forskellige inputdata.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klik på billedet ovenfor for en kort videooversigt over lineær regression.

> Gennem hele dette pensum antager vi minimal kendskab til matematik og søger at gøre det tilgængeligt for studerende fra andre fagområder, så hold øje med noter, 🧮 opkald, diagrammer og andre læringsværktøjer for at hjælpe forståelsen.

### Forudsætning

Du bør nu være fortrolig med strukturen af græskardataene, som vi undersøger. Du finder dem forudindlæst og renset i denne lektions _notebook.ipynb_-fil. I filen vises græskarprisen per bushel i en ny data frame. Sørg for, at du kan køre disse notebooks i kerner i Visual Studio Code.

### Forberedelse

Som en påmindelse, indlæser du disse data for at kunne stille spørgsmål til dem.

- Hvornår er det bedste tidspunkt at købe græskar?
- Hvilken pris kan jeg forvente for en kasse miniaturegræskar?
- Skal jeg købe dem i halvbustkurve eller i 1 1/9 bushel kasser?
Lad os fortsætte med at grave i disse data.

I den forrige lektion oprettede du en Pandas data frame og fyldte den med en del af det oprindelige datasæt, standardiseret prisen pr. bushel. Ved at gøre det var du dog kun i stand til at samle omkring 400 datapunktoplysninger og kun for efterårsmånederne.

Tag et kig på dataene, som vi forudindlæste i denne lektions ledsagende notebook. Dataene er forindlæst, og et initialt spredningsdiagram er vist for månedsdata. Måske kan vi få lidt flere detaljer om dataenes natur ved at rense dem mere.

## En lineær regressionslinje

Som du lærte i Lektion 1, er målet med en lineær regressionsøvelse at kunne plotte en linje til at:

- **Vis variable relationer**. Vis forholdet mellem variable
- **Foretage forudsigelser**. Lav nøjagtige forudsigelser om, hvor et nyt datapunkt vil falde i forhold til den linje.

Det er typisk for **Mindste Kvadraters Regression** at tegne denne type linje. Udtrykket "Mindste Kvadraters" refererer til processen med at minimere den samlede fejl i vores model. For hvert datapunkt måler vi den lodrette afstand (kaldet residual) mellem det faktiske punkt og vores regressionslinje.

Vi kvadrerer disse afstande af to hovedårsager:

1. **Størrelse frem for retning:** Vi vil behandle en fejl på -5 på samme måde som en fejl på +5. Kvadrering gør alle værdier positive.

2. **Straffe Udliggere:** Kvadrering giver større vægt til større fejl, hvilket tvinger linjen til at være tættere på punkter, der ligger langt væk.

Vi lægger så alle disse kvadrerede værdier sammen. Vores mål er at finde den specifikke linje, hvor dette endelige sum er mindst (den mindste mulige værdi)—deraf navnet "Mindste Kvadraters".

> **🧮 Vis mig matematikken**
>
> Denne linje, kaldet _line of best fit_, kan udtrykkes ved [et ligning](https://en.wikipedia.org/wiki/Simple_linear_regression):
>
> ```
> Y = a + bX
> ```
>
> `X` er den 'forklarende variabel'. `Y` er den 'afhængige variabel'. Linjens hældning er `b` og `a` er y-aksens skæringspunkt, hvilket refererer til værdien af `Y`, når `X = 0`.
>
>![beregn hældningen](../../../../translated_images/da/slope.f3c9d5910ddbfcf9.webp)
>
> Først beregnes hældningen `b`. Infografik af [Jen Looper](https://twitter.com/jenlooper)
>
> Med andre ord, og med henvisning til vores græskar data oprindelige spørgsmål: "forudsig prisen på et græskar per bushel pr. måned", ville `X` referere til prisen og `Y` ville referere til salgs måneden.
>
>![fuldfør ligningen](../../../../translated_images/da/calculation.a209813050a1ddb1.webp)
>
> Beregn værdien af Y. Hvis du betaler omkring $4, må det være april! Infografik af [Jen Looper](https://twitter.com/jenlooper)
>
> Den matematik, der beregner linjen, skal demonstrere linjens hældning, som også afhænger af skæringspunktet, eller hvor `Y` befinder sig, når `X = 0`.
>
> Du kan iagttage metoden til beregning af disse værdier på webstedet [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Besøg også [denne Mindste Kvadraters regnemaskine](https://www.mathsisfun.com/data/least-squares-calculator.html) for at se, hvordan talværdier påvirker linjen.

## Korrelation

Endnu et begreb, der skal forstås, er **korrelationskoefficienten** mellem givne X og Y variable. Ved at bruge et spredningsdiagram kan du hurtigt visualisere denne koefficient. En plot med datapunkter, der er spredt i en pæn linje, har høj korrelation, men en plot med datapunkter spredt tilfældigt mellem X og Y har lav korrelation.

En god lineær regressionsmodel vil være en, der har en høj (tættere på 1 end 0) korrelationskoefficient ved brug af Mindste Kvadraters Regression med en regressionslinje.

✅ Kør notebook'en, der ledsager denne lektion, og se på spredningsdiagrammet fra måned til pris. Ser data, der forbinder måned og pris for græskar salg, ud til at have høj eller lav korrelation ifølge din visuelle fortolkning af spredningsdiagrammet? Ændrer det sig, hvis du bruger en mere finmasket måling i stedet for `Month`, fx *dag i året* (dvs. antal dage siden årets start)?

I koden nedenfor vil vi antage, at vi har renset dataene og opnået en data frame kaldet `new_pumpkins`, der ligner følgende:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Koden til at rense dataene findes i [`notebook.ipynb`](notebook.ipynb). Vi har foretaget de samme rensetrin som i den tidligere lektion og har beregnet kolonnen `DayOfYear` ved hjælp af følgende udtryk:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Nu hvor du har en forståelse af matematikken bag lineær regression, lad os oprette en regressionsmodel for at se, om vi kan forudsige, hvilken pakke af græskar der vil have de bedste græskarpriser. Nogen, der køber græskar til en feriegræskarmark, vil måske bruge disse oplysninger til at optimere deres køb af græskarpakker til marken.

## Leder efter korrelation

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klik på billedet ovenfor for en kort videooversigt over korrelation.

Fra den forrige lektion har du sandsynligvis set, at gennemsnitsprisen for forskellige måneder ser sådan ud:

<img alt="Average price by month" src="../../../../translated_images/da/barchart.a833ea9194346d76.webp" width="50%"/>

Dette antyder, at der bør være en vis korrelation, og vi kan prøve at træne en lineær regressionsmodel for at forudsige forholdet mellem `Month` og `Price`, eller mellem `DayOfYear` og `Price`. Her er spredningsdiagrammet, der viser det sidste forhold:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/da/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Lad os se, om der er korrelation ved hjælp af `corr` funktionen:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Det ser ud til, at korrelationen er ret lille, -0,15 for `Month` og -0,17 for `DayOfMonth`, men der kunne være en anden vigtig sammenhæng. Det ser ud til, at der er forskellige klynger af priser, der svarer til forskellige græskartyper. For at bekræfte denne hypotese, lad os plotte hver græskarkategori med en forskellig farve. Ved at sende en `ax` parameter til `scatter` plotfunktionen kan vi plotte alle punkter i det samme diagram:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/da/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Vores undersøgelse antyder, at sort har mere effekt på den samlede pris end den faktiske salgsdato. Vi kan se dette med et søjlediagram:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/da/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Lad os for øjeblikket fokusere kun på en græskar sort, 'pie type', og se hvilken effekt datoen har på prisen:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/da/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Hvis vi nu beregner korrelationen mellem `Price` og `DayOfYear` ved hjælp af `corr` funktionen, får vi noget i retning af `-0.27` - hvilket betyder, at træning af en forudsigelsesmodel giver mening.

> Før du træner en lineær regressionsmodel, er det vigtigt at sikre, at vores data er rene. Lineær regression fungerer ikke godt med manglende værdier, derfor giver det mening at fjerne alle tomme celler:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

En anden tilgang ville være at udfylde disse tomme værdier med gennemsnitsværdier fra den tilsvarende kolonne.

## Simple Lineær Regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klik på billedet ovenfor for en kort videooversigt over lineær og polynomiel regression.

For at træne vores Lineær Regressionsmodel vil vi bruge **Scikit-learn** biblioteket.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Vi starter med at adskille inputværdierne (funktioner) og det forventede output (etiket) i separate numpy-arrays:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Bemærk, at vi var nødt til at udføre `reshape` på inputdataene, for at Linear Regression-pakken kunne forstå det korrekt. Lineær Regression forventer et 2D-array som input, hvor hver række i arrayet svarer til en vektor af inputfunktioner. I vores tilfælde, hvor vi kun har én input - har vi brug for et array med form N&times;1, hvor N er datasætstørrelsen.

Dernæst skal vi opdele dataene i trænings- og testdatasæt, så vi kan validere vores model efter træning:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Endelig tager træningen af den faktiske Lineær Regression-model kun to kode linjer. Vi definerer `LinearRegression`-objektet og tilpasser det til vores data ved brug af `fit` metoden:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression`-objektet efter at være blevet `fit`-tet indeholder alle regressionskoefficienterne, som kan tilgås via `.coef_`-egenskaben. I vores tilfælde er der kun én koefficient, som skulle være omkring `-0.017`. Det betyder, at priserne ser ud til at falde en smule med tiden, men ikke meget, cirka 2 cent per dag. Vi kan også tilgå skæringspunktet med Y-aksen via `lin_reg.intercept_` - det vil være omkring `21` i vores tilfælde, hvilket indikerer prisen i begyndelsen af året.

For at se, hvor præcis vores model er, kan vi forudsige priser på et testdatasæt, og derefter måle, hvor tæt vores forudsigelser er på de forventede værdier. Dette kan gøres ved hjælp af root mean square error (RMSE) metrikken, som er kvadratroden af gennemsnittet af alle kvadrerede forskelle mellem forventet og forudsagt værdi.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```
  
Vores fejl ser ud til at være omkring 2 point, hvilket er ca. 17%. Ikke særlig godt. En anden indikator for modellens kvalitet er **determinationskoefficienten**, som kan opnås sådan her:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
  
Hvis værdien er 0, betyder det, at modellen ikke tager inputdata i betragtning og fungerer som den *værste lineære forudsigelse*, som blot er middelværdien af resultatet. Værdien 1 betyder, at vi kan forudsige alle forventede outputs perfekt. I vores tilfælde er koefficienten omkring 0.06, hvilket er ret lavt.

Vi kan også plotte testdataene sammen med regressionslinjen for bedre at se, hvordan regressionen fungerer i vores tilfælde:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```
  
<img alt="Linear regression" src="../../../../translated_images/da/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

En anden type lineær regression er polynomial regression. Mens der nogle gange er et lineært forhold mellem variabler – jo større græskar i volumen, jo højere pris – kan disse forhold nogle gange ikke plottes som et plan eller en ret linje.

✅ Her er [nogle flere eksempler](https://online.stat.psu.edu/stat501/lesson/9/9.8) på data, som kunne bruge polynomial regression.

Tag et kig på forholdet mellem Dato og Pris. Ser dette scatterplot ud som om, det nødvendigvis skal analyseres med en lige linje? Kan priserne ikke svinge? I dette tilfælde kan du prøve polynomial regression.

✅ Polynomier er matematiske udtryk, som kan bestå af en eller flere variable og koefficienter.

Polynomial regression laver en buet linje for bedre at passe til ikke-lineære data. I vores tilfælde, hvis vi inkluderer en kvadreret `DayOfYear`-variabel i inputdata, burde vi kunne tilpasse vores data med en parabolsk kurve, som vil have et minimum på et bestemt tidspunkt i løbet af året.

Scikit-learn inkluderer et nyttigt [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) til at kombinere forskellige trin i databehandling. En **pipeline** er en kæde af **estimators**. I vores tilfælde vil vi oprette en pipeline, der først tilføjer polynomial features til vores model og derefter træner regressionen:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```
  
At bruge `PolynomialFeatures(2)` betyder, at vi vil inkludere alle andengrads polynomier fra inputdata. I vores tilfælde betyder det blot `DayOfYear`<sup>2</sup>, men givet to inputvariable X og Y, vil dette tilføje X<sup>2</sup>, XY og Y<sup>2</sup>. Vi kan også bruge polynomier af højere grad, hvis vi ønsker det.

Pipelines kan bruges på samme måde som det originale `LinearRegression` objekt, dvs. vi kan `fit` pipelinen og derefter bruge `predict` til at få forudsigelserne. Her er grafen, der viser testdata og tilpasningskurven:

<img alt="Polynomial regression" src="../../../../translated_images/da/poly-results.ee587348f0f1f60b.webp" width="50%" />

Ved at bruge polynomial regression kan vi opnå en lidt lavere MSE og højere determinationskoefficient, men ikke signifikant. Vi skal tage andre features i betragtning!

> Du kan se, at de laveste priser på græskar observeres omkring Halloween. Hvordan kan du forklare det?

🎃 Tillykke, du har netop skabt en model, der kan hjælpe med at forudsige prisen på dessertgræskar. Du kan sandsynligvis gentage samme procedure for alle græskar-typer, men det ville være besværligt. Lad os nu lære, hvordan vi tager græskartype i betragtning i vores model!

## Kategoriske Features

I den ideelle verden ønsker vi at kunne forudsige priser for forskellige græskarsorter med samme model. Dog er kolonnen `Variety` lidt anderledes end kolonner som `Month`, fordi den indeholder ikke-numeriske værdier. Sådanne kolonner kaldes **kategoriske**.

[![ML for begyndere - Kategoriske Feature Forudsigelser med Lineær Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for begyndere - Kategoriske Feature Forudsigelser med Lineær Regression")

> 🎥 Klik på billedet ovenfor for en kort videooversigt om brug af kategoriske features.

Her kan du se, hvordan gennemsnitsprisen afhænger af sort:

<img alt="Average price by variety" src="../../../../translated_images/da/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

For at tage sort i betragtning skal vi først konvertere den til numerisk form eller **kode** den. Der er flere måder at gøre det på:

* Simpel **numerisk kodning** bygger en tabel over forskellige sorter og erstatter så sortens navn med et indeks i denne tabel. Dette er ikke den bedste idé for lineær regression, fordi lineær regression tager den faktiske numeriske værdi af indekset og lægger det til resultatet vægtet med en koefficient. I vores tilfælde er forholdet mellem indeksnummer og pris klart ikke-lineært, selv hvis vi sørger for, at indeksene er ordnet på en bestemt måde.
* **One-hot encoding** erstatter `Variety`-kolonnen med 4 forskellige kolonner, én for hver sort. Hver kolonne indeholder `1`, hvis den tilsvarende række er af den pågældende sort, og `0` ellers. Det betyder, at der vil være fire koefficienter i den lineære regression, én for hver græskartype, som er ansvarlige for "startpris" (eller rettere "ekstra pris") for netop den sort.

Koden nedenfor viser, hvordan vi kan one-hot kode en sort:

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

For at træne lineær regression med one-hot kodet sort som input behøver vi bare at initialisere `X` og `y` korrekt:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```
  
Resten af koden er den samme som den, vi brugte ovenfor til at træne Lineær Regression. Hvis du prøver det, vil du se, at mean squared error er cirka den samme, men vi får en meget højere determinationskoefficient (~77%). For at få endnu mere præcise forudsigelser kan vi tage flere kategoriske features samt numeriske features som `Month` eller `DayOfYear` i betragtning. For at få en stor samlet feature-array kan vi bruge `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```
  
Her tager vi også højde for `City` og `Package` type, hvilket giver os MSE 2.84 (10%) og determinationskoefficient 0.94!

## Sæt det hele sammen

For at lave den bedste model kan vi bruge kombinerede (one-hot kodede kategoriske + numeriske) data fra ovenstående eksempel sammen med polynomial regression. Her er det komplette kodeeksempel for din bekvemmelighed:

```python
# opret træningsdata
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# lav trænings-test opdeling
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# opsæt og træn pipelinen
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# forudsig resultater for testdata
pred = pipeline.predict(X_test)

# beregn MSE og bestemmelse
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```
  
Dette burde give os den bedste determinationskoefficient på næsten 97%, og MSE=2.23 (~8% fejl i forudsigelse).

| Model | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Lineær | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomiel | 2.73 (17.0%) | 0.08 |
| `Variety` Lineær | 5.24 (19.7%) | 0.77 |
| Alle features Lineær | 2.84 (10.5%) | 0.94 |
| Alle features Polynomiel | 2.23 (8.25%) | 0.97 |

🏆 Godt gået! Du har lavet fire regressionsmodeller i én lektion og forbedret modelkvaliteten til 97%. I den sidste del om regression vil du lære om logistisk regression til at bestemme kategorier.

---
## 🚀Udfordring

Test flere forskellige variable i denne notesbog for at se, hvordan korrelation svarer til modelnøjagtighed.

## [Quiz efter lektionen](https://ff-quizzes.netlify.app/en/ml/)

## Review & Selvlæring

I denne lektion lærte vi om lineær regression. Der findes andre vigtige typer regression. Læs om Stepwise, Ridge, Lasso og Elasticnet teknikker. Et godt kursus at studere for at lære mere er [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Opgave

[Byg en model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Ansvarsfraskrivelse**:
Dette dokument er oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på nøjagtighed, bedes du være opmærksom på, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets modersmål bør betragtes som den autoritative kilde. For kritisk information anbefales en professionel menneskelig oversættelse. Vi påtager os intet ansvar for misforståelser eller fejltolkninger, der opstår som følge af brugen af denne oversættelse.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->