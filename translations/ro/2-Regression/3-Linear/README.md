# Construiește un model de regresie folosind Scikit-learn: regresie în patru moduri

## Notă pentru începători

Regresia liniară este folosită atunci când dorim să prezicem o **valoare numerică** (de exemplu, prețul unei case, temperatura sau vânzările).
Funcționează prin găsirea unei linii drepte care reprezintă cel mai bine relația dintre caracteristicile de intrare și ieșire.

În această lecție, ne concentrăm pe înțelegerea conceptului înainte de a explora tehnici de regresie mai avansate.
![Linear vs polynomial regression infographic](../../../../translated_images/ro/linear-polynomial.5523c7cb6576ccab.webp)
> Infografic de [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Test pre-lectură](https://ff-quizzes.netlify.app/en/ml/)

> ### [Această lecție este disponibilă în R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introducere

Până acum ați explorat ce este regresia cu date de probă adunate din setul de date despre prețurile dovlecilor pe care îl vom folosi pe parcursul acestei lecții. De asemenea, ați vizualizat datele folosind Matplotlib.

Acum sunteți gata să aprofundați regresia pentru învățarea automată (ML). Deși vizualizarea permite să înțelegeți datele, adevărata putere a învățării automate vine din _antrenarea modelelor_. Modelele sunt antrenate pe date istorice pentru a captura automat dependențele din date și vă permit să preziceți rezultate pentru date noi, pe care modelul nu le-a văzut anterior.

În această lecție veți învăța mai multe despre două tipuri de regresie: _regresie liniară de bază_ și _regresie polinomială_, împreună cu unele dintre elementele matematice ale acestor tehnici. Aceste modele ne vor permite să prezicem prețurile dovlecilor în funcție de diferite date de intrare.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Faceți click pe imaginea de mai sus pentru un scurt videoclip introductiv despre regresia liniară.

> Pe tot parcursul acestui curriculum, presupunem cunoștințe minime de matematică și ne propunem să o facem accesibilă pentru studenți din alte domenii, așa că urmăriți notele, 🧮 apelurile, diagramele și alte unelte de învățare pentru a ajuta la înțelegere.

### Cerință prealabilă

Ar trebui să fiți familiarizați până acum cu structura datelor despre dovleci pe care le examinăm. Le puteți găsi preîncărcate și preprocesate în fișierul _notebook.ipynb_ al acestei lecții. În fișier, prețul dovlecilor este afișat pe bushel într-un nou DataFrame. Asigurați-vă că puteți rula aceste noteboooks în kerneluri din Visual Studio Code.

### Pregătire

Ca un memento, încărcați aceste date pentru a putea pune întrebări despre ele. 

- Când este cel mai bun moment pentru a cumpăra dovleci? 
- Ce preț pot să aștept pentru un coș de dovleci miniatură?
- Ar trebui să îi cumpăr în coșuri de jumătate de bushel sau în cutii de 1 1/9 bushel?
Să continuăm să explorăm aceste date.

În lecția anterioară, ați creat un DataFrame Pandas și l-ați populat cu o parte din setul original de date, standardizând prețurile pe bushel. Prin aceasta, totuși, ați putut colecta doar aproximativ 400 de puncte de date și numai pentru lunile de toamnă.

Aruncați o privire la datele pe care le-am preîncărcat în notebook-ul însoțitor al acestei lecții. Datele sunt preîncărcate și este afișat un grafic de dispersie inițial pentru a arăta datele pe lună. Poate putem obține mai multe detalii despre natura datelor dacă le curățăm mai bine.

## O linie de regresie liniară

După cum ați învățat în Lecția 1, scopul unui exercițiu de regresie liniară este să puteți trasa o linie care să:

- **Arate relațiile variabilelor**. Să arate relația dintre variabile
- **Facă predicții**. Să facă predicții precise despre unde ar cădea un nou punct de date în raport cu acea linie.

Este tipic pentru **Regresia celor mai mici pătrate (Least-Squares Regression)** să traseze acest tip de linie. Termenul „Cei mai mici pătrate” se referă la procesul de minimizare a erorii totale în modelul nostru. Pentru fiecare punct de date, măsurăm distanța verticală (numită reziduală) între punctul real și linia noastră de regresie.

Aceste distanțe le pătrățim din două motive principale:

1. **Magnitudine în loc de Direcție:** Dorim să tratăm o eroare de -5 la fel ca o eroare de +5. Pătratul transformă toate valorile în pozitive.

2. **Penalizarea valorilor aberante:** Pătratul dă o greutate mai mare erorilor mari, forțând linia să rămână mai aproape de punctele care sunt departe.

Apoi adunăm toate aceste valori pătrate. Scopul nostru este să găsim linia specifică unde această sumă finală este minimă (cea mai mică valoare posibilă) - de aici și numele „Cei mai mici pătrate”.

> **🧮 Arată-mi matematica**  
>  
> Această linie, denumită _linia cea mai potrivită_ poate fi exprimată prin [o ecuație](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>
> `X` este 'variabila explicativă'. `Y` este 'variabila dependentă'. Panta liniei este `b` iar `a` este interceptul pe axa y, care se referă la valoarea lui `Y` când `X = 0`.  
>
>![calculate the slope](../../../../translated_images/ro/slope.f3c9d5910ddbfcf9.webp)
>
> Mai întâi, calculăm panta `b`. Infografic de [Jen Looper](https://twitter.com/jenlooper)
>
> Cu alte cuvinte, referindu-ne la întrebarea inițială din datele noastre despre dovleci: „prezice prețul unui dovleac pe bushel pe lună”, `X` s-ar referi la preț iar `Y` s-ar referi la luna vânzării.
>
>![complete the equation](../../../../translated_images/ro/calculation.a209813050a1ddb1.webp)
>
> Calculează valoarea lui Y. Dacă plătești în jur de 4 dolari, trebuie să fie aprilie! Infografic de [Jen Looper](https://twitter.com/jenlooper)
>
> Matematica care calculează linia trebuie să demonstreze panta liniei, care depinde și de intercept, sau unde se situează `Y` când `X = 0`.
>
> Puteți observa metoda de calcul pentru aceste valori pe site-ul [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Vizitați și [acest calculator pentru cele mai mici pătrate](https://www.mathsisfun.com/data/least-squares-calculator.html) pentru a vedea cum valorile numerelor influențează linia.

## Corelație

Un alt termen pe care trebuie să-l înțelegem este **Coeficientul de Corelație** între variabilele date X și Y. Folosind un grafic de dispersie, puteți vizualiza rapid acest coeficient. Un grafic cu puncte de date răspândite într-o linie ordonată are corelație ridicată, iar un grafic cu punctele de date presărate peste tot între X și Y are corelație scăzută.

Un model bun de regresie liniară va fi unul care are un coeficient de corelație mare (mai aproape de 1 decât de 0) folosind metoda regresiei celor mai mici pătrate cu linia de regresie.

✅ Rulați notebook-ul care însoțește această lecție și priviți graficul de dispersie Lună versus Preț. Datele care asociază Luna cu Prețul pentru vânzările de dovleci par să aibă corelație mare sau mică, conform interpretării dvs. vizuale a graficului? Se schimbă dacă folosiți o măsură mai detaliată în loc de `Lună`, de ex. *ziua din an* (adică numărul de zile de la începutul anului)?

În codul de mai jos, vom presupune că am curățat datele și am obținut un DataFrame numit `new_pumpkins`, similar cu următorul:

ID | Lună | ZiDinAn | Varietate | Oraș | Ambalaj | Preț Minim | Preț Maxim | Preț
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | TIP PENTRU PLĂCINTĂ | BALTIMORE | cutii de 1 1/9 bushel | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | TIP PENTRU PLĂCINTĂ | BALTIMORE | cutii de 1 1/9 bushel | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | TIP PENTRU PLĂCINTĂ | BALTIMORE | cutii de 1 1/9 bushel | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | TIP PENTRU PLĂCINTĂ | BALTIMORE | cutii de 1 1/9 bushel | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | TIP PENTRU PLĂCINTĂ | BALTIMORE | cutii de 1 1/9 bushel | 15.0 | 15.0 | 13.636364

> Codul pentru curățarea datelor este disponibil în [`notebook.ipynb`](notebook.ipynb). Am efectuat aceiași pași de curățare ca în lecția anterioară și am calculat coloana `DayOfYear` folosind expresia următoare:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Acum că aveți o înțelegere a matematicii din spatele regresiei liniare, să creăm un model de regresie pentru a vedea dacă putem prezice care ambalaj de dovleci va avea cele mai bune prețuri. Cineva care cumpără dovleci pentru o copertină specială pentru sărbători ar putea dori aceste informații pentru a-și optimiza achizițiile de pachete de dovleci pentru acea copertină.

## Căutarea corelației

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Faceți click pe imaginea de mai sus pentru un scurt videoclip despre corelație.

Din lecția anterioară probabil ați văzut că prețul mediu pentru diferite luni arată astfel:

<img alt="Average price by month" src="../../../../translated_images/ro/barchart.a833ea9194346d76.webp" width="50%"/>

Acest lucru sugerează că ar trebui să existe o corelație și putem încerca să antrenăm un model de regresie liniară pentru a prezice relația dintre `Lună` și `Preț`, sau între `ZiDinAn` și `Preț`. Iată graficul de dispersie care arată ultima relație:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ro/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />

Să vedem dacă există o corelație folosind funcția `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Se pare că corelația este destul de mică, -0.15 folosind `Month` și -0.17 folosind `DayOfMonth`, dar ar putea exista o altă relație importantă. Se pare că există grupuri diferite de prețuri care corespund diferitelor varietăți de dovleci. Pentru a confirma această ipoteză, să afișăm fiecare categorie de dovleci folosind o culoare diferită. Prin trecerea unui parametru `ax` funcției de plotare `scatter` putem afișa toate punctele pe același grafic:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ro/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" />

Investigația noastră sugerează că varietatea are mai mult efect asupra prețului general decât data efectivă de vânzare. Putem observa acest lucru cu un grafic cu bare:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/ro/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Să ne concentrăm pentru moment doar pe o varietate de dovleac, „tip plăcintă”, și să vedem ce efect are data asupra prețului:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ro/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" />

Dacă acum calculăm corelația între `Price` și `DayOfYear` folosind funcția `corr`, vom obține ceva în jur de `-0.27` - ceea ce înseamnă că antrenarea unui model predictiv are sens.

> Înainte de a antrena un model de regresie liniară, este important să ne asigurăm că datele noastre sunt curate. Regresia liniară nu funcționează bine cu valori lipsă, astfel că are sens să eliminăm toate celulele goale:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

O altă abordare ar fi să completăm acele valori goale cu valorile medii din coloana corespunzătoare.

## Regresie liniară simplă

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Faceți click pe imaginea de mai sus pentru un scurt videoclip despre regresia liniară și polinomială.

Pentru a antrena modelul nostru de regresie liniară, vom folosi biblioteca **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Începem prin separarea valorilor de intrare (caracteristici) și a ieșirii așteptate (eticheta) în array-uri numpy separate:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Observați că a fost necesar să facem `reshape` pe datele de intrare pentru ca pachetul de Regresie Liniară să înțeleagă corect datele. Regresia liniară așteaptă un array 2D ca intrare, unde fiecare rând al array-ului corespunde unui vector de caracteristici. În cazul nostru, pentru că avem o singură intrare - avem nevoie de un array cu forma N&times;1, unde N este dimensiunea setului de date.

Apoi, trebuie să împărțim datele în seturi de antrenament și de test, astfel încât să putem valida modelul după antrenare:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

În final, antrenarea propriu-zisă a modelului de regresie liniară durează doar două linii de cod. Definim obiectul `LinearRegression`, și îl ajustăm la datele noastre folosind metoda `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Obiectul `LinearRegression` după ce a fost `fit`-at conține toți coeficienții regresiei, care pot fi accesati folosind proprietatea `.coef_`. În cazul nostru, există un singur coeficient, care ar trebui să fie în jur de `-0.017`. Aceasta înseamnă că prețurile par să scadă puțin în timp, dar nu prea mult, în jur de 2 cenți pe zi. Putem, de asemenea, să accesăm punctul de intersecție al regresiei cu axa Y folosind `lin_reg.intercept_` - acesta va fi în jur de `21` în cazul nostru, indicând prețul la începutul anului.

Pentru a vedea cât de precis este modelul nostru, putem prezice prețurile pe un set de date de testare și apoi măsura cât de apropiate sunt predicțiile noastre de valorile așteptate. Acest lucru se poate face folosind metrici de eroare pătratică medie rădăcină (RMSE), care este rădăcina mediei tuturor diferențelor pătratice între valoarea așteptată și cea prezisă.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Eroarea noastră pare să fie în jur de 2 puncte, ceea ce este ~17%. Nu foarte bine. Un alt indicator al calității modelului este **coeficientul de determinare**, care poate fi obținut astfel:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Dacă valoarea este 0, înseamnă că modelul nu ia în considerare datele de intrare și acționează ca *cel mai slab predictor liniar*, care este pur și simplu valoarea medie a rezultatului. Valoarea 1 înseamnă că putem prezice perfect toate ieșirile așteptate. În cazul nostru, coeficientul este în jur de 0.06, ceea ce este destul de mic.

Putem, de asemenea, să reprezentăm grafic datele de test împreună cu linia de regresie pentru a vedea mai bine cum funcționează regresia în cazul nostru:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/ro/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regresie Polinomială

Un alt tip de Regresie Liniară este Regresia Polinomială. Deși uneori există o relație liniară între variabile - cu cât dovleacul are un volum mai mare, cu atât prețul este mai mare - uneori aceste relații nu pot fi reprezentate ca un plan sau o linie dreaptă.

✅ Iată [câteva exemple suplimentare](https://online.stat.psu.edu/stat501/lesson/9/9.8) de date pentru care s-ar putea folosi Regresia Polinomială

Uită-te din nou la relația dintre Data și Preț. Se pare că acest scatterplot ar trebui neapărat analizat cu o linie dreaptă? Nu pot prețurile să fluctueze? În acest caz, poți încerca regresia polinomială.

✅ Polinoamele sunt expresii matematice care pot consta din una sau mai multe variabile și coeficienți

Regresia polinomială creează o curbă pentru a se potrivi mai bine datelor neliniare. În cazul nostru, dacă includem o variabilă `DayOfYear` la pătrat în datele de intrare, ar trebui să putem potrivi datele noastre cu o curbă parabolică, care va avea un minim într-un anumit punct al anului.

Scikit-learn include un API util [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) pentru a combina împreună diferitele etape ale procesării datelor. Un **pipeline** este un lanț de **estimatori**. În cazul nostru, vom crea un pipeline care mai întâi adaugă caracteristici polinomiale modelului nostru, apoi antrenează regresia:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Folosind `PolynomialFeatures(2)` înseamnă că vom include toate polinoamele de gradul al doilea din datele de intrare. În cazul nostru, aceasta va însemna doar `DayOfYear`<sup>2</sup>, dar dat fiind două variabile de intrare X și Y, aceasta va adăuga X<sup>2</sup>, XY și Y<sup>2</sup>. Putem folosi, de asemenea, polinoame de grad mai mare dacă dorim.

Pipeline-urile pot fi folosite în același mod ca obiectul original `LinearRegression`, adică putem face `fit` pe pipeline, apoi folosi `predict` pentru a obține rezultatele predicției. Iată graficul care arată datele de test și curba de aproximare:

<img alt="Polynomial regression" src="../../../../translated_images/ro/poly-results.ee587348f0f1f60b.webp" width="50%" />

Folosind Regresia Polinomială, putem obține un MSE ușor mai mic și un coeficient de determinare mai mare, dar nu semnificativ. Trebuie să luăm în considerare și alte caracteristici!

> Poți vedea că prețurile minime ale dovlecilor sunt observate undeva în jurul Halloween-ului. Cum poți explica asta?

🎃 Felicitări, ai creat un model care te poate ajuta să prezici prețul dovlecilor pentru plăcintă. Probabil că poți repeta aceeași procedură pentru toate tipurile de dovleci, dar ar fi obositor. Hai să învățăm acum cum să luăm în considerare varietatea de dovleci în modelul nostru!

## Caracteristici Categorice

În lumea ideală, vrem să putem prezice prețurile pentru diferite varietăți de dovleci folosind același model. Totuși, coloana `Variety` este oarecum diferită față de coloane precum `Month`, pentru că conține valori nenumerice. Astfel de coloane sunt numite **categorice**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Apasă pe imaginea de mai sus pentru un scurt videoclip despre folosirea caracteristicilor categorice.

Aici poți vedea cum depinde prețul mediu de varietate:

<img alt="Average price by variety" src="../../../../translated_images/ro/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Pentru a lua în considerare varietatea, trebuie mai întâi să o convertim în formă numerică, sau să o **encodăm**. Există mai multe moduri în care putem face asta:

* Encodarea numerică simplă construită o tabelă cu diferite varietăți, apoi înlocuiește numele varietății cu un indice în acea tabelă. Aceasta nu este o idee bună pentru regresia liniară, deoarece regresia liniară ia valoarea numerică reală a indicelui și o adaugă la rezultat, înmulțind cu un coeficient. În cazul nostru, relația dintre numărul indicelui și preț este clar neliniară, chiar dacă ne asigurăm că indicii sunt ordonați într-un anumit mod.
* Encodarea one-hot va înlocui coloana `Variety` cu 4 coloane diferite, câte una pentru fiecare varietate. Fiecare coloană va conține `1` dacă rândul respectiv aparține acestei varietăți și `0` altfel. Aceasta înseamnă că vor exista patru coeficienți în regresia liniară, câte unul pentru fiecare varietate de dovleac, responsabili pentru "prețul de pornire" (sau mai bine zis "prețul suplimentar") pentru acea varietate anume.

Codul de mai jos arată cum putem face one-hot encoding pentru o varietate:

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

Pentru a antrena regresia liniară folosind varietatea encodată one-hot ca intrare, trebuie doar să inițializăm corect datele `X` și `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Restul codului este la fel ca cel folosit mai sus pentru antrenarea regresiei liniare. Dacă încerci, vei vedea că eroarea pătratică medie este cam la fel, dar coeficientul de determinare crește mult (~77%). Pentru a obține predicții și mai precise, putem lua în considerare mai multe caracteristici categorice, precum și caracteristici numerice, cum ar fi `Month` sau `DayOfYear`. Pentru a obține un singur tablou mare de caracteristici, putem folosi `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Aici luăm în considerare și `City` și tipul de `Package`, ceea ce ne oferă un MSE de 2.84 (10%) și un coeficient de determinare de 0.94!

## Punând totul cap la cap

Pentru a face cel mai bun model, putem folosi date combinate (categorice one-hot encode + numerice) din exemplul de mai sus împreună cu Regresia Polinomială. Iată codul complet pentru confortul tău:

```python
# configurează datele de antrenament
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# realizează împărțirea în seturi de antrenament și test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# configurează și antrenează pipeline-ul
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prezice rezultatele pentru datele de test
pred = pipeline.predict(X_test)

# calculează MSE și coeficientul de determinare
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Aceasta ne va da cel mai bun coeficient de determinare de aproape 97%, și MSE=2.23 (~8% eroare de predicție).

| Model | MSE | Determinarea |
|-------|-----|--------------|
| Liniară `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Polinomială `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Liniară `Variety` | 5.24 (19.7%) | 0.77 |
| Toate caracteristicile Liniară | 2.84 (10.5%) | 0.94 |
| Toate caracteristicile Polinomială | 2.23 (8.25%) | 0.97 |

🏆 Foarte bine! Ai creat patru modele de regresie într-o lecție și ai îmbunătățit calitatea modelului la 97%. În secțiunea finală despre Regresie, vei învăța despre Regresia Logistică pentru clasificare.

---
## 🚀Provocare

Testează mai multe variabile diferite în acest notebook pentru a vedea cum corespunde corelația cu acuratețea modelului.

## [Chestionar post-lectură](https://ff-quizzes.netlify.app/en/ml/)

## Recenzie & Studiu individual

În această lecție am învățat despre Regresia Liniară. Există și alte tipuri importante de regresie. Citește despre tehnicile Stepwise, Ridge, Lasso și Elasticnet. Un curs bun pentru a învăța mai multe este [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Temă

[Construiește un Model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Declinare a responsabilității**:  
Acest document a fost tradus folosind serviciul de traducere AI [Co-op Translator](https://github.com/Azure/co-op-translator). Deși ne străduim pentru acuratețe, vă rugăm să rețineți că traducerile automate pot conține erori sau inexactități. Documentul original în limba sa nativă trebuie considerat sursa autorizată. Pentru informații critice, se recomandă traducerea profesională realizată de un specialist uman. Nu ne asumăm răspunderea pentru eventualele neînțelegeri sau interpretări greșite rezultate din utilizarea acestei traduceri.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->