# Sukurkite regresijos modelį naudojant Scikit-learn: keturi regresijos būdai

## Pradedančiojo pastaba

Linijinė regresija naudojama tada, kai norime prognozuoti **skaitinę reikšmę** (pvz., namo kainą, temperatūrą ar pardavimus).
Ji veikia ieškant tiesės, kuri geriausiai atspindi ryšį tarp įvesties požymių ir išvesties.

Šioje pamokoje daugiausia dėmesio skirsime koncepcijos supratimui prieš nagrinėjant pažangesnes regresijos technikas.
![Linear vs polynomial regression infographic](../../../../translated_images/lt/linear-polynomial.5523c7cb6576ccab.webp)
> Infografika iš [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Priešpaskaitos testas](https://ff-quizzes.netlify.app/en/ml/)

> ### [Ši pamoka prieinama ir R kalba!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Įvadas

Iki šiol jau tyrinėjote, kas yra regresija, naudodamiesi pavyzdiniais duomenimis iš moliūgų kainų duomenų rinkinio, kurį naudosime visos pamokos metu. Taip pat jį vizualizavote naudodami Matplotlib.

Dabar esate pasiruošę gilintis į regresiją mašininio mokymosi srityje. Nors vizualizacija leidžia suprasti duomenis, tikroji mašininio mokymosi galia yra modelių _mokymas_. Modeliai yra mokomi pagal istoriniai duomenys, kad automatiškai aptiktų duomenų priklausomybes ir leistų prognozuoti rezultatus naujiems, modeliui nematytiems duomenims.

Šioje pamokoje sužinosite daugiau apie du regresijos tipus: _pagrindinę linijinę regresiją_ ir _polinominę regresiją_, kartu su kai kuriais šių technikų matematiniu pagrindu. Šie modeliai leis prognozuoti moliūgų kainas, atsižvelgiant į skirtingus įvesties duomenis.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Spustelėkite aukščiau esantį paveikslėlį, norėdami peržiūrėti trumpą vaizdo įrašą apie linijinę regresiją.

> Visos šios mokymo programos metu pradedame nuo minimalių matematikos žinių, siekdami, kad ji būtų prieinama studentams iš kitų sričių, todėl atkreipkite dėmesį į pastabas, 🧮 išryškinimus, diagramas ir kitas mokymosi priemones.

### Priešžinios

Turėtumėte jau būti susipažinę su moliūgų duomenų struktūra, kurią nagrinėjame. Juos rasite iš anksto įkeltus ir išvalytus šiame pamokos _notebook.ipynb_ faile. faile moliūgų kaina pateikiama už sklypą naujame duomenų rinkinyje. Įsitikinkite, kad galite paleisti šiuos užrašų knygeles Visual Studio Code branduoliuose.

### Paruošimas

Primename, kad įkeliate šiuos duomenis, kad galėtumėte užduoti klausimus apie juos.

- Kada geriausia pirkti moliūgus?
- Kokios kainos galima tikėtis už dėžę miniatiūrinių moliūgų?
- Ar juos verta pirkti pusės sklypo krepšyje, ar vieno ir vienos devintosios sklypo dėžėje?
Toliau gilinkimės į šiuos duomenis.

Ankstesnėje pamokoje sukūrėte Pandų duomenų rėmelį ir užpildėte jį dalimi pradinio duomenų rinkinio, standartizuodami kainas pagal sklypą. Tačiau tai leido užfiksuoti tik apie 400 duomenų taškų ir tik rudens mėnesiams.

Pažvelkite į duomenis, kuriuos iš anksto įkėlėme šios pamokos knygoje. Duomenys yra įkelti ir pavaizduota pradinė paskirstymo diagrama, rodanti mėnesių duomenis. Galbūt galime gauti šiek tiek daugiau informacijos apie duomenų prigimtį, juos dar labiau išvalydami.

## Linijinės regresijos tiesė

Kaip sužinojote 1 pamokoje, linijinės regresijos tikslas yra nubrėžti tiesę, kad galėtume:

- **Rodyti kintamųjų santykius**. Parodyti santykį tarp kintamųjų
- **Daryti prognozes**. Tiksliai prognozuoti, kur nukris naujas taškas, palyginti su ta linija.

Įprasta naudoti **mažiausių kvadratų regresiją** tokio tipo linijai nubrėžti. Terminas „mažiausių kvadratų“ reiškia procesą, kai sumažinamas bendras modelio klaidos dydis. Kiekvienam duomenų taškui matuojamas vertikalus atstumas (vadinamas likučiu) tarp tikro taško ir mūsų regresijos linijos.

Šiuos atstumus pakeliame kvadratu dėl dviejų pagrindinių priežasčių:

1. **Dydis svarbiau už kryptį:** Norime, kad klaida -5 būtų tokia pat reikšminga kaip ir klaida +5. Keldami kvadratu visa paverčiame teigiama.

2. **Išskirtinių reikšmių bausmė:** Kvadratu pakeldami didesnė klaida sveria labiau, priversdami tiesę artėti prie tolimų taškų.

Tada sudedame visas pakeltas kvadratu klaidas. Mūsų tikslas yra rasti tokią tiesę, kurioje ši suma būtų mažiausia (mažiausia įmanoma reikšmė) – todėl pavadinimas „mažiausių kvadratų“.

> **🧮 Parodykite man matematiką** 
> 
> Ši linija, vadinama _geriausiai atitinkančia linija_, gali būti išreikšta [lygtimi](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` yra „paaiškinamasis kintamasis“. `Y` yra „priklausomas kintamasis“. Linijos nuolydis yra `b`, o `a` yra y-kirčio reikšmė, kuri nurodo `Y` reikšmę, kai `X = 0`.
>
>![calculate the slope](../../../../translated_images/lt/slope.f3c9d5910ddbfcf9.webp)
>
> Pirmiausia apskaičiuokite nuolydį `b`. Infografika iš [Jen Looper](https://twitter.com/jenlooper)
>
> Kitais žodžiais tariant, ir remiantis mūsų moliūgų duomenų pradiniu klausimu: „prognozuoti moliūgo kainą už sklypą pagal mėnesį“, `X` būtų kaina, o `Y` – pardavimo mėnuo.
>
>![complete the equation](../../../../translated_images/lt/calculation.a209813050a1ddb1.webp)
>
> Apskaičiuokite `Y` reikšmę. Jei mokate apie 4 dolerius, tai turi būti balandis! Infografika iš [Jen Looper](https://twitter.com/jenlooper)
>
> Formulė, kuri apskaičiuoja liniją, turi parodyti linijos nuolydį, kuris taip pat priklauso nuo kirčio, arba kur yra `Y`, kai `X = 0`.
>
> Galite pamatyti šios vertės skaičiavimo metodą svetainėje [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Taip pat apsilankykite [šiame mažiausių kvadratų skaičiuoklyje](https://www.mathsisfun.com/data/least-squares-calculator.html), norėdami pamatyti, kaip skaičių vertės veikia liniją.

## Koreliacija

Dar vienas suprantamas terminas yra **koreliacijos koeficientas** tarp pasirinktų `X` ir `Y` kintamųjų. Naudodami sklaidos diagramą galite greitai vizualizuoti šį koeficientą. Taškai, išsidėstę tvarkingai linijoje, rodo aukštą koreliaciją, o taškai, išmėtyti plačiai tarp X ir Y, rodo mažą koreliaciją.

Geras linijinės regresijos modelis bus tas, kuris turi aukštą (artimą 1, o ne 0) koreliacijos koeficientą, naudojant mažiausių kvadratų regresijos metodą su regresijos linija.

✅ Paleiskite šios pamokos užrašų knygą ir pažiūrėkite į mėnesio ir kainos sklaidos diagramą. Ar pagal jūsų sklaidos diagramos vizualinį įvertinimą moliūgų pardavimų duomenys, susiejantys mėnesį su kaina, atrodo turintys aukštą ar žemą koreliaciją? Ar tai pasikeičia, jei naudotumėte smulkesnį matavimą, pvz., *metų dienos* (t. y. dienų skaičių nuo metų pradžios)?

Žemiau pateiktame kode laikysimės, kad duomenys yra išvalyti ir turime duomenų rėmelį `new_pumpkins`, panašų į šį:

ID | Mėnuo | MetųDiena | Veislė | Miestas | Pakuotė | Žemiausia Kaina | Aukščiausia Kaina | Kaina  
---|-------|-----------|---------|---------|---------|----------------|-------------------|------
70 | 9     | 267       | PIETIPAS | BALTIMORE | 1 1/9 sklypo dėžės | 15.0           | 15.0              | 13.636364  
71 | 9     | 267       | PIETIPAS | BALTIMORE | 1 1/9 sklypo dėžės | 18.0           | 18.0              | 16.363636  
72 | 10    | 274       | PIETIPAS | BALTIMORE | 1 1/9 sklypo dėžės | 18.0           | 18.0              | 16.363636  
73 | 10    | 274       | PIETIPAS | BALTIMORE | 1 1/9 sklypo dėžės | 17.0           | 17.0              | 15.454545  
74 | 10    | 281       | PIETIPAS | BALTIMORE | 1 1/9 sklypo dėžės | 15.0           | 15.0              | 13.636364

> Duomenų valymo kodas pateiktas [`notebook.ipynb`](notebook.ipynb). Atlikome tokius pačius valymo veiksmus kaip ankstesnėje pamokoje ir apskaičiavome `DayOfYear` stulpelį naudodami šią išraišką: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Dabar, kai suprantate linijinės regresijos matematiką, sukurkime regresijos modelį, kad pamatytume, ar galime prognozuoti, kuri moliūgų pakuotė turės geriausias kainas. Moliūgų pirkėjas, norintis sukurti moliūgų dekoracijų kampelį šventėms, gali norėti šios informacijos, kad optimizuotų moliūgų pirkimą.

## Ieškome koreliacijos

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Spustelėkite aukščiau esantį paveikslėlį, norėdami peržiūrėti trumpą vaizdo įrašą apie koreliaciją.

Iš ankstesnės pamokos tikriausiai matėte, kad vidutinė kaina skirtingais mėnesiais atrodo maždaug taip:

<img alt="Average price by month" src="../../../../translated_images/lt/barchart.a833ea9194346d76.webp" width="50%"/>

Tai leidžia manyti, kad turėtų būti tam tikra koreliacija, ir galime pabandyti apmokyti linijinį regresijos modelį, prognozuojant santykį tarp `Month` ir `Price` arba tarp `DayOfYear` ir `Price`. Žemiau pateikta sklaidos diagrama rodo pastarąjį ryšį:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/lt/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Pažiūrėkime, ar yra koreliacija, naudodami funkciją `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Atrodo, kad koreliacija yra gana maža, -0.15 pagal `Mėnesį` ir -0.17 pagal `Metų dieną`, tačiau gali būti kita svarbi priklausomybė. Atrodo, kad yra skirtingų kainų grupių, atitinkančių skirtingas moliūgų veisles. Norint patvirtinti šią hipotezę, nubraižykime kiekvieną moliūgų kategoriją skirtinga spalva. Pateikdami parametrą `ax` funkcijai `scatter` galime nubrėžti visus taškus viename grafike:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/lt/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Mūsų tyrimas rodo, kad veislė daro didesnį poveikį bendrai kainai nei tikrasis pardavimo laikas. Tai matosi ir stulpeline diagramoje:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/lt/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Šiuo metu sutelkime dėmesį tik į vieną moliūgų veislę, 'pie type', ir pažiūrėkime, kokį poveikį datą turi kaina:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/lt/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Jei dabar apskaičiuosime koreliaciją tarp `Price` ir `DayOfYear`, naudodami funkciją `corr`, gausime apie `-0.27` - tai reiškia, kad verta mokyti prognozinį modelį.

> Prieš mokant linijinį regresijos modelį svarbu įsitikinti, kad mūsų duomenys yra švarūs. Linijinė regresija blogai veikia su trūkstamomis reikšmėmis, todėl verta atsikratyti visų tuščių langelių:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Kita galimybė būtų užpildyti trūkstamas reikšmes vidutinėmis tos stulpelio reikšmėmis.

## Paprasta linijinė regresija

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Spustelėkite aukščiau esantį paveikslėlį, norėdami peržiūrėti trumpą vaizdo įrašą apie linijinę ir polinominę regresiją.

Norėdami apmokyti mūsų linijinį regresijos modelį, naudosime **Scikit-learn** biblioteką.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Pradėsime atskirdami įvesties reikšmes (požymius) ir tikėtiną išvestį (etiketę) į atskirus numpy masyvus:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Atkreipkite dėmesį, kad turėjome naudoti metodą `reshape` su įvesties duomenimis, kad linijinės regresijos paketas teisingai juos suprastų. Linijinė regresija tikisi 2D masyvo kaip įvesties, kur kiekviena masyvo eilutė atitinka požymių vektorių. Mūsų atveju, kadangi turime tik vieną įvestį – mums reikia masyvo formos N×1, kur N yra duomenų rinkinio dydis.

Tuomet turime padalyti duomenis į mokymo ir testavimo rinkinius, kad vėliau patikrintume modelio veikimą:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Galiausiai, tikrasis linijinės regresijos modelio apmokymas užtrunka tik dvi kodo eilutes. Sukuriame `LinearRegression` objektą ir pritaikome jį mūsų duomenims naudodami metodą `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression` objektas po `fit` treniravimo turi visas regresijos koeficientus, kuriuos galima pasiekti naudojant `.coef_` savybę. Mūsų atveju yra tik vienas koeficientas, kuris turėtų būti apie `-0.017`. Tai reiškia, kad kainos, atrodo, šiek tiek krinta su laiku, bet ne per daug, apie 2 centus per dieną. Taip pat galime pasiekti regresijos sankirtos su Y ašimi tašką naudodami `lin_reg.intercept_` – mūsų atveju jis bus apie `21`, rodantis kainą metų pradžioje.

Kad pamatytume, kaip tikslus mūsų modelis, galime prognozuoti kainas testiniame duomenų rinkinyje ir tada išmatuoti, kiek mūsų prognozės yra arti tikėtinų reikšmių. Tai galima padaryti naudojant šaknies kvadratinės vidutinės klaidos (RMSE) metriką, kuri yra visų kvadratinių skirtumų tarp tikėtinos ir prognozuotos reikšmės vidurkio šaknis.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Mūsų klaida atrodo apie 2 taškus, tai yra ~17%. Ne per gera. Kitas modelio kokybės rodiklis yra **determinacijos koeficientas**, kurį galima gauti taip:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
 Jei reikšmė yra 0, tai reiškia, kad modelis neatsižvelgia į įvesties duomenis ir veikia kaip *blogiausias tiesinis prognozuotojas*, kuris tiesiog yra rezultatų vidurkis. 1 reikšmė reiškia, kad galime tobulai prognozuoti visus tikėtinus rezultatus. Mūsų atveju koeficientas yra apie 0.06, kas yra gana žema reikšmė.

Taip pat galime pavaizduoti testinius duomenis kartu su regresijos linija, kad geriau matytume, kaip regresija veikia mūsų atveju:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/lt/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polinominė regresija

Kitas tiesinės regresijos tipas yra polinominė regresija. Nors kartais tarp kintamųjų yra tiesinis ryšys – kuo didesnė moliūgo apimtis, tuo didesnė kaina – kartais šių ryšių negalima nubraižyti kaip plokštumos ar tiesės.

✅ Štai [dar keletas pavyzdžių](https://online.stat.psu.edu/stat501/lesson/9/9.8) duomenų, kuriuose galima naudoti polinominę regresiją.

Dar kartą pažiūrėkite į ryšį tarp Datos ir Kainos. Ar šis sklaidos grafikas tikrai turėtų būti analizuojamas tiesės pagalba? Ar kainos negali svyruoti? Tokiu atveju galima išbandyti polinominę regresiją.

✅ Polinomai yra matematiniai reiškiniai, galintys susidaryti iš vieno ar daugiau kintamųjų ir koeficientų.

Polinominė regresija sukuria išlenktą liniją, kad geriau atitiktų netiesinius duomenis. Mūsų atveju, jei įvesime kvadratinį `DayOfYear` kintamąjį, galėsime pritaikyti parabolinį kreivę, kuri turės minimumą tam tikru metų momentu.

Scikit-learn turi naudingą [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline), leidžiantį sujungti kelis duomenų apdorojimo žingsnius. **Pipeline** yra **vertintojų** grandinė. Mūsų atveju sukursime pipeline, kuris pirmiausia pridės polinominius bruožus modelyje, o tada išmokys regresiją:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Naudojant `PolynomialFeatures(2)` reiškia, kad naudosime visus antrinės laipsnio polinomus iš įvesties duomenų. Mūsų atveju tai reikš tik `DayOfYear`<sup>2</sup>, tačiau turint du įvesties kintamuosius, pvz., X ir Y, bus pridėta X<sup>2</sup>, XY ir Y<sup>2</sup>. Taip pat galime naudoti aukštesnių laipsnių polinomus, jei norime.

Pipeline galima naudoti taip pat kaip ir pradinį `LinearRegression` objektą, t.y. galime `fit` treniruoti pipeline ir tada naudoti `predict`, kad gautume prognozių rezultatus. Štai grafikas, rodantis testinius duomenis ir apytikslę kreivę:

<img alt="Polynomial regression" src="../../../../translated_images/lt/poly-results.ee587348f0f1f60b.webp" width="50%" />

Naudodami polinominę regresiją galime gauti šiek tiek mažesnę MSE ir didesnį determinacijos koeficientą, bet ne žymiai. Turime atsižvelgti į kitas savybes!

> Matote, kad mažiausios moliūgų kainos fiksuojamos kažkur apie Heloviną. Kaip tai galima paaiškinti?

🎃 Sveikiname, ką tik sukūrėte modelį, kuris gali padėti prognozuoti moliūgų rūšių kainas pyragams. Tikriausiai tą patį procedūrą galima pakartoti visoms moliūgų rūšims, tačiau tai būtų varginantis darbas. Dabar išmokime, kaip mūsų modelyje atsižvelgti į moliūgo veislę!

## Kategoriniai bruožai

Idealioje situacijoje norėtume prognozuoti kainas skirtingoms moliūgų veislėms naudojant tą patį modelį. Tačiau stulpelis `Variety` šiek tiek skiriasi nuo tokių stulpelių kaip `Month`, nes jis turi ne skaitines reikšmes. Tokie stulpeliai vadinami **kategoriniais**.

[![ML pradedantiesiems – kategorinių bruožų prognozės su tiesine regresija](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML pradedantiesiems – kategorinių bruožų prognozės su tiesine regresija")

> 🎥 Paspauskite aukščiau esantį paveikslėlį, kad peržiūrėtumėte trumpą vaizdo įrašą apie kategorinius bruožus.

Čia matote, kaip vidutinė kaina priklauso nuo veislės:

<img alt="Average price by variety" src="../../../../translated_images/lt/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Kad atsižvelgtume į veislę, pirmiausia turime ją paversti į skaitmeninę formą arba **užkoduoti**. Yra keli būdai, kaip tai padaryti:

* Paprastas **skaitmeninis kodavimas** sukurs lentelę skirtingų veislių ir pakeis veislės pavadinimą į tos lentelės indeksą. Tai nėra geriausia idėja tiesinei regresijai, nes tiesinė regresija ima tikrąjį skaitinę indekso vertę ir prideda ją prie rezultato, daugindama iš tam tikro koeficiento. Mūsų atveju ryšys tarp indekso ir kainos yra akivaizdžiai nelinijinis, net jei užtikrinsime, kad indeksai būtų tam tikra tvarka.
* **Vieno karšto kodavimas (one-hot encoding)** pakeis `Variety` stulpelį į 4 atskirus stulpelius, po vieną kiekvienai veislei. Kiekviename stulpelyje bus `1`, jei atitinkamas įrašas priklauso tai veislei, ir `0` kitu atveju. Tai reiškia, kad tiesinėje regresijoje bus keturi koeficientai, po vieną kiekvienai moliūgų veislei, atsakingi už „pradinę kainą“ (ar tiksliau „papildomą kainą“) už tą tam tikrą veislę.

Žemiau esantis kodas rodo, kaip galima vieno karšto kodavimo būdu užkoduoti veislę:

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

Kad treniruotume tiesinę regresiją su vieno karšto kodavimu kaip įvestimi, tereikia tinkamai inicializuoti `X` ir `y` duomenis:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Likusi kodo dalis ta pati, kaip ir anksčiau treniruojant tiesinę regresiją. Jei pabandysite, pamatysite, kad vidutinė kvadratinė klaida yra maždaug ta pati, tačiau gauname daug aukštesnį determinacijos koeficientą (~77%). Norint gauti dar tikslesnes prognozes, galime atsižvelgti į daugiau kategorinių savybių, taip pat ir į skaitmeninius kintamuosius, pavyzdžiui, `Month` ar `DayOfYear`. Kad gautume vieną didelį savybių masyvą, galime naudoti `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Čia taip pat atsižvelgiama į `City` ir `Package` tipus, kas suteikia MSE 2.84 (10%) ir determinaciją 0.94!

## Viso sujungimas

Kad sukurtume geriausią modelį, galime naudoti sujungtus (vieno karšto kodavimo kategorinius + skaitmeninius) duomenis kartu su polinomine regresija. Štai visas kodas jūsų patogumui:

```python
# nustatyti mokymo duomenis
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# atlikti mokymo ir testavimo duomenų padalijimą
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# nustatyti ir apmokyti srautą
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prognozuoti rezultatus testavimo duomenims
pred = pipeline.predict(X_test)

# apskaičiuoti vidutinę kvadratinę paklaidą ir determinacijos koeficientą
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Tai turėtų suteikti geriausią determinacijos koeficientą, beveik 97%, ir MSE=2.23 (~8% prognozės klaida).

| Modelis | MSE | Determinacija |
|---------|-----|--------------|
| `DayOfYear` tiesinė | 2.77 (17.2%) | 0.07 |
| `DayOfYear` polinominė | 2.73 (17.0%) | 0.08 |
| `Variety` tiesinė | 5.24 (19.7%) | 0.77 |
| Visos savybės tiesinė | 2.84 (10.5%) | 0.94 |
| Visos savybės polinominė | 2.23 (8.25%) | 0.97 |

🏆 Puikiai padirbėta! Šiame užsiėmime sukūrėte keturis regresijos modelius ir pagerinote modelio kokybę iki 97%. Paskutinėje regresijos dalyje sužinosite apie logistinę regresiją, skirtą klasių nustatymui.

---
## 🚀Iššūkis

Išbandykite kelis skirtingus kintamuosius šiame užrašų knygelėje, kad pamatytumėte, kaip koreliacija atitinka modelio tikslumą.

## [Paskaitos testas](https://ff-quizzes.netlify.app/en/ml/)

## Peržiūra ir savarankiškas mokymasis

Šioje pamokoje sužinojome apie tiesinę regresiją. Yra ir kitų svarbių regresijos tipų. Perskaitykite apie žingsninę, Ridge, Lasso ir Elasticnet metodikas. Gera kursų programa norint gilintis yra [Stanfordo statistinės mokymosi kursas](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Užduotis

[Sudaryti modelį](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Atsakomybės apribojimas**:  
Šis dokumentas buvo išverstas naudojant dirbtinio intelekto vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, prašome atkreipti dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Kritinėje informacijoje rekomenduojama naudotis profesionaliu žmogaus atliktu vertimu. Mes neatsakome už bet kokias nesusipratimus ar neteisingas interpretacijas, kylančias naudojant šį vertimą.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->