# Bouw een regressiemodel met Scikit-learn: regressie op vier manieren

## Notitie voor beginners

Lineaire regressie wordt gebruikt wanneer we een **numerieke waarde** willen voorspellen (bijvoorbeeld huisprijs, temperatuur, of verkoop).
Het werkt door een rechte lijn te vinden die de relatie tussen invoerkenmerken en de uitvoer het beste weergeeft.

In deze les richten we ons op het begrijpen van het concept voordat we meer geavanceerde regressietechnieken verkennen.
![Lineaire versus polynoom regressie infographic](../../../../translated_images/nl/linear-polynomial.5523c7cb6576ccab.webp)
> Infographic door [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Voorcollege quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Deze les is beschikbaar in R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Inleiding

Tot nu toe heb je onderzocht wat regressie is met voorbeelddata verzameld uit de pompoenprijs dataset die we gedurende deze les zullen gebruiken. Je hebt het ook gevisualiseerd met Matplotlib.

Nu ben je klaar om dieper in regressie voor ML te duiken. Terwijl visualisatie je in staat stelt om data te begrijpen, komt de echte kracht van Machine Learning van het _trainen van modellen_. Modellen worden getraind op historische data om automatisch afhankelijkheden te vangen, en ze stellen je in staat om uitkomsten te voorspellen voor nieuwe data die het model nog niet eerder heeft gezien.

In deze les leer je meer over twee types regressie: _basis lineaire regressie_ en _polynomiale regressie_, samen met wat van de onderliggende wiskunde van deze technieken. Deze modellen stellen ons in staat om pompoenprijzen te voorspellen afhankelijk van verschillende invoerdata.

[![ML voor beginners - Begrijpen van lineaire regressie](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML voor beginners - Begrijpen van lineaire regressie")

> 🎥 Klik op de afbeelding hierboven voor een korte video-overzicht van lineaire regressie.

> Gedurende deze cursus veronderstellen we minimale wiskundige kennis, en streven we ernaar om het toegankelijk te maken voor studenten uit andere vakgebieden, let daarom op notities, 🧮 uitleg, diagrammen en andere leermiddelen ter ondersteuning van het begrip.

### Vereisten

Je zou inmiddels bekend moeten zijn met de structuur van de pompoendata die we onderzoeken. Je kunt het voorbeladen en schoongemaakt terugvinden in het _notebook.ipynb_ bestand van deze les. In dit bestand is de pompoenprijs per bushel weergegeven in een nieuw data frame. Zorg ervoor dat je deze notebooks kunt draaien in kernels in Visual Studio Code.

### Voorbereiding

Als herinnering, je laadt deze data om er vragen over te kunnen stellen.

- Wanneer is de beste tijd om pompoenen te kopen? 
- Welke prijs kan ik verwachten voor een kist miniatuurpompoenen?
- Moet ik ze kopen in halve bushel manden of per 1 1/9 bushel doos?
Laten we dieper graven in deze data.

In de vorige les heb je een Pandas data frame gemaakt en gevuld met een deel van de originele dataset, waarbij de prijzen zijn genormaliseerd per bushel. Door dat te doen was je echter maar in staat ongeveer 400 datapunten te verzamelen en alleen voor de herfstmaanden.

Bekijk de data die we voorbeladen hebben in de bijbehorende notebook van deze les. De data is voorbeladen en er is een initiële scatterplot gemaakt om maanddata te tonen. Misschien kunnen we iets meer detail krijgen over de aard van de data door het verder te schonen.

## Een lineaire regressielijn

Zoals je hebt geleerd in Les 1, is het doel van een lineaire regressie-oefening om in staat te zijn een lijn te plotten om:

- **Variabelenrelaties te tonen**. Toon het verband tussen variabelen
- **Voorspellingen te doen**. Maak nauwkeurige voorspellingen waar een nieuw datapunt zou vallen ten opzichte van die lijn. 

Het is typisch voor **Kleinstekwadratenregressie** om dit type lijn te tekenen. De term "Kleinstekwadraten" verwijst naar het proces van het minimaliseren van de totale fout in ons model. Voor elk datapunt meten we de verticale afstand (genaamd residu) tussen het werkelijke punt en onze regressielijn.

We kwadrateren deze afstanden om twee hoofdredenen:

1. **Grootte boven Richting:** We willen een fout van -5 hetzelfde behandelen als een fout van +5. Kwadrateren maakt alle waarden positief.

2. **Straffen van Uitbijters:** Kwadrateren geeft meer gewicht aan grotere fouten, waardoor de lijn dichter bij punten die ver weg liggen blijft.

We tellen vervolgens al deze gekwadrateerde waarden bij elkaar op. Ons doel is om de specifieke lijn te vinden waarbij deze eind-som het kleinst is (de kleinste mogelijke waarde)—vandaar de naam "Kleinstekwadraten".

> **🧮 Laat me de wiskunde zien** 
> 
> Deze lijn, genaamd de _beste fit lijn_, kan worden uitgedrukt door [een vergelijking](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` is de 'verklarende variabele'. `Y` is de 'afhankelijke variabele'. De helling van de lijn is `b` en `a` is het snijpunt op de y-as, dat verwijst naar de waarde van `Y` wanneer `X = 0`. 
>
>![bereken de helling](../../../../translated_images/nl/slope.f3c9d5910ddbfcf9.webp)
>
> Bereken eerst de helling `b`. Infographic door [Jen Looper](https://twitter.com/jenlooper)
>
> Met andere woorden, en verwijzend naar onze originele vraag over pompoendata: "voorspel de prijs van een pompoen per bushel op maand", zou `X` verwijzen naar de prijs en `Y` naar de maand van verkoop.
>
>![vul de vergelijking in](../../../../translated_images/nl/calculation.a209813050a1ddb1.webp)
>
> Bereken de waarde van Y. Als je ongeveer $4 betaalt, moet het april zijn! Infographic door [Jen Looper](https://twitter.com/jenlooper)
>
> De wiskunde die de lijn berekent moet de helling van de lijn aantonen, die ook afhankelijk is van het intercept, of waar `Y` ligt wanneer `X = 0`.
>
> Je kunt de methode van berekening voor deze waarden bekijken op de [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) website. Bezoek ook [deze Kleinstekwadraten calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) om te zien hoe de getallen de lijn beïnvloeden.

## Correlatie

Een andere term om te begrijpen is de **correlatiecoëfficiënt** tussen gegeven X en Y variabelen. Met een scatterplot kun je deze coëfficiënt snel visualiseren. Een plot met datapunten netjes verspreid in een lijn heeft een hoge correlatie, maar een plot met datapunten verspreid over het hele vlak tussen X en Y heeft een lage correlatie.

Een goed lineair regressiemodel zal een hoge (meer dichtbij 1 dan 0) correlatiecoëfficiënt hebben met behulp van de Kleinstekwadratenregressie methode met een regressielijn.

✅ Voer het notebook uit dat bij deze les hoort en bekijk de scatterplot van Maand tegen Prijs. Lijkt de data die maand aan prijs koppelt voor pompoenverkoop een hoge of lage correlatie te hebben volgens jouw visuele interpretatie van de scatterplot? Verandert dat als je een fijnere maat gebruikt in plaats van `Maand`, bijvoorbeeld *dag van het jaar* (i.e. aantal dagen sinds het begin van het jaar)?

In onderstaande code gaan we ervan uit dat we de data hebben opgeschoond, en een data frame verkregen genaamd `new_pumpkins`, vergelijkbaar met het volgende:

ID | Maand | DagVanHetJaar | Variëteit | Stad | Verpakking | Laagste Prijs | Hoogste Prijs | Prijs
---|-------|---------------|-----------|-------|------------|---------------|---------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel kratjes | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel kratjes | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel kratjes | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel kratjes | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel kratjes | 15.0 | 15.0 | 13.636364

> De code om de data schoon te maken is beschikbaar in [`notebook.ipynb`](notebook.ipynb). We hebben dezelfde schoonmaakstappen uitgevoerd als in de vorige les, en de kolom `DagVanHetJaar` berekend met de volgende uitdrukking:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Nu je inzicht hebt in de wiskunde achter lineaire regressie, laten we een regressiemodel maken om te zien of we kunnen voorspellen welke verpakking pompoenen de beste prijzen zal hebben. Iemand die pompoenen koopt voor een feestelijke pompoen-perk wil mogelijk deze informatie om hun aankopen van pompoenverpakkingen voor het perk te optimaliseren.

## Op zoek naar correlatie

[![ML voor beginners - Op zoek naar correlatie: de sleutel tot lineaire regressie](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML voor beginners - Op zoek naar correlatie: de sleutel tot lineaire regressie")

> 🎥 Klik op de afbeelding hierboven voor een korte video-overzicht van correlatie.

Uit de vorige les heb je waarschijnlijk gezien dat de gemiddelde prijs voor verschillende maanden er ongeveer zo uitziet:

<img alt="Gemiddelde prijs per maand" src="../../../../translated_images/nl/barchart.a833ea9194346d76.webp" width="50%"/>

Dit suggereert dat er enige correlatie zou moeten zijn, en we kunnen proberen een lineair regressiemodel te trainen om de relatie tussen `Maand` en `Prijs` te voorspellen, of tussen `DagVanHetJaar` en `Prijs`. Hier is de scatterplot die de laatste relatie toont:

<img alt="Scatterplot van Prijs versus Dag van het Jaar" src="../../../../translated_images/nl/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />

Laten we kijken of er een correlatie is met de `corr` functie:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Het lijkt erop dat de correlatie vrij klein is, -0.15 bij `Maand` en -0.17 bij de `DagVanHetJaar`, maar er kan een andere belangrijke relatie zijn. Het lijkt alsof er verschillende clusters prijzen zijn die overeenkomen met verschillende pompoenvariëteiten. Om deze hypothese te bevestigen, laten we elke pompoencategorie met een andere kleur plotten. Door een `ax` parameter door te geven aan de `scatter` plotfunctie kunnen we alle punten op dezelfde grafiek plotten:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatterplot van Prijs versus Dag van het Jaar" src="../../../../translated_images/nl/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Ons onderzoek suggereert dat variëteit meer effect heeft op de prijs dan de daadwerkelijke verkoopdatum. Dit kunnen we zien met een staafdiagram:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Staafdiagram van prijs versus variëteit" src="../../../../translated_images/nl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Laten we ons voor nu alleen richten op één pompoenvariëteit, de 'pie type', en kijken welk effect de datum heeft op de prijs:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatterplot van Prijs versus Dag van het Jaar" src="../../../../translated_images/nl/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Als we nu de correlatie tussen `Prijs` en `DagVanHetJaar` berekenen met de `corr` functie, krijgen we iets als `-0.27` - wat betekent dat het zinvol is om een voorspellend model te trainen.

> Voordat je een lineair regressiemodel traint is het belangrijk ervoor te zorgen dat onze data schoon is. Lineaire regressie werkt niet goed met ontbrekende waarden, dus het is zinvol om alle lege cellen te verwijderen:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Een andere benadering is om die lege waarden te vullen met gemiddelde waardes uit de betreffende kolom.

## Eenvoudige lineaire regressie

[![ML voor beginners - Lineaire en polynomiale regressie met Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML voor beginners - Lineaire en polynomiale regressie met Scikit-learn")

> 🎥 Klik op de afbeelding hierboven voor een korte video-overzicht van lineaire en polynomiale regressie.

Om ons lineaire regressiemodel te trainen gebruiken we de **Scikit-learn** bibliotheek.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

We beginnen met het scheiden van invoerwaarden (features) en verwachte uitvoer (label) in afzonderlijke numpy-arrays:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Let op dat we `reshape` moesten uitvoeren op de invoerdata zodat het Linear Regression-pakket het correct kan begrijpen. Lineaire regressie verwacht een 2D-array als invoer waarbij elke rij van de array overeenkomt met een vector van invoerkenmerken. In ons geval, omdat we slechts één invoer hebben, hebben we een array nodig met de vorm N&times;1, waarbij N de grootte van de dataset is.

Dan moeten we de data splitsen in train- en testdatasets, zodat we ons model na het trainen kunnen valideren:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Tenslotte kost het trainen van het eigenlijke lineaire regressiemodel maar twee regels code. We definiëren het `LinearRegression` object en passen het toe op onze data met de `fit` methode:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Het `LinearRegression` object bevat na het fitten alle coëfficiënten van de regressie, die toegankelijk zijn via de `.coef_` eigenschap. In ons geval is er slechts één coëfficiënt, die ongeveer `-0.017` zou moeten zijn. Dit betekent dat prijzen enigszins lijken te dalen in de tijd, maar niet te veel, ongeveer 2 cent per dag. We kunnen ook het snijpunt van de regressie met de Y-as benaderen via `lin_reg.intercept_` - dit zal rond `21` liggen in ons geval, wat de prijs aan het begin van het jaar aangeeft.

Om te zien hoe nauwkeurig ons model is, kunnen we prijzen voorspellen op een testdataset, en vervolgens meten hoe dicht onze voorspellingen bij de verwachte waarden liggen. Dit kan worden gedaan met root mean square error (RMSE) metrics, wat de wortel van het gemiddelde van alle gekwadrateerde verschillen tussen de verwachte en voorspelde waarde is.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Onze fout lijkt rond de 2 punten te liggen, wat ongeveer 17% is. Niet zo goed. Een andere indicator van de modelkwaliteit is de **bepalingscoëfficiënt**, die als volgt kan worden verkregen:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Als de waarde 0 is, betekent dit dat het model geen rekening houdt met de invoergegevens en fungeert als de *slechtste lineaire voorspeller*, die simpelweg de gemiddelde waarde van het resultaat is. Een waarde van 1 betekent dat we perfect alle verwachte uitkomsten kunnen voorspellen. In ons geval is de coëfficiënt ongeveer 0.06, wat vrij laag is.

We kunnen ook de testdata plotten samen met de regressielijn om beter te zien hoe de regressie in ons geval werkt:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Lineaire regressie" src="../../../../translated_images/nl/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomiale Regressie

Een ander type lineaire regressie is polynomiale regressie. Hoewel er soms een lineair verband is tussen variabelen - hoe groter de pompoen in volume, hoe hoger de prijs - kunnen deze relaties soms niet als een vlak of rechte lijn worden geplot.

✅ Hier zijn [nog enkele voorbeelden](https://online.stat.psu.edu/stat501/lesson/9/9.8) van data die polynomiale regressie kunnen gebruiken

Bekijk nogmaals de relatie tussen Datum en Prijs. Lijkt deze spreidingsgrafiek er echt op dat het noodzakelijk via een rechte lijn geanalyseerd moet worden? Kunnen prijzen niet fluctueren? In dat geval kun je polynomiale regressie proberen.

✅ Polynomen zijn wiskundige expressies die kunnen bestaan uit een of meer variabelen en coëfficiënten

Polynomiale regressie creëert een gekromde lijn om niet-lineaire data beter te passen. In ons geval, als we een gekwadrateerde `DayOfYear` variabele opnemen in de invoerdata, zouden we onze data moeten kunnen passen met een parabolische curve die een minimum heeft op een bepaald punt binnen het jaar.

Scikit-learn bevat een handige [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) om verschillende stappen van dataverwerking te combineren. Een **pipeline** is een keten van **estimators**. In ons geval maken we een pipeline die eerst polynomiale kenmerken toevoegt aan ons model, en vervolgens de regressie traint:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Door `PolynomialFeatures(2)` te gebruiken, nemen we alle tweede-graads polynomen van de invoerdata op. In ons geval betekent dit alleen `DayOfYear`<sup>2</sup>, maar met twee invoervariabelen X en Y voegt dit X<sup>2</sup>, XY en Y<sup>2</sup> toe. We kunnen ook hogere graads polynomen gebruiken als we willen.

Pipelines kunnen op dezelfde manier worden gebruikt als het originele `LinearRegression` object, d.w.z. we kunnen de pipeline `fitten` en vervolgens `predict` gebruiken om de resultaten te krijgen. Hier is de grafiek met testdata en de benaderingscurve:

<img alt="Polynomiale regressie" src="../../../../translated_images/nl/poly-results.ee587348f0f1f60b.webp" width="50%" />

Met polynomiale regressie krijgen we iets lagere MSE en hogere bepalingscoëfficiënt, maar niet significant. We moeten rekening houden met andere kenmerken!

> Je ziet dat de minimale pompoenprijzen ergens rond Halloween zijn. Hoe kun je dat verklaren?

🎃 Gefeliciteerd, je hebt zojuist een model gemaakt dat kan helpen de prijs van taartpompoenen te voorspellen. Waarschijnlijk kun je dezelfde procedure voor alle pompoentypes herhalen, maar dat zou saai zijn. Laten we nu leren hoe we pompoensoorten rekening kunnen laten houden in ons model!

## Categorische Kenmerken

In de ideale wereld willen we prijzen kunnen voorspellen voor verschillende pompoenrassen met hetzelfde model. De kolom `Variety` is echter anders dan kolommen zoals `Month`, omdat deze niet-numerieke waarden bevat. Zulke kolommen heten **categorisch**.

[![ML voor beginners - Categorische Kenmerken voorspellen met Lineaire Regressie](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML voor beginners - Categorische Kenmerken voorspellen met Lineaire Regressie")

> 🎥 Klik op de afbeelding hierboven voor een korte video-overzicht van het gebruik van categorische kenmerken.

Hier zie je hoe de gemiddelde prijs afhangt van de variëteit:

<img alt="Gemiddelde prijs per variëteit" src="../../../../translated_images/nl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Om variëteit mee te nemen, moeten we het eerst omzetten naar numerieke vorm, oftewel **encoderen**. We kunnen dat op verschillende manieren doen:

* Eenvoudige **numerieke codering** maakt een tabel van verschillende variëteiten en vervangt dan de variëteitnaam door een index in die tabel. Dit is niet de beste methode voor lineaire regressie, omdat lineaire regressie de daadwerkelijke numerieke waarde van de index neemt en toevoegt aan het resultaat, vermenigvuldigd met een coëfficiënt. In ons geval is de relatie tussen het indexnummer en de prijs duidelijk niet-lineair, zelfs als we zorgen dat indices op bepaalde orde staan.
* **One-hot encoding** vervangt de kolom `Variety` door 4 verschillende kolommen, één voor elke variëteit. Elke kolom bevat `1` als de overeenkomstige rij van die variëteit is, en `0` anders. Dit betekent dat er vier coëfficiënten in de lineaire regressie zijn, één per pompoenvariëteit, verantwoordelijk voor de "startprijs" (of beter gezegd "extra prijs") voor die specifieke variëteit.

De volgende code laat zien hoe we variëteit one-hot encoderen:

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

Om lineaire regressie te trainen met one-hot encoded variëteit als invoer, hoeven we `X` en `y` alleen correct te initialiseren:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

De rest van de code is hetzelfde als wat we eerder gebruikten om lineaire regressie te trainen. Als je dit probeert, zie je dat de mean squared error ongeveer hetzelfde is, maar we krijgen veel een hogere bepalingscoëfficiënt (~77%). Om nog nauwkeurigere voorspellingen te krijgen, kunnen we meer categorische kenmerken meenemen, evenals numerieke kenmerken zoals `Month` of `DayOfYear`. Om één grote array van kenmerken te verkrijgen, kunnen we `join` gebruiken:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Hier houden we ook rekening met `City` en `Package` type, wat ons een MSE van 2.84 (10%) en een bepalingscoëfficiënt van 0.94 geeft!

## Alles samenvoegen

Om het beste model te maken, kunnen we gecombineerde (one-hot encoded categorische + numerieke) data van het bovenstaande voorbeeld samen met polynomiale regressie gebruiken. Hier is de complete code voor jouw gemak:

```python
# stel trainingsgegevens in
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# maak train-test splitsing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# stel de pijplijn in en train deze
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# voorspel resultaten voor testgegevens
pred = pipeline.predict(X_test)

# bereken MSE en determinatie
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Dit zou ons de beste bepalingscoëfficiënt van bijna 97% moeten geven, en MSE=2.23 (~8% voorspellingsfout).

| Model | MSE | Bepalingscoëfficiënt |
|-------|-----|----------------------|
| `DayOfYear` Lineair | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomiaal | 2.73 (17.0%) | 0.08 |
| `Variety` Lineair | 5.24 (19.7%) | 0.77 |
| Alle kenmerken Lineair | 2.84 (10.5%) | 0.94 |
| Alle kenmerken Polynomiaal | 2.23 (8.25%) | 0.97 |

🏆 Goed gedaan! Je maakte vier regressiemodellen in één les en verbeterde de modelkwaliteit tot 97%. In de laatste sectie over regressie leer je over logistieke regressie om categorieën te bepalen.

---
## 🚀Uitdaging

Test verschillende variabelen in dit notebook om te zien hoe correlatie overeenkomt met modelnauwkeurigheid.

## [Quiz na de les](https://ff-quizzes.netlify.app/en/ml/)

## Review & Zelfstudie

In deze les leerden we over lineaire regressie. Er zijn andere belangrijke typen regressie. Lees over Stepwise, Ridge, Lasso en Elasticnet technieken. Een goede cursus om meer te leren is de [Stanford Statistical Learning cursus](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Opdracht

[Maak een model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Disclaimer**:
Dit document is vertaald met behulp van de AI-vertalingsdienst [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, moet u er rekening mee houden dat geautomatiseerde vertalingen fouten of onjuistheden kunnen bevatten. Het originele document in de oorspronkelijke taal dient als de gezaghebbende bron te worden beschouwd. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor eventuele misverstanden of verkeerde interpretaties voortvloeiend uit het gebruik van deze vertaling.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->