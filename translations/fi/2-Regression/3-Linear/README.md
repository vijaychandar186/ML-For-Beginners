# Rakennetaan regressiomalli Scikit-learnillä: regressio neljällä tavalla

## Aloittelijan huomautus

Lineaarista regressiota käytetään, kun haluamme ennustaa **numeraalista arvoa** (esimerkiksi talon hinta, lämpötila tai myynti).
Se toimii etsimällä suoran viivan, joka parhaiten kuvaa syöteominaisuuksien ja tuloksen välistä suhdetta.

Tässä oppitunnissa keskitymme käsitteen ymmärtämiseen ennen kuin tutustumme edistyneempiin regressiomenetelmiin.
![Linear vs polynomial regression infographic](../../../../translated_images/fi/linear-polynomial.5523c7cb6576ccab.webp)
> Infografiikka tekijältä [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Esiluento-testi](https://ff-quizzes.netlify.app/en/ml/)

> ### [Tämä oppitunti saatavilla R:llä!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Johdanto 

Tähän mennessä olet tutustunut regressioon esimerkkidatan avulla, joka on kerätty kurpitsahintojen aineistosta, jota käytämme koko tämän oppitunnin ajan. Olet myös visualisoinut sen käyttäen Matplotlibia.

Nyt olet valmis sukeltamaan syvemmälle koneoppimisen regressioon. Vaikka visualisointi auttaa sinua hahmottamaan dataa, koneoppimisen todellinen voima tulee _mallien harjoittamisesta_. Mallit koulutetaan historiallisella datalla kaappaamaan automaattisesti datan riippuvuuksia, ja niiden avulla voit ennustaa tuloksia uudelle datalle, jota malli ei ole aiemmin nähnyt.

Tässä oppitunnissa opit lisää kahdesta regressiotyypistä: _perus lineaarisesta regressiosta_ ja _polynomiregressiosta_, sekä joistakin näiden tekniikoiden taustalla olevista matematiikoista. Näillä malleilla voimme ennustaa kurpitsahintoja eri lähtötietojen perusteella.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klikkaa yllä olevaa kuvaa katsomaan lyhyt videoyhteenveto lineaarisesta regressiosta.

> Koko tämän opetussuunnitelman aikana oletamme vähäisen matematiikan osaamisen ja pyrimme tekemään sisällöstä saavutettavaa muilta aloilta tuleville opiskelijoille, joten pidä silmällä huomautuksia, 🧮 merkintöjä, kaavioita ja muita oppimistyökaluja, jotka auttavat ymmärtämisessä.

### Esivaatimukset

Sinun tulisi nyt olla tuttu kurpitsadatan rakenteen kanssa, jota tarkastelemme. Sen löydät valmiiksi ladattuna ja siistittynä tämän oppitunnin _notebook.ipynb_-tiedostosta. Tiedostossa kurpitsan hinta näytetään per hehtolitran (bushel) uutena dataframenä. Varmista, että voit ajaa näitä muistikirjoja Visual Studio Code -ympäristössä.

### Valmistelu

Muistutuksena, lataat tätä dataa, jotta voit esittää sille kysymyksiä.

- Milloin on paras aika ostaa kurpitsoja?
- Minkä hinnan voin odottaa pikkukurpitsalaatikosta?
- Kannattaako ostaa ne puolen hehtolitran koreissa vai 1 1/9 hehtolitran laatikossa?

Jatketaan tämän datan tutkimista.

Edellisessä oppitunnissa loit Pandas-dataframen ja täytit sen osalla alkuperäisestä aineistosta, vakioimalla hinnat hehtolitran mukaan. Tällä tavoin onnistuimme keräämään noin 400 datapistettä ja vain syksyn kuukausilta.

Katso data, jonka olemme ladanneet valmiiksi tämän oppitunnin mukanaolevaan muistikirjaan. Data on esiladattu ja ensimmäinen hajontakaavio piirretty kuukausidatan näyttämiseksi. Ehkä voimme saada hieman tarkempaa tietoa datan luonteesta puhdistamalla sitä vielä lisää.

## Lineaarisen regression suora

Kuten opit oppitunnissa 1, lineaarisen regression harjoituksen tavoite on pystyä piirtämään suora, joka:

- **Näyttää muuttujien väliset suhteet:** Havainnollistaa muuttujien välisen yhteyden
- **Tekee ennusteita:** Tekee tarkkoja ennusteita siitä, mihin uusi datapiste sijoittuu verrattuna tähän viivaan.

On tavallista käyttää **vähimmän neliösumman regressiota** (Least-Squares Regression) tällaisten suorien piirtämiseen. Termi "vähimmän neliösumman" viittaa prosessiin, jossa minimoidaan mallimme kokonaisvirhe. Jokaiselle datapisteelle mittaamme pystysuoran etäisyyden (jota kutsutaan jäännökseksi) todellisen pisteen ja regressiosuoran välillä.

Neliöimme nämä etäisyydet kahdesta pääsyystä:

1. **Suuruus, ei suunta:** Haluamme kohdata virheen -5 samalla tavalla kuin virheen +5. Neliöiminen muuttaa kaikki arvot positiivisiksi.

2. **Poikkeamien rankaisu:** Neliöinti antaa suuremman painon suuremmille virheille, pakottaen viivan pysymään lähempänä kauempana olevia pisteitä.

Lisäämme sitten kaikki nämä neliöt yhteen. Tavoitteemme on löytää juuri se viiva, jossa tämä loppusumma on mahdollisimman pieni – tästä nimi "vähimmän neliösumman" regressio.

> **🧮 Näytä matematiikka** 
> 
> Tätä viivaa, jota kutsutaan _sopivaksi suoraksi_, voidaan ilmaista [kaavalla](https://en.wikipedia.org/wiki/Simple_linear_regression):
> 
> ```
> Y = a + bX
> ```
>
> `X` on selittävä muuttuja. `Y` on selitettävä muuttuja. Viivan kulmakerroin on `b` ja `a` on y-leikkauspiste, joka tarkoittaa arvoa `Y`, kun `X = 0`.
>
>![laske kulmakerroin](../../../../translated_images/fi/slope.f3c9d5910ddbfcf9.webp)
>
> Laske ensin kulmakerroin `b`. Infografiikka tekijältä [Jen Looper](https://twitter.com/jenlooper)
>
> Toisin sanoen ja viitaten kurpitsadatan alkuperäiseen kysymykseen: "ennustetaan kurpitsan hinta per hehtolitran myyntikuukauden mukaan", `X` viittaa aikaan (kuukauteen) ja `Y` hintaan.
>
>![täydennä kaava](../../../../translated_images/fi/calculation.a209813050a1ddb1.webp)
>
> Laske Y:n arvo. Jos maksat noin 4 dollaria, sen täytyy olla huhtikuu! Infografiikka tekijältä [Jen Looper](https://twitter.com/jenlooper)
>
> Laskelmassa viivan kulman täytyy myös ottaa huomioon leikkauspiste, eli missä `Y` sijaitsee, kun `X = 0`.
>
> Voit tutustua laskentamenetelmään arvonlaskennasta [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) -sivustolla. Käy myös [vähimmän neliösumman laskurilla](https://www.mathsisfun.com/data/least-squares-calculator.html) nähdäksesi, miten numeroarvot vaikuttavat viivaan.

## Korrelaatio

Yksi termi, jonka ymmärtäminen on tärkeää, on **korrelaatiokerroin** annetuille X- ja Y-muuttujille. Hajontakaaviolla voit nopeasti havainnollistaa tämän kertoimen. Jos pisteet ovat kauniissa rivissä, korrelaatio on korkea, mutta jos pisteet ovat hajallaan kaikkialla X:n ja Y:n välillä, korrelaatio on matala.

Hyvä lineaarinen regressiomalli on sellainen, jonka korrelaatiokerroin on korkea (lähellä 1 eikä 0) vähimmän neliösumman regressiomallissa.

✅ Aja tämän oppitunnin mukana tuleva muistikirja ja tutki 'Kuukausi – Hinta' -hajontakaaviota. Vaikuttaako kurpitsan myyntimäärän kuukausien ja hintojen data korkean vai matalan korrelaation omaavalta, visuaalisen tulkintasi perusteella? Muuttuuko tämä, jos käytät hienojakoisempaa mittaria kuin `Kuukausi`, esim. *vuoden päivä* (eli päivien määrä vuodenvaihteesta lähtien)?

Alla olevassa koodissa oletamme, että data on puhdistettu ja saatu data frame nimeltä `new_pumpkins`, joka on samanlainen kuin seuraava:

ID | Kuukausi | PäiväVuodessa | Lajike | Kaupunki | Pakkaus | Alhainen hinta | Korkea hinta | Hinta
---|----------|---------------|--------|----------|---------|----------------|--------------|--------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 hehtolitran laatikot | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 hehtolitran laatikot | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 hehtolitran laatikot | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 hehtolitran laatikot | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 hehtolitran laatikot | 15.0 | 15.0 | 13.636364

> Koodin datan puhdistamiseen löydät [`notebook.ipynb`](notebook.ipynb)-tiedostosta. Olemme tehneet samat puhdistusvaiheet kuin edellisessä oppitunnissa ja laskeneet `DayOfYear`-sarakkeen seuraavan lausekkeen avulla:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Koska sinulla on nyt käsitys lineaarisen regression taustalla olevasta matematiikasta, luodaan regressiomalli nähdäksesi, voimmeko ennustaa, mikä kurpitsapakkaus tarjoaa parhaat kurpitsanhinnat. Joulun kurpitsatilaisuutta varten ostava saattaa haluta tämän tiedon optimoidakseen ostoksensa.

## Korrelatorin etsiminen

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klikkaa yllä olevaa kuvaa katsomaan lyhyt videoyhteenveto korrelaatiosta.

Viimeisestä oppitunnista olet varmaankin nähnyt, että eri kuukausien hintojen keskiarvot näyttävät tältä:

<img alt="Average price by month" src="../../../../translated_images/fi/barchart.a833ea9194346d76.webp" width="50%"/>

Tämä viittaa siihen, että jonkinlainen korrelaatio on olemassa, ja voimme yrittää kouluttaa lineaarisen regressiomallin ennustamaan suhdetta `Kuukausi` ja `Hinta` tai `PäiväVuodessa` ja `Hinta` välillä. Tässä on hajontakaavio, joka näyttää jälkimmäisen suhteen:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/fi/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Katsotaan, onko korrelaatiota `corr`-funktion avulla:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Näyttää siltä, että korrelaatio on melko pieni, -0.15 kuukauden mukaan ja -0.17 päivän mukaan, mutta voi olla jokin toinen tärkeä suhde. Näyttää siltä, että hinnat muodostavat eri klustereita eri kurpitsalajien mukaan. Vahvistaaksemme tämän hypoteesin piirretään jokainen kurpitsakategoria omalla värillään. Antamalla `ax`-parametri `scatter`-piirtotoiminnolle voimme piirtää kaikki pisteet samaan kuvaajaan:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/fi/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Tutkimuksemme viittaa siihen, että lajike vaikuttaa enemmän hintaan kuin myyntipäivämäärä. Näin näkyy myös palkkikaaviosta:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/fi/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Keskitymme tällä hetkellä vain yhteen kurpitsalajikkeeseen, 'pie type' -lajikkeeseen, ja katsotaan, mitä vaikutusta päivämäärällä on hintaan:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/fi/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Jos nyt lasket korrelaation `Hinnan` ja `PäiväVuodessa`-arvon välillä `corr`-funktiolla, saat jotain -0.27:n tienoilla – mikä tarkoittaa, että ennustemallin kouluttaminen on järkevää.

> Ennen lineaarisen regressiomallin kouluttamista on tärkeää varmistaa, että data on puhdasta. Lineaarinen regressio ei toimi hyvin puuttuvien arvojen kanssa, joten on järkevää poistaa kaikki tyhjät solut:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Toinen lähestymistapa olisi täyttää tyhjät arvot vastaavan sarakkeen keskiarvolla.

## Yksinkertainen lineaarinen regressio

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klikkaa yllä olevaa kuvaa katsomaan lyhyt videoyhteenveto lineaarisesta ja polynomiregressiosta.

Kouluttaaksemme lineaarisen regressiomallimme käytämme **Scikit-learn**-kirjastoa.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Aloitamme erottelemalla syötearvot (ominaisuudet) ja odotetun tuloksen (label) omiin numpy-taulukoihinsa:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Huomaa, että jouduimme tekemään `reshape`-muunnoksen syötteisiin, jotta Linear Regression -paketti ymmärtää ne oikein. Lineaarinen regressio odottaa 2-ulotteista taulukkoa syötteeksi, jossa jokainen taulukon rivi vastaa ominaisuusvektoria. Meillä on vain yksi syöte, joten tarvitaan N&times;1-muotoinen taulukko, missä N on datan koko.

Seuraavaksi jaamme datan koulutus- ja testidatasettiin, jotta voimme validoida mallimme koulutuksen jälkeen:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Lopuksi lineaarisen regressiomallin kouluttaminen tapahtuu kahdella koodirivillä. Määrittelemme `LinearRegression`-olion ja sovitamme sen dataan `fit`-metodilla:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

LinearRegression-objekti fitauksen jälkeen sisältää kaikki regressiokertoimet, joihin pääsee käsiksi .coef_-ominaisuuden kautta. Meidän tapauksessamme on vain yksi kerroin, jonka tulisi olla noin -0,017. Tämä tarkoittaa, että hinnat näyttävät laskevan hieman ajan myötä, mutta ei paljoa, noin 2 senttiä päivässä. Pääsemme käsiksi myös regressiokäyrän leikkauspisteeseen Y-akselin kanssa käyttämällä lin_reg.intercept_ -ominaisuutta - se on meidän tapauksessamme noin 21, mikä ilmaisee hinnan vuoden alussa.

Nähdäksemme, kuinka tarkka mallimme on, voimme ennustaa testidatan hinnat ja mitata sitten, kuinka lähellä ennusteemme ovat odotettuja arvoja. Tämä voidaan tehdä käyttäen neliöllisen keskiarvon neliöjuurivirhettä (RMSE), joka on kaikkien odotetun ja ennustetun arvon neliöllisten erotusten keskiarvon neliöjuuri.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```
 Virheemme näyttää olevan noin 2 pistettä, eli ~17%. Ei kovin hyvä. Toinen mallin laadun mittari on **määrityskerroin**, joka voidaan saada näin:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Jos arvo on 0, se tarkoittaa, että malli ei huomioi syötteitä ja toimii *huonoimpana lineaarisena ennustajana*, joka on yksinkertaisesti tuloksen keskiarvo. Arvo 1 tarkoittaa, että pystymme täydellisesti ennustamaan kaikki odotetut arvot. Meillä kerroin on noin 0,06, mikä on melko alhainen.

Voimme myös piirtää testidatan ja regressiokäyrän samaan kuvaajaan, jotta näemme paremmin, miten regressio toimii tapauksessamme:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/fi/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynominen regressio

Toinen lineaarisen regression tyyppi on polynominen regressio. Vaikka joskus muuttujien välillä on lineaarinen suhde - mitä suurempi kurpitsa tilavuudeltaan, sitä korkeampi hinta - joskus näitä suhteita ei voi esittää tasona tai suorana viivana.

✅ Tässä on [joitakin lisää esimerkkejä](https://online.stat.psu.edu/stat501/lesson/9/9.8) aineistosta, johon polynominen regressio sopii

Katso uudelleen suhdetta Päivämäärän ja Hinnan välillä. Näyttääkö tämä hajontakuvio siltä, että se pitäisi välttämättä analysoida suoralla viivalla? Eikö hinnat voi vaihdella? Tässä tapauksessa voit kokeilla polynomista regressiota.

✅ Polynomit ovat matemaattisia lausekkeita, jotka voivat sisältää yhden tai useamman muuttujan ja kertoimen

Polynominen regressio luo käyrän, joka istuu paremmin epälineaariseen dataan. Meidän tapauksessamme, jos lisäämme syötteisiin itseisarvoltaan neliöidyn DayOfYear-muuttujan, pystymme sovittamaan dataa parabolisella käyrällä, jolla on minimi tietyssä vuoden kohdassa.

Scikit-learn sisältää hyödyllisen [pipeline API:n](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) eri datankäsittelyvaiheiden yhdistämistä varten. **Pipeline** on ketju **estimaattoreita**. Meidän tapauksessamme luomme pipelineketjun, joka ensin lisää polynomiset piirteet malliin, ja sen jälkeen opettaa regression:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```
 Käyttäen PolynomialFeatures(2) tarkoittaa, että otamme mukaan kaikki toisen asteen polynomit syötteestä. Meidän tapauksessamme se tarkoittaa vain DayOfYear<sup>2</sup>, mutta jos on kaksi syötemuuttujaa X ja Y, tämä lisää X<sup>2</sup>, XY ja Y<sup>2</sup>. Voimme myös käyttää korkeampiasteisia polynomeja, jos haluamme.

Pipelinetä voi käyttää samoin kuin alkuperäistä LinearRegression-objektia, eli voimme fitata pipelinen ja sitten predictata saadaksemme ennusteita. Tässä kuvaaja, jossa testidata ja likimääräinen käyrä:

<img alt="Polynomial regression" src="../../../../translated_images/fi/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polynomista regressiota käyttäen saamme hieman pienemmän MSE:n ja korkeamman määrityskertoimen, mutta ei merkittävästi. Tarvitsemme mukaan muita piirteitä!

> Näet, että kurpitsan pienimmät hinnat ovat havaittavissa jossakin Halloweenin tienoilla. Miten selität tämän? 

🎃 Onneksi olkoon, olet juuri luonut mallin, joka voi auttaa ennustamaan piirakkakurpitsojen hintaa. Voit todennäköisesti toistaa saman menetelmän kaikille kurpistyyppilajikkeille, mutta se olisi työlästä. Opitaan nyt, miten kurpislajike otetaan mallissa huomioon!

## Kategorialliset piirteet

Ihanteellisessa maailmassa haluamme pystyä ennustamaan eri kurpislajikkeiden hinnat samalla mallilla. Kuitenkin Variety-sarake on hieman erilainen kuin esimerkiksi Month, koska se sisältää ei-numeerisia arvoja. Tällaisia sarakkeita kutsutaan **kategoriallisiksi**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Klikkaa yllä olevaa kuvaa nähdäksesi lyhyen videon kategoriapiirteiden käytöstä.

Tässä voit nähdä, miten keskihinta riippuu lajikkeesta:

<img alt="Average price by variety" src="../../../../translated_images/fi/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Ottaksemme lajikkeen huomioon, meidän tulee ensin muuntaa se numeeriseksi eli **enkoodata**. On useita tapoja tehdä tämä:

* Yksinkertainen **numeraalinen enkoodaus** rakentaa taulukon eri lajikkeista ja korvaa lajikenimen taulukon indeksillä. Tämä ei ole paras idea lineaarisessa regressiossa, koska lineaarinen regressio ottaa indeksin numeerisen arvon ja lisää sen tulokseen kertoimen kanssa kerrottuna. Meidän tapauksessamme suhde indeksiluvun ja hinnan välillä on selvästi epälineaarinen, vaikka indeksit järjestettäisiin tietyllä tavalla.
* **One-hot-enkoodaus** korvaa Variety-sarakkeen neljällä eri sarakkeella, yksi kullekin lajikkeelle. Jokainen sarake sisältää arvon 1 jos rivi kuuluu kyseiseen lajikkeeseen, ja muuten 0. Tämä tarkoittaa, että lineaarisessa regressiossa on neljä kerrointa, yksi kullekin kurpislajikkeelle, jotka vastaavat "aloitushintaa" (tai pikemminkin "lisähintaa") kyseiselle lajikkeelle.

Alla on koodi, jolla voimme one-hot enkoodata lajikkeen:

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

Kouluttaaksemme lineaarisen regression käyttäen one-hot enkoodattua lajiketta syötteenä, meidän tarvitsee vain alustaa X ja y -data oikein:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```
 Loput koodista on sama kuin mitä käytimme aiemmin LinearRegressionin opettamiseen. Jos kokeilet, näet, että keskimääräinen neliövirhe on suunnilleen sama, mutta saamme paljon korkeamman määrityskertoimen (~77%). Saadaksemme vieläkin tarkempia ennusteita voimme ottaa huomioon enemmän kategoriallisia piirteitä sekä numeerisia piirteitä, kuten Month tai DayOfYear. Saadaksemme yhden suuren piirteiden taulukon, voimme käyttää join-metodia:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```
 Tässä otamme lisäksi huomioon Cityn ja Package-tyypin, jolloin MSE on 2,84 (10%) ja määrityskerroin 0,94!

## Yhdistetään kaikki

Tehdäksemme parhaan mallin voimme käyttää yhdistettyä (one-hot enkoodattu kategoriallinen + numeerinen) dataa yllä olevasta esimerkistä yhdessä polynomisen regression kanssa. Tässä on koko koodi käyttöösi:

```python
# aseta harjoitusdata
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# tee harjoitus-testaus-jako
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# asenna ja kouluta putkisto
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# ennusta tulokset testidatalle
pred = pipeline.predict(X_test)

# laske MSE ja selitysaste
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```
 Tämä antaa meille parhaan määrityskertoimen lähes 97 %, ja MSE=2,23 (~8 % ennustvirhe).

| Malli | MSE | Määrityskerroin |
|-------|-----|---------------|
| `DayOfYear` Lineaarinen | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynominen | 2.73 (17.0%) | 0.08 |
| `Variety` Lineaarinen | 5.24 (19.7%) | 0.77 |
| Kaikki piirteet Lineaarinen | 2.84 (10.5%) | 0.94 |
| Kaikki piirteet Polynominen | 2.23 (8.25%) | 0.97 |

🏆 Hienoa työtä! Loit neljä regressiomallia yhdessä oppitunnissa ja paransit mallin laatua 97 %:iin. Regressio-osan lopussa opit logistisesta regressiosta luokitusten määrittämiseksi.

---
## 🚀Haaste

Testaa tässä muistikirjassa useampaa eri muuttujaa nähdäksesi, miten korrelaatio vastaa mallin tarkkuutta.

## [Luentotentin jälkeinen tietovisa](https://ff-quizzes.netlify.app/en/ml/)

## Kertaus & Itsestä opiskelua

Tässä oppitunnissa opimme lineaarisesta regression mallinnuksesta. On olemassa myös muita tärkeitä regressiotyyppejä. Lue Stepwise-, Ridge-, Lasso- ja Elasticnet-teknikoista. Hyvä kurssi syventymiseen on [Stanfordin statistiikan oppimisjakso](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tehtävä

[Rakenna malli](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Vastuuvapauslauseke**:  
Tämä asiakirja on käännetty käyttämällä tekoälypohjaista käännöspalvelua [Co-op Translator](https://github.com/Azure/co-op-translator). Vaikka pyrimme tarkkuuteen, ole ystävällinen ja huomioi, että automatisoiduissa käännöksissä saattaa esiintyä virheitä tai epätarkkuuksia. Alkuperäistä asiakirjaa sen omalla kielellä tulee pitää ensisijaisena lähteenä. Tärkeiden tietojen osalta suositellaan ammattimaista ihmiskäännöstä. Emme ole vastuussa mahdollisista väärinymmärryksistä tai virhetulkingoista, jotka johtuvat tämän käännöksen käytöstä.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->