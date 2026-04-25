# Zgradite regresijski model s Scikit-learn: regresija na štiri načine

## Opomba za začetnike

Linearna regresija se uporablja, kadar želimo napovedati **numerično vrednost** (na primer cena hiše, temperatura ali prodaja).
Deluje tako, da najde najboljšo ravno črto, ki predstavlja povezavo med vhodnimi značilnostmi in izhodom.

V tej lekciji se osredotočamo na razumevanje koncepta, preden raziščemo bolj napredne regresijske tehnike.
![Linear vs polynomial regression infographic](../../../../translated_images/sl/linear-polynomial.5523c7cb6576ccab.webp)
> Infografika avtorja [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Kviz pred predavanjem](https://ff-quizzes.netlify.app/en/ml/)

> ### [Ta lekcija je na voljo tudi v R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Uvod

Do zdaj ste raziskovali, kaj je regresija, z vzorčnimi podatki, zbranimi iz podatkovnega nabora za cene buč, ki jih bomo uporabljali v tej lekciji. Prav tako ste ju vizualizirali z uporabo Matplotlib.

Zdaj ste pripravljeni poglobljeno raziskati regresijo za ML. Medtem ko vizualizacija omogoča razumevanje podatkov, prava moč strojnega učenja izvira iz _usposabljanja modelov_. Modeli se usposabljajo na zgodovinskih podatkih, da samodejno zajamejo odvisnosti med podatki in omogočajo napovedovanje izidov za nove podatke, ki jih model še ni videl.

V tej lekciji boste spoznali dve vrsti regresije: _osnovno linearno regresijo_ in _polinomsko regresijo_, skupaj z nekaj matematike, ki je podlaga za ti tehniki. Ti modeli nam bodo omogočili napovedovanje cen buč glede na različne vhodne podatke.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Kliknite na zgornjo sliko za kratek video pregled linearne regresije.

> V celotnem tematskem sklopu predvidevamo minimalno matematično znanje in želimo, da bo dostopno študentom iz drugih področij, zato bodite pozorni na opombe, 🧮 oznake, diagrame in druge učne pripomočke za lažje razumevanje.

### Predpogoj

Zdaj morate biti seznanjeni s strukturo podatkov o bučah, ki jih preučujemo. Te podatke najdete prednaložene in očiščene v datoteki _notebook.ipynb_ te lekcije. V tej datoteki je cena buče prikazana na merico (bushel) v novem podatkovnem okviru. Poskrbite, da lahko te zvezke zaženete v jedrih (kernels) v Visual Studio Code.

### Priprava

Kot opomnik, te podatke nalagate, da bi lahko postavili vprašanja.

- Kdaj je najboljši čas za nakup buč?
- Kakšno ceno lahko pričakujem za škatlo miniaturnih buč?
- Naj jih kupim v košarah za pol bushela ali v škatlah za 1 1/9 bushela?
Poglobimo se še naprej v te podatke.

V prejšnji lekciji ste ustvarili Pandas podatkovni okvir in vanj vnesli del originalnega nabora podatkov, kjer ste standardizirali cene glede na bushel. S tem ste lahko zajeli približno 400 podatkovnih točk in le za jesenske mesece.

Oglejte si podatke, ki smo jih prednaložili v pripadajočem zvezku te lekcije. Podatki so prednaloženi in kaže se začetni razpršeni diagram (scatterplot), ki prikazuje mesečne podatke. Morda lahko pridobimo več podrobnosti o naravi podatkov z dodatnim čiščenjem.

## Linearna regresijska črta

Kot ste se naučili v lekciji 1, je cilj linearne regresije sposobnost narisati črto, ki:

- **Prikazuje razmerja med spremenljivkami.** Prikaže odnos med spremenljivkami.
- **Omogoča napovedi.** Natančno napoveduje, kje bi nova podatkovna točka padla v odnosu do te črte.

Tipično za **regresijo z najmanjšimi kvadrati** je, da se nariše takšna črta. Izraz "najmanjši kvadrati" se nanaša na postopek minimiziranja skupne napake v našem modelu. Za vsako podatkovno točko merimo navpično razdaljo (imenuje se ostanek) med dejansko točko in regresijsko črto.

Te razdalje kvadriramo iz dveh glavnih razlogov:

1. **Velikost pred smerjo:** Želimo, da se napaka -5 in +5 obravnavata enako. Kvadriranje naredi vse vrednosti pozitivne.

2. **Kaznovanje odstopanj:** Kvadriranje daje večjo težo večjim napakam in sili črto, da ostane bližje točk, ki so bolj oddaljene.

Nato seštejemo vse te kvadrirane vrednosti. Naš cilj je poiskati črto, kjer je ta vsota najmanjša (najnižja možna vrednost) — od tod ime "najmanjši kvadrati".

> **🧮 Pokaži mi formulo**
>
> Ta črta, imenovana _črta najboljšega prileganja_, je izražena z [enačbo](https://en.wikipedia.org/wiki/Simple_linear_regression):
>
> ```
> Y = a + bX
> ```
>
> `X` je 'razložilna spremenljivka'. `Y` je 'odvisna spremenljivka'. Naklon črte je `b`, `a` pa je y-presečišče, kar pomeni vrednost `Y`, ko je `X = 0`.
>
>![izrračunaj naklon](../../../../translated_images/sl/slope.f3c9d5910ddbfcf9.webp)
>
> Najprej izračunajte naklon `b`. Infografika avtorice [Jen Looper](https://twitter.com/jenlooper)
>
> Z drugimi besedami in glede na vprašanje iz podatkov o bučah: "napovedati ceno buče na bushel glede na mesec", `X` bi se nanašal na ceno, `Y` pa na mesec prodaje.
>
>![dopovej enačbo](../../../../translated_images/sl/calculation.a209813050a1ddb1.webp)
>
> Izračunajte vrednost Y. Če plačujete okoli 4 dolarje, mora biti april! Infografika avtorice [Jen Looper](https://twitter.com/jenlooper)
>
> Matematika, ki izračuna črto, mora prikazati naklon črte, ki je tudi odvisen od presečišča, oziroma kje se `Y` nahaja, ko je `X = 0`.
>
> Metode za izračun teh vrednosti lahko opazujete na spletni strani [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Obiščite tudi [ta kalkulator najmanjših kvadratov](https://www.mathsisfun.com/data/least-squares-calculator.html), da vidite, kako vrednosti vplivajo na črto.

## Korelacija

Še en izraz za razumevanje je **korelacijski koeficient** med danima spremenljivkama X in Y. Z uporabo scatterplota lahko hitro vizualizirate ta koeficient. Diagram, kjer so podatkovne točke razvrščene v lepo črto, ima visoko korelacijo, medtem ko ima diagram z razpršenimi točkami po celotnem območju X in Y nizko korelacijo.

Dober linearni regresijski model bo tisti, ki ima visok (bližje 1 kot 0) korelacijski koeficient z metodo najmanjših kvadratov in regresijsko črto.

✅ Zaženite zvezek, ki spremlja to lekcijo, in si oglejte scatterplot Medijec glede na Ceno. Ali se podatki povezani z mesecem in ceno za prodajo buč zdijo imeti visoko ali nizko korelacijo glede na vašo vizualno interpretacijo scatterplota? Se to spremeni, če uporabite bolj natančno mero namesto `Month`, npr. *dan v letu* (tj. število dni od začetka leta)?

V spodnji kodi bomo predpostavili, da smo podatke očistili in dobili podatkovni okvir z imenom `new_pumpkins`, podoben naslednjemu:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Koda za čiščenje podatkov je na voljo v [`notebook.ipynb`](notebook.ipynb). Izvedli smo enake korake čiščenja kot v prejšnji lekciji in izračunali stolpec `DayOfYear` z naslednjim izrazom:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Zdaj, ko imamo razumevanje matematike za linearno regresijo, ustvarimo regresijski model, da vidimo, ali lahko napovemo, kateri paket buč bo imel najboljše cene. Nekdo, ki kupuje buče za praznično bučno okrasje, bi morda želel to informacijo, da bi lahko optimiziral nakupe paketov.

## Iskanje korelacije

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Kliknite na zgornjo sliko za kratek video pregled korelacije.

Iz prejšnje lekcije ste verjetno videli, da povprečna cena za različne mesece izgleda takole:

<img alt="Average price by month" src="../../../../translated_images/sl/barchart.a833ea9194346d76.webp" width="50%"/>

To nakazuje, da bi morala obstajati neka korelacija, in lahko poskusimo usposobiti linearni regresijski model, ki napoveduje odnos med `Month` in `Price` ali med `DayOfYear` in `Price`. Tukaj je scatterplot, ki prikazuje slednji odnos:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sl/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />

Poglejmo, ali je korelacija ob uporabi funkcije `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Zdi se, da je korelacija precej majhna, -0,15 glede na `Month` in -0,17 glede na `DayOfMonth`, vendar je lahko še kakšen drug pomemben odnos. Zdi se, da obstajajo različni grozdi cen, ki ustrezajo različnim sortam buč. Za potrditev te hipoteze prikažimo vsak razred buč z drugo barvo. Z uporabo parametra `ax` funkciji `scatter` lahko narišemo vse točke na istem diagramu:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sl/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Naša preiskava nakazuje, da ima sorta večji vpliv na ceno kot dejanski datum prodaje. To lahko vidimo s stolpčnim diagramom:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/sl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Za trenutek se osredotočimo samo na eno sorto buč, 'tip pite', in si oglejmo, kakšen vpliv ima datum na ceno:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/sl/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Če zdaj izračunamo korelacijo med `Price` in `DayOfYear` z uporabo funkcije `corr`, bomo dobili nekaj okoli `-0,27` - kar pomeni, da ima smisel usposabljanje napovednega modela.

> Pred usposabljanjem linearnega regresijskega modela je pomembno, da podatki niso nepopolni. Linearna regresija ne deluje dobro z manjkajočimi vrednostmi, zato je smiselno odstraniti vse prazne celice:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Drugi pristop bi bil, da prazne vrednosti zapolnimo s povprečnimi vrednostmi iz ustreznega stolpca.

## Preprosta linearna regresija

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Kliknite na zgornjo sliko za kratek video pregled linearne in polinomske regresije.

Za usposabljanje našega modela linearne regresije bomo uporabili knjižnico **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Najprej ločimo vhodne vrednosti (značilnosti) in pričakovani izhod (oznake) v ločene numpy tabele:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Upoštevajte, da smo morali vhodne podatke preoblikovati z uporabo `reshape`, da jih paket Linear Regression pravilno razume. Linearna regresija pričakuje 2D-tabelo kot vhod, kjer vsak vrstica predstavlja vektor vhodnih značilnosti. V našem primeru, ker imamo samo eno vhodno vrednost, potrebujemo tabelo oblike N×1, kjer je N velikost nabora podatkov.

Nato moramo podatke razdeliti na učni in testni nabor, da lahko preverimo model po usposabljanju:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Nazadnje usposabljanje samega linearnega regresijskega modela vzame le dve vrstici kode. Definiramo objekt `LinearRegression` in ga prilagodimo našim podatkom z metodo `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objekt `LinearRegression` po `fit`-anju vsebuje vse koeficiente regresije, do katerih lahko dostopamo z lastnostjo `.coef_`. V našem primeru je le en koeficient, ki naj bi bil okoli `-0.017`. To pomeni, da se cene zdi, da rahlo upadajo sčasoma, vendar ne preveč, približno 2 centa na dan. Dostopamo lahko tudi do presečišča regresije z Y-osjo z uporabo `lin_reg.intercept_` - v našem primeru bo to okoli `21`, kar nakazuje ceno na začetku leta.

Da vidimo, kako natančen je naš model, lahko napovemo cene na testnem naboru podatkov in nato izmerimo, kako blizu so naše napovedi pričakovanim vrednostim. To lahko storimo z uporabo metrike korenskega povprečnega kvadratnega odklona (RMSE), ki je koren povprečja vseh kvadratnih razlik med pričakovano in napovedano vrednostjo.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Naša napaka je približno 2 točki, kar je ~17%. Ni prav dobro. Drugi pokazatelj kakovosti modela je **koeficient determinacije**, ki ga lahko dobimo tako:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Če je vrednost 0, to pomeni, da model ne upošteva vhodnih podatkov in deluje kot *najslabši linearni napovedovalec*, ki je preprosto povprečna vrednost rezultata. Vrednost 1 pomeni, da lahko dokončno napovemo vse pričakovane izhode. V našem primeru je koeficient okoli 0,06, kar je precej nizko.

Lahko tudi narišemo testne podatke skupaj z regresijsko premico, da lažje vidimo, kako regresija deluje v našem primeru:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/sl/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polinomska regresija

Druga vrsta linearne regresije je polinomska regresija. Medtem ko je včasih linearni odnos med spremenljivkami - večja kot je buča po volumnu, višja je cena - so včasih ti odnosi takšni, da jih ne moremo prikazati kot ravnino ali ravno črto.

✅ Tukaj je [še nekaj primerov](https://online.stat.psu.edu/stat501/lesson/9/9.8) podatkov, ki bi lahko uporabili polinomsko regresijo.

Poglejmo še enkrat odnos med datumom in ceno. Ali se vam ta raščrtani graf zdi, da bi ga bilo treba nujno analizirati z ravno črto? Se cene ne morejo spreminjati? V tem primeru lahko poskusite polinomsko regresijo.

✅ Polinomi so matematični izrazi, ki lahko vsebujejo eno ali več spremenljivk in koeficientov.

Polinomska regresija ustvari ukrivljeno črto, da bolje prilepi nelinearne podatke. V našem primeru, če vključimo spremenljivko z kvadratom `DayOfYear` v vhodne podatke, bi morali biti sposobni prilegati naše podatke s parabolično krivuljo, ki bo imela minimum na določeni točki v letu.

Scikit-learn vključuje uporaben [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) za združevanje različnih korakov obdelave podatkov. **Pipeline** je veriga **estimatorjev**. V našem primeru bomo ustvarili pipeline, ki najprej doda polinomske značilnosti k našemu modelu, nato pa izvede učenje regresije:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Uporaba `PolynomialFeatures(2)` pomeni, da bomo vključili vse polinome druge stopnje iz vhodnih podatkov. V našem primeru bo to samo pomenilo `DayOfYear`<sup>2</sup>, vendar pa pri dveh vhodnih spremenljivkah X in Y doda X<sup>2</sup>, XY in Y<sup>2</sup>. Lahko uporabimo tudi višje stopnje polinomov, če želimo.

Pipeline lahko uporabljamo na enak način kot izvorni objekt `LinearRegression`, tj. lahko uporabimo `fit` na pipelineu in nato uporabimo `predict` za pridobitev rezultatov napovedi. Tukaj je graf, ki prikazuje testne podatke in približno krivuljo:

<img alt="Polynomial regression" src="../../../../translated_images/sl/poly-results.ee587348f0f1f60b.webp" width="50%" />

Z uporabo polinomske regresije lahko dosežemo nekoliko nižjo MSE in višji koeficient determinacije, vendar ne bistveno. Upoštevati moramo še druge značilnosti!

> Vidite, da so minimalne cene buč opažene nekje okoli noči čarovnic. Kako to pojasnite?

🎃 Čestitamo, ravnokar ste ustvarili model, ki lahko pomaga napovedati ceno buč za pito. Verjetno lahko isto proceduro ponovite za vse vrste buč, vendar bi bilo to zamudno. Naučimo se zdaj, kako upoštevati različico buče v našem modelu!

## Kategorijske značilnosti

V idealnem svetu želimo z istim modelom napovedovati cene za različne vrste buč. Vendar je stolpec `Variety` nekoliko drugačen od stolpcev, kot je `Month`, saj vsebuje neničelne vrednosti. Takšni stolpci se imenujejo **kategorijski**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Kliknite na sliko zgoraj za kratek video pregled uporabe kategorijskih značilnosti.

Tukaj lahko vidite, kako povprečna cena zaleži od različice:

<img alt="Average price by variety" src="../../../../translated_images/sl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Da bi upoštevali različico, jo moramo najprej pretvoriti v številčno obliko ali jo **kodirati**. Obstaja več načinov, kako to storiti:

* Preprosta **numerična kodiranja** zgradi tabelo različnih različic in nato nadomesti ime različice z indeksom v tej tabeli. To ni najboljša ideja za linearno regresijo, ker linearna regresija upošteva dejansko številčno vrednost indeksa in ga prišteje rezultatu, množi z nekim koeficientom. V našem primeru je razmerje med številko indeksa in ceno očitno nelinearno, tudi če zagotovimo, da so indeksi urejeni na določen način.
* **One-hot kodiranje** nadomesti stolpec `Variety` s 4 različnimi stolpci, po enim za vsako različico. Vsak stolpec bo vseboval `1`, če je ustrezni vrstici dodeljena dana različica, in `0` sicer. To pomeni, da bo v linearni regresiji štiri koeficiente, po enega za vsako vrsto buč, odgovornega za "začetno ceno" (ali bolje "dopolnilno ceno") za to določeno vrsto.

Spodnja koda prikazuje, kako lahko one-hot kodiramo vrsto:

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

Za učenje linearne regresije z uporabo one-hot kodirane različice kot vhodnih podatkov moramo le pravilno inicializirati podatke `X` in `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Ostali del kode je enak kot tisti, ki smo ga uporabili zgoraj za učenje linearne regresije. Če to poskusite, boste videli, da je povprečni kvadratni odklon približno enak, vendar dobimo veliko višji koeficient determinacije (~77%). Za še natančnejše napovedi lahko upoštevamo več kategorijskih spremenljivk, kot tudi številčne značilnosti, kot so `Month` ali `DayOfYear`. Za pridobitev ene velike tabele značilnosti lahko uporabimo `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Tukaj upoštevamo tudi `City` in tip `Package`, kar nam da MSE 2,84 (10%) in koeficient determinacije 0,94!

## Združevanje vsega skupaj

Da ustvarimo najboljši model, lahko uporabimo kombinirane podatke (one-hot kodirane kategorijske + številčne) iz zgornjega primera skupaj s polinomsko regresijo. Tukaj je za vašo udobje celotna koda:

```python
# nastavite podatke za usposabljanje
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# naredite razdelitev treninga in testa
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# nastavite in usposobite cevovod
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# napovejte rezultate za testne podatke
pred = pipeline.predict(X_test)

# izračunajte MSE in koeficient determinacije
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

To bi nam moralo dati najboljši koeficient determinacije skoraj 97% in MSE=2,23 (~8% napaka napovedi).

| Model | MSE | Koeficient determinacije |
|-------|-----|--------------------------|
| Linearni `DayOfYear` | 2,77 (17,2%) | 0,07 |
| Polinomski `DayOfYear` | 2,73 (17,0%) | 0,08 |
| Linearni `Variety` | 5,24 (19,7%) | 0,77 |
| Linearni z vsemi značilnostmi | 2,84 (10,5%) | 0,94 |
| Polinomski z vsemi značilnostmi | 2,23 (8,25%) | 0,97 |

🏆 Odlično! Ustvarili ste štiri regresijske modele v eni lekciji in izboljšali kakovost modela na 97%. V zadnjem razdelku o regresiji se boste naučili o logistični regresiji za določanje kategorij.

---
## 🚀Izziv

Preizkusite več spremenljivk v tem zvezku, da vidite, kako korelacija ustreza natančnosti modela.

## [Kviz po predavanju](https://ff-quizzes.netlify.app/en/ml/)

## Pregled & Samostojno učenje

V tej lekciji smo se naučili o linearni regresiji. Obstajajo še druge pomembne vrste regresije. Preberite o tehnikah Stepwise, Ridge, Lasso in Elasticnet. Dobro je tudi študirati tečaj [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning), da se naučite več.

## Naloga

[Izdelajte model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Omejitev odgovornosti**:
Ta dokument je bil preveden z uporabo AI prevajalske storitve [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, upoštevajte, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v svojem izvirnem jeziku naj velja kot avtoritativni vir. Za ključne informacije priporočamo strokovni človeški prevod. Nismo odgovorni za kakršne koli napačne razlage ali napačne interpretacije, ki izhajajo iz uporabe tega prevoda.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->