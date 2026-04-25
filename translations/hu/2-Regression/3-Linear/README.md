# Regressziós modell építése Scikit-learn segítségével: regresszió négyféle módon

## Kezdő jegyzet

A lineáris regressziót akkor használjuk, amikor egy **numerikus értéket** szeretnénk előre jelezni (például ház árát, hőmérsékletet vagy eladásokat).  
Az a működése, hogy megkeresi azt a legjobb egyenest, amely bemeneti jellemzők és a kimenet közötti kapcsolatot leginkább reprezentálja.

Ebben a leckében a koncepció megértésére fókuszálunk, mielőtt fejlettebb regressziós technikákba merülnénk.  
![Lineáris vs polinomiális regresszió infografika](../../../../translated_images/hu/linear-polynomial.5523c7cb6576ccab.webp)  
> Infografika készítője: [Dasani Madipalli](https://twitter.com/dasani_decoded)

## [Előadás előtti kvíz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Ez a lecke elérhető R-ben is!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)

### Bevezetés

Eddig megvizsgáltad, hogy mi az a regresszió, mint fogalom, mintapéldákon keresztül a sütőtök árképzési adatkészletéből, amelyet a leckén át használni fogunk. Vizualizáltad is az adatokat Matplotlib segítségével.

Most készen állsz, hogy mélyebbre áss a gépi tanulás regressziós modelljeiben. Míg a vizualizáció segít az adatok értelmezésében, a gépi tanulás valódi ereje az _modellek betanításából_ ered. A modelleket történelmi adatokra tanítjuk, hogy automatikusan megragadják az adatok közötti összefüggéseket, és lehetővé tegyék, hogy előrejelzéseket készítsenek új, korábban nem látott adatokról.

Ebben a leckében két regressziótípusról tanulsz: az _alap lineáris regresszióról_ és a _polinomiális regresszióról_, illetve ezek mögött álló matematikáról. Ezek a modellek lehetővé teszik, hogy előre jelezzük a sütőtök árakat a különböző bemeneti adatok alapján.

[![Gépi tanulás kezdőknek – A lineáris regresszió megértése](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "Gépi tanulás kezdőknek – A lineáris regresszió megértése")

> 🎥 Kattints a fenti képre egy rövid videós áttekintésért a lineáris regresszióról.

> Az egész tananyag során minimális matematikai előismeretet feltételezünk, és más területekről érkező hallgatók számára is érthetővé tesszük, ezért figyelj a jegyzetekre, 🧮 hívásokra, diagramokra és más tanulást segítő eszközökre.

### Előfeltétel

Már ismerned kell a sütőtök adatstruktúráját, amelyet vizsgálunk. Ezt megtalálod előbetöltve és előtisztítva a leckéhez tartozó _notebook.ipynb_ fájlban. Ebben a fájlban a sütőtök árát bushelenként jelenítjük meg egy új adatkeretben. Győződj meg róla, hogy futtatni tudod ezeket a notebookokat a Visual Studio Code kerneljeiben.

### Előkészítés

Emlékeztetőül, az adatokat azért töltöd be, hogy kérdéseket tehess fel velük kapcsolatban.

- Mikor a legjobb idő sütőtököt vásárolni?  
- Milyen árat várhatok egy kisebb sütőtökös dobozra?  
- Érdemes fél busheles kosárban vagy 1 1/9 busheles dobozban vásárolni?

Folytassuk az adatok vizsgálatát.

Az előző leckében létrehoztál egy Pandas adatkeretet és feltöltötted azt az eredeti adatkészlet egy részével, szabványosítva az árakat bushel alapján. Ez azonban csak kb. 400 adatpontot eredményezett, és csak az őszi hónapokra.

Nézd meg a leckéhez tartozó előre betöltött adatokat és az első szórásdiagramot a hónapok megjelenítésére. Talán részletesebben megérthetjük az adat természettét, ha jobban megtisztítjuk azt.

## Egy lineáris regressziós egyenes

Amint az 1. leckében tanultad, egy lineáris regressziós gyakorlat célja, hogy egy egyenest tudjunk ábrázolni, amely:

- **Változók közötti kapcsolatot mutat.** Bemutatja a változók közötti összefüggést  
- **Előrejelzést tesz lehetővé.** Pontosan megjósolja, hol esik egy új adatpont az egyeneshez képest.

Tipikusan a **legkisebb négyzetes regresszió** rajzol ilyen egyenest. A "legkisebb négyzetes" kifejezés arra utal, hogy minimalizáljuk a modell összes hibáját. Minden adatok ponthoz lemérjük a vertikális távolságot (reziduális), azaz a tényleges pont és az egyenes közötti függőleges távolságot.

Ezeket a távolságokat négyzetre emeljük két fő okból:

1. **Nagyság irány helyett:** Az -5 hibát ugyanúgy kezeljük, mint a +5 hibát, mert a négyzetre emelés minden értéket pozitívvá tesz.

2. **Kiemelt büntetés a kiugró értékeknek:** A négyzetre emelés nagyobb súlyt ad a nagyobb hibáknak, így az egyenes közelebbi marad a távolabbi pontokhoz.

Ezek után összeadjuk az összes négyzetre emelt távolságot. Célunk, hogy megtaláljuk azt az egyenest, amelynél ez az összeg a legkisebb (legkisebb érték) — innen a név: "legkisebb négyzetes".

> **🧮 Mutasd a matematikát**  
>  
> Ezt az egyenest, amit _legjobb illeszkedő egyenesnek_ nevezünk, a [következő egyenlettel](https://en.wikipedia.org/wiki/Simple_linear_regression) kifejezhetjük:  
>  
> ```
> Y = a + bX
> ```
>  
> `X` az 'magyarázó változó', `Y` a 'függő változó'. Az egyenes meredeksége `b`, az `a` az y-tengely metszéspontja, vagyis az `Y` értéke, amikor `X = 0`.  
>  
>![meredekség kiszámítása](../../../../translated_images/hu/slope.f3c9d5910ddbfcf9.webp)  
>  
> Először számítsd ki a `b` meredekséget. Infografika készítője: [Jen Looper](https://twitter.com/jenlooper)  
>  
> Más szóval, a sütőtök adataink eredeti kérdése alapján: "előre jelezzük a sütőtök árát bushelre vetítve hónap szerint", itt az `X` az árra, az `Y` az eladási hónapra utalna.  
>  
>![egyenlet kiegészítése](../../../../translated_images/hu/calculation.a209813050a1ddb1.webp)  
>  
> Számítsd ki az Y értékét. Ha kb. 4 dollárt fizetsz, az bizonyára április! Infografika készítője: [Jen Looper](https://twitter.com/jenlooper)  
>  
> Az egyenes számításánál a meredekséget mutatja a formula, amely az y-metszési értéken is múlik, vagyis hol helyezkedik el az `Y`, amikor `X = 0`.  
>  
> A számítási módszert megtekintheted a [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) weboldalon. Használd a [Legkisebb négyzetek kalkulátort](https://www.mathsisfun.com/data/least-squares-calculator.html) is, hogy lásd, hogyan befolyásolják a számok az egyenest.

## Korreláció

Az utolsó fontos fogalom, amit érdemes megérteni, az adott X és Y változók közötti **korrelációs együttható**. A szórásdiagram segítségével ezt gyorsan meg tudjuk jeleníteni. Ha a pontok rendezett vonal mentén helyezkednek el, magas korrelációról beszélhetünk, míg ha szétszórtak mindenhol az X és Y között, akkor alacsony korrelációról beszélünk.

Egy jó lineáris regressziós modell magas (közelebb 1-hez, mint 0-hoz) korrelációs együtthatóval rendelkezik, a Legkisebb Négyzetes Regresszió módszerével és regressziós egyenessel.

✅ Futtasd a leckéhez mellékelt jegyzetet, és nézd meg a Hónap és Ár szórásdiagramját. A süvőtökeladások hónap és ár közötti adatai szerinted magas vagy alacsony korrelációt mutatnak a diagram vizuális értelmezése alapján? Változik ez, ha a `Month` helyett finomabb időmérő mértéket használunk, pl. *az év napja* (az év eleje óta eltelt napok száma)?

Az alábbi kódban feltételezzük, hogy megtisztítottuk az adatokat, és egy `new_pumpkins` nevű adatkeretet kaptunk, amely hasonló az alábbihoz:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  

> Az adatok tisztítására vonatkozó kód a [`notebook.ipynb`](notebook.ipynb) fájlban található. Ugyanazokat a tisztítási lépéseket hajtottuk végre, mint az előző leckében, és a `DayOfYear` oszlopot a következő kifejezés segítségével számoltuk ki:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Most, hogy megértetted a lineáris regresszió mögötti matematikát, hozzunk létre egy regressziós modellt, hogy megnézzük, tudjuk-e megjósolni, melyik sütőtökcsomagnak lesz a legjobb ára. Valaki, aki egy ünnepi sütőtöksátorba vásárol, biztosan szeretné ezt az információt, hogy optimalizálhassa vásárlásait.

## Korreláció keresése

[![Gépi tanulás kezdőknek – Korreláció keresése: a lineáris regresszió kulcsa](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "Gépi tanulás kezdőknek – Korreláció keresése: a lineáris regresszió kulcsa")

> 🎥 Kattints a fenti képre egy rövid videós áttekintésért a korrelációról.

Az előző leckéből valószínűleg láttad, hogy az átlagárak hónaponként így néznek ki:

<img alt="Átlagár hónaponként" src="../../../../translated_images/hu/barchart.a833ea9194346d76.webp" width="50%"/>

Ez arra utal, hogy van valamilyen korreláció, és megpróbálhatunk egy lineáris regressziós modellt tanítani, amely előrejelzi a `Month` és `Price`, vagy a `DayOfYear` és `Price` közötti kapcsolatot. Az alábbi szórásdiagram az utóbbi kapcsolatot mutatja be:

<img alt="Ár szórásdiagram az év napja szerint" src="../../../../translated_images/hu/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Nézzük meg, van-e korreláció a `corr` függvénnyel:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Úgy tűnik, hogy a korreláció meglehetősen kicsi, -0,15 a `Month`, és -0,17 a `DayOfMonth` szerint, de lehet egy másik fontos összefüggés. Úgy tűnik, hogy különböző árklaszterek vannak a sütőtök fajták szerint. Ennek megerősítésére ábrázoljuk az egyes sütőtökkategóriákat más-más színnel. Az `ax` paraméter átadásával a `scatter` függvénynek az összes pont ugyanabban a grafikonban jelenik meg:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Ár szórásdiagram az év napja szerint, színesen" src="../../../../translated_images/hu/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Vizsgálatunk azt sugallja, hogy a fajta nagyobb hatással van a teljes árra, mint az eladási időpont. Ezt egy oszlopdiagramon is láthatjuk:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Ár oszlopdiagram fajta szerint" src="../../../../translated_images/hu/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Most csak egy sütőtökfajtára, a 'pie type'-ra (pite típusra) koncentrálunk, és megnézzük, milyen hatása van az eladási dátumnak az árra:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
  
<img alt="Ár szórásdiagram az év napja szerint, pite típus" src="../../../../translated_images/hu/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Ha most kiszámoljuk a korrelációt a `Price` és a `DayOfYear` között a `corr` függvénnyel, valami ilyesmit kapunk: `-0.27` - ami azt jelenti, hogy érdemes predikciós modellt tanítani.

> Egy lineáris regressziós modell betanítása előtt fontos, hogy az adataink tiszták legyenek. Mivel a lineáris regresszió nem működik jól hiányzó értékekkel, ezért érdemes eltávolítani az összes üres cellát:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
Egy másik megközelítés lehet, hogy az üres értékeket az adott oszlop átlagával töltjük fel.

## Egyszerű lineáris regresszió

[![Gépi tanulás kezdőknek – Lineáris és polinomiális regresszió Scikit-learn használatával](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "Gépi tanulás kezdőknek – Lineáris és polinomiális regresszió Scikit-learn használatával")

> 🎥 Kattints a fenti képre egy rövid videós áttekintésért a lineáris és polinomiális regresszióról.

A lineáris regressziós modellünk betanításához a **Scikit-learn** könyvtárat fogjuk használni.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
Először szétválasztjuk a bemeneti értékeket (jellemzők) és a várt kimenetet (címkét) külön numpy tömbökbe:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Figyeld meg, hogy a bemeneti adaton `reshape` műveletet kellett végeznünk, hogy a Linear Regression csomag helyesen értelmezze azt. A lineáris regresszió 2D tömböt vár bemenetként, ahol a tömb minden sora egy bemeneti jellemzővektort képvisel. Mivel esetünkben csak egy bemenet van, N×1 alakú tömböt kell biztosítanunk, ahol N az adatkészlet mérete.

Ezután az adatokat szét kell osztani tanuló (train) és teszt (test) adathalmazra, hogy a modell betanítása után ellenőrizni tudjuk azt:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
Végül, a lineáris regressziós modell tényleges betanítása csak két kód sor. Definiáljuk a `LinearRegression` objektumot, és megtanítjuk az adatokra a `fit` metódussal:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

A `LinearRegression` objektum a `fit`-elés után tartalmazza az összes regressziós együtthatót, amelyek a `.coef_` tulajdonsággal érhetők el. Esetünkben csak egyetlen együttható van, amely nagyjából `-0.017` körül kell, hogy legyen. Ez azt jelenti, hogy az árak idővel kissé csökkennek, de nem túl sokat, körülbelül napi 2 centtel. A regresszió Y-tengellyel való metszéspontját a `lin_reg.intercept_`-tel érhetjük el – nálunk ez kb. `21` lesz, ami az év eleji árat jelzi.

Annak megmutatására, hogy a modellünk mennyire pontos, megjósolhatjuk az árakat egy teszt adathalmazon, majd mérhetjük, mennyire közel vannak az előrejelzéseink a várt értékekhez. Ez az átlagos négyzetes hiba négyzetgyökével (RMSE - root mean square error) tehető meg, ami az összes négyzetes különbség átlaga és gyöke.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Az általunk kapott hiba körülbelül 2 pont, ami ~17%. Nem túl jó. A modell minőségének másik mutatója a **determinációs együttható**, amely így szerezhető meg:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```

Ha az érték 0, az azt jelenti, hogy a modell nem veszi figyelembe a bemeneti adatokat, és egy *legrosszabb lineáris prediktorként* működik, ami egyszerűen az eredmény átlagértéke. Az 1-es érték azt jelenti, hogy tökéletesen meg tudjuk jósolni az összes elvárt kimenetet. Nálunk a koefficiens körülbelül 0,06, ami elég alacsony.

A tesztadatokat is ábrázolhatjuk a regressziós egyenessel együtt, hogy jobban lássuk a regresszió működését a mi esetünkben:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/hu/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polinomiális regresszió

A lineáris regresszió másik típusa a polinomiális regresszió. Bár néha lineáris kapcsolat van a változók között – minél nagyobb a tök térfogata, annál magasabb az ár –, előfordul, hogy ezeket a kapcsolatokat nem lehet egy síkkal vagy egyenes vonallal ábrázolni.

✅ Itt van néhány [további példa](https://online.stat.psu.edu/stat501/lesson/9/9.8) adatokról, amelyekhez polinomiális regressziót lehet használni.

Nézzük meg újra a Date és Price kapcsolatát. Ez a szórt diagram feltétlenül úgy néz ki, hogy egyenes vonallal kellene elemezni? Nem ingadozhatnak-e az árak? Ebben az esetben érdemes kipróbálni a polinomiális regressziót.

✅ A polinomok olyan matematikai kifejezések, amelyek egy vagy több változóból és együtthatóból állhatnak.

A polinomiális regresszió egy görbült vonalat hoz létre, hogy jobban illeszkedjen nemlineáris adatokra. A mi esetünkben, ha bevonjuk a négyzetes `DayOfYear` változót a bemeneti adatok közé, képesek leszünk az adatokat egy parabolikus görbével illeszteni, amelynek minimuma egy adott pontban lesz az éven belül.

A Scikit-learn tartalmaz egy hasznos [pipeline API-t](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline), amely lehetővé teszi a különböző adatfeldolgozási lépések együttes használatát. Egy **pipeline** egy **becslők** láncolata. A mi esetünkben olyan pipeline-t hozunk létre, amely először polinomiális jellemzőket ad a modellhez, majd betanítja a regressziót:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

A `PolynomialFeatures(2)` használata azt jelenti, hogy a bemeneti adatokból az összes másodfokú polinomot bevonjuk. Esetünkben ez csak a `DayOfYear`<sup>2</sup> változót jelenti, de ha két bemeneti változó X és Y, akkor hozzáadja az X<sup>2</sup>, XY és Y<sup>2</sup> kifejezéseket is. Magasabb fokú polinomokat is használhatunk, ha akarunk.

A pipeline-okat ugyanúgy használhatjuk, mint az eredeti `LinearRegression` objektumot, azaz `fit`-elhetjük a pipeline-t, majd `predict`-tel lekérhetjük az előrejelzéseket. Íme egy grafikon, amely a tesztadatokat és az illesztett görbét mutatja:

<img alt="Polynomial regression" src="../../../../translated_images/hu/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polinomiális regresszióval kicsit alacsonyabb MSE és magasabb determináció érhető el, de nem jelentősen. Más jellemzőket is figyelembe kell vennünk!

> Látható, hogy a tök árak legalacsonyabbak valahol Halloween körül. Hogyan magyarázhatod ezt? 

🎃 Gratulálok, most hoztál létre egy modellt, ami segíthet előre jelezni a sütőtök árát. Valószínűleg ugyanezt a módszert megismételheted az összes tökfajtánál, de az egy kicsit fárasztó lenne. Most tanuljuk meg, hogyan vegyük figyelembe a tökfajta különbségeket a modellben!

## Kategóriás jellemzők

Az ideális világban képesek vagyunk ugyanazt a modellt használni különböző tökfajták árának előrejelzésére. A `Variety` oszlop azonban némileg eltér a `Month`-től, mert nem numerikus értékeket tartalmaz. Az ilyen oszlopokat **kategóriásnak** nevezzük.

[![ML for beginners - Kategóriás jellemzők előrejelzése lineáris regresszióval](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Kategóriás jellemzők előrejelzése lineáris regresszióval")

> 🎥 Kattints a fenti képre egy rövid videós bemutatóért kategóriás jellemzők használatáról.

Itt látható, hogyan függ az átlagár a fajtától:

<img alt="Átlagár fajta szerint" src="../../../../translated_images/hu/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

A fajta figyelembevételéhez először számmá kell alakítanunk, vagyis **kódolnunk** kell. Többféle módon megtehetjük ezt:

* Egyszerű **numerikus kódolás** egy táblázatot épít az eltérő fajtákról, majd a fajta nevét egy indexre cseréli ebben a táblázatban. Ez nem a legjobb ötlet lineáris regresszióhoz, mert a lineáris regresszió az index tényleges numerikus értékét veszi figyelembe, amit egy együtthatóval megszoroz, majd hozzáad az eredményhez. Nálunk az indexszám és az ár közötti kapcsolat jól láthatóan nemlineáris, még akkor sem, ha az indexeket valamilyen specifikus sorrendbe rendezzük.
* **One-hot kódolás** a `Variety` oszlopot 4 külön oszlopra bontja, egy-egy minden fajtához. Mindegyik oszlopban `1` lesz, ha az adott sor a szóban forgó fajta, és `0` egyébként. Ez azt jelenti, hogy négy regressziós együtthatónk lesz, egyenként minden tökfajta esetében, amelyek az adott fajta "kezdő ára" (vagy inkább "kiegészítő ára") felelnek.

Az alábbi kód megmutatja, hogyan lehet one-hot kódolni a fajtát:

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

A lineáris regresszió tanításához one-hot kódolt fajtára egyszerűen csak helyesen kell inicializálni az `X` és `y` adatokat:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

A kód többi része ugyanaz, mint amit fent használtunk a lineáris regresszió tanításához. Ha kipróbálod, látni fogod, hogy az átlagos négyzetes hiba nagyjából ugyanaz marad, de a determinációs együttható sokkal magasabb lesz (~77%). Az még pontosabb előrejelzésekhez több kategóriás jellemzőt és egyben numerikus jellemzőket is figyelembe vehetünk, például `Month` vagy `DayOfYear`. Az összes jellemzőt egy nagy tömbbe egyesíthetjük a `join` segítségével:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Itt szintén figyelembe vesszük a `City` és a `Package` típust, melyeknek az eredménye 2.84 MSE (10%) és 0.94 determináció!

## Összefoglalás

A legjobb modell készítéséhez kombinált (one-hot kódolt kategóriás + numerikus) adatokat használhatunk a fenti példából, együtt a polinomiális regresszióval. Íme az egész kód az egyszerűség kedvéért:

```python
# beállítja a tanító adatokat
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# készít egy tanító-teszt felosztást
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# beállítja és tanítja a folyamatot
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# megjósolja az eredményeket a teszt adatokra
pred = pipeline.predict(X_test)

# kiszámítja az MSE-t és a determinációt
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Ez az eredmény majdnem 97%-os determinációs együtthatót, és MSE=2.23-at (~8% előrejelzési hibát) ad.

| Modell | MSE | Determináció |
|-------|-----|---------------|
| `DayOfYear` lineáris | 2.77 (17.2%) | 0.07 |
| `DayOfYear` polinomiális | 2.73 (17.0%) | 0.08 |
| `Variety` lineáris | 5.24 (19.7%) | 0.77 |
| Minden jellemző lineáris | 2.84 (10.5%) | 0.94 |
| Minden jellemző polinomiális | 2.23 (8.25%) | 0.97 |

🏆 Szép munka! Egy órán belül négy regressziós modellt hoztál létre, és a modell minőségét 97%-ra javítottad. A regresszió záró részében a logisztikus regresszióról fogsz tanulni, ami kategóriák meghatározására szolgál.

---
## 🚀Kihívás

Tesztelj több különböző változót ebben a jegyzetfüzetben, hogy lásd, hogyan függ a korreláció a modell pontosságától.

## [Előadás utáni kvíz](https://ff-quizzes.netlify.app/en/ml/)

## Áttekintés & Önálló tanulás

Ebben a leckében a lineáris regressziót tanultuk meg. Vannak más fontos regressziós típusok is. Olvass a lépésenkénti, Ridge, Lasso és Elasticnet technikákról. Egy jó tanfolyam további tanulásra a [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning).

## Feladat

[Modellezés](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Felmentés**:
Ez a dokumentum az [Co-op Translator](https://github.com/Azure/co-op-translator) AI fordító szolgáltatásával készült. Bár az pontosságra törekszünk, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum anyanyelvű változata tekinthető hivatalos forrásnak. Fontos információk esetén szakmai emberi fordítást javasolunk. Nem vállalunk felelősséget a fordítás használatából eredő félreértésekért vagy félreértelmezésekért.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->