# Vytvorte regresný model pomocou Scikit-learn: regresia štyrmi spôsobmi

## Poznámka pre začiatočníkov

Lineárna regresia sa používa, keď chceme predpovedať **číselnú hodnotu** (napríklad cenu domu, teplotu alebo predaj).
Funguje tak, že nájde priamku, ktorá najlepšie reprezentuje vzťah medzi vstupnými vlastnosťami a výstupom.

V tejto lekcii sa zameriame na pochopenie konceptu predtým, než preskúmame pokročilejšie regresné techniky.
![Lineárna verzus polynomiálna regresia infografika](../../../../translated_images/sk/linear-polynomial.5523c7cb6576ccab.webp)
> Infografika od [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Kvíz pred prednáškou](https://ff-quizzes.netlify.app/en/ml/)

> ### [Táto lekcia je dostupná aj v R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Úvod 

Doteraz ste preskúmali, čo je regresia, na vzorových dátach získaných z datasetu s cenami tekvíc, ktoré budeme používať počas celej tejto lekcie. Tiež ste ich vizualizovali pomocou Matplotlib.

Teraz ste pripravení ponoriť sa hlbšie do regresie v strojovom učení. Kým vizualizácia umožňuje lepšie pochopiť dáta, skutočná sila strojového učenia spočíva v _trénovaní modelov_. Modely sa trénujú na historických dátach, aby automaticky zachytili závislosti v dátach, a umožňujú predpovedať výsledky pre nové dáta, ktoré model predtým nevidel.

V tejto lekcii sa naučíte viac o dvoch typoch regresie: _základná lineárna regresia_ a _polynomiálna regresia_, spolu s niektorou matematikou, ktorá stojí za týmito technikami. Tieto modely nám umožnia predpovedať ceny tekvíc v závislosti od rôznych vstupných dát. 

[![ML pre začiatočníkov - Pochopenie lineárnej regresie](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML pre začiatočníkov - Pochopenie lineárnej regresie")

> 🎥 Kliknite na obrázok vyššie pre krátky video prehľad lineárnej regresie.

> V celom tomto kurze predpokladáme minimálne matematické znalosti a snažíme sa sprístupniť učenie študentom z iných odborov, preto sledujte poznámky, 🧮 odkazy, diagramy a iné nástroje na uľahčenie pochopenia.

### Predpoklady

Teraz by ste mali byť oboznámení so štruktúrou dát o tekviciach, ktoré skúmame. Nájdete ich prednačítané a predčistené v súbore _notebook.ipynb_ tejto lekcie. V súbore je cena tekvíc zobrazená na jeden košík. Uistite sa, že viete spustiť tieto notebooky v kerneloch Visual Studio Code.

### Príprava

Pripomíname, že tieto dáta načítavate preto, aby ste im mohli klásť otázky.

- Kedy je najlepší čas kúpiť tekvice? 
- Akú cenu môžem očakávať za balík minitekvíc?
- Mali by ste ich kupovať v polovičných košíkoch alebo v 1 1/9 košíkových krabiciach?
Poďme sa ďalej ponoriť do týchto dát.

V predchádzajúcej lekcii ste vytvorili Pandas dátový rámec a naplnili ho časťou pôvodného datasetu, štandardizujúc ceny podľa košíka. Týmto spôsobom ste však získali iba asi 400 dátových bodov a len za jesenné mesiace.

Pozrite sa na dáta, ktoré sme prednačítali v notebooku k tejto lekcii. Dáta sú načítané a zobrazený je počiatočný bodový graf podľa mesiaca. Možno získame viac detailov o povahe dát ich ďalším čistením.

## Lineárna regresná priamka

Ako ste sa naučili v Lekcii 1, cieľom cvičenia lineárnej regresie je byť schopný vyrenderovať priamku, ktorá:

- **Ukáže vzťahy premenných**. Zobrazí vzťah medzi premennými.
- **Umožní predpovede**. Presne predpovedá, kde by sa nový dátový bod mohol nachádzať vzhľadom na túto priamku.

Typickým prístupom **Metódy najmenších štvorcov** je nakresliť tento typ priamky. Termín „Najmenšie štvorce“ sa vzťahuje na proces minimalizácie celkovej chyby v našom modeli. Pre každý dátový bod meriame zvislú vzdialenosť (nazývanú reziduál) medzi skutočným bodom a našou regresnou priamkou.

Tieto vzdialenosti umocňujeme na druhú z dvoch hlavných dôvodov:

1. **Veľkosť nad smerom:** Chceme, aby chyba -5 bola braná rovnako ako chyba +5. Umocnením na druhú sa všetky hodnoty stanú kladnými.

2. **Postihovanie odľahlých hodnôt:** Umocnenie na druhú dáva väčšiu váhu väčším chybám, nútiac priamku zostať bližšie k bodom, ktoré sú ďaleko.

Potom tieto štvorcové hodnoty sčítame. Naším cieľom je nájsť konkrétnu priamku, kde je tento súčet najmenší (najnižšia možná hodnota) — odtiaľ pochádza názov „Najmenšie štvorce“.

> **🧮 Ukáž mi matematiku**
> 
> Táto priamka, nazývaná _priamkou najlepšieho prispôsobenia_, môže byť vyjadrená [rovnicou](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` je 'vysvetľujúca premenná'. `Y` je 'závislá premenná'. Sklon priamky je `b` a `a` je y-priesečník, teda hodnota `Y` keď `X = 0`.
>
>![vypočítajte sklon](../../../../translated_images/sk/slope.f3c9d5910ddbfcf9.webp)
>
> Najskôr vypočítajte sklon `b`. Infografika od [Jen Looper](https://twitter.com/jenlooper)
>
> Inými slovami, ak sa vraciame k pôvodnej otázke nášho datasetu o tekviciach: „predpovedať cenu tekvice na košík podľa mesiaca“, `X` by odkazovalo na cenu a `Y` by predstavovalo mesiac predaja.
>
>![doplnte rovnicu](../../../../translated_images/sk/calculation.a209813050a1ddb1.webp)
>
> Vypočítajte hodnotu Y. Ak platíte okolo 4 dolárov, musí to byť apríl! Infografika od [Jen Looper](https://twitter.com/jenlooper)
>
> Matematika, ktorá vypočíta priamku, musí ukázať sklon priamky, ktorý závisí aj od priesečníka, čiže kde sa nachádza `Y`, keď `X = 0`.
>
> Metódu výpočtu týchto hodnôt si môžete pozrieť na stránke [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Navštívte tiež [tento kalkulátor najmenších štvorcov](https://www.mathsisfun.com/data/least-squares-calculator.html) a sledujte, ako hodnoty čísel ovplyvňujú priamku.

## Korelácia

Je potrebné pochopiť ešte jeden pojem — **korelačný koeficient** medzi danými premennými X a Y. Pomocou bodového grafu môžete tento koeficient rýchlo vizualizovať. Graf, kde sú body poukladané do peknej priamky, má vysokú koreláciu, no graf, kde sú body rozptýlené všade medzi X a Y, má nízku koreláciu.

Dobrý lineárny regresný model bude mať vysoký (bližší k 1 než k 0) korelačný koeficient pomocou metódy najmenších štvorcov s regresnou priamkou.

✅ Spustite notebook priložený k tejto lekcii a pozrite si bodový graf Mesiac voči cene. Má dátový vzťah medzi Mesiacom a cenou pri predaji tekvíc vysokú alebo nízku koreláciu podľa vašej vizuálnej interpretácie grafu? Zmení sa to, ak namiesto `Mesiaca` použijete jemnejšie meradlo, napríklad *deň v roku* (t.j. počet dní od začiatku roka)?

V nižšie uvedenom kóde predpokladáme, že sme dáta očistili a získali dátový rámec s názvom `new_pumpkins`, podobný nasledujúcemu:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Kód na čistenie dát je dostupný v [`notebook.ipynb`](notebook.ipynb). Prešli sme rovnakými krokmi čistenia ako v predchádzajúcej lekcii a vypočítali sme stĺpec `DayOfYear` podľa nasledujúceho výrazu:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Teraz, keď máte pochopenie matematiky za lineárnou regresiou, vytvorme regresný model, aby sme zistili, či vieme predpovedať, ktorý balík tekvíc bude mať najlepšie ceny. Niekto, kto kupuje tekvice na jesennú výzdobu, môže potrebovať tieto informácie na optimalizáciu svojich nákupov.

## Hľadanie korelácie

[![ML pre začiatočníkov - Hľadanie korelácie: Kľúč k lineárnej regresii](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML pre začiatočníkov - Hľadanie korelácie: Kľúč k lineárnej regresii")

> 🎥 Kliknite na obrázok vyššie pre krátky video prehľad korelácie.

Z predchádzajúcej lekcie ste pravdepodobne videli, že priemerná cena za jednotlivé mesiace vyzerá takto:

<img alt="Priemerná cena podľa mesiaca" src="../../../../translated_images/sk/barchart.a833ea9194346d76.webp" width="50%"/>

To naznačuje, že by mala existovať určitá korelácia, a môžeme skúsiť natrénovať lineárny regresný model na predpovedanie vzťahu medzi `Month` a `Price`, alebo medzi `DayOfYear` a `Price`. Tu je bodový graf znázorňujúci druhý vzťah:

<img alt="Bodový graf Cena vs. Deň v roku" src="../../../../translated_images/sk/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Pozrime sa, či existuje korelácia pomocou funkcie `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Zdá sa, že korelácia je dosť malá, -0.15 podľa `Month` a -0.17 podľa `DayOfYear`, ale môže tam byť iný dôležitý vzťah. Vyzerá to, že existujú rôzne skupiny cien zodpovedajúce rôznym odrodám tekvíc. Aby sme túto hypotézu potvrdili, zobrazme každú kategóriu tekvíc inou farbou. Odovzdaním parametra `ax` funkcii `scatter` môžeme nakresliť všetky body na rovnakom grafe:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Bodový graf Cena vs. Deň v roku so zvýraznením farby" src="../../../../translated_images/sk/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Naše vyšetrovanie naznačuje, že odroda má väčší vplyv na celkovú cenu než skutočný dátum predaja. Vidieť to môžeme aj na stĺpcovom grafe:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Stĺpcový graf cena vs odroda" src="../../../../translated_images/sk/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Zamerajme sa teraz len na jednu odrodu tekvíc, 'pie type', a pozrime sa, aký vplyv má dátum na cenu:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Bodový graf Cena vs. Deň v roku pre odrodu Pie Type" src="../../../../translated_images/sk/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Ak teraz vypočítame koreláciu medzi `Price` a `DayOfYear` pomocou funkcie `corr`, dostaneme niečo okolo `-0.27` — čo znamená, že trénovanie predikčného modelu dáva zmysel.

> Pred trénovaním lineárneho regresného modelu je dôležité uistiť sa, že naše dáta sú čisté. Lineárna regresia nefunguje dobre s chýbajúcimi hodnotami, preto je rozumné odstrániť všetky prázdne bunky:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Iný prístup je vyplniť prázdne hodnoty priemernými hodnotami zo zodpovedajúceho stĺpca.

## Jednoduchá lineárna regresia

[![ML pre začiatočníkov - Lineárna a polynomiálna regresia pomocou Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML pre začiatočníkov - Lineárna a polynomiálna regresia pomocou Scikit-learn")

> 🎥 Kliknite na obrázok vyššie pre krátky video prehľad lineárnej a polynomiálnej regresie.

Na natrénovanie nášho lineárneho regresného modelu použijeme knižnicu **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Začneme oddelením vstupných hodnôt (vlastností) a očakávaného výstupu (štítku) do samostatných numpy polí:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Všimnite si, že sme museli vykonať `reshape` na vstupných dátach, aby ich lineárna regresia správne rozpoznala. Lineárna regresia očakáva 2D pole ako vstup, kde každý riadok poľa zodpovedá vektoru vstupných vlastností. V našom prípade, keďže máme len jeden vstup, potrebujeme pole tvaru N&times;1, kde N je veľkosť datasetu.

Potom musíme rozdeliť dáta na trénovaciu a testovaciu množinu, aby sme mohli model po trénovaní overiť:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Nakoniec samotné trénovanie lineárneho regresného modelu trvá len dve riadky kódu. Definujeme objekt `LinearRegression` a fitting vykonáme pomocou metódy `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objekt `LinearRegression` po príkaze `fit` obsahuje všetky koeficienty regresie, ku ktorým je možné pristúpiť pomocou vlastnosti `.coef_`. V našom prípade je tam len jeden koeficient, ktorý by mal byť okolo hodnoty `-0.017`. Znamená to, že ceny sa zdajú s časom mierne znižovať, ale nie príliš, približne o 2 centy za deň. Môžeme tiež pristúpiť k priesečníku regresie s osou Y pomocou `lin_reg.intercept_` - v našom prípade to bude okolo `21`, čo označuje cenu na začiatku roka.

Aby sme videli, aká je presnosť nášho modelu, môžeme predikovať ceny na testovacej sade dát a potom zmerať, ako blízko sú naše predikcie očakávaným hodnotám. To je možné urobiť pomocou metriky root mean square error (RMSE), čo je odmocnina z priemeru všetkých štvorcových rozdielov medzi očakávanými a predikovanými hodnotami.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Naša chyba sa zdá byť okolo 2 bodov, čo je približne 17%. Nie príliš dobre. Ďalším ukazovateľom kvality modelu je **koeficient determinácie**, ktorý je možné získať takto:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Ak je hodnota 0, znamená to, že model nezohľadňuje vstupné dáta a správa sa ako *najhorší lineárny prediktor*, čo je jednoducho priemerná hodnota výsledku. Hodnota 1 znamená, že dokážeme dokonale predpovedať všetky očakávané výstupy. V našom prípade je koeficient okolo 0,06, čo je pomerne nízke.

Môžeme tiež zobraziť testovacie dáta spolu s regresnou čiarou, aby sme lepšie videli, ako regresia funguje v našom prípade:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Lineárna regresia" src="../../../../translated_images/sk/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomická regresia

Ďalším typom lineárnej regresie je polynomická regresia. Zatiaľ čo niekedy existuje lineárny vzťah medzi premennými - čím väčšia tekvica objemom, tým vyššia cena - niekedy tieto vzťahy nemožno zobraziť ako rovinu alebo priamku.

✅ Tu sú [niektoré ďalšie príklady](https://online.stat.psu.edu/stat501/lesson/9/9.8) dát, ktoré by mohli využiť polynomickú regresiu

Pozrite sa opäť na vzťah medzi Dátumom a Cenou. Zdá sa, že by tento rozptylový graf mal byť nevyhnutne analyzovaný priamkou? Nemôžu ceny kolísať? V takom prípade môžete skúsiť polynomickú regresiu.

✅ Polynómy sú matematické výrazy, ktoré môžu pozostávať z jednej alebo viacerých premenných a koeficientov

Polynomická regresia vytvára zakrivenú čiaru, aby sa lepšie prispôsobila nelineárnym dátam. V našom prípade, ak zahrnieme do vstupných dát štvorcovú premennú `DayOfYear`, mali by sme byť schopní prispôsobiť naše dáta parabolickou krivkou, ktorá bude mať minimum v určitom bode počas roka.

Scikit-learn obsahuje užitočné [API pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) na spojenie rôznych krokov spracovania dát. **Pipeline** je reťazec **estimatorov**. V našom prípade vytvoríme pipeline, ktorá najprv pridá polynomické príznaky do nášho modelu a potom vytrénuje regresiu:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Použitie `PolynomialFeatures(2)` znamená, že zahrnieme všetky polynómy druhého stupňa z vstupných dát. V našom prípade to bude iba `DayOfYear`<sup>2</sup>, ale ak máme dve vstupné premenné X a Y, pridajú sa X<sup>2</sup>, XY a Y<sup>2</sup>. Môžeme tiež použiť polynómy vyššieho stupňa, ak chceme.

Pipeline môžeme používať rovnako ako pôvodný objekt `LinearRegression`, t.j. môžeme `fit` pipeline a potom použiť `predict` na získanie výsledkov predpovede. Tu je graf zobrazujúci testovacie dáta a aproximačnú krivku:

<img alt="Polynomická regresia" src="../../../../translated_images/sk/poly-results.ee587348f0f1f60b.webp" width="50%" />

Pomocou polynomickej regresie môžeme dosiahnuť mierne nižšiu MSE a vyšší koeficient determinácie, ale nie výrazne. Musíme zohľadniť aj ďalšie vlastnosti!

> Môžete vidieť, že minimálne ceny tekvíc sa vyskytujú niekde okolo Halloween. Ako by ste to vysvetlili? 

🎃 Gratulujeme, práve ste vytvorili model, ktorý môže pomôcť predpovedať cenu tekvíc na pečenie. Pravdepodobne môžete zopakovať rovnaký postup pre všetky druhy tekvíc, ale to by bolo zdĺhavé. Teraz sa naučíme, ako zohľadniť druh tekvice v našom modeli!

## Kategóriové premenné

V ideálnom svete chceme byť schopní predpovedať ceny rôznych druhov tekvíc pomocou toho istého modelu. Avšak stĺpec `Variety` je trochu iný ako stĺpce ako `Month`, pretože obsahuje nečíselné hodnoty. Takéto stĺpce sa nazývajú **kategóriové**.

[![ML pre začiatočníkov - Predikcie kategóriových premenných pomocou lineárnej regresie](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML pre začiatočníkov - Predikcie kategóriových premenných pomocou lineárnej regresie")

> 🎥 Kliknite na obrázok vyššie pre krátke video o použití kategóriových premenných.

Tu vidíte, ako sa priemerná cena líši podľa druhu:

<img alt="Priemerná cena podľa druhu" src="../../../../translated_images/sk/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Aby sme zohľadnili druh, musíme ho najskôr previesť na číselnú formu, teda ho **zakódovať**. Existuje niekoľko spôsobov, ako to môžeme urobiť:

* Jednoduché **číselné kódovanie** vytvorí tabuľku rôznych druhov a potom nahradí názov druhu jeho indexom v tejto tabuľke. Toto nie je najlepšia myšlienka pre lineárnu regresiu, pretože lineárna regresia berie skutočnú číselnú hodnotu indexu a pripočítava ju k výsledku, násobenú nejakým koeficientom. V našom prípade je vzťah medzi číslom indexu a cenou jasne nelineárny, aj keď by sme triedili indexy nejakým špecifickým spôsobom.
* **One-hot encoding** nahradí stĺpec `Variety` štyrmi rôznymi stĺpcami, po jednom pre každú odrodu. Každý stĺpec bude obsahovať `1`, ak príslušný riadok je daného druhu, a `0` inak. To znamená, že budú štyri koeficienty v lineárnej regresii, po jednom pre každú odrodu tekvín, ktoré budú zodpovedné za "počátečnú cenu" (alebo skôr "prídavok k cene") pre tento konkrétny druh.

Nižšie je ukážka, ako môžeme pomocou one-hot encoding označiť druh:

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

Na trénovanie lineárnej regresie používajúcej one-hot kódované druhy ako vstupné premenné je potrebné správne inicializovať dáta `X` a `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Zvyšok kódu je rovnaký ako sme použili vyššie pre trénovanie lineárnej regresie. Ak to vyskúšate, uvidíte, že stredná štvorcová chyba je asi rovnaká, ale koeficient determinácie bude oveľa vyšší (~77%). Na ešte presnejšie predikcie môžeme zohľadniť viac kategóriových premenných, ako aj numerické premenné, napríklad `Month` alebo `DayOfYear`. Na vytvorenie jednej veľkej množiny príznakov môžeme použiť `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Tu tiež zohľadňujeme `City` a typ balenia (`Package`), čo nám dáva MSE 2.84 (10%) a koeficient determinácie 0.94!

## Zhrnutie všetkého dokopy

Aby sme vytvorili najlepší model, môžeme použiť kombinované (one-hot kódované kategóriové + numerické) dáta z vyššie uvedeného príkladu spolu s polynomickou regresiou. Tu je kompletný kód pre vaše pohodlie:

```python
# nastaviť tréningové dáta
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# vykonať rozdelenie na trénovaciu a testovaciu množinu
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# nastaviť a natrénovať pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# predpovedať výsledky pre testovacie dáta
pred = pipeline.predict(X_test)

# vypočítať MSE a koeficient determinácie
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Toto by nám malo dať najlepší koeficient determinácie takmer 97% a MSE=2.23 (~8% chyba predikcie).

| Model | MSE | Koeficient determinácie |
|-------|-----|-------------------------|
| `DayOfYear` lineárny | 2.77 (17.2%) | 0.07 |
| `DayOfYear` polynomický | 2.73 (17.0%) | 0.08 |
| `Variety` lineárny | 5.24 (19.7%) | 0.77 |
| Všetky príznaky lineárny | 2.84 (10.5%) | 0.94 |
| Všetky príznaky polynomický | 2.23 (8.25%) | 0.97 |

🏆 Výborne! Vytvorili ste štyri regresné modely v jednej lekcii a zlepšili kvalitu modelu na 97%. V poslednej časti o regresii sa naučíte o logistickej regresii na určovanie kategórií.

---
## 🚀Výzva

Otestujte niekoľko rôznych premenných v tomto notebooku a zistite, ako korelácia súvisí s presnosťou modelu.

## [Kvíz po prednáške](https://ff-quizzes.netlify.app/en/ml/)

## Opakovanie a samostatné štúdium

V tejto lekcii sme sa naučili o lineárnej regresii. Existujú aj iné dôležité typy regresie. Prečítajte si o metódach Stepwise, Ridge, Lasso a Elasticnet. Dobrou študijnou pomôckou na osvojenie je kurz [Stanford Statistical Learning](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Zadanie

[Postavte model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Zrieknutie sa zodpovednosti**:
Tento dokument bol preložený pomocou AI prekladateľskej služby [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, vezmite prosím na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne výklady vyplývajúce z použitia tohto prekladu.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->