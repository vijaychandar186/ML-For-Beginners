# Ehita regressioonimudel kasutades Scikit-learn'i: regressioon neljal moel

## Algaja märkus

Lineaarset regressiooni kasutatakse siis, kui soovime ennustada **numbrilist väärtust** (näiteks maja hind, temperatuur või müük).
See toimib, leides sirgjoone, mis kõige paremini esindab seost sisendomaduste ja väljundi vahel.

Selles õppetükis keskendume mõiste mõistmisele enne kui uurime keerukamaid regressioonitehnikaid.
![Lineaarne vs polünoomne regressioon infograafik](../../../../translated_images/et/linear-polynomial.5523c7cb6576ccab.webp)
> Infograafik autorilt [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Loengu-eelne viktoriin](https://ff-quizzes.netlify.app/en/ml/)

> ### [See õppetükk on saadaval R keeles!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Sissejuhatus

Nii kaugele oled uurinud, mis on regressioon, kasutades proovidataid kõrvitsahindade andmestikust, mida kasutame kogu selle õppetüki vältel. Sa oled ka visualiseerinud andmeid Matplotlibi abil.

Nüüd oled valmis süvenema sügavamalt regressioonisse masinõppes. Kuigi visualiseerimine aitab andmeid mõista, tuleb masinõppe tõeline jõud mudelite koolitamisest. Mudelid koolitatakse ajalooliste andmetega, et automaatselt tabada andmete seoseid, ja need võimaldavad prognoosida uusi tulemusi, mida mudel pole varem näinud.

Selles õppetükis õpid rohkem kahe regressioonitüübi kohta: _põhiline lineaarne regressioon_ ja _polünoomne regressioon_, koos mõne nende tehnika matemaatikaga. Need mudelid võimaldavad meil ennustada kõrvitsahindu sõltuvalt erinevatest sisendandmetest.

[![Masinõpe algajatele - Lineaarse regressiooni mõistmine](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "Masinõpe algajatele - Lineaarse regressiooni mõistmine")

> 🎥 Kliki pildil ülalpool, et vaadata lühike video ülevaade lineaarse regressiooni kohta.

> Kogu selle õppekava jooksul eeldame minimaalseid teadmisi matemaatikast ja püüame teha selle ligipääsetavaks teiste valdkondade tudengitele, seega pööra tähelepanu märkmetele, 🧮 kõrvalinfole, diagrammidele ja teistele õppimisvahenditele mõistmise hõlbustamiseks.

### Eelteadmised

Peaksid olema nüüd tuttav kõrvitsate andmete struktuuriga, mida me uurime. Selle leiad eellaadituna ja puhastatuna selle õppetüki _notebook.ipynb_ failist. Failis on kõrvitsahind kuvatud korvi kohta uues andmeraamis. Veendu, et suudaksid neid sülearvutieeskirju Visual Studio Code kernelites käivitada.

### Ettevalmistus

Meenutuseks, laadid neid andmeid, et esitada neile küsimusi.

- Millal on parim aeg kõrvitsaid osta?
- Millist hinda võin oodata väikeste kõrvitsakastide eest?
- Kas peaksin ostma neid poolkorvi kaupa või 1 1/9-korviku hulka?
Jätkame selle andmestiku uurimist.

Eelmises õppetükis lõid Pandase andmeraami ja täitsid selle osa originaalandmestikust, standardiseerides hinnad korvi kohta. Sellega suutsid koguda umbes 400 andmepunkti ja ainult sügiskuude kohta.

Vaata andmeid, mis on eellaaditud selle õppetüki kaasnevas sülearvutis. Andmed on eellaaditud ja esimene hajuvdiagramm joonistatud näitamaks kuuandmeid. Võime saada rohkem üksikasju andmete olemuse kohta, neid rohkem puhastades.

## Lineaarne regressioonijoon

Nagu õppisid õppetükis 1, on lineaarse regressiooni eesmärk joonistada joon, mis:

- **Näitab muutujate seoseid**. Näitab muutujate omavahelist seost
- **Teeb ennustusi**. Teeb täpseid ennustusi, kus uus andmepunkt joonel paikneb.

Tavaline on kasutada **väikseimruutude regressiooni**, et seda tüüpi joon joonistada. Mõiste "väikseim ruut" viitab protsessile, mille käigus minimeeritakse kogu vea summa mudelis. Iga andmepunkti jaoks mõõdame vertikaalse kauguse (nn residuaal) tegeliku punkti ja meie regressioonijoone vahel.

Me ruudutame need kaugused kahest põhjusest:

1. **Suurus, mitte suund:** Soovime käsitleda viga -5 samaväärsena veaga +5. Ruudutamine muudab kõik väärtused positiivseks.

2. **Outlierite karistamine:** Ruudutamine annab suurematele vigadele suurema kaalu, sundides joont jääma kaugel olevate punktide lähedusse.

Seejärel liidame kõik need ruudutatud väärtused kokku. Meie eesmärk on leida see konkreetne joon, kus see summa on minimaalne – seega nimi "väikseim ruut".

> **🧮 Näita matemaatikat**  
>  
> Seda joont, mida nimetatakse _parima sobivuse jooneks_, saab väljendada [valemiga](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` on "selgitav muutuja". `Y` on "sõltuv muutuja". Joonise tõus on `b` ja `a` on y-telgi lõikepunkt, mis tähendab väärtust `Y`, kui `X = 0`. 
>
>![tõusu arvutus](../../../../translated_images/et/slope.f3c9d5910ddbfcf9.webp)
>
> Esiteks arvuta tõus `b`. Infograafik autorilt [Jen Looper](https://twitter.com/jenlooper)
>
> Teisisõnu ja viidates meie kõrvitsate andmete algsele küsimusele: "prognoosi kõrvitsa hind korvi kohta kuude kaupa", võib `X` tähistada hinda ja `Y` müügikuud.
>
>![täienda valemit](../../../../translated_images/et/calculation.a209813050a1ddb1.webp)
>
> Arvuta Y väärtus. Kui maksad umbes 4 dollarit, peab olema aprill! Infograafik autorilt [Jen Looper](https://twitter.com/jenlooper)
>
> Matemaatika, mis arvutab joone, peab näitama joone tõusu, mis sõltub ka lõikepunktist ehk kus `Y` paikneb kui `X = 0`.
>
> Selle väärtuse arvutusmeetodi võid vaadata veebisaidil [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Samuti külasta [Väikseima ruudu kalkulaatorit](https://www.mathsisfun.com/data/least-squares-calculator.html), et näha, kuidas arvude väärtused joont mõjutavad.

## Korrelatsioon

Veel üks mõiste, mida mõista, on **korrelatsioonikordaja** antud X ja Y muutujate vahel. Hajuvdiagrammi abil saad seda kiiresti visualiseerida. Diagramm, kus andmepunktid on ilusti joonel, näitab kõrget korrelatsiooni, aga hajuv diagramm, kus andmepunktid on kõikjal X ja Y vahel, näitab madalat korrelatsiooni.

Hea lineaarne regressioonimudel on selline, millel on kõrge (lähemal 1 kui 0) korrelatsioonikordaja, kasutades väikseimruutude regressioonimeetodit koos regressioonijoonega.

✅ Käivita selle õppetüki kaasas olev sülearvuti ja vaata kuhjumist kuu ja hinna vahel. Kas andmed, mis seovad kuu ja kõrvitsahinna müüki, tunduvad visuaalse hinnangu põhjal kõrge või madala korrelatsiooniga? Kas see muutub, kui kasutad üksikasjalikumat mõõdet kui `Month`, nt *aasta päeva* (st päevade arv aasta algusest)?

Alljärgnevas koodis eeldame, et oleme andmed puhastanud ja saame andmeraami nimega `new_pumpkins`, mis sarnaneb järgmisele:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Andmete puhastamise kood on saadaval [`notebook.ipynb`](notebook.ipynb) failis. Oleme teinud samad puhastusetapid nagu eelnevas õppetükis ja arvutanud `DayOfYear` veeru järgmise avaldisega:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Nüüd kui sul on arusaam lineaarse regressiooni matemaatikast, loome regressioonimudeli, et näha, kas suudame ennustada, millisel kõrvitsapakendil on parim hind. Keegi, kes ostab kõrvitsaid püha kõrvitsapeenra jaoks, võib seda infot vajada, et oma ostusid optimeerida.

## Korrelatsiooni otsimine

[![Masinõpe algajatele - korrelatsiooni otsimine: võti lineaarse regressiooni jaoks](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "Masinõpe algajatele - korrelatsiooni otsimine: võti lineaarse regressiooni jaoks")

> 🎥 Kliki pildil ülalpool, et vaadata lühike video ülevaade korrelatsioonist.

Eelmises õppetükis nägid ilmselt, et keskmine hind kuude lõikes näeb välja selline:

<img alt="Keskmine hind kuude lõikes" src="../../../../translated_images/et/barchart.a833ea9194346d76.webp" width="50%"/>

See viitab sellele, et peaks olema mingi korrelatsioon ja saame proovida koolitada lineaarse regressiooni mudelit, et prognoosida seost `Month` ja `Price` vahel või `DayOfYear` ja `Price` vahel. Järgnevalt on hajuvdiagramm, mis näitab viimast seost:

<img alt="Hajuvdiagramm: hind versus aasta päev" src="../../../../translated_images/et/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Vaatame, kas korrelatsioon olemas on, kasutades `corr` funktsiooni:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Tundub, et korrelatsioon on üsna väike, -0.15 kuu järgi ja -0.17 kuupäeva järgi, aga võib olla teine oluline seos. Näib, et on erinevad hinnaklastrid eri kõrvitsatüüpide jaoks. Selle hüpoteesi kinnitamiseks joonistame iga kategooria erinevas värvis. Edastades `scatter` funktsioonile `ax` parameetri, saame joonistada kõik punktid samale graafikule:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Hajuvdiagramm: hind versus aasta päev värvilinea" src="../../../../translated_images/et/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Uuring viitab, et sort mõjutab hinda rohkem kui müügi kuupäev. Seda näeme ka tulpdiagrammil:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Tulpdiagramm hinna ja sorti kohta" src="../../../../translated_images/et/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Jätkame esialgu ainult ühe kõrvitsatüübi, 'pie type', uurimisega ja vaatame, kuidas müügikuupäev hindadele mõjub:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Hajuvdiagramm hind versus aasta päev" src="../../../../translated_images/et/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Kui nüüd arvutada korrelatsioon `Price` ja `DayOfYear` vahel `corr` funktsiooniga, saame midagi sellist nagu `-0.27` - mis tähendab, et prognoosimudeliga koolitamine on mõistlik.

> Enne lineaarse regressioonimudeli koolitamist on oluline veenduda, et andmed on puhastatud. Lineaarne regressioon ei tööta hästi puuduvate väärtustega, seega on mõistlik need tühjad lahtrid eemaldada:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Teine lähenemine oleks need puuduolevad väärtused täita vastava veeru keskmiste väärtustega.

## Lihtne lineaarne regressioon

[![Masinõpe algajatele - lineaarne ja polünoomne regressioon Scikit-learniga](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "Masinõpe algajatele - lineaarne ja polünoomne regressioon Scikit-learniga")

> 🎥 Kliki pildil ülalpool, et vaadata lühike video ülevaade lineaarse ja polünoomse regressiooni kohta.

Lineaarse regressioonimudeli koolitamiseks kasutame **Scikit-learn**i teeki.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Alustame sisendväärtuste (omaduste) ja ootuspärase väljundi (sildi) eraldamisest eraldi numpy massiividesse:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Märka, et pidime kasutama `reshape` meetodit sisendandmetel, et Linear Regression pakett mõistaks seda õigesti. Lineaarne regressioon ootab 2-maatriksit sisendina, kus iga rida on vektor sisendomadustest. Kuna meil on ainult üks sisend, vajame N×1 kujuga massiivi, kus N on andmestiku suurus.

Seejärel tuleb andmestik jagada treening- ja testandmestikeks, et saaksime mudelit pärast koolitamist valideerida:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Lõpuks võtab lineaarse regressioonimudeli treenimine vaid kaks koodirida. Määratleme `LinearRegression` objekti ning sobitame selle meie andmetega `fit` meetodi abil:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression` objekt pärast `fit`-imist sisaldab regressiooni kõiki koefitsiente, millele saab ligi `.coef_` omaduse kaudu. Meie puhul on ainult üks koefitsient, mis peaks olema umbes `-0.017`. See tähendab, et hinnad näivad aja jooksul veidi langevat, kuid mitte väga palju, umbes 2 senti päevas. Meile on ka võimalik juurdepääs regressiooni lõikepunktile Y-teljel, kasutades `lin_reg.intercept_` - see on meie puhul umbes `21`, mis näitab hinna alguses aasta alguses.

Selleks, et näha, kui täpne meie mudel on, võime prognoosida hindu testiandmestikul ja siis mõõta, kui lähedal meie ennustused on oodatud väärtustele. Seda saab teha ruutkeskmise vea (RMSE) mõõdiku abil, mis on kõigi ruutude erinevuste keskmise ruutjuur oodatud ja ennustatud väärtuste vahel.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Meie viga paistab olevat umbes 2 punkti, mis on ~17%. Mitte väga hea. Mudeli kvaliteedi teine näitaja on **määramise koefitsient**, mida saab saada järgmiselt:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Kui väärtus on 0, tähendab see, et mudel ei arvesta sisendiandmeid ja käitub kui *kõige halvem lineaarne ennustaja*, mis on lihtsalt tulemuse keskmine väärtus. Väärtus 1 tähendab, et me suudame täiuslikult ennustada kõiki oodatud väljundeid. Meie puhul on koefitsient umbes 0.06, mis on üsna madal.

Võime ka joonistada testandmed koos regressioonijoonega, et paremini näha, kuidas regressioon meie juhul töötab:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/et/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polünoomne regressioon

Teine lineaarse regressiooni tüüp on polünoomne regressioon. Kuigi mõnikord on muutujate vahel lineaarne seos - kui kõrvitsa maht suureneb, tõuseb hind - vahel ei saa neid seoseid joonistada tasapinnana või sirgjoonena.

✅ Siin on [veel mõned näited](https://online.stat.psu.edu/stat501/lesson/9/9.8) andmetest, mille jaoks võiks sobida polünoomne regressioon

Vaadake uuesti suhet kuupäeva ja hinna vahel. Kas see hajuvusdiagramm peaks tingimata olema analüüsitud sirgjoonena? Kas hinnad ei saa kõikuda? Sellisel juhul võite proovida polünoomset regressiooni.

✅ Polünoomid on matemaatilised avaldised, mis võivad koosneda ühest või mitmest muutujast ja koefitsiendist

Polünoomne regressioon loob kõverjoone, mis sobib paremini mitte-lineaarsete andmetega. Meie puhul, kui lisame sisendandmetesse ruudus oleva `DayOfYear` muutuja, peaksime suutma sobitada andmed paraboolkõveraga, millel on teatud aasta jooksul minimaalne punkt.

Scikit-learn sisaldab kasulikku [torujuhtme (pipeline) API-t](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline), et ühendada erinevad andmetöötlusetapid. **Torujuhtme** moodustab **estimatsioonide** ahel. Meie puhul loome torujuhtme, mis esmalt lisab polünoomsed tunnused mudelile ja siis treenib regressiooni:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

`PolynomialFeatures(2)` kasutamine tähendab, et kaasame kõik teise astme polünoomid sisendandmetest. Meie puhul tähendab see vaid `DayOfYear`<sup>2</sup>, aga kahe sisendmuutuja X ja Y korral lisab see X<sup>2</sup>, XY ja Y<sup>2</sup>. Võime ka kasutada kõrgema astme polünoome, kui soovime.

Torujuhtmeid võib kasutada samamoodi nagu algset `LinearRegression` objekti, st võime `fit` torujuhtme ja seejärel kasutada `predict`, et saada ennustustulemused. Siin on graafik, mis näitab testiandmeid ja ligikaudset kõverat:

<img alt="Polynomial regression" src="../../../../translated_images/et/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polünoomse regressiooni kasutades saame veidi madalama MSE ja kõrgema määramise, kuid mitte oluliselt. Peame arvesse võtma ka muid tunnuseid!

> Näete, et madalaimad kõrvitsahinnad esinevad kuskil Halloween’i ajal. Kuidas seda seletate? 

🎃 Palju õnne, just lõite mudeli, mis aitab prognoosida pirukakõrvitsate hinda. Tõenäoliselt saate sama protseduuri korrata kõigi kõrvitsatüüpide puhul, kuid see oleks tüütu. Õpime nüüd, kuidas mudelis arvesse võtta kõrvitsatüüpi!

## Kategoorilised tunnused

Ideaalis tahame suuta erinevate kõrvitsatüüpide hindu ennustada sama mudeli abil. Kuid `Variety` veerg on mõnevõrra erinev veergudest nagu `Month`, sest see sisaldab mittenumerilisi väärtusi. Selliseid veerge nimetatakse **kategoorilisteks**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Klõpsake ülaloleval pildil, et vaadata lühivideot kategooriliste tunnuste kasutamisest.

Siin näete, kuidas keskmine hind sõltub sordist:

<img alt="Average price by variety" src="../../../../translated_images/et/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Sordi arvestamiseks peame esmalt selle teisendama numbriliseks, ehk **kodeerima**. Selleks on mitu võimalust:

* Lihtne **numbriline kodeerimine** loob tabeli erinevatest sortidest ja seejärel asendab sordinime indeksiga selles tabelis. See pole lineaarse regressiooni puhul parim mõte, sest lineaarne regressioon võtab indeksinumbri tegeliku numbrilise väärtuse ja lisab selle tulemile, korrutades selle mõne koefitsiendiga. Meie puhul on seos indeksinumbri ja hinna vahel selgelt mittelineaarne, isegi kui tagada indeksite spetsiifiline järjekord.
* **Ühe-kuuma kodeerimine (one-hot encoding)** asendab `Variety` veeru nelja erineva veeruga, iga kõrvitsasordi jaoks eraldi. Igas veerus on `1`, kui vastaval real on see sort, ja muidu `0`. See tähendab, et lineaarse regressiooni puhul on neli koefitsienti, üks iga kõrvitsatüübi kohta, mis vastutab selle sordi "algushinna" (või pigem "lisahinna") eest.

Allolev kood näitab, kuidas sort ühekoodina kodeerida:

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

Lineaarse regressiooni treenimiseks, kasutades ühe-kuuma kodeeritud sorti sisendina, peame lihtsalt õigesti initsialiseerima `X` ja `y` andmed:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Ülejäänud kood on sama, mida kasutasime ees lineaarse regressiooni treenimiseks. Kui proovite, näete, et ruutkeskmine viga on umbes sama, kuid saame palju kõrgema määramise koefitsiendi (~77%). Veelgi täpsemate ennustuste saamiseks võime lisada ka teisi kategoorilisi tunnuseid ja numbrilisi tunnuseid nagu `Month` või `DayOfYear`. Et saada üks suur tunnuste massiiv, võime kasutada `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Siin arvestame ka `City` ja `Package` tüüpi, mis annab meile MSE 2.84 (10%) ja määramise 0.94!

## Kõige kokku panek

Parima mudeli tegemiseks võime kasutada kombineeritud (ühe-kuuma kodeeritud kategoorilised + numbrilised) andmeid eelmisest näitest koos polünoomse regressiooniga. Siin on mugavaks kasutamiseks kogu kood:

```python
# seadista treeningandmed
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# tee treening- ja testandmete jagamine
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# seadista ja treeni andmevoog
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# ennusta tulemused testandmete jaoks
pred = pipeline.predict(X_test)

# arvuta keskmine ruutviga ja määramise koefitsient
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

See peaks andma peaaegu 97% määramise koefitsiendi ja MSE=2.23 (~8% prognoosiviga).

| Mudel | MSE | Määramine |
|-------|-----|-----------|
| `DayOfYear` lineaarne | 2.77 (17.2%) | 0.07 |
| `DayOfYear` polünoomne | 2.73 (17.0%) | 0.08 |
| `Variety` lineaarne | 5.24 (19.7%) | 0.77 |
| Kõik tunnused lineaarne | 2.84 (10.5%) | 0.94 |
| Kõik tunnused polünoomne | 2.23 (8.25%) | 0.97 |

🏆 Väga tubli! Sa lõid ühe õppetunni jooksul neli regressioonimudelit ja parandasid mudeli kvaliteeti 97%-ni. Regressiooni lõpus peatükis õpid ka logistilise regressiooni kategooriate määramiseks.

---
## 🚀Väljakutse

Testeeri selles märkmikus mitut erinevat muutujat ja vaata, kuidas korrelatsioon mõjutab mudeli täpsust.

## [Loengu järel test](https://ff-quizzes.netlify.app/en/ml/)

## Ülevaade ja iseseisev õppimine

Selles õppetükis õppisime lineaarse regressiooni kohta. On ka teisi olulisi regressiooniliike. Loe stepwise, ridge, lasso ja elasticnet tehnikate kohta. Hea kursus õppimiseks on [Stanfordi statistikõppe kursus](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning).

## Kodune ülesanne 

[Ehita mudel](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Vastutusest loobumine**:  
See dokument on tõlgitud kasutades AI tõlketeenust [Co-op Translator](https://github.com/Azure/co-op-translator). Kuigi püüame täpsust, palun arvestage, et automaatsed tõlked võivad sisaldada vigu või ebatäpsusi. Originaaldokument selle emakeeles tuleks pidada autoriteetseks allikaks. Kriitilise informatsiooni puhul soovitatakse kasutada professionaalset inimtõlget. Me ei vastuta selle tõlkega seotud võimalike arusaamatuste või valesti tõlgenduste eest.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->