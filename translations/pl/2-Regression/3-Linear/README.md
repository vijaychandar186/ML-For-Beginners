# Zbuduj model regresji za pomocą Scikit-learn: regresja na cztery sposoby

## Notatka dla początkujących

Regresja liniowa jest stosowana, gdy chcemy przewidzieć **wartość numeryczną** (na przykład cenę domu, temperaturę lub sprzedaż).
Działa poprzez znalezienie prostej linii, która najlepiej reprezentuje zależność między cechami wejściowymi a wyjściem.

W tej lekcji skupiamy się na zrozumieniu koncepcji, zanim przejdziemy do bardziej zaawansowanych technik regresji.
![Infografika regresji liniowej vs. wielomianowej](../../../../translated_images/pl/linear-polynomial.5523c7cb6576ccab.webp)
> Infografika autorstwa [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Quiz przedwykładowy](https://ff-quizzes.netlify.app/en/ml/)

> ### [Ta lekcja jest dostępna w R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Wprowadzenie

Do tej pory poznaliście, czym jest regresja na podstawie przykładowych danych z zestawu danych dotyczącego cen dyni, które będziemy wykorzystywać w trakcie tej lekcji. Wizualizowaliście je także za pomocą Matplotlib.

Teraz jesteście gotowi, by zagłębić się bardziej w regresję dla ML. Podczas gdy wizualizacja pozwala zrozumieć dane, prawdziwa siła uczenia maszynowego pochodzi z _trenowania modeli_. Modele są trenowane na danych historycznych, aby automatycznie wychwytywać zależności w danych i umożliwiają przewidywanie wyników dla nowych danych, których model wcześniej nie widział.

W tej lekcji dowiecie się więcej o dwóch rodzajach regresji: _podstawowej regresji liniowej_ i _regresji wielomianowej_, wraz z wyjaśnieniem matematyki stojącej za tymi technikami. Te modele pozwolą nam przewidzieć ceny dyni w zależności od różnych danych wejściowych.

[![ML dla początkujących - Zrozumienie regresji liniowej](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML dla początkujących - Zrozumienie regresji liniowej")

> 🎥 Kliknij powyższy obrazek, aby obejrzeć krótki przegląd regresji liniowej.

> W całym tym kursie zakładamy minimalną znajomość matematyki i staramy się uczynić ją dostępną dla uczniów z innych dziedzin, więc zwracaj uwagę na notatki, 🧮 wzmianki, diagramy i inne narzędzia wspomagające naukę.

### Wymagania wstępne

Powinieneś już znać strukturę danych dotyczących dyni, które badamy. Możesz je znaleźć wstępnie załadowane i wyczyszczone w pliku _notebook.ipynb_ towarzyszącym tej lekcji. W tym pliku cena dyni jest wyświetlana za korzec w nowej ramce danych. Upewnij się, że potrafisz uruchomić te notatniki w kernelach w Visual Studio Code.

### Przygotowanie

Dla przypomnienia, ładujesz te dane, aby móc zadawać im pytania.

- Kiedy jest najlepszy czas na kupno dyni?
- Jakiej ceny mogę oczekiwać za skrzynkę miniaturowych dyń?
- Czy powinienem kupić je w półkorcowych koszach czy w pudełku o pojemności 1 1/9 korca?
Zanurzmy się dalej w te dane.

W poprzedniej lekcji stworzyłeś ramkę danych Pandas i wypełniłeś ją częścią oryginalnego zestawu danych, standaryzując ceny za korzec. Zrobienie tego pozwoliło zebrać około 400 punktów danych tylko dla miesięcy jesiennych.

Spójrz na dane, które wstępnie załadowaliśmy w notatniku towarzyszącym tej lekcji. Dane są już załadowane, a na wykresie rozrzutu wstępnie pokazano dane miesięczne. Być może możemy uzyskać trochę więcej szczegółów o naturze danych, oczyszczając je bardziej.

## Linia regresji liniowej

Jak nauczyliście się w Lekcji 1, celem regresji liniowej jest stworzenie linii, która:

- **Pokaże zależności między zmiennymi**.
- **Pozwoli na dokonywanie predykcji** nowych punktów danych względem tej linii.

Typowo dla **Metody najmniejszych kwadratów** rysowana jest właśnie taka linia. Termin "Najmniejszych kwadratów" odnosi się do procesu minimalizowania całkowitego błędu naszego modelu. Dla każdego punktu danych mierzymy pionową odległość (zwaną resztą) pomiędzy rzeczywistym punktem a naszą linią regresji.

Te odległości kwadratujemy z dwóch głównych powodów:

1. **Wielkość ważniejsza od kierunku:** Chcemy traktować błąd -5 tak samo jak błąd +5. Kwadrat zamienia wszystkie wartości na dodatnie.

2. **Karanie wartości odstających:** Kwadratowanie nadaje większą wagę większym błędom, zmuszając linię do bycia bliżej punktów odstających.

Następnie sumujemy wszystkie te kwadraty. Naszym celem jest znalezienie właśnie takiej linii, dla której ta suma jest najmniejsza — stąd nazwa "Najmniejszych kwadratów".

> **🧮 Pokaż mi matematykę**
>
> Ta linia, zwana _linią najlepszego dopasowania_, może być wyrażona za pomocą [równania](https://en.wikipedia.org/wiki/Simple_linear_regression): 
>
> ```
> Y = a + bX
> ```
>
> `X` to 'zmienna objaśniająca'. `Y` to 'zmienna zależna'. Nachylenie linii to `b`, a `a` to punkt przecięcia z osią Y, czyli wartość `Y` gdy `X = 0`.
>
>![obliczanie nachylenia](../../../../translated_images/pl/slope.f3c9d5910ddbfcf9.webp)
>
> Najpierw obliczamy nachylenie `b`. Infografika autorstwa [Jen Looper](https://twitter.com/jenlooper)
>
> Innymi słowy, odnosząc się do naszego oryginalnego pytania o dynie: "przewidzieć cenę dyni za korzec w zależności od miesiąca", `X` będzie odpowiadać cenie, a `Y` będzie odpowiadać miesiącowi sprzedaży.
>
>![uzupełnij równanie](../../../../translated_images/pl/calculation.a209813050a1ddb1.webp)
>
> Oblicz wartość Y. Jeśli płacisz około 4 dolarów, musi to być kwiecień! Infografika autorstwa [Jen Looper](https://twitter.com/jenlooper)
>
> Matematyka obliczająca linię musi uwzględniać nachylenie, które zależy też od punktu przecięcia, czyli wartości `Y` gdy `X = 0`.
>
> Możesz zobaczyć metodę obliczania tych wartości na stronie [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Odwiedź także [Ten kalkulator najmniejszych kwadratów](https://www.mathsisfun.com/data/least-squares-calculator.html), aby zobaczyć, jak wartości liczb wpływają na linię.

## Korelacja

Jeszcze jedno pojęcie, które warto poznać, to **współczynnik korelacji** między danymi zmiennymi X i Y. Korzystając z wykresu rozrzutu, można szybko zwizualizować ten współczynnik. Wykres z punktami ułożonymi w porządną linię ma wysoką korelację, natomiast wykres, gdzie punkty są rozrzucone wszędzie pomiędzy X i Y, ma niską korelację.

Dobry model regresji liniowej będzie miał wysoki (bliższy 1 niż 0) współczynnik korelacji wyznaczony metodą najmniejszych kwadratów z linią regresji.

✅ Uruchom notatnik dołączony do tej lekcji i spójrz na wykres rozrzutu Miesiąc a Cena. Czy dane łączące miesiąc z ceną sprzedaży dyni mają wysoką czy niską korelację według Twojej wizualnej interpretacji wykresu rozrzutu? Czy to się zmienia, jeśli użyjesz bardziej szczegółowej miary niż `Miesiąc`, np. *dzień roku* (liczba dni od początku roku)?

W poniższym kodzie założymy, że wyczyściliśmy dane i uzyskaliśmy ramkę danych o nazwie `new_pumpkins`, podobną do poniższej:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Kod do oczyszczenia danych jest dostępny w [`notebook.ipynb`](notebook.ipynb). Wykonaliśmy te same kroki czyszczenia, co w poprzedniej lekcji, i obliczyliśmy kolumnę `DayOfYear` według następującego wyrażenia:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Teraz, gdy rozumiesz matematykę stojącą za regresją liniową, stwórzmy model regresji, aby sprawdzić, czy potrafimy przewidzieć, która paczka dyń będzie miała najlepsze ceny. Ktoś kupujący dynie na świąteczną plantację może chcieć tych informacji, by zoptymalizować swoje zakupy paczek dyń na plantację.

## Szukanie korelacji

[![ML dla początkujących - Szukanie korelacji: klucz do regresji liniowej](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML dla początkujących - Szukanie korelacji: klucz do regresji liniowej")

> 🎥 Kliknij powyższy obrazek, aby zobaczyć krótki przegląd korelacji.

Z poprzedniej lekcji prawdopodobnie widziałeś, że średnia cena dla różnych miesięcy wygląda tak:

<img alt="Średnia cena wg miesiąca" src="../../../../translated_images/pl/barchart.a833ea9194346d76.webp" width="50%"/>

To sugeruje, że może istnieć korelacja, i możemy spróbować wytrenować liniowy model regresji, by przewidzieć zależność między `Month` a `Price` lub między `DayOfYear` a `Price`. Oto wykres rozrzutu pokazujący tę drugą zależność:

<img alt="Wykres rozrzutu Cena vs. Dzień roku" src="../../../../translated_images/pl/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Sprawdźmy, czy jest korelacja, używając funkcji `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Wygląda na to, że korelacja jest dość mała, -0.15 wg `Month` i -0.17 wg `DayOfMonth`, ale mogłaby istnieć inna ważna zależność. Wygląda na to, że istnieją różne grupy cen odpowiadające różnym odmianom dyni. Aby potwierdzić tę hipotezę, nanieśmy każdy gatunek dyń innym kolorem. Przekazując argument `ax` funkcji `scatter`, możemy nanieść wszystkie punkty na tym samym wykresie:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Wykres rozrzutu Cena vs. Dzień roku" src="../../../../translated_images/pl/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Nasze dochodzenie sugeruje, że odmiana dyni ma większy wpływ na cenę niż faktyczna data sprzedaży. Możemy to zobaczyć na wykresie słupkowym:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Wykres słupkowy ceny wg odmiany" src="../../../../translated_images/pl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Skupmy się na razie tylko na jednej odmianie dyni, 'pie type', i zobaczmy jaki wpływ ma data na cenę:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Wykres rozrzutu Cena vs. Dzień roku" src="../../../../translated_images/pl/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Jeśli teraz obliczymy korelację między `Price` a `DayOfYear` funkcją `corr`, otrzymamy wartość około `-0.27` – co oznacza, że trening modelu predykcyjnego ma sens.

> Przed wytrenowaniem modelu regresji liniowej ważne jest, aby upewnić się, że dane są czyste. Regresja liniowa źle radzi sobie z brakującymi wartościami, więc warto usunąć wszystkie puste komórki:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Innym podejściem byłoby wypełnienie tych pustych wartości średnimi wartościami z odpowiednich kolumn.

## Prosta regresja liniowa

[![ML dla początkujących - regresja liniowa i wielomianowa z użyciem Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML dla początkujących - regresja liniowa i wielomianowa z użyciem Scikit-learn")

> 🎥 Kliknij powyższy obrazek, aby obejrzeć krótki przegląd regresji liniowej i wielomianowej.

Aby wytrenować nasz model regresji liniowej, użyjemy biblioteki **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Zaczynamy od rozdzielenia wartości wejściowych (cech) i oczekiwanego wyniku (etykiety) do osobnych tablic numpy:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Zauważ, że musieliśmy wykonać `reshape` na danych wejściowych, aby pakiet Linear Regression zrozumiał je poprawnie. Regresja liniowa oczekuje 2-wymiarowej tablicy jako wejścia, gdzie każdy wiersz tablicy odpowiada wektorowi cech wejściowych. W naszym przypadku, ponieważ mamy tylko jedno wejście – potrzebujemy tablicy o kształcie N×1, gdzie N to rozmiar zestawu danych.

Następnie musimy podzielić dane na zbiory treningowy i testowy, aby móc zweryfikować model po treningu:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Na koniec wytrenowanie faktycznego modelu regresji liniowej zajmuje tylko dwie linijki kodu. Definiujemy obiekt `LinearRegression` i dopasowujemy go do naszych danych za pomocą metody `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Obiekt `LinearRegression` po dopasowaniu (`fit`) zawiera wszystkie współczynniki regresji, do których można uzyskać dostęp za pomocą właściwości `.coef_`. W naszym przypadku jest tylko jeden współczynnik, który powinien wynosić około `-0.017`. Oznacza to, że ceny wydają się nieco spadać z czasem, ale niezbyt mocno, około 2 centów dziennie. Możemy również uzyskać punkt przecięcia regresji z osią Y, korzystając z `lin_reg.intercept_` - będzie to około `21` w naszym przypadku, co wskazuje na cenę na początku roku.

Aby sprawdzić, jak dokładny jest nasz model, możemy przewidzieć ceny na zbiorze testowym, a następnie zmierzyć, jak bliskie są nasze przewidywania wartościom oczekiwanym. Można to zrobić za pomocą wskaźnika błędu średniokwadratowego (RMSE), który jest pierwiastkiem średniej ze wszystkich kwadratów różnic między wartością oczekiwaną a przewidywaną.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Nasz błąd wydaje się wynosić około 2 punktów, co stanowi ~17%. Niezbyt dobrze. Innym wskaźnikiem jakości modelu jest **współczynnik determinacji**, który można uzyskać w ten sposób:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Jeśli wartość jest równa 0, oznacza to, że model nie uwzględnia danych wejściowych i działa jako *najgorszy liniowy predyktor*, którym jest po prostu średnia z wyniku. Wartość 1 oznacza, że możemy idealnie przewidzieć wszystkie wartości oczekiwane. W naszym przypadku współczynnik wynosi około 0.06, co jest dość niskie.

Możemy również narysować dane testowe razem z linią regresji, aby lepiej zobaczyć, jak działa regresja w naszym przypadku:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/pl/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regresja wielomianowa

Innym typem regresji liniowej jest regresja wielomianowa. Chociaż czasem istnieje liniowa zależność między zmiennymi – im większa dynia pod względem objętości, tym wyższa cena – to czasem tych zależności nie da się przedstawić jako płaszczyzna lub prosta.

✅ Oto [kilka innych przykładów](https://online.stat.psu.edu/stat501/lesson/9/9.8) danych, dla których można zastosować regresję wielomianową

Spójrz ponownie na zależność między Datą a Ceną. Czy ta wykres rozrzutu koniecznie powinien być analizowany za pomocą prostej? Czy ceny nie mogą się wahać? W takim przypadku można spróbować regresji wielomianowej.

✅ Wielomiany to wyrażenia matematyczne, które mogą się składać z jednej lub więcej zmiennych oraz współczynników

Regresja wielomianowa tworzy zakrzywioną linię, aby lepiej dopasować dane nieliniowe. W naszym przypadku, jeśli do danych wejściowych dodamy zmienną `DayOfYear` podniesioną do kwadratu, powinniśmy być w stanie dopasować nasze dane krzywą paraboliczną, która będzie miała minimum w pewnym punkcie w ciągu roku.

Scikit-learn zawiera przydatne [API do łączenia etapów przetwarzania danych](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline). **Pipeline** to łańcuch **estymatorów**. W naszym przypadku stworzymy pipeline, który najpierw doda cechy wielomianowe do naszego modelu, a następnie wytrenuje regresję:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Użycie `PolynomialFeatures(2)` oznacza, że uwzględnimy wszystkie wielomiany drugiego stopnia z danych wejściowych. W naszym przypadku będzie to po prostu `DayOfYear`<sup>2</sup>, ale przy dwóch zmiennych wejściowych X i Y doda X<sup>2</sup>, XY oraz Y<sup>2</sup>. Możemy również użyć wielomianów wyższego stopnia, jeśli chcemy.

Pipeline można używać tak samo jak oryginalny obiekt `LinearRegression`, tj. możemy `fit` pipeline, a następnie użyć `predict`, aby uzyskać przewidywania. Oto wykres pokazujący dane testowe i krzywą aproksymacji:

<img alt="Polynomial regression" src="../../../../translated_images/pl/poly-results.ee587348f0f1f60b.webp" width="50%" />

Korzystając z regresji wielomianowej, możemy uzyskać nieco niższy MSE i wyższy współczynnik determinacji, ale nieznacznie. Musimy uwzględnić inne cechy!

> Możesz zauważyć, że minimalne ceny dyń są obserwowane około Halloween. Jak to wyjaśnisz?

🎃 Gratulacje, właśnie stworzyłeś model, który może pomóc przewidzieć cenę dyń na ciasto. Prawdopodobnie możesz powtórzyć tę samą procedurę dla wszystkich typów dyń, ale byłoby to żmudne. Nauczmy się teraz, jak uwzględnić odmianę dyni w naszym modelu!

## Cechy kategoryczne

W idealnym świecie chcielibyśmy móc przewidywać ceny dla różnych odmian dyni przy użyciu tego samego modelu. Jednak kolumna `Variety` jest nieco inna niż kolumny takie jak `Month`, ponieważ zawiera wartości niebędące liczbami. Takie kolumny nazywamy **kategorycznymi**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Kliknij powyższy obraz, aby obejrzeć krótki film o użyciu cech kategorycznych.

Tutaj możesz zobaczyć, jak średnia cena zależy od odmiany:

<img alt="Average price by variety" src="../../../../translated_images/pl/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Aby uwzględnić odmianę, najpierw musimy przekonwertować ją na postać numeryczną, czyli ją **zdekodować (zakodować)**. Istnieje kilka sposobów, jak to zrobić:

* Proste **kodowanie numeryczne** zbuduje tabelę różnych odmian, a następnie zastąpi nazwę odmiany indeksem w tej tabeli. To nie jest najlepszy pomysł dla regresji liniowej, ponieważ regresja liniowa bierze rzeczywistą wartość numeryczną indeksu i dodaje ją do wyniku, mnożąc przez pewien współczynnik. W naszym przypadku zależność między numerem indeksu a ceną jest wyraźnie nieliniowa, nawet jeśli upewnimy się, że indeksy są uporządkowane w konkretny sposób.
* **Kodowanie one-hot** zastąpi kolumnę `Variety` 4 różnymi kolumnami, po jednej dla każdej odmiany. Każda kolumna będzie zawierać `1`, jeśli odpowiadający wiersz jest danej odmiany, i `0` w przeciwnym wypadku. Oznacza to, że w regresji liniowej będzie cztery współczynniki, po jednym dla każdej odmiany dyni, odpowiedzialnych za "cenę startową" (a raczej "dodatkową cenę") dla danej odmiany.

Poniższy kod pokazuje, jak można zakodować odmianę metodą one-hot:

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

Aby wytrenować regresję liniową używając zakodowanej metodą one-hot odmiany jako dane wejściowe, wystarczy poprawnie zainicjalizować dane `X` i `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Reszta kodu jest taka sama, jak używana wcześniej do trenowania regresji liniowej. Jeśli to wypróbujesz, zobaczysz, że średni błąd kwadratowy jest mniej więcej taki sam, ale uzyskujemy znacznie wyższy współczynnik determinacji (~77%). Aby uzyskać jeszcze dokładniejsze przewidywania, możemy uwzględnić więcej cech kategorycznych oraz numerycznych, takich jak `Month` czy `DayOfYear`. Aby uzyskać jedną dużą tablicę cech, możemy użyć `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Tutaj uwzględniamy również `City` i typ `Package`, co daje MSE 2.84 (10%) oraz współczynnik determinacji 0.94!

## Łączenie wszystkiego w całość

Aby stworzyć najlepszy model, możemy użyć połączonych (zakodowanych one-hot kategorycznych + numerycznych) danych z powyższego przykładu wraz z regresją wielomianową. Oto kompletny kod dla Twojej wygody:

```python
# przygotuj dane treningowe
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# wykonaj podział na zbiór treningowy i testowy
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# skonfiguruj i wytrenuj pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# przewiduj wyniki dla danych testowych
pred = pipeline.predict(X_test)

# oblicz MSE i współczynnik determinacji
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

To powinno dać nam najlepszy współczynnik determinacji prawie 97% oraz MSE=2.23 (~8% błąd przewidywania).

| Model | MSE | Współczynnik determinacji |
|-------|-----|----------------------------|
| `DayOfYear` liniowa | 2.77 (17.2%) | 0.07 |
| `DayOfYear` wielomianowa | 2.73 (17.0%) | 0.08 |
| `Variety` liniowa | 5.24 (19.7%) | 0.77 |
| Wszystkie cechy liniowe | 2.84 (10.5%) | 0.94 |
| Wszystkie cechy wielomianowe | 2.23 (8.25%) | 0.97 |

🏆 Świetna robota! Stworzyłeś cztery modele regresji w jednej lekcji i poprawiłeś jakość modelu do 97%. W ostatnim rozdziale o regresji poznasz regresję logistyczną do określania kategorii.

---
## 🚀Wyzwanie

Przetestuj kilka różnych zmiennych w tym zeszycie, aby zobaczyć, jak korelacja przekłada się na dokładność modelu.

## [Quiz po wykładzie](https://ff-quizzes.netlify.app/en/ml/)

## Powtórka i samodzielna nauka

W tej lekcji poznaliśmy regresję liniową. Istnieją także inne ważne typy regresji. Przeczytaj o technikach Stepwise, Ridge, Lasso i Elasticnet. Dobrym kursem do nauki jest [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Zadanie

[Zbuduj model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Zastrzeżenie**:  
Dokument ten został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dążymy do dokładności, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w języku źródłowym należy traktować jako autorytatywne źródło. W przypadku informacji krytycznych zaleca się profesjonalne tłumaczenie wykonane przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->