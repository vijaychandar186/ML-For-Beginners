# Izgradnja regresijskog modela pomoću Scikit-learn: četiri načina regresije

## Napomena za početnike

Linearna regresija se koristi kada želimo predvidjeti **numeričku vrijednost** (na primjer, cijenu kuće, temperaturu ili prodaju).  
Funkcionira tako da pronalazi pravu koja najbolje predstavlja odnos između ulaznih značajki i izlaza.

U ovoj lekciji se fokusiramo na razumijevanje koncepta prije nego što istražimo naprednije tehnike regresije.  
![Linear vs polynomial regression infographic](../../../../translated_images/hr/linear-polynomial.5523c7cb6576ccab.webp)  
> Infografika autora [Dasani Madipalli](https://twitter.com/dasani_decoded)  
## [Kviz prije lekcije](https://ff-quizzes.netlify.app/en/ml/)

> ### [Ova je lekcija dostupna i u R-u!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)  
### Uvod

Do sada ste istraživali što je regresija koristeći uzorke podataka prikupljenih iz skupa podataka o cijenama bundeva koje ćemo koristiti kroz cijelu ovu lekciju. Također ste ih vizualizirali pomoću Matplotlib.

Sada ste spremni dublje zaroniti u regresiju za ML. Dok vizualizacija omogućuje razumijevanje podataka, prava snaga strojnog učenja dolazi iz _treninga modela_. Modeli se treniraju na povijesnim podacima kako bi automatski uhvatili ovisnosti u podacima i omogućuju predviđanje ishoda za nove podatke koje model prije nije vidio.

U ovoj lekciji ćete naučiti više o dvije vrste regresije: _osnovna linearna regresija_ i _polinomijalna regresija_, zajedno s dijelom matematike koja stoji iza tih tehnika. Ti modeli će nam omogućiti predviđanje cijena bundeva ovisno o različitim ulaznim podacima.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Kliknite na sliku gore za kratak video pregled linearne regresije.

> Kroz ovaj kurikulum pretpostavljamo minimalno znanje iz matematike i nastojimo ga učiniti dostupnim studentima iz drugih područja, stoga obratite pažnju na bilješke, 🧮 oznake, dijagrame i druge nastavne alate koji pomažu u razumijevanju.

### Preduvjeti

Sada biste trebali biti upoznati sa strukturom podataka o bundevama koje promatramo. One su unaprijed učitane i očišćene u datoteci _notebook.ipynb_ ove lekcije. U datoteci je cijena bundeve prikazana po košari. Provjerite da možete pokretati ove bilježnice u kernelima u Visual Studio Codeu.

### Priprema

Kao podsjetnik, učitavate ove podatke kako biste mogli postavljati pitanja o njima.

- Kada je najbolje vrijeme za kupnju bundeva?  
- Koju cijenu mogu očekivati za kutiju mini bundeva?  
- Trebam li ih kupovati u košarama od pola bushela ili u kutiji od 1 1/9 bushela?  
Nastavimo dalje kopati u ove podatke.

U prethodnoj lekciji ste napravili Pandas DataFrame i popunili ga dijelom izvornog skupa podataka, standardizirajući cijene po bushelu. Time ste uspjeli prikupiti oko 400 podataka samo za jesenske mjesece.

Pogledajte podatke koje smo unaprijed učitali u pratećoj bilježnici za ovu lekciju. Podaci su unaprijed učitani i nacrtan je početni scatterplot koji prikazuje podatke po mjesecima. Možda možemo dobiti malo više detalja o prirodi podataka dodatnim čišćenjem.

## Linearna regresijska crta

Kao što ste naučili u Lekciji 1, cilj linearne regresije je moći nacrtati liniju da:

- **Prikaže odnose varijabli**. Prikaže odnos između varijabli  
- **Napraviti predviđanja**. Precizno predvidjeti gdje će se novi podatak smjestiti u odnosu na tu liniju.

Tipično za **regresiju najmanjih kvadrata** je crtanje takve linije. Termin "najmanjih kvadrata" odnosi se na proces minimiziranja ukupne pogreške u našem modelu. Za svaku točku mjerimo vertikalnu udaljenost (zvanu rezidual) između stvarne točke i naše regresijske linije.

Te udaljenosti kvadriramo iz dva glavna razloga:

1. **Veličina nasuprot smjeru:** Želimo tretirati pogrešku od -5 isto kao i pogrešku od +5. Kvadriranjem sve vrijednosti postaju pozitivne.  

2. **Kazna za odstupanja:** Kvadriranjem se daje veća težina većim pogreškama, tjerajući liniju da bude bliža točkama koje su daleko.  

Zatim zbrojimo sve te kvadrirane vrijednosti. Cilj je pronaći specifičnu liniju za koju je taj konačni zbroj najmanji (najmanja moguća vrijednost)—otuda i naziv "najmanjih kvadrata".

> **🧮 Pokaži mi matematiku**  
>  
> Ova linija, nazvana _linijom najboljeg pristajanja_, može se izraziti [jednadžbom](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` je 'objašnjavajuća varijabla'. `Y` je 'ovisna varijabla'. Nagib linije je `b` a `a` je y-presjek, što je vrijednost `Y` kad je `X = 0`.  
>  
>![izračun nagiba](../../../../translated_images/hr/slope.f3c9d5910ddbfcf9.webp)  
>  
> Prvo, izračunajte nagib `b`. Infografika autora [Jen Looper](https://twitter.com/jenlooper)  
>  
> Drugim riječima, i referirajući se na originalno pitanje naših podataka o bundevama: "predvidjeti cijenu bundeve po bushelu po mjesecu", `X` bi označavalo cijenu a `Y` mjesec prodaje.  
>  
>![dovršavanje jednadžbe](../../../../translated_images/hr/calculation.a209813050a1ddb1.webp)  
>  
> Izračunajte vrijednost Y. Ako plaćate oko 4 dolara, mora biti travanj! Infografika autora [Jen Looper](https://twitter.com/jenlooper)  
>  
> Matematika koja izračunava liniju mora pokazati nagib linije, koji također ovisi o presjeku, odnosno gdje se `Y` nalazi kada je `X = 0`.  
>  
> Metodu izračuna ovih vrijednosti možete proučiti na stranici [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Posjetite i [ovaj kalkulator najmanjih kvadrata](https://www.mathsisfun.com/data/least-squares-calculator.html) da vidite kako vrijednosti brojeva utječu na liniju.

## Korelacija

Još jedan pojam koji treba razumjeti je **koeficijent korelacije** između zadanih X i Y varijabli. Pomoću scatterplota možete brzo vizualizirati ovaj koeficijent. Grafikon s točkama razbacanim u lijepoj liniji ima visoku korelaciju, dok graf s točkama razbacanim posvuda između X i Y ima nisku korelaciju.

Dobar linearni regresijski model će imati visok koeficijent korelacije (bliži 1 nego 0) koristeći metodu najmanjih kvadrata s regresijskom linijom.

✅ Pokrenite bilježnicu koja prati ovu lekciju i pogledajte scatterplot Mjeseca prema Cijeni. Ima li podataka koji povezuju Mjesec i Cijenu kod prodaje bundeva visoku ili nisku korelaciju prema vašoj vizualnoj interpretaciji scatterplota? Mijenja li se to ako koristite finiju mjeru umjesto `Month`, npr. *dan u godini* (tj. broj dana od početka godine)?

U sljedećem kodu pretpostavit ćemo da smo očistili podatke i dobili DataFrame nazvan `new_pumpkins`, sličan sljedećem:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  

> Kod za čišćenje podataka dostupan je u [`notebook.ipynb`](notebook.ipynb). Izveli smo iste korake čišćenja kao u prethodnoj lekciji i izračunali stupac `DayOfYear` koristeći sljedeći izraz:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Sada, kad imate razumijevanje matematike iza linearne regresije, stvorimo regresijski model da vidimo možemo li predvidjeti koja će pakiranja bundeva imati najbolje cijene. Netko tko kupuje bundeve za natjecanje ili ukrasnu parcelu možda želi ove informacije kako bi optimizirao svoje kupovine pakiranja bundeva.

## Traženje korelacije

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Kliknite na sliku gore za kratak video pregled korelacije.

Iz prethodne lekcije vjerojatno ste vidjeli da prosječna cijena po mjesecima izgleda ovako:

<img alt="Average price by month" src="../../../../translated_images/hr/barchart.a833ea9194346d76.webp" width="50%"/>

Ovo sugerira da bi trebala postojati neka korelacija, i možemo pokušati trenirati linearni regresijski model koji predviđa odnos između `Month` i `Price`, ili između `DayOfYear` i `Price`. Slijedi scatter plot koji prikazuje posljednji odnos:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/hr/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Pogledajmo je li korelacija prisutna uz pomoć funkcije `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Izgleda da je korelacija prilično mala, -0.15 po `Month` i -0.17 po `DayOfMonth`, ali može postojati još neki važan odnos. Izgleda da postoje različite skupine cijena koje odgovaraju različitim sortama bundeva. Da bismo potvrdili ovu hipotezu, prikažimo svaku kategoriju bundeva različitom bojom. Prosljeđivanjem parametra `ax` funkciji za crtanje `scatter` možemo nacrtati sve točke na istom grafikonu:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/hr/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Naša istraga pokazuje da sorta ima veći utjecaj na ukupnu cijenu nego stvarni datum prodaje. Ovo vidimo i na stupčastom grafikonu:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Bar graph of price vs variety" src="../../../../translated_images/hr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Za sada se usredotočimo samo na jednu sortu bundeve, 'pie type', i pogledajmo kako datum utječe na cijenu:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/hr/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Ako sada izračunamo korelaciju između `Price` i `DayOfYear` pomoću funkcije `corr`, dobit ćemo nešto poput `-0.27` - što znači da je treniranje prediktivnog modela smisleno.

> Prije nego treniramo linearni regresijski model, važno je osigurati da su naši podaci čisti. Linearna regresija ne radi dobro s nedostajućim vrijednostima, stoga ima smisla ukloniti sve prazne ćelije:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
Drugi pristup bi bio popuniti prazne vrijednosti prosječnim vrijednostima iz odgovarajućeg stupca.

## Jednostavna linearna regresija

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Kliknite na sliku gore za kratak video pregled linearne i polinomijalne regresije.

Za treniranje našeg linearno regresijskog modela koristit ćemo biblioteku **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
Počinjemo odvajajući ulazne vrijednosti (značajke) i očekivane izlazne vrijednosti (etikete) u zasebne numpy nizove:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Primijetite da smo morali izvršiti `reshape` na ulaznim podacima da bi Linear Regression paket pravilno razumio ulaz. Linearna regresija očekuje 2D niz kao ulaz, gdje svaki redak niza predstavlja vektor ulaznih značajki. U našem slučaju, budući da imamo samo jednu ulaznu varijablu, treba nam niz oblika N&times;1, gdje je N veličina skupa podataka.

Zatim trebamo podijeliti podatke u skupove za treniranje i testiranje, kako bismo mogli validirati naš model nakon treninga:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
Na kraju, treniranje samog modela linearne regresije traje samo dvije linije koda. Definiramo objekt `LinearRegression` i prilagođavamo ga naša podacima pomoću metode `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objekt `LinearRegression` nakon treniranja (`fit`) sadrži sve koeficijente regresije, do kojih se može pristupiti putem svojstva `.coef_`. U našem slučaju postoji samo jedan koeficijent, koji bi trebao biti oko `-0.017`. To znači da cijene djeluju kao da nešto padaju s vremenom, ali ne previše, oko 2 centa dnevno. Također možemo pristupiti točki presjeka regresije s Y-osi koristeći `lin_reg.intercept_` - u našem slučaju bit će oko `21`, što označava cijenu na početku godine.

Da bismo vidjeli koliko je naš model točan, možemo predvidjeti cijene na testnom skupu podataka i zatim izmjeriti koliko su naša predviđanja bliska očekivanim vrijednostima. To se može napraviti koristeći metriku korijen srednje kvadratne pogreške (RMSE), što je korijen sredine svih kvadrata razlika između očekivane i predviđene vrijednosti.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Naša pogreška je otprilike oko 2 boda, što je ~17%. Nije baš dobro. Još jedan pokazatelj kvalitete modela je **koeficijent determinacije**, koji se može dobiti ovako:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```

Ako je vrijednost 0, to znači da model ne uzima u obzir ulazne podatke i djeluje kao *najgori linearni prediktor*, što je jednostavno srednja vrijednost rezultata. Vrijednost 1 znači da možemo savršeno predvidjeti sve očekivane izlaze. U našem slučaju koeficijent je oko 0.06, što je prilično nisko.

Također možemo prikazati testne podatke zajedno s regresijskom linijom da bolje vidimo kako regresija funkcionira u našem slučaju:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/hr/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polinomijalna regresija

Još jedna vrsta linearne regresije je polinomijalna regresija. Iako ponekad postoji linearna veza između varijabli - što je veća bundeva po volumenu, to je veća cijena - ponekad te veze nije moguće prikazati kao ravninu ili pravu liniju.

✅ Evo [još nekoliko primjera](https://online.stat.psu.edu/stat501/lesson/9/9.8) podataka za koje bi se mogla koristiti polinomijalna regresija.

Ponovno pogledajte odnos između Datuma i Cijene. Izgleda li ovaj scatterplot kao da bi ga nužno trebalo analizirati linijom? Zar cijene ne mogu varirati? U tom slučaju možete pokušati polinomijalnu regresiju.

✅ Polinomi su matematički izrazi koji mogu sadržavati jednu ili više varijabli i koeficijenata.

Polinomijalna regresija stvara zakrivljenu liniju kako bi bolje pristajala nelinearnim podacima. U našem slučaju, ako uključimo kvadratnu varijablu `DayOfYear` u ulazne podatke, trebali bismo biti u mogućnosti uklopiti podatke parabolom, koja će imati minimum u nekoj točki tijekom godine.

Scikit-learn uključuje korisni [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) za spajanje različitih koraka obrade podataka zajedno. **Pipeline** je niz **estimatora**. U našem slučaju ćemo napraviti pipeline koji prvo dodaje polinomijalne značajke našem modelu, a zatim trenira regresiju:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Korištenjem `PolynomialFeatures(2)` znači da će se uključiti svi polinomi drugog stupnja iz ulaznih podataka. U našem slučaju to će biti samo `DayOfYear`<sup>2</sup>, ali ako imamo dvije ulazne varijable X i Y, to će uključiti X<sup>2</sup>, XY i Y<sup>2</sup>. Također možemo koristiti i polinome višeg stupnja ako želimo.

Pipeline-ovi se mogu koristiti na isti način kao i originalni objekt `LinearRegression`, tj. možemo `fit` pipeline, a zatim koristiti `predict` za dobivanje rezultata predviđanja. Evo grafa koji prikazuje testne podatke i aproksimacijsku krivulju:

<img alt="Polynomial regression" src="../../../../translated_images/hr/poly-results.ee587348f0f1f60b.webp" width="50%" />

Upotrebom polinomijalne regresije možemo dobiti nešto niži MSE i viši koeficijent determinacije, ali ne značajno. Moramo uzeti u obzir i druge značajke!

> Možete primijetiti da su minimalne cijene bundeva zabilježene negdje oko Noći vještica. Kako to možete objasniti?

🎃 Čestitamo, upravo ste kreirali model koji može pomoći u predviđanju cijene bundeva za pite. Vjerojatno možete ponoviti isti postupak za sve vrste bundeva, ali to bi bilo zamorno. Sada ćemo naučiti kako u našem modelu uzeti u obzir sortu bundeve!

## Kategorizirane značajke

U idealnom svijetu želimo moći predvidjeti cijene za različite sorte bundeva koristeći isti model. Međutim, stupac `Variety` se donekle razlikuje od stupaca poput `Month`, jer sadrži nenumeričke vrijednosti. Takvi se stupci nazivaju **kategorizirani**.

[![ML for beginners - Kategorizirano predviđanje s linearnom regresijom](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Kategorizirano predviđanje s linearnom regresijom")

> 🎥 Kliknite na sliku iznad za kratki video pregled korištenja kategoriziranih značajki.

Ovdje možete vidjeti kako se prosječna cijena razlikuje po sorti:

<img alt="Average price by variety" src="../../../../translated_images/hr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Da bismo uzeli sortu u obzir, prvo je moramo pretvoriti u numerički oblik, odnosno **enkodirati**. Postoji nekoliko načina kako to možemo napraviti:

* Jednostavna **numerička enkodiranja** izgradi će tablicu različitih sorti, a zatim zamijeni ime sorte njezinim indeksom u toj tablici. To nije najbolja ideja za linearnu regresiju, jer linearna regresija uzima stvarnu numeričku vrijednost indeksa i dodaje je rezultatu, množeći koeficijentom. U našem slučaju odnos između broja indeksa i cijene je jasno nelinearan, čak i ako osiguramo da su indeksi sortirani na neki specifičan način.
* **One-hot enkodiranje** će zamijeniti stupac `Variety` sa 4 različita stupca, po jedan za svaku sortu. Svaki stupac će imati vrijednost `1` ako je odgovarajući redak te sorte, i `0` inače. To znači da će u linearnoj regresiji biti četiri koeficijenta, jedan za svaku sortu bundeve, koji su odgovorni za "početnu cijenu" (ili bolje rečeno "dodatnu cijenu") za tu sortu.

Sljedeći kod pokazuje kako možemo napraviti one-hot enkodiranje sorte:

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

Za treniranje linearne regresije koristeći one-hot enkodiranu sortu kao ulaz, samo trebamo ispravno inicijalizirati podatke `X` i `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Ostatak koda je isti kao onaj koji smo koristili gore za treniranje linearne regresije. Ako probate, vidjet ćete da je srednja kvadratna pogreška otprilike ista, ali koeficijent determinacije je znatno veći (~77%). Da bismo dobili još točnija predviđanja, možemo uzeti u obzir i više kategoriziranih značajki, kao i numeričke kao što su `Month` ili `DayOfYear`. Da bismo dobili jedan veliki niz značajki, možemo koristiti `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Ovdje također uzimamo u obzir grad i tip pakiranja, što nam daje MSE 2.84 (10%) i determinaciju 0.94!

## Sve zajedno

Da bismo napravili najbolji model, možemo koristiti kombinirane (one-hot enkodirane kategorizirane + numeričke) podatke iz gornjeg primjera zajedno s polinomijalnom regresijom. Evo kompletnog koda radi vaše udobnosti:

```python
# postavi podatke za trening
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# napravi podjelu na trening i test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# postavi i treniraj pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# predvidi rezultate za test podatke
pred = pipeline.predict(X_test)

# izračunaj MSE i determinaciju
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

To bi nam trebalo dati najbolji koeficijent determinacije od gotovo 97% i MSE=2.23 (~8% pogreške u predviđanju).

| Model | MSE | Determinacija |
|-------|-----|---------------|
| Linearni model na `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Polinomijalni model na `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Linearni model na `Variety` | 5.24 (19.7%) | 0.77 |
| Linearni model na svim značajkama | 2.84 (10.5%) | 0.94 |
| Polinomijalni model na svim značajkama | 2.23 (8.25%) | 0.97 |

🏆 Odlično! Kreirali ste četiri modela regresije u jednoj lekciji i poboljšali kvalitetu modela do 97%. U završnom dijelu o regresiji naučit ćete o logističkoj regresiji za određivanje kategorija.

---
## 🚀Izazov

Isprobajte nekoliko različitih varijabli u ovoj bilježnici kako biste vidjeli kako korelacija odgovara točnosti modela.

## [Kviz nakon predavanja](https://ff-quizzes.netlify.app/en/ml/)

## Pregled i samostalno učenje

U ovoj lekciji smo naučili o linearnoj regresiji. Postoje i druge važne vrste regresija. Pročitajte o tehnikama Stepwise, Ridge, Lasso i Elasticnet. Dobar tečaj koji vrijedi proučiti je [Stanford tečaj statističkog učenja](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Zadatak

[Izgradi model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Odricanje od odgovornosti**:
Ovaj dokument je preveden pomoću AI usluge prevođenja [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo postići točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku trebao bi se smatrati službenim izvorom. Za ključne informacije preporučuje se profesionalni ljudski prijevod. Ne snosimo odgovornost za bilo kakve nesporazume ili kriva tumačenja proizašla iz korištenja ovog prijevoda.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->