# Erstellen eines Regressionsmodells mit Scikit-learn: Regression auf vier Arten

## Anfängerhinweis

Lineare Regression wird verwendet, wenn wir einen **numerischen Wert** vorhersagen wollen (zum Beispiel Hauspreis, Temperatur oder Umsatz).  
Sie funktioniert, indem sie eine Gerade findet, die die Beziehung zwischen Eingabefunktionen und Ausgabe am besten darstellt.

In dieser Lektion konzentrieren wir uns darauf, das Konzept zu verstehen, bevor wir uns fortgeschritteneren Regressionsmethoden zuwenden.  
![Lineare vs. polynomiale Regression Infografik](../../../../translated_images/de/linear-polynomial.5523c7cb6576ccab.webp)  
> Infografik von [Dasani Madipalli](https://twitter.com/dasani_decoded)

## [Pre-lecture Quiz](https://ff-quizzes.netlify.app/en/ml/)

> ### [Diese Lektion ist auch in R verfügbar!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)

### Einführung

Bisher hast du untersucht, was Regression ist, mit Beispieldaten aus dem Kürbispreis-Datensatz, den wir während dieser Lektion verwenden werden. Du hast ihn auch mit Matplotlib visualisiert.

Jetzt bist du bereit, tiefer in die Regression für ML einzutauchen. Während Visualisierung dir hilft, Daten zu verstehen, liegt die wahre Stärke von Machine Learning im _Trainieren von Modellen_. Modelle werden mit historischen Daten trainiert, um Datenabhängigkeiten automatisch zu erfassen, und sie ermöglichen die Vorhersage von Ergebnissen für neue Daten, die das Modell vorher nicht gesehen hat.

In dieser Lektion lernst du zwei Arten der Regression kennen: _einfache lineare Regression_ und _polynomiale Regression_, sowie einige der mathematischen Grundlagen dieser Techniken. Diese Modelle ermöglichen uns, Kürbispreise in Abhängigkeit von unterschiedlichen Eingabedaten vorherzusagen.

[![ML für Anfänger – Verständnis der linearen Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML für Anfänger – Verständnis der linearen Regression")

> 🎥 Klicke auf das Bild oben für eine kurze Videoübersicht zur linearen Regression.

> Im gesamten Curriculum gehen wir von minimalen Mathematikkenntnissen aus und möchten das Thema für Studierende aus anderen Bereichen zugänglich machen. Achte daher auf Hinweise, 🧮 Erklärungen, Diagramme und andere Lernhilfen zur Unterstützung des Verständnisses.

### Voraussetzungen

Du solltest inzwischen mit der Struktur der Kürbisdaten vertraut sein, die wir untersuchen. Die Daten sind in der Datei _notebook.ipynb_ dieser Lektion vorab geladen und bereinigt. Dort wird der Kürbispreis pro Scheffel in einem neuen DataFrame angezeigt. Stelle sicher, dass du diese Notebooks in Visual Studio Code ausführen kannst.

### Vorbereitung

Zur Erinnerung: Du lädst diese Daten, um Fragen an sie stellen zu können.

- Wann ist die beste Zeit, Kürbisse zu kaufen?  
- Welchen Preis kann ich für eine Kiste Mini-Kürbisse erwarten?  
- Sollte ich sie in Halbscheffel-Körben oder in 1 1/9 Scheffel Kisten kaufen?

Lass uns tiefer in diese Daten eintauchen.

In der vorherigen Lektion hast du ein Pandas DataFrame erstellt und mit einem Teil des ursprünglichen Datensatzes befüllt, wobei die Preise auf den Scheffel normiert wurden. Damit konntest du allerdings nur etwa 400 Datenpunkte sammeln und nur für die Herbstmonate.

Schau dir die Daten an, die wir im Notebook dieser Lektion vorab geladen haben. Die Daten sind vorab geladen, und ein erster Streudiagramm wurde gezeichnet, um Monatsdaten zu zeigen. Vielleicht können wir durch weitergehende Bereinigung mehr über die Natur der Daten erfahren.

## Eine lineare Regressionsgerade

Wie du in Lektion 1 gelernt hast, ist das Ziel einer linearen Regression, eine Gerade zu zeichnen, die:

- **Variablenbeziehungen zeigt**. Zeigt die Beziehung zwischen Variablen  
- **Vorhersagen ermöglicht**. Ermöglicht genaue Vorhersagen, wo ein neuer Datenpunkt relativ zu dieser Linie liegen würde.

Typisch ist bei der **Methode der kleinsten Quadrate** (Least-Squares Regression) das Ziehen dieser Art von Linie. Der Begriff "Methode der kleinsten Quadrate" bezieht sich auf den Prozess der Minimierung des Gesamtfehlers im Modell. Für jeden Datenpunkt messen wir den vertikalen Abstand (genannt Residuum) zwischen dem tatsächlichen Punkt und unserer Regressionslinie.

Wir quadrieren diese Abstände aus zwei Hauptgründen:

1. **Betrag statt Richtung:** Wir wollen einen Fehler von -5 genauso behandeln wie einen Fehler von +5. Das Quadrieren macht alle Werte positiv.

2. **Bestrafung von Ausreißern:** Das Quadrieren gibt größeren Fehlern mehr Gewicht und zwingt die Gerade, näher an weiter entfernte Punkte heranzurücken.

Dann addieren wir alle quadrierten Werte zusammen. Unser Ziel ist es, genau die Linie zu finden, bei der diese Summe am geringsten ist (der kleinstmögliche Wert) – daher der Name „Methode der kleinsten Quadrate“.

> **🧮 Zeig mir die Mathematik**  
>  
> Diese Linie, genannt die _Bestanpassungslinie_, kann mit [einer Gleichung](https://de.wikipedia.org/wiki/Einfache_lineare_Regression) dargestellt werden:  
>  
> ```
> Y = a + bX
> ```
>  
> `X` ist die „erklärende Variable“. `Y` ist die „abhängige Variable“. Die Steigung der Geraden ist `b` und `a` ist der Achsenabschnitt, also der Wert von `Y`, wenn `X = 0` ist.  
>  
>![Berechnung der Steigung](../../../../translated_images/de/slope.f3c9d5910ddbfcf9.webp)  
>  
> Berechne zuerst die Steigung `b`. Infografik von [Jen Looper](https://twitter.com/jenlooper)  
>  
> Anders ausgedrückt und bezogen auf unsere ursprüngliche Kürbisdatenfrage: "Vorhersage des Preises eines Kürbisses pro Scheffel nach Monat" entspricht `X` dem Preis und `Y` dem Verkaufsmonat.  
>  
>![Gleichung vervollständigen](../../../../translated_images/de/calculation.a209813050a1ddb1.webp)  
>  
> Berechne den Wert von Y. Wenn du etwa 4 Dollar bezahlst, muss es April sein! Infografik von [Jen Looper](https://twitter.com/jenlooper)  
>  
> Die Mathematik, die die Gerade berechnet, muss die Steigung der Geraden darstellen, die auch vom Achsenabschnitt abhängt, also wo `Y` liegt, wenn `X = 0`.  
>  
> Du kannst die Berechnungsmethode für diese Werte auf der Webseite [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) nachlesen. Besuche auch [diesen Least-squares Rechner](https://www.mathsisfun.com/data/least-squares-calculator.html), um zu sehen, wie die Werte die Gerade beeinflussen.

## Korrelation

Ein weiterer Begriff, den du verstehen solltest, ist der **Korrelationskoeffizient** zwischen gegebenen X- und Y-Variablen. Mithilfe eines Streudiagramms kannst du diesen Koeffizienten schnell visualisieren. Ein Plot mit Punkten, die sich auf einer klaren Linie befinden, hat eine hohe Korrelation, während ein Plot mit zufällig verteilten Punkten eine geringe Korrelation aufweist.

Ein gutes lineares Regressionsmodell hat einen hohen (näher bei 1 als bei 0) Korrelationskoeffizienten, wenn die Methode der kleinsten Quadrate mit einer Regressionslinie verwendet wird.

✅ Führe das Notebook zu dieser Lektion aus und sieh dir das Streudiagramm von Monat zu Preis an. Scheint die Assoziation vom Monat zum Kürbiskaufpreis nach deiner visuellen Interpretation des Streudiagramms eine hohe oder niedrige Korrelation zu haben? Ändert sich das, wenn du statt `Month` eine feinere Maßeinheit wie *Tag des Jahres* (also Anzahl der Tage seit Jahresbeginn) nutzt?

Im folgenden Code gehen wir davon aus, dass wir die Daten bereinigt haben und ein DataFrame namens `new_pumpkins` vorliegt, das in etwa so aussieht:

ID | Monat | TagDesJahres | Sorte | Stadt | Verpackung | Niedriger Preis | Hoher Preis | Preis  
---|-------|--------------|-------|-------|------------|-----------------|-------------|--------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 Scheffel Kartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 Scheffel Kartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 Scheffel Kartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 Scheffel Kartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 Scheffel Kartons | 15.0 | 15.0 | 13.636364

> Der Code zur Datenbereinigung ist in [`notebook.ipynb`](notebook.ipynb) verfügbar. Wir haben die gleichen Bereinigungsschritte wie in der vorherigen Lektion durchgeführt und die Spalte `DayOfYear` mit folgendem Ausdruck berechnet:  

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Jetzt, da du die Mathematik hinter der linearen Regression verstehst, lass uns ein Regressionsmodell erstellen, um zu sehen, ob wir vorhersagen können, welches Kürbispaket die besten Preise haben wird. Jemand, der Kürbisse für einen Kürbisgarten zu Halloween kauft, möchte diese Informationen, um seinen Einkauf zu optimieren.

## Auf der Suche nach Korrelation

[![ML für Anfänger – Auf der Suche nach Korrelation: Der Schlüssel zur linearen Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML für Anfänger – Auf der Suche nach Korrelation: Der Schlüssel zur linearen Regression")

> 🎥 Klicke auf das Bild oben für eine kurze Videoübersicht zur Korrelation.

Aus der vorherigen Lektion hast du wahrscheinlich gesehen, dass der Durchschnittspreis für unterschiedliche Monate so aussieht:

<img alt="Durchschnittspreis nach Monat" src="../../../../translated_images/de/barchart.a833ea9194346d76.webp" width="50%"/>

Das deutet darauf hin, dass es eine bestimmte Korrelation geben sollte, und wir können versuchen, ein lineares Regressionsmodell zu trainieren, um die Beziehung zwischen `Monat` und `Preis` oder zwischen `TagDesJahres` und `Preis` vorherzusagen. Hier ist das Streudiagramm, das letztere Beziehung zeigt:

<img alt="Streudiagramm von Preis vs. Tag des Jahres" src="../../../../translated_images/de/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />

Sehen wir uns die Korrelation mit der Funktion `corr` an:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Es sieht so aus, als sei die Korrelation ziemlich klein, -0,15 für `Monat` und -0,17 für `TagDesJahres`, aber es könnte eine andere wichtige Beziehung geben. Es sieht so aus, als gäbe es unterschiedliche Cluster von Preisen, die verschiedenen Kürbissorten zugeordnet sind. Zur Bestätigung dieser Hypothese wollen wir jede Kürbissorte mit einer anderen Farbe darstellen. Indem wir der `scatter`-Plotfunktion einen `ax`-Parameter übergeben, können wir alle Punkte auf demselben Diagramm darstellen:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Streudiagramm von Preis vs. Tag des Jahres mit Farbunterscheidung" src="../../../../translated_images/de/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" />

Unsere Untersuchung legt nahe, dass die Sorte mehr Einfluss auf den Gesamtpreis hat als das tatsächliche Verkaufsdatum. Das können wir mit einem Balkendiagramm sehen:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Balkendiagramm Preis vs. Sorte" src="../../../../translated_images/de/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Konzentrieren wir uns für den Moment nur auf eine Kürbissorte, den 'Pie Type', und schauen, welchen Einfluss das Datum auf den Preis hat:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Streudiagramm von Preis vs. Tag des Jahres für Pie-Kürbisse" src="../../../../translated_images/de/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" />

Wenn wir jetzt die Korrelation zwischen `Preis` und `TagDesJahres` mit der Funktion `corr` berechnen, erhalten wir etwa `-0.27` – was bedeutet, dass das Trainieren eines Vorhersagemodells sinnvoll ist.

> Bevor wir ein lineares Regressionsmodell trainieren, ist es wichtig sicherzustellen, dass unsere Daten sauber sind. Lineare Regression funktioniert nicht gut mit fehlenden Werten, daher ist es sinnvoll, alle leeren Zellen zu entfernen:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
Ein anderer Ansatz wäre, diese fehlenden Werte mit Mittelwerten der entsprechenden Spalte zu füllen.

## Einfache lineare Regression

[![ML für Anfänger – Lineare und polynomiale Regression mit Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML für Anfänger – Lineare und polynomiale Regression mit Scikit-learn")

> 🎥 Klicke auf das Bild oben für eine kurze Videoübersicht zur linearen und polynomialen Regression.

Um unser Lineares Regressionsmodell zu trainieren, verwenden wir die **Scikit-learn**-Bibliothek.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
Wir beginnen damit, Eingabewerte (Features) und die erwartete Ausgabe (Label) in separate numpy-Arrays aufzuteilen:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Beachte, dass wir auf die Eingabedaten `reshape` anwenden mussten, damit das Linear Regression-Paket sie korrekt versteht. Die lineare Regression erwartet als Eingabe ein 2D-Array, wobei jede Zeile einem Vektor von Eingabefunktionen entspricht. Da wir nur eine Eingabevariable haben, brauchen wir ein Array mit der Form N×1, wobei N die Größe des Datensatzes ist.

Dann müssen wir die Daten in Trainings- und Testdaten aufteilen, damit wir unser Modell nach dem Training validieren können:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
Schließlich nimmt das Training des eigentlichen Linearen Regressionsmodells nur zwei Codezeilen in Anspruch. Wir definieren das `LinearRegression`-Objekt und passen es mit der Methode `fit` an unsere Daten an:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Das `LinearRegression`-Objekt enthält nach dem `fit`-ten alle Koeffizienten der Regression, auf die über die `.coef_`-Eigenschaft zugegriffen werden kann. In unserem Fall gibt es nur einen Koeffizienten, der ungefähr `-0.017` sein sollte. Das bedeutet, dass die Preise mit der Zeit etwas zu sinken scheinen, aber nicht zu stark, ungefähr 2 Cent pro Tag. Wir können auch den Schnittpunkt der Regression mit der Y-Achse über `lin_reg.intercept_` abrufen – dieser wird in unserem Fall ungefähr `21` sein und den Preis zu Beginn des Jahres anzeigen.

Um zu sehen, wie genau unser Modell ist, können wir die Preise auf einem Testdatensatz vorhersagen und dann messen, wie nah unsere Vorhersagen an den erwarteten Werten sind. Dies kann mithilfe der Metrik Root Mean Square Error (RMSE) erfolgen, welche die Wurzel des Mittels aller quadrierten Differenzen zwischen erwartetem und vorhergesagtem Wert ist.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Unser Fehler scheint etwa 2 Punkte zu betragen, was ca. 17 % sind. Nicht besonders gut. Ein weiterer Indikator für die Modellqualität ist der **Bestimmtheitsmaß**, der folgendermaßen ermittelt werden kann:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Wenn der Wert 0 ist, bedeutet dies, dass das Modell die Eingabedaten nicht berücksichtigt und als *schlechtester linearer Prädiktor* fungiert, was einfach ein Mittelwert des Ergebnisses ist. Ein Wert von 1 bedeutet, dass wir alle erwarteten Ausgaben perfekt vorhersagen können. In unserem Fall liegt der Koeffizient bei etwa 0,06, was ziemlich niedrig ist.

Wir können auch die Testdaten zusammen mit der Regressionslinie darstellen, um besser zu sehen, wie die Regression in unserem Fall funktioniert:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Lineare Regression" src="../../../../translated_images/de/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomiale Regression

Eine andere Art der linearen Regression ist die polynomiale Regression. Manchmal besteht zwar eine lineare Beziehung zwischen Variablen – je größer der Kürbis in Volumen, desto höher der Preis – aber manchmal können diese Beziehungen nicht als Ebene oder Gerade dargestellt werden.

✅ Hier sind [weitere Beispiele](https://online.stat.psu.edu/stat501/lesson/9/9.8) für Daten, die polynomiale Regression benötigen könnten.

Betrachte nochmal die Beziehung zwischen Datum und Preis. Sieht dieses Streudiagramm so aus, als sollte es unbedingt mit einer Geraden analysiert werden? Können Preise nicht schwanken? In diesem Fall kann man es mit polynomieller Regression versuchen.

✅ Polynome sind mathematische Ausdrücke, die aus einer oder mehreren Variablen und Koeffizienten bestehen können.

Die polynomiale Regression erstellt eine gekrümmte Linie, um nichtlineare Daten besser anzupassen. In unserem Fall, wenn wir eine quadrierte Variable `DayOfYear` in die Eingabedaten aufnehmen, sollten wir unsere Daten mit einer parabolischen Kurve anpassen können, die ihr Minimum an einem bestimmten Punkt im Jahr hat.

Scikit-learn enthält eine hilfreiche [Pipeline-API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline), um verschiedene Verarbeitungsschritte von Daten zu kombinieren. Eine **Pipeline** ist eine Kette von **Estimatoren**. In unserem Fall erstellen wir eine Pipeline, die zunächst polynomialen Features zum Modell hinzufügt und dann die Regression trainiert:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Die Verwendung von `PolynomialFeatures(2)` bedeutet, dass wir alle Polynome zweiten Grades aus den Eingabedaten einschließen. In unserem Fall ist das nur `DayOfYear`<sup>2</sup>, aber mit zwei Eingabevariablen X und Y fügt dies X<sup>2</sup>, XY und Y<sup>2</sup> hinzu. Wir können auch Polynome höheren Grades verwenden, wenn wir möchten.

Pipelines können genauso verwendet werden wie das ursprüngliche `LinearRegression`-Objekt, d.h. wir können die Pipeline `fit`ten und anschließend `predict` verwenden, um Vorhersagen zu erhalten. Hier ist das Diagramm mit den Testdaten und der Approximationskurve:

<img alt="Polynomiale Regression" src="../../../../translated_images/de/poly-results.ee587348f0f1f60b.webp" width="50%" />

Mit Polynom-Regression können wir leicht geringere MSE und einen höheren Bestimmtheitsmaß erreichen, aber nicht signifikant. Wir müssen auch andere Merkmale berücksichtigen!

> Man sieht, dass die minimalen Kürbispreise irgendwo um Halloween zu beobachten sind. Wie kann man das erklären?

🎃 Glückwunsch, du hast gerade ein Modell erstellt, das helfen kann, den Preis von Backkürbissen vorherzusagen. Du kannst das wahrscheinlich für alle Kürbissorten wiederholen, aber das wäre mühsam. Lernen wir jetzt, wie wir Kürbissorten in unser Modell einbeziehen können!

## Kategorische Merkmale

In einer idealen Welt wollen wir in der Lage sein, Preise für verschiedene Kürbissorten mit demselben Modell vorherzusagen. Allerdings ist die Spalte `Variety` etwas anders als z.B. `Month`, weil sie nicht numerische Werte enthält. Solche Spalten nennt man **kategorische**.

[![ML für Anfänger - Kategorische Merkmalvorhersagen mit Linearer Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML für Anfänger - Kategorische Merkmalvorhersagen mit Linearer Regression")

> 🎥 Klicke das obige Bild für eine kurze Videoübersicht zur Verwendung kategorischer Merkmale.

Hier sieht man, wie der Durchschnittspreis von der Sorte abhängt:

<img alt="Durchschnittspreis nach Sorte" src="../../../../translated_images/de/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Um die Sorte zu berücksichtigen, müssen wir sie zunächst in eine numerische Form umwandeln, oder **kodieren**. Es gibt mehrere Möglichkeiten:

* Eine einfache **numerische Kodierung** erstellt eine Tabelle der verschiedenen Sorten und ersetzt anschließend den Sortennamen durch einen Index in dieser Tabelle. Dies ist keine gute Idee für lineare Regression, da die lineare Regression den tatsächlichen numerischen Wert des Index nimmt und ihn mit einem Koeffizienten multipliziert zum Ergebnis hinzufügt. In unserem Fall ist die Beziehung zwischen Indexnummer und Preis klar nichtlinear, auch wenn wir sicherstellen, dass die Indizes in einer bestimmten Reihenfolge sind.
* **One-Hot-Kodierung** ersetzt die Spalte `Variety` durch 4 verschiedene Spalten, eine für jede Sorte. Jede Spalte enthält eine `1`, wenn die entsprechende Zeile die gegebene Sorte hat, andernfalls `0`. Das bedeutet, dass es vier Koeffizienten in der linearen Regression gibt, einen für jede Kürbissorte, der für den „Startpreis“ (besser gesagt den „zusätzlichen Preis“) dieser Sorte verantwortlich ist.

Der folgende Code zeigt, wie wir eine Sorte one-hot kodieren können:

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

Um lineare Regression mit one-hot kodierter Sorte als Eingabe zu trainieren, müssen wir nur `X` und `y` richtig initialisieren:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Der restliche Code ist derselbe wie der obige zum Trainieren der linearen Regression. Wenn du es ausprobierst, wirst du sehen, dass der mittlere quadratische Fehler ungefähr gleich ist, aber wir erhalten einen viel höheren Bestimmtheitsmaß (~77 %). Für noch genauere Vorhersagen können wir mehr kategorische Merkmale sowie numerische Merkmale wie `Month` oder `DayOfYear` berücksichtigen. Um ein großes Array von Merkmalen zu erhalten, können wir `join` verwenden:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Hier beziehen wir auch `City` und `Package`-Typ ein, was uns eine MSE von 2,84 (10 %) und eine Bestimmtheit von 0,94 verschafft!

## Alles zusammenführen

Um das beste Modell zu erstellen, können wir kombinierte (one-hot kodierte kategoriale + numerische) Daten aus dem obigen Beispiel zusammen mit polynomieller Regression verwenden. Hier ist der komplette Code zu deiner Bequemlichkeit:

```python
# Trainingsdaten einrichten
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# Train-Test-Aufteilung machen
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# Pipeline einrichten und trainieren
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# Ergebnisse für Testdaten vorhersagen
pred = pipeline.predict(X_test)

# MSE und Bestimmtheitsmaß berechnen
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Dies sollte uns den besten Bestimmtheitsmaß von fast 97 % und eine MSE von 2,23 (~8 % Vorhersagefehler) liefern.

| Modell | MSE | Bestimmtheitsmaß |
|-------|-----|------------------|
| `DayOfYear` Linear | 2,77 (17,2 %) | 0,07 |
| `DayOfYear` Polynomial | 2,73 (17,0 %) | 0,08 |
| `Variety` Linear | 5,24 (19,7 %) | 0,77 |
| Alle Merkmale Linear | 2,84 (10,5 %) | 0,94 |
| Alle Merkmale Polynomial | 2,23 (8,25 %) | 0,97 |

🏆 Gut gemacht! Du hast in einer Lektion vier Regressionsmodelle erstellt und die Modellqualität auf 97 % verbessert. Im abschließenden Abschnitt zur Regression lernst du mehr über logistische Regression zur Bestimmung von Kategorien.

---
## 🚀 Herausforderung

Teste in diesem Notebook verschiedene Variablen, um zu sehen, wie die Korrelation mit der Modellgenauigkeit zusammenhängt.

## [Post-Vorlesungs-Quiz](https://ff-quizzes.netlify.app/en/ml/)

## Rückblick & Selbststudium

In dieser Lektion haben wir lineare Regression kennengelernt. Es gibt weitere wichtige Regressionsarten. Lies über Stepwise, Ridge, Lasso und Elasticnet-Techniken. Ein guter Kurs zur Vertiefung ist der [Stanford Statistical Learning Kurs](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning).

## Aufgabenstellung

[Erstelle ein Modell](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Haftungsausschluss**:  
Dieses Dokument wurde mit dem KI-Übersetzungsdienst [Co-op Translator](https://github.com/Azure/co-op-translator) übersetzt. Obwohl wir uns um Genauigkeit bemühen, beachten Sie bitte, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das ursprüngliche Dokument in seiner Ursprungssprache gilt als maßgebliche Quelle. Für wichtige Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die aus der Nutzung dieser Übersetzung entstehen.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->