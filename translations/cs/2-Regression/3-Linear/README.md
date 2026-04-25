# Vytvoření regresního modelu pomocí Scikit-learn: regrese čtyřmi způsoby

## Poznámka pro začátečníky

Lineární regrese se používá tehdy, když chceme predikovat **číselnou hodnotu** (například cenu domu, teplotu nebo tržby).
Funguje tak, že najde přímku, která nejlépe reprezentuje vztah mezi vstupními vlastnostmi a výstupem.

V této lekci se zaměříme na pochopení konceptu, než přejdeme k pokročilejším regresním technikám.
![Lineární vs polynomiální regrese infographic](../../../../translated_images/cs/linear-polynomial.5523c7cb6576ccab.webp)
> Infografika od [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Přednáškový kvíz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Tato lekce je dostupná i v R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Úvod

Dosud jste prozkoumali, co regrese je, s použitím ukázkových dat získaných z datasetu s cenami dýní, který budeme používat v celé této lekci. Také jste data vizualizovali pomocí Matplotlib.

Nyní jste připraveni ponořit se hlouběji do regrese pro strojové učení. Zatímco vizualizace vám umožňuje data lépe pochopit, skutečná síla strojového učení spočívá ve _tréninku modelů_. Modely jsou trénovány na historických datech, aby automaticky zachytily závislosti v datech a umožnily vám predikovat výsledky pro nová data, která model ještě neviděl.

V této lekci se dozvíte více o dvou typech regrese: _základní lineární regresi_ a _polynomiální regresi_, spolu s některou z matematiky, která tyto techniky podkládá. Tyto modely nám umožní predikovat ceny dýní podle různých vstupních dat.

[![Strojové učení pro začátečníky - Pochopení lineární regrese](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "Strojové učení pro začátečníky - Pochopení lineární regrese")

> 🎥 Klikněte na obrázek výše pro krátké video shrnutí lineární regrese.

> V celém tomto kurikulu předpokládáme minimální znalosti matematiky a snažíme se ji zpřístupnit studentům z jiných oborů, proto sledujte poznámky, 🧮 doplňky, diagramy a další výukové pomůcky pro usnadnění pochopení.

### Předpoklady

Nyní byste měli být obeznámeni se strukturou dat o dýních, která zkoumáme. Najdete je přednačtená a předčištěná v souboru _notebook.ipynb_ této lekce. V souboru je cena dýně zobrazena za koš (bushel) v novém datovém rámci. Ujistěte se, že tyto notebooky můžete spustit v jádrech ve Visual Studio Code.

### Příprava

Jako připomínku, tato data načítáte proto, abyste na ně mohli klást otázky.

- Kdy je nejlepší doba na nákup dýní?
- Jakou cenu mohu očekávat za balení mini dýní?
- Měl bych je koupit v koších o půl bushelu, nebo v krabici o 1 1/9 bushelu?

Pojďme dále prozkoumat tato data.

V předchozí lekci jste vytvořili Pandas data frame a naplnili ho částí původního datasetu, standardizovali ceny na bushel. Tím jste však získali asi 400 datových bodů, a to pouze pro podzimní měsíce.

Podívejte se na data, která jsme přednačetli v notebooku doprovázejícím tuto lekci. Data jsou přednačtená a zobrazený je počáteční scatterplot dle měsíce. Možná získáme více podrobností o povaze dat jejich důkladnějším vyčištěním.

## Lineární regresní přímka

Jak jste se naučili v lekci 1, cílem cvičení lineární regrese je umět nakreslit přímku, která:

- **Ukáže vztahy mezi proměnnými**.
- **Umožní predikce**. Přesně predikovat, kde by se nový datový bod nacházel vzhledem k této přímce.

Typickým přístupem u **regrese nejmenších čtverců** (Least-Squares Regression) je nakreslit právě tento typ přímky. Termín "nejmenších čtverců" odkazuje na proces minimalizace celkové chyby v našem modelu. Pro každý datový bod měříme vertikální vzdálenost (zvanou reziduum) mezi skutečným bodem a naší regresní přímkou.

Tyto vzdálenosti umocníme na druhou ze dvou hlavních důvodů:

1. **Velikost nad směrem:** Chceme, aby chyba -5 byla považována za stejnou jako chyba +5. Umocněním získáme všechny hodnoty kladné.

2. **Trestat odlehlé hodnoty:** Umocnění dá větší váhu větším chybám, díky čemuž se přímka snaží zůstat blíže k bodům, které jsou vzdálené.

Poté všechny tyto umocněné hodnoty sečteme. Naším cílem je najít právě tu přímku, kde je tento součet nejmenší (možná nejmenší hodnota) — odtud název "nejmenších čtverců".

> **🧮 Ukázat mi matematiku**  
>  
> Tuto přímku, nazývanou _přímka nejlepšího přizpůsobení_, lze vyjádřit [rovnicí](https://cs.wikipedia.org/wiki/Line%C3%A1rn%C3%AD_regrese#Jednoduch%C3%A1_line%C3%A1rn%C3%AD_regrese): 
> 
> ```
> Y = a + bX
> ```
>
> `X` je 'vysvětlující proměnná'. `Y` je 'závislá proměnná'. Směrnice přímky je `b` a `a` je průsečík s osou y, který odpovídá hodnotě `Y` když `X = 0`.
>
>![výpočet směrnice](../../../../translated_images/cs/slope.f3c9d5910ddbfcf9.webp)
>
> Nejprve spočítejte směrnici `b`. Infografika od [Jen Looper](https://twitter.com/jenlooper)
>
> Jinými slovy, a s ohledem na původní otázku k našim datům o dýních: "predikujte cenu dýně za bushel podle měsíce", pak `X` představuje cenu a `Y` měsíc prodeje.
>
>![doplnění rovnice](../../../../translated_images/cs/calculation.a209813050a1ddb1.webp)
>
> Spočítejte hodnotu `Y`. Pokud platíte kolem 4 dolarů, musí být duben! Infografika od [Jen Looper](https://twitter.com/jenlooper)
>
> Matematika, která vypočítá přímku, musí zohlednit směrnici této přímky, která také závisí na průsečíku, tedy místě, kde je `Y`, když `X = 0`.
>
> Metodu výpočtu těchto hodnot můžete sledovat na webu [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Navštivte také [tento kalkulátor nejmenších čtverců](https://www.mathsisfun.com/data/least-squares-calculator.html), který ukazuje, jak hodnoty čísel ovlivňují přímku.

## Korelace

Ještě jeden termín, který je dobré pochopit, je **korelační koeficient** mezi proměnnými X a Y. Pomocí scatterplotu můžete rychle tento koeficient vizualizovat. Graf s body roztroušenými v pěkné přímce má vysokou korelaci, zatímco graf s body rozesetými všude má nízkou korelaci.

Dobrý lineární regresní model bude ten, který má vysoký (blíže jedné než nule) korelační koeficient pomocí metody nejmenších čtverců.

✅ Spusťte notebook doprovázející tuto lekci a podívejte se na scatterplot měsíce vs. ceny. Zdá se, že data spojující měsíc s cenou při prodeji dýní mají vysokou nebo nízkou korelaci podle vaší vizuální interpretace scatterplotu? Změní se to, pokud použijete jemnější měřítko než `Month`, např. *den v roce* (tj. počet dní od začátku roku)?

V níže uvedeném kódu budeme předpokládat, že jsme data vyčistili a získali datový rámec nazvaný `new_pumpkins`, podobný tomuto:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Kód na čištění dat je k dispozici v [`notebook.ipynb`](notebook.ipynb). Provedli jsme stejné kroky čištění jako v předchozí lekci a vypočítali sloupec `DayOfYear` pomocí následujícího výrazu: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Nyní, když máte pochopení matematiky za lineární regresí, vytvoříme regresní model, abychom zjistili, jestli dokážeme předpovědět, které balení dýní bude mít nejlepší cenu. Někdo, kdo kupuje dýně pro záhony na svátky, by tuto informaci mohl chtít, aby mohl optimalizovat nákupy.

## Hledání korelace

[![Strojové učení pro začátečníky - Hledání korelace: Klíč k lineární regresi](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "Strojové učení pro začátečníky - Hledání korelace: Klíč k lineární regresi")

> 🎥 Klikněte na obrázek výše pro krátké video shrnutí korelace.

Z předchozí lekce jste pravděpodobně viděli, že průměrná cena v různých měsících vypadá takto:

<img alt="Průměrná cena podle měsíce" src="../../../../translated_images/cs/barchart.a833ea9194346d76.webp" width="50%"/>

To naznačuje, že existuje nějaká korelace a můžeme zkusit vytrénovat lineární regresní model k předpovědi vztahu mezi `Month` a `Price`, nebo mezi `DayOfYear` a `Price`. Zde je scatter plot ukazující druhý vztah:

<img alt="Scatter plot Price vs. Day of Year" src="../../../../translated_images/cs/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Podívejme se, jestli existuje korelace pomocí funkce `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Zdá se, že korelace je poměrně malá, -0.15 podle `Month` a -0.17 podle `DayOfMonth`, ale může být ještě nějaký důležitý vztah. Zdá se, že existují různé shluky cen odpovídající různým odrůdám dýní. Abychom tuto hypotézu potvrdili, vykreslíme každou kategorii dýní jinou barvou. Předáním parametru `ax` do funkce `scatter` můžeme všechny body vykreslit do stejného grafu:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot Price vs. Day of Year color" src="../../../../translated_images/cs/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Naše vyšetřování naznačuje, že odrůda má větší vliv na celkovou cenu než skutečné datum prodeje. Vidíme to na sloupcovém diagramu:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Sloupcový graf cena podle odrůdy" src="../../../../translated_images/cs/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Zaměříme se nyní pouze na jednu odrůdu dýní, 'pie type', a podíváme se, jaký vliv má datum na cenu:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot Price vs. Day of Year" src="../../../../translated_images/cs/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Pokud nyní spočítáme korelaci mezi `Price` a `DayOfYear` pomocí funkce `corr`, dostaneme hodnotu cca `-0.27` - což znamená, že má smysl trénovat prediktivní model.

> Než začnete trénovat lineární regresní model, je důležité zajistit, že naše data jsou čistá. Lineární regrese nefunguje dobře s chybějícími hodnotami, proto je rozumné odstranit všechny prázdné buňky:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Jiný přístup by byl tyto prázdné hodnoty vyplnit průměrnými hodnotami z příslušného sloupce.

## Jednoduchá lineární regrese

[![Strojové učení pro začátečníky - Lineární a polynomiální regrese pomocí Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "Strojové učení pro začátečníky - Lineární a polynomiální regrese pomocí Scikit-learn")

> 🎥 Klikněte na obrázek výše pro krátké video shrnutí lineární a polynomiální regrese.

Pro trénink našeho modelu lineární regrese použijeme knihovnu **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Začneme oddělením vstupních hodnot (vlastností) a očekávaného výstupu (štítku) do samostatných numpy polí:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Všimněte si, že jsme museli provést `reshape` vstupních dat, aby je balíček lineární regrese správně pochopil. Lineární regrese očekává jako vstup 2D pole, kde každý řádek pole odpovídá vektoru vstupních vlastností. V našem případě, protože máme jen jeden vstup, potřebujeme pole s rozměrem N×1, kde N je velikost datasetu.

Poté musíme data rozdělit na trénovací a testovací sady, abychom mohli ověřit náš model po tréninku:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Nakonec trénink samotného modelu lineární regrese zabere jen dva řádky kódu. Definujeme objekt `LinearRegression` a přizpůsobíme ho našim datům pomocí metody `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objekt `LinearRegression` po `fit`-ování obsahuje všechny koeficienty regrese, ke kterým lze přistupovat pomocí vlastnosti `.coef_`. V našem případě je zde pouze jeden koeficient, který by měl být kolem `-0.017`. To znamená, že se ceny s časem zdají mírně snižovat, ale ne příliš, asi o 2 centy za den. K průsečíku regrese s osou Y můžeme přistoupit pomocí `lin_reg.intercept_` - v našem případě bude kolem `21`, což znamená cenu na začátku roku.

Abychom zjistili, jak přesný náš model je, můžeme předpovídat ceny na testovacím datasetu a poté změřit, jak blízko jsou naše předpovědi očekávaným hodnotám. To lze provést pomocí metriky root mean square error (RMSE), což je odmocnina průměru všech čtverců rozdílů mezi očekávanou a předpovězenou hodnotou.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Naše chyba se zdá být kolem 2 bodů, což je přibližně 17 %. Ne příliš dobré. Dalším ukazatelem kvality modelu je **koeficient determinace**, který lze získat takto:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Pokud je hodnota 0, znamená to, že model nebere vstupní data v úvahu a funguje jako *nejhorší lineární prediktor*, kterým je jednoduše průměrná hodnota výsledku. Hodnota 1 znamená, že můžeme dokonale předpovědět všechny očekávané výstupy. V našem případě je koeficient kolem 0,06, což je celkem nízké.

Můžeme také nakreslit testovací data spolu s regresní přímkou, abychom lépe viděli, jak regrese v našem případě funguje:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Lineární regrese" src="../../../../translated_images/cs/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomická regrese

Dalším typem Lineární regrese je Polynomická regrese. Zatímco někdy existuje lineární vztah mezi proměnnými - čím větší objem dýně, tím vyšší cena - někdy tyto vztahy nelze vykreslit jako rovinu nebo přímku.

✅ Zde jsou [některé další příklady](https://online.stat.psu.edu/stat501/lesson/9/9.8) dat, která by mohla využít Polynomickou regresi

Podívejte se znovu na vztah mezi Datem a Cenou. Zdá se, že tento scatterplot by nutně měl být analyzován pomocí přímky? Nemohou ceny kolísat? V takovém případě můžete zkusit polynomickou regresi.

✅ Polynomické výrazy jsou matematické výrazy, které mohou sestávat z jedné nebo více proměnných a koeficientů.

Polynomická regrese vytváří zakřivenou čáru, aby lépe seděla na nelineární data. V našem případě, pokud do vstupních dat zahrneme druhou mocninu proměnné `DayOfYear`, měli bychom být schopni fitovat naše data parabolickou křivkou, která bude mít minimum v určitém bodě během roku.

Knihovna Scikit-learn obsahuje užitečné [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) pro spojení různých kroků zpracování dat. **Pipeline** je řetězec **estimatorů**. V našem případě vytvoříme pipeline, která nejprve přidá polynomické funkce k našemu modelu a pak provede trénování regrese:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Použití `PolynomialFeatures(2)` znamená, že zahrneme všechny druhé mocniny polynomů z vstupních dat. V našem případě to bude jen `DayOfYear`<sup>2</sup>, ale pokud máme dvě vstupní proměnné X a Y, přidá to X<sup>2</sup>, XY a Y<sup>2</sup>. Můžeme také použít polynomy vyššího stupně, pokud chceme.

Pipeline lze používat stejným způsobem jako původní objekt `LinearRegression`, tj. můžeme pipeline `fit`-nout a pak použít `predict` pro získání výsledků predikce. Zde je graf ukazující testovací data a aproximační křivku:

<img alt="Polynomická regrese" src="../../../../translated_images/cs/poly-results.ee587348f0f1f60b.webp" width="50%" />

Použitím polynomické regrese můžeme získat mírně nižší MSE a vyšší koeficient determinace, ale nikoliv výrazně. Musíme vzít v úvahu také další vlastnosti!

> Můžete vidět, že minimální ceny dýní se zaznamenávají někde kolem Halloweenu. Jak byste to vysvětlili? 

🎃 Gratulujeme, právě jste vytvořili model, který může pomoci předpovědět cenu dýňových koláčů. Pravděpodobně můžete zopakovat stejný postup pro všechny typy dýní, ale to by bylo únavné. Naučíme se nyní, jak zohlednit odrůdu dýně v našem modelu!

## Kategorie vlastností

V ideálním světě chceme být schopni předpovídat ceny různých odrůd dýní pomocí jednoho modelu. Sloupec `Variety` je však poněkud odlišný od sloupců jako `Month`, protože obsahuje nenumerické hodnoty. Takové sloupce se nazývají **kategoriální**.

[![ML pro začátečníky - Předpovědi kategoriálních vlastností pomocí lineární regrese](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML pro začátečníky - Předpovědi kategoriálních vlastností pomocí lineární regrese")

> 🎥 Klikněte na obrázek výše pro krátký video přehled použití kategoriálních vlastností.

Zde vidíte, jak průměrná cena závisí na odrůdě:

<img alt="Průměrná cena podle odrůdy" src="../../../../translated_images/cs/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Abychom vzali odrůdu v úvahu, musíme ji nejprve převést do numerické formy, tj. **zakódovat** ji. Existuje několik způsobů, jak toho dosáhnout:

* Jednoduché **číselné kódování** vytvoří tabulku různých odrůd, a pak nahradí název odrůdy indexem z této tabulky. To ale není nejlepší nápad pro lineární regresi, protože lineární regrese vezme skutečnou číselnou hodnotu indexu a přidá ji k výsledku, násobenou nějakým koeficientem. Ve našem případě je vztah mezi číslem indexu a cenou zjevně nelineární, i když zajistíme, že indexy budou v určitém specifickém pořadí.
* **One-hot encoding** nahradí sloupec `Variety` čtyřmi různými sloupci, každým pro jednu odrůdu. Každý sloupec bude obsahovat `1`, pokud odpovídající řádek patří dané odrůdě, a `0` jinak. To znamená, že v lineární regresi budou čtyři koeficienty, každý pro jednu odrůdu dýně, odpovědné za "počáteční cenu" (spíše "příplatek") za tuto konkrétní odrůdu.

Níže uvedený kód ukazuje, jak můžeme one-hot kódovat odrůdu:

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

K natrénování lineární regrese s one-hot kódovanou odrůdou jako vstupem stačí správně inicializovat data `X` a `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Zbytek kódu je stejný jako ten, který jsme použili výše k trénování lineární regrese. Pokud to vyzkoušíte, uvidíte, že střední kvadratická chyba je přibližně stejná, ale získáme výrazně vyšší koeficient determinace (~77 %). Pro ještě přesnější předpovědi můžeme vzít v úvahu více kategoriálních vlastností, stejně jako číselné vlastnosti, například `Month` nebo `DayOfYear`. Pro získání jednoho velkého pole vlastností můžeme použít `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Zde také vezmeme v úvahu `City` a typ `Package`, což nám dává MSE 2.84 (10 %) a determinaci 0.94!

## Spojení všeho dohromady

Pro nejlepší model můžeme použít kombinovaná (one-hot kódovaná kategoriální + numerická) data z výše uvedeného příkladu společně s polynomickou regresí. Zde je kompletní kód pro vaše pohodlí:

```python
# nastavit tréninková data
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# provést rozdělení na tréninkovou a testovací sadu
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# nastavit a trénovat pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# předpovědět výsledky pro testovací data
pred = pipeline.predict(X_test)

# vypočítat střední kvadratickou chybu a koeficient determinace
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Toto by nám mělo dát nejlepší koeficient determinace téměř 97 % a MSE=2.23 (~8% chyba předpovědi).

| Model | MSE | Determinace |
|-------|-----|-------------|
| Lineární `DayOfYear` | 2.77 (17,2 %) | 0.07 |
| Polynomický `DayOfYear` | 2.73 (17,0 %) | 0.08 |
| Lineární `Variety` | 5.24 (19,7 %) | 0.77 |
| Lineární všechny vlastnosti | 2.84 (10,5 %) | 0.94 |
| Polynomický všechny vlastnosti | 2.23 (8,25 %) | 0.97 |

🏆 Dobrá práce! Vytvořili jste čtyři regresní modely v jedné lekci a zlepšili kvalitu modelu na 97 %. V závěrečné části o regresi se naučíte o logistické regresi pro určení kategorií.

---
## 🚀Výzva

Otestujte v tomto notebooku několik různých proměnných a zjistěte, jak korelace odpovídá přesnosti modelu.

## [Kvíz po přednášce](https://ff-quizzes.netlify.app/en/ml/)

## Přezkum a samostudium

V této lekci jsme se naučili o lineární regresi. Existují další důležité typy regrese. Přečtěte si o technikách Stepwise, Ridge, Lasso a Elasticnet. Dobrým kurzem ke studiu je [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Zadání 

[Postavte model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Prohlášení o vyloučení odpovědnosti**:  
Tento dokument byl přeložen pomocí AI překladatelské služby [Co-op Translator](https://github.com/Azure/co-op-translator). I když usilujeme o přesnost, mějte prosím na paměti, že automatizované překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho mateřském jazyce by měl být považován za autoritativní zdroj. Pro zásadní informace se doporučuje profesionální lidský překlad. Nejsme odpovědní za jakékoli nedorozumění nebo nesprávné výklady vzniklé použitím tohoto překladu.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->