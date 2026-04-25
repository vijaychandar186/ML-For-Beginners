# Bygg en regresjonsmodell med Scikit-learn: regresjon på fire måter

## Nybegynnermerknad

Lineær regresjon brukes når vi ønsker å forutsi en **numerisk verdi** (for eksempel boligpris, temperatur eller salg).
Den fungerer ved å finne en rett linje som best representerer forholdet mellom inngangsfunksjonene og utgangen.

I denne leksjonen fokuserer vi på å forstå konseptet før vi utforsker mer avanserte regresjonsteknikker.
![Infografikk lineær vs polynomisk regresjon](../../../../translated_images/no/linear-polynomial.5523c7cb6576ccab.webp)
> Infografikk av [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Pre-forelesningsquiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Denne leksjonen er tilgjengelig på R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introduksjon

Så langt har du utforsket hva regresjon er med eksempeldatahentet fra gresskarprisingsdatasettet som vi skal bruke gjennom denne leksjonen. Du har også visualisert det ved hjelp av Matplotlib.

Nå er du klar til å gå dypere inn i regresjon for ML. Mens visualisering hjelper deg med å forstå data, kommer den virkelige styrken i maskinlæring fra _trening av modeller_. Modeller trenes på historiske data for automatisk å fange dataavhengigheter, og de lar deg forutsi utfall for nye data som modellen ikke har sett før.

I denne leksjonen vil du lære mer om to typer regresjon: _grunnleggende lineær regresjon_ og _polynomisk regresjon_, sammen med noe av matematikken som ligger til grunn for disse teknikkene. Disse modellene vil tillate oss å forutsi gresskarpriser avhengig av ulike inngangsdata.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klikk på bildet over for en kort videooversikt over lineær regresjon.

> Gjennom denne lærestien antar vi minimal matematikkunnskap, og søker å gjøre den tilgjengelig for studenter fra andre fagfelt, så se etter notater, 🧮 markeringer, diagrammer og andre læringsverktøy for å lette forståelsen.

### Forutsetning

Du bør nå være kjent med strukturen til gresskardataene vi undersøker. Du finner dem ferdig lastet og forhåndsrenset i denne leksjonens _notebook.ipynb_-fil. I filen vises gresskarprisen per bushel i en ny datastruktur. Sørg for at du kan kjøre disse notatbøkene i miljøer i Visual Studio Code.

### Forberedelse

Som en påminnelse lastes disse dataene inn for at du skal kunne stille spørsmål til dem.

- Når er det beste tidspunktet å kjøpe gresskar?
- Hvilken pris kan jeg forvente for en kasse med miniatyrgresskar?
- Bør jeg kjøpe dem i halvbusselkurver, eller i 1 1/9 bushel-esker?
La oss grave videre i disse dataene.

I forrige leksjon opprettet du en Pandas-dataramme og fylte den med deler av det originale datasettet, og standardiserte prisene per bushel. Ved å gjøre det fikk du imidlertid bare omtrent 400 datapunkter og kun for høstmånedene.

Ta en titt på dataene vi har lastet inn i denne leksjonens medfølgende notatbok. Dataene er forhåndslastet, og det lages et første spredningsdiagram for å vise månedens data. Kanskje vi kan få litt mer detalj rundt datanaturen ved å rense det mer.

## En lineær regresjonslinje

Som du lærte i leksjon 1, er målet med en lineær regresjonsøvelse å kunne plotte en linje for å:

- **Vise variabelrelasjoner**. Vise forholdet mellom variabler
- **Lage spådommer**. Lage nøyaktige spådommer om hvor et nytt datapunkt vil falle i forhold til den linjen.
 
Det er typisk med **Minimum kvadraters regresjon** å tegne denne typen linje. Begrepet "Minimum kvadraters" refererer til prosessen med å minimere den totale feilen i modellen vår. For hvert datapunkt måler vi den vertikale avstanden (kalt residual) mellom det faktiske punktet og vår regresjonslinje.

Vi kvadrerer disse avstandene av to hovedgrunner:

1. **Størrelse over retning:** Vi ønsker å behandle en feil på -5 likt som en feil på +5. Kvadrering gjør alle verdier positive.

2. **Straffe uteliggere:** Kvadrering gir større vekt til større feil, og tvinger linjen til å holde seg nærmere punkter som er langt unna.

Vi legger deretter sammen alle disse kvadrerte verdiene. Målet vårt er å finne den spesifikke linjen der denne endelige summen er minst (den minste mulige verdien)—derav navnet "Minimum kvadraters".

> **🧮 Vis meg matematikken**
> 
> Denne linjen, kalt _beste tilpassede linje_, kan uttrykkes ved [en ligning](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` er 'den forklarende variabelen'. `Y` er 'den avhengige variabelen'. Helningen til linjen er `b` og `a` er y-aksens skjæringspunkt, som refererer til verdien av `Y` når `X = 0`.
>
>![beregn helningen](../../../../translated_images/no/slope.f3c9d5910ddbfcf9.webp)
>
> Først beregner vi helningen `b`. Infografikk av [Jen Looper](https://twitter.com/jenlooper)
>
> Med andre ord, og med referanse til vår originale gresskardataspørsmål: "forutsi prisen på et gresskar per bushel etter måned", ville `X` referere til prisen og `Y` til salgs måneden.
>
>![fullfør ligningen](../../../../translated_images/no/calculation.a209813050a1ddb1.webp)
>
> Beregn verdien av Y. Hvis du betaler rundt $4, må det være april! Infografikk av [Jen Looper](https://twitter.com/jenlooper)
>
> Matematikken som beregner linjen må vise helningen til linjen, som også avhenger av skjæringspunktet, altså hvor `Y` befinner seg når `X = 0`.
>
> Du kan se metoden for beregning av disse verdiene på [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) sin nettside. Besøk også [denne Minimum kvadraters kalkulatoren](https://www.mathsisfun.com/data/least-squares-calculator.html) for å se hvordan tallverdiene påvirker linjen.

## Korrelasjon

Et siste begrep å forstå er **Korrelasjonskoeffisienten** mellom gitte X- og Y-variabler. Ved bruk av et spredningsdiagram kan du raskt visualisere denne koeffisienten. Et plot med datapunkter spredt langs en fin linje har høy korrelasjon, mens et plot med datapunkter spredt overalt mellom X og Y har lav korrelasjon.

En god lineær regresjonsmodell vil være en som har høy (nærmere 1 enn 0) korrelasjonskoeffisient ved bruk av Minimum kvadraters regresjonsmetode med en regresjonslinje.

✅ Kjør notatboken som følger denne leksjonen og se på spredningsdiagrammet mellom måned og pris. Ser dataene som assosierer måned til pris for gresskarsalg ut til å ha høy eller lav korrelasjon, i henhold til din visuelle tolkning av spredningsplottet? Endrer det seg om du bruker en mer finmasket måling i stedet for `Month`, f.eks. *dag på året* (altså antall dager siden starten på året)?

I koden nedenfor antar vi at vi har renset dataene, og fått en dataramme kalt `new_pumpkins`, som ligner på følgende:

ID | Måned | DagPåÅret | Variasjon | By | Pakke | Lav Pris | Høy Pris | Pris
---|-------|-----------|-----------|----|-------|----------|----------|-----
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel kartonger | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel kartonger | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel kartonger | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel kartonger | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel kartonger | 15.0 | 15.0 | 13.636364

> Koden for å rense dataene er tilgjengelig i [`notebook.ipynb`](notebook.ipynb). Vi har utført de samme rensetrinnene som i forrige leksjon, og har beregnet `DayOfYear`-kolonnen med følgende uttrykk:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```


Nå som du har forstått matematikken bak lineær regresjon, la oss lage en regresjonsmodell for å se om vi kan forutsi hvilken pakke gresskar som vil ha de beste prisene. Noen som kjøper gresskar til en høytidssesong kanskje vil ha denne informasjonen for å kunne optimalisere sine gresskarpakkeinnkjøp til sesongen.

## På jakt etter korrelasjon

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klikk på bildet over for en kort videooversikt over korrelasjon.

Fra forrige leksjon har du sannsynligvis sett at gjennomsnittsprisen for ulike måneder ser slik ut:

<img alt="Gjennomsnittspris per måned" src="../../../../translated_images/no/barchart.a833ea9194346d76.webp" width="50%"/>

Dette antyder at det bør finnes en viss korrelasjon, og vi kan prøve å trene en lineær regresjonsmodell for å forutsi forholdet mellom `Month` og `Price`, eller mellom `DayOfYear` og `Price`. Her er spredningsdiagrammet som viser sistnevnte forhold:

<img alt="Spredningsdiagram av pris vs. dag på året" src="../../../../translated_images/no/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

La oss se om det er korrelasjon ved å bruke `corr`-funksjonen:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```


Det ser ut som korrelasjonen er ganske liten, -0.15 for `Month` og -0.17 for `DayOfMonth`, men det kan finnes en annen viktig sammenheng. Det ser ut til å være forskjellige klynger av priser som tilsvarer ulike gresskartyper. For å bekrefte denne hypotesen, la oss plotte hver gresskarkategori med forskjellig farge. Ved å sende med `ax`-parameteren til `scatter` plottefunksjonen kan vi plotte alle punktene i samme graf:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Spredningsdiagram av pris vs. dag på året med farge" src="../../../../translated_images/no/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Vår undersøkelse antyder at variasjon har større effekt på den totale prisen enn selve salgsdatoen. Vi kan se dette med et stolpediagram:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Stolpediagram av pris vs variasjon" src="../../../../translated_images/no/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

La oss fokusere for øyeblikket kun på én gresskartype, 'pie type', og se hvilken effekt datoen har på prisen:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Spredningsdiagram av pris vs. dag på året for pie pumpkins" src="../../../../translated_images/no/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Hvis vi nå beregner korrelasjonen mellom `Price` og `DayOfYear` ved bruk av `corr`-funksjonen, får vi omtrent `-0.27` – noe som betyr at det gir mening å trene en prediksjonsmodell.

> Før du trener en lineær regresjonsmodell, er det viktig å sørge for at dataene våre er rene. Lineær regresjon fungerer ikke godt med manglende verdier, så det er lurt å kvitte seg med tomme celler:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```


En annen tilnærming kan være å fylle disse tomme verdiene med gjennomsnittsverdier fra den tilsvarende kolonnen.

## Enkel lineær regresjon

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klikk på bildet over for en kort videooversikt over lineær og polynomisk regresjon.

For å trene vår lineære regresjonsmodell, bruker vi **Scikit-learn** biblioteket.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```


Vi begynner med å separere inngangsverdiene (funksjoner) og forventet utgang (etikett) i separate numpy-arrays:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```


> Merk at vi måtte utføre `reshape` på inngangsdataene for at Linear Regression-pakken skulle forstå dem riktig. Lineær regresjon forventer et 2D-array som input, hvor hver rad i arrayet tilsvarer en vektor av inngangsfunksjoner. I vårt tilfelle, siden vi bare har én inngang, trenger vi et array med form N×1, hvor N er dataset-størrelsen.

Deretter må vi dele dataene i trenings- og testdatasett, slik at vi kan validere modellen vår etter trening:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```


Til slutt tar det bare to linjer med kode å trene den faktiske lineære regresjonsmodellen. Vi definerer `LinearRegression`-objektet, og passer det til dataene våre ved hjelp av `fit`-metoden:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression`-objektet etter at vi har "fit"-tet det inneholder alle koeffisientene til regresjonen, som kan aksesseres ved hjelp av `.coef_`-egenskapen. I vårt tilfelle er det bare én koeffisient, som skal være rundt `-0.017`. Det betyr at prisene ser ut til å synke litt med tiden, men ikke for mye, omtrent 2 cent per dag. Vi kan også aksessere skjæringspunktet for regresjonen med Y-aksen ved å bruke `lin_reg.intercept_` - det vil være rundt `21` i vårt tilfelle, noe som indikerer prisen i begynnelsen av året.

For å se hvor nøyaktig modellen vår er, kan vi forutsi priser på en testdatasett, og deretter måle hvor nær våre prediksjoner er de forventede verdiene. Dette kan gjøres ved hjelp av rotmiddelkvadratfeil (RMSE) metrikk, som er roten av gjennomsnittet av alle kvadrerte forskjeller mellom forventet og forutsagt verdi.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Feilen vår ser ut til å være rundt 2 poeng, som er ~17%. Ikke så bra. En annen indikator på modellkvalitet er **bestemmelseskoeffisienten**, som kan oppnås slik:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Hvis verdien er 0, betyr det at modellen ikke tar hensyn til inngangsdata, og oppfører seg som den *verste lineære prediktoren*, som rett og slett er et gjennomsnitt av resultatet. Verdien 1 betyr at vi kan perfekt forutsi alle forventede utganger. I vårt tilfelle er koeffisienten rundt 0.06, som er ganske lavt.

Vi kan også plotte testdata sammen med regresjonslinjen for bedre å se hvordan regresjonen fungerer i vårt tilfelle:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/no/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomregresjon

En annen type lineær regresjon er polynomregresjon. Selv om det noen ganger er et lineært forhold mellom variabler - jo større gresskaret er i volum, desto høyere pris - kan disse forholdene noen ganger ikke plottes som et plan eller en rett linje.

✅ Her er [noen flere eksempler](https://online.stat.psu.edu/stat501/lesson/9/9.8) på data som kan bruke polynomregresjon.

Ta en ny titt på forholdet mellom dato og pris. Virker dette spredningsplottet som det nødvendigvis bør analyseres med en rett linje? Kan ikke prisene fluktuere? I så fall kan du prøve polynomregresjon.

✅ Polynomuttrykk er matematiske uttrykk som kan bestå av én eller flere variabler og koeffisienter.

Polynomregresjon lager en buet linje for bedre å tilpasse ikke-lineære data. I vårt tilfelle, hvis vi inkluderer en kvadratert `DayOfYear`-variabel i inputdataene, bør vi kunne tilpasse dataene våre med en parabolsk kurve som har et minimum på et bestemt punkt i løpet av året.

Scikit-learn inkluderer en nyttig [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) for å kombinere forskjellige steg i databehandlingen. En **pipeline** er en kjede av **estimatorer**. I vårt tilfelle lager vi en pipeline som først legger til polynomfunksjoner i modellen, og deretter trener regresjonen:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Å bruke `PolynomialFeatures(2)` betyr at vi vil inkludere alle polynomer av andre grad fra inputdataene. I vårt tilfelle betyr det bare `DayOfYear`<sup>2</sup>, men gitt to inputvariabler X og Y, vil dette legge til X<sup>2</sup>, XY og Y<sup>2</sup>. Vi kan også bruke polynomer av høyere grad om vi ønsker.

Pipelines kan brukes på samme måte som det originale `LinearRegression`-objektet, altså kan vi `fit` pipe-linen, og deretter bruke `predict` for å få prediksjonsresultatene. Her er grafen som viser testdataene og tilnærmingskurven:

<img alt="Polynomial regression" src="../../../../translated_images/no/poly-results.ee587348f0f1f60b.webp" width="50%" />

Ved å bruke polynomregresjon kan vi få litt lavere MSE og høyere bestemmelseskoeffisient, men ikke signifikant. Vi må ta hensyn til andre funksjoner!

> Du kan se at de minimale gresskarprisene observeres en plass rundt Halloween. Hvordan kan du forklare dette?

🎃 Gratulerer, du har nettopp laget en modell som kan hjelpe med å forutsi prisen på paigresskar. Du kan sannsynligvis gjenta den samme prosedyren for alle gresskartypene, men det ville være tidkrevende. La oss nå lære hvordan vi tar hensyn til gresskarvarianter i modellen vår!

## Kategoriske funksjoner

I den ideelle verden ønsker vi å kunne forutsi priser for forskjellige gresskarvarianter ved hjelp av samme modell. Men `Variety`-kolonnen er noe annerledes enn kolonner som `Month`, fordi den inneholder ikke-numeriske verdier. Slike kolonner kalles **kategoriske**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Klikk bildet over for en kort videooversikt over bruk av kategoriske funksjoner.

Her kan du se hvordan gjennomsnittsprisen avhenger av variant:

<img alt="Average price by variety" src="../../../../translated_images/no/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

For å ta hensyn til variant må vi først konvertere den til numerisk form, eller **kode** den. Det finnes flere måter vi kan gjøre dette på:

* Enkel **nummerisk koding** vil bygge en tabell over ulike varianter, og deretter erstatte variantnavnet med en indeks i denne tabellen. Dette er ikke det beste for lineær regresjon, fordi lineær regresjon tar den faktiske numeriske verdien av indeksen og legger den til resultatet, multiplisert med en koeffisient. I vårt tilfelle er forholdet mellom indeksnummer og pris tydelig ikke-lineært, selv om vi sørger for at indeksene er ordnet på en bestemt måte.
* **One-hot-koding** vil erstatte `Variety`-kolonnen med 4 ulike kolonner, én for hver variant. Hver kolonne vil inneholde `1` hvis den tilsvarende raden er av en gitt variant, og `0` ellers. Dette betyr at det vil være fire koeffisienter i lineær regresjon, én for hver gresskarvariant, som er ansvarlige for "startpris" (eller heller "tilleggpris") for akkurat den varianten.

Koden nedenfor viser hvordan vi kan one-hot kode en variant:

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

For å trene lineær regresjon med one-hot-kodet variant som input, trenger vi bare å initialisere `X` og `y` data riktig:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Resten av koden er den samme som vi brukte overfor for å trene Linear Regression. Hvis du prøver det, vil du se at middel kvadratfeil er omtrent den samme, men vi får mye høyere bestemmelseskoeffisient (~77%). For å få enda mer nøyaktige prediksjoner kan vi ta med flere kategoriske funksjoner, samt numeriske funksjoner som `Month` eller `DayOfYear`. For å få en stor tabell med alle funksjoner kan vi bruke `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Her tar vi også hensyn til `City` og `Package` type, som gir oss MSE 2.84 (10%), og bestemmelse 0.94!

## Å sette det hele sammen

For å lage den beste modellen kan vi bruke kombinert (one-hot kodet kategorisk + numerisk) data fra eksempelet ovenfor sammen med polynomregresjon. Her er den komplette koden for din bekvemmelighet:

```python
# Sett opp treningsdata
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# Lag trenings- og testdeling
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# Sett opp og tren pipelinen
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# Forutsi resultater for testdata
pred = pipeline.predict(X_test)

# Beregn MSE og bestemthet
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Dette skal gi oss den beste bestemmelseskoeffisienten på nesten 97%, og MSE=2.23 (~8% prediksjonsfeil).

| Modell | MSE | Bestemmelse |
|-------|-----|---------------|
| `DayOfYear` Lineær | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynom | 2.73 (17.0%) | 0.08 |
| `Variety` Lineær | 5.24 (19.7%) | 0.77 |
| Alle funksjoner Lineær | 2.84 (10.5%) | 0.94 |
| Alle funksjoner Polynom | 2.23 (8.25%) | 0.97 |

🏆 Bra jobbet! Du har laget fire regresjonsmodeller i én lekse, og forbedret modellkvaliteten til 97%. I den siste delen om regresjon vil du lære om logistisk regresjon for kategoribestemmelse.

---
## 🚀Utfordring

Test flere forskjellige variabler i denne notatboken for å se hvordan korrelasjon stemmer med modellnøyaktighet.

## [Quiz etter forelesning](https://ff-quizzes.netlify.app/en/ml/)

## Gjennomgang & Selvstudium

I denne leksjonen lærte vi om lineær regresjon. Det finnes andre viktige typer regresjon. Les om Stepwise, Ridge, Lasso og Elasticnet teknikker. Et godt kurs å studere for å lære mer er [Stanford Statistical Learning-kurset](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Oppgave

[Bygg en modell](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi streber etter nøyaktighet, vennligst vær oppmerksom på at automatiserte oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på originalsproget bør betraktes som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for eventuelle misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->