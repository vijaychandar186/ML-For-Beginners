# Costruire un modello di regressione usando Scikit-learn: quattro tipi di regressione

## Nota per principianti

La regressione lineare viene usata quando vogliamo prevedere un **valore numerico** (per esempio, prezzo di una casa, temperatura, o vendite).  
Funziona trovando una linea retta che rappresenta nel miglior modo possibile la relazione tra le caratteristiche in input e l'output.

In questa lezione, ci concentriamo sulla comprensione del concetto prima di esplorare tecniche di regressione più avanzate.  
![Infografica su regressione lineare vs polinomiale](../../../../translated_images/it/linear-polynomial.5523c7cb6576ccab.webp)  
> Infografica di [Dasani Madipalli](https://twitter.com/dasani_decoded)  
## [Quiz pre-lezione](https://ff-quizzes.netlify.app/en/ml/)

> ### [Questa lezione è disponibile in R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)  
### Introduzione

Finora hai esplorato cosa sia la regressione con dati di esempio raccolti dal dataset dei prezzi delle zucche che useremo per tutta questa lezione. Hai anche visualizzato i dati usando Matplotlib.

Ora sei pronto per approfondire la regressione per l’apprendimento automatico. Mentre la visualizzazione ti permette di dare un senso ai dati, la vera potenza del Machine Learning deriva dall’_addestramento dei modelli_. I modelli vengono addestrati su dati storici per catturare automaticamente le dipendenze nei dati, e ti permettono di prevedere risultati per dati nuovi, che il modello non ha mai visto prima.

In questa lezione, imparerai di più su due tipi di regressione: _regressione lineare base_ e _regressione polinomiale_, insieme ad alcune delle matematiche sottostanti a queste tecniche. Questi modelli ci permetteranno di predire il prezzo delle zucche in base a diversi dati in input.

[![ML per principianti - Comprendere la regressione lineare](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML per principianti - Comprendere la regressione lineare")

> 🎥 Clicca sull'immagine sopra per una breve panoramica video sulla regressione lineare.

> In tutto questo curriculum, presumiamo una conoscenza minima di matematica, e cerchiamo di renderlo accessibile a studenti provenienti da altri campi, quindi fai attenzione a note, 🧮 richiamo di concetti, diagrammi e altri strumenti didattici per aiutare nella comprensione.

### Prerequisiti

Dovresti ora essere familiare con la struttura dei dati delle zucche che stiamo esaminando. Puoi trovarli precaricati e già puliti nel file _notebook.ipynb_ di questa lezione. Nel file, il prezzo delle zucche è mostrato per bushel in un nuovo dataframe. Assicurati di poter eseguire questi notebook nei kernel in Visual Studio Code.

### Preparazione

Come promemoria, stai caricando questi dati per poter porre domande su di essi.

- Qual è il momento migliore per acquistare zucche?  
- Quale prezzo posso aspettarmi per una cassa di zucche miniatura?  
- Conviene acquistarle in cestini da mezzo bushel o nella scatola da 1 1/9 bushel?  
Continuiamo a scavare in questi dati.

Nella lezione precedente, hai creato un dataframe Pandas e l'hai popolato con parte del dataset originale, standardizzando i prezzi per bushel. Facendo così, però, hai potuto raccogliere solo circa 400 punti dati e solo per i mesi autunnali.

Dai un’occhiata ai dati precaricati nel notebook allegato a questa lezione. I dati sono già caricati e viene mostrato un primo scatterplot per visualizzare i dati mensili. Forse possiamo ottenere qualche dettaglio in più sulla natura dei dati pulendoli ulteriormente.

## Una linea di regressione lineare

Come hai appreso nella Lezione 1, l'obiettivo di un esercizio di regressione lineare è poter disegnare una linea per:

- **Mostrare le relazioni tra variabili**. Mostrare la relazione tra le variabili  
- **Fare previsioni**. Fare previsioni accurate su dove cadrebbe un nuovo punto dati in relazione a quella linea.  

È tipico della **regressione ai minimi quadrati** tracciare questo tipo di linea. Il termine "minimi quadrati" si riferisce al processo di minimizzazione dell'errore totale nel nostro modello. Per ogni punto dati, misuriamo la distanza verticale (chiamata residuo) tra il punto effettivo e la nostra linea di regressione.

Eleviamo al quadrato queste distanze per due motivi principali:

1. **Magnitudo oltre alla direzione:** Vogliamo trattare un errore di -5 allo stesso modo di uno di +5. Elevando al quadrato tutti i valori diventano positivi.

2. **Pena per gli outlier:** Elevando al quadrato si dà più peso agli errori più grandi, costringendo la linea a stare più vicina ai punti lontani.

Poi sommiamo tutti questi valori al quadrato. Il nostro obiettivo è trovare la specifica linea dove questa somma finale è minima (il valore più piccolo possibile)—da qui il nome "minimi quadrati".

> **🧮 Mostrami la matematica**  
>  
> Questa linea, chiamata _linea di miglior adattamento_ può essere espressa con [un'equazione](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` è la 'variabile esplicativa'. `Y` è la 'variabile dipendente'. La pendenza della linea è `b` e `a` è l'intercetta y, cioè il valore di `Y` quando `X = 0`.  
>  
>![calcolare la pendenza](../../../../translated_images/it/slope.f3c9d5910ddbfcf9.webp)  
>  
> Per prima cosa, calcola la pendenza `b`. Infografica di [Jen Looper](https://twitter.com/jenlooper)  
>  
> In altre parole, e riferendoci alla nostra domanda originale sui dati delle zucche: "prevedere il prezzo di una zucca per bushel in base al mese", `X` si riferirebbe al prezzo e `Y` al mese di vendita.  
>  
>![completa l'equazione](../../../../translated_images/it/calculation.a209813050a1ddb1.webp)  
>  
> Calcola il valore di Y. Se stai pagando circa 4 dollari, deve essere aprile! Infografica di [Jen Looper](https://twitter.com/jenlooper)  
>  
> La matematica che calcola la linea deve dimostrare la pendenza della linea, che dipende anche dall’intercetta, ovvero dove si trova `Y` quando `X = 0`.  
>  
> Puoi osservare il metodo di calcolo di questi valori sul sito [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Visita anche [questa calcolatrice per i minimi quadrati](https://www.mathsisfun.com/data/least-squares-calculator.html) per vedere come i valori influenzano la linea.

## Correlazione

Un altro termine da comprendere è il **coefficiente di correlazione** tra le variabili X e Y date. Usando uno scatterplot, puoi visualizzare rapidamente questo coefficiente. Un grafico con punti dati disposti su una linea ordinata ha alta correlazione, mentre un grafico con punti sparsi ovunque tra X e Y ha bassa correlazione.

Un buon modello di regressione lineare sarà quello che ha un coefficiente di correlazione alto (più vicino a 1 che a 0) usando il metodo di regressione ai minimi quadrati con una linea di regressione.

✅ Esegui il notebook allegato a questa lezione e guarda lo scatterplot da Mese a Prezzo. I dati che associano il mese al prezzo per la vendita delle zucche sembrano avere alta o bassa correlazione, secondo la tua interpretazione visiva dello scatterplot? Cambia qualcosa se usi una misura più dettagliata invece di `Month`, per esempio *giorno dell’anno* (cioè numero di giorni dall’inizio dell’anno)?

Nel codice seguente, supponiamo di aver pulito i dati, e ottenuto un dataframe chiamato `new_pumpkins`, simile al seguente:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Il codice per pulire i dati è disponibile in [`notebook.ipynb`](notebook.ipynb). Abbiamo eseguito gli stessi passaggi di pulizia della lezione precedente e abbiamo calcolato la colonna `DayOfYear` con l’espressione seguente:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Ora che hai una comprensione della matematica dietro la regressione lineare, creiamo un modello di regressione per vedere se possiamo prevedere quale confezione di zucche avrà i prezzi migliori. Qualcuno che compra zucche per una festa di Halloween potrebbe voler questa informazione per ottimizzare i propri acquisti di zucche.

## Cercare la correlazione

[![ML per principianti - Cercare la correlazione: la chiave per la regressione lineare](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML per principianti - Cercare la correlazione: la chiave per la regressione lineare")

> 🎥 Clicca sull'immagine sopra per una breve panoramica video sulla correlazione.

Dalla lezione precedente probabilmente hai visto che il prezzo medio per diversi mesi si presenta così:

<img alt="Prezzo medio per mese" src="../../../../translated_images/it/barchart.a833ea9194346d76.webp" width="50%"/>

Questo suggerisce che ci dovrebbe essere qualche correlazione, e possiamo provare ad addestrare un modello di regressione lineare per predire la relazione tra `Month` e `Price`, o tra `DayOfYear` e `Price`. Qui c’è lo scatter plot che mostra quest’ultima relazione:

<img alt="Scatter plot di Prezzo vs. Giorno dell'anno" src="../../../../translated_images/it/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Vediamo se c’è una correlazione usando la funzione `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Sembra che la correlazione sia piuttosto bassa, -0.15 rispetto a `Month` e -0.17 rispetto a `DayOfMonth`, ma potrebbe esserci un’altra relazione importante. Sembra che ci siano diversi cluster di prezzi corrispondenti a diverse varietà di zucche. Per confermare questa ipotesi, tracciamo ogni categoria di zucca usando un colore diverso. Passando un parametro `ax` alla funzione di plot `scatter` possiamo disegnare tutti i punti sullo stesso grafico:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Scatter plot di Prezzo vs. Giorno dell'anno" src="../../../../translated_images/it/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

La nostra indagine suggerisce che la varietà ha un effetto maggiore sul prezzo complessivo rispetto alla data reale di vendita. Vediamo questo con un grafico a barre:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Grafico a barre del prezzo per varietà" src="../../../../translated_images/it/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Concentriamoci per un momento solamente su una varietà di zucca, la 'pie type', e vediamo quale effetto ha la data sul prezzo:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot di Prezzo vs. Giorno dell'anno" src="../../../../translated_images/it/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Se ora calcoliamo la correlazione tra `Price` e `DayOfYear` usando la funzione `corr`, otterremo qualcosa come `-0.27` - il che significa che ha senso addestrare un modello predittivo.

> Prima di addestrare un modello di regressione lineare, è importante assicurarsi che i nostri dati siano puliti. La regressione lineare non funziona bene con valori mancanti, dunque ha senso eliminare tutte le celle vuote:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
Un altro approccio sarebbe quello di riempire quei valori mancanti con la media delle rispettive colonne.

## Regressione Lineare Semplice

[![ML per principianti - Regressione Lineare e Polinomiale usando Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML per principianti - Regressione Lineare e Polinomiale usando Scikit-learn")

> 🎥 Clicca sull'immagine sopra per una breve panoramica video sulla regressione lineare e polinomiale.

Per addestrare il nostro modello di Regressione Lineare, useremo la libreria **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
Iniziamo separando i valori input (caratteristiche) e l’output atteso (etichetta) in array numpy separati:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Nota che abbiamo dovuto eseguire il `reshape` sui dati di input affinché il pacchetto di Regressione Lineare li capisse correttamente. La Regressione Lineare si aspetta un array 2D come input, dove ogni riga dell’array corrisponde a un vettore di caratteristiche in input. Nel nostro caso, poiché abbiamo un solo input, ci serve un array di forma N&times;1, dove N è la dimensione del dataset.

Poi, dobbiamo dividere i dati in set di addestramento e di test, così possiamo validare il modello dopo l’addestramento:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
Infine, addestrare il modello vero e proprio di Regressione Lineare richiede solo due righe di codice. Definiamo l’oggetto `LinearRegression`, e lo adattiamo ai nostri dati usando il metodo `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

L'oggetto `LinearRegression` dopo aver effettuato il `fit` contiene tutti i coefficienti della regressione, che possono essere accessi utilizzando la proprietà `.coef_`. Nel nostro caso, c'è un solo coefficiente, che dovrebbe essere intorno a `-0.017`. Questo significa che i prezzi sembrano diminuire un po' col passare del tempo, ma non troppo, circa 2 centesimi al giorno. Possiamo anche accedere al punto di intersezione della regressione con l'asse Y usando `lin_reg.intercept_` - sarà intorno a `21` nel nostro caso, indicando il prezzo all'inizio dell'anno.

Per vedere quanto è accurato il nostro modello, possiamo prevedere i prezzi su un dataset di test e quindi misurare quanto le nostre previsioni siano vicine ai valori attesi. Questo può essere fatto utilizzando la metrica dell'errore quadratico medio (RMSE), che è la radice della media di tutte le differenze quadrate tra valore atteso e valore previsto.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Il nostro errore sembra essere intorno a 2 punti, cioè ~17%. Non troppo bene. Un altro indicatore della qualità del modello è il **coefficiente di determinazione**, che può essere ottenuto così:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Se il valore è 0, significa che il modello non considera i dati di input e agisce come il *peggior predittore lineare*, che è semplicemente un valore medio del risultato. Il valore 1 significa che possiamo prevedere perfettamente tutti i risultati attesi. Nel nostro caso, il coefficiente è intorno a 0.06, cioè abbastanza basso.

Possiamo anche tracciare i dati di test insieme alla linea di regressione per vedere meglio come funziona la regressione nel nostro caso:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Regressione lineare" src="../../../../translated_images/it/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regressione Polinomiale

Un altro tipo di regressione lineare è la Regressione Polinomiale. Sebbene a volte ci sia una relazione lineare tra le variabili - più grande è la zucca in volume, più alto è il prezzo - a volte queste relazioni non possono essere rappresentate come un piano o una linea retta.

✅ Ecco [alcuni esempi in più](https://online.stat.psu.edu/stat501/lesson/9/9.8) di dati che possono richiedere una Regressione Polinomiale

Dai un'altra occhiata alla relazione tra Data e Prezzo. Questo scatterplot sembra necessariamente dover essere analizzato da una linea retta? I prezzi non possono fluttuare? In questo caso, puoi provare la regressione polinomiale.

✅ I polinomi sono espressioni matematiche che possono consistere in una o più variabili e coefficienti

La regressione polinomiale crea una linea curva per adattarsi meglio ai dati non lineari. Nel nostro caso, se includiamo una variabile `DayOfYear` al quadrato nei dati di input, dovremmo essere in grado di adattare i dati con una curva parabolica, che avrà un minimo in un certo punto dell'anno.

Scikit-learn include un utile [API pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) per combinare insieme diversi passaggi di elaborazione dati. Una **pipeline** è una catena di **stimatori**. Nel nostro caso, creeremo una pipeline che prima aggiunge caratteristiche polinomiali al nostro modello e poi addestra la regressione:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Usare `PolynomialFeatures(2)` significa che includeremo tutti i polinomi di secondo grado dai dati di input. Nel nostro caso significherà solo `DayOfYear`<sup>2</sup>, ma dati due variabili di input X e Y, questo aggiungerà X<sup>2</sup>, XY e Y<sup>2</sup>. Possiamo anche utilizzare polinomi di grado superiore se vogliamo.

Le pipeline possono essere utilizzate nello stesso modo dell'oggetto `LinearRegression` originale, cioè possiamo `fit`tare la pipeline e quindi usare `predict` per ottenere i risultati della previsione. Ecco il grafico che mostra i dati di test e la curva di approssimazione:

<img alt="Regressione polinomiale" src="../../../../translated_images/it/poly-results.ee587348f0f1f60b.webp" width="50%" />

Usando la regressione polinomiale, possiamo ottenere un MSE leggermente più basso e un coefficiente di determinazione più alto, ma non in modo significativo. Dobbiamo prendere in considerazione altre caratteristiche!

> Puoi vedere che i prezzi minimi delle zucche si osservano intorno a Halloween. Come puoi spiegare questo?

🎃 Congratulazioni, hai appena creato un modello che può aiutare a prevedere il prezzo delle zucche da torta. Probabilmente puoi ripetere la stessa procedura per tutti i tipi di zucca, ma sarebbe tedioso. Impariamo ora come considerare la varietà di zucca nel nostro modello!

## Caratteristiche Categoricali

Nel mondo ideale, vogliamo poter prevedere i prezzi per diverse varietà di zucca usando lo stesso modello. Tuttavia, la colonna `Variety` è un po' diversa da colonne come `Month`, perché contiene valori non numerici. Queste colonne sono chiamate **categoriche**.

[![ML per principianti - Previsioni con caratteristiche categoriche e regressione lineare](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML per principianti - Previsioni con caratteristiche categoriche e regressione lineare")

> 🎥 Clicca sull'immagine sopra per un breve video di overview sull'uso delle caratteristiche categoriche.

Qui puoi vedere come il prezzo medio dipende dalla varietà:

<img alt="Prezzo medio per varietà" src="../../../../translated_images/it/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Per considerare la varietà, dobbiamo prima convertirla in forma numerica, o **codificarla**. Ci sono diversi modi per farlo:

* La semplice **codifica numerica** costruisce una tabella delle diverse varietà e poi sostituisce il nome della varietà con un indice in quella tabella. Questa non è la scelta migliore per regressione lineare, perché questa prende il valore numerico effettivo dell'indice e lo aggiunge al risultato moltiplicandolo per un coefficiente. Nel nostro caso, la relazione tra il numero indice e il prezzo è chiaramente non lineare, anche se facciamo in modo che gli indici siano ordinati in un certo modo.
* La **one-hot encoding** sostituirà la colonna `Variety` con 4 colonne diverse, una per ogni varietà. Ogni colonna conterrà `1` se la riga corrispondente è della data varietà, e `0` altrimenti. Questo significa che ci saranno quattro coefficienti nella regressione lineare, uno per ogni varietà di zucca, responsabili del "prezzo di partenza" (o meglio "prezzo aggiuntivo") per quella particolare varietà.

Il codice sotto mostra come possiamo applicare la codifica one-hot alla varietà:

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

Per addestrare la regressione lineare usando la varietà codificata one-hot come input, dobbiamo solo inizializzare correttamente i dati `X` e `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Il resto del codice è lo stesso che abbiamo usato sopra per addestrare la regressione lineare. Se provi, vedrai che l’errore quadratico medio è circa lo stesso, ma otteniamo un coefficiente di determinazione molto più alto (~77%). Per avere previsioni ancora più precise, possiamo considerare altre caratteristiche categoriche oltre che caratteristiche numeriche, come `Month` o `DayOfYear`. Per avere un unico grande array di caratteristiche, possiamo usare `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Qui consideriamo anche `City` e il tipo di `Package`, che ci dà MSE 2.84 (10%) e coefficiente di determinazione 0.94!

## Mettere tutto insieme

Per creare il miglior modello, possiamo usare i dati combinati (categorici codificati one-hot + numerici) dall'esempio sopra insieme alla regressione polinomiale. Ecco il codice completo per la tua comodità:

```python
# impostare i dati di addestramento
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# fare la divisione train-test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# configurare e addestrare la pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prevedere i risultati per i dati di test
pred = pipeline.predict(X_test)

# calcolare MSE e coefficiente di determinazione
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Questo dovrebbe darci il miglior coefficiente di determinazione di quasi 97% e MSE=2.23 (~8% di errore nella previsione).

| Modello | MSE | Coefficiente di determinazione |
|---------|-----|-------------------------------|
| Lineare `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Polinomiale `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Lineare `Variety` | 5.24 (19.7%) | 0.77 |
| Lineare tutte le caratteristiche | 2.84 (10.5%) | 0.94 |
| Polinomiale tutte le caratteristiche | 2.23 (8.25%) | 0.97 |

🏆 Ben fatto! Hai creato quattro modelli di regressione in una lezione e migliorato la qualità del modello fino al 97%. Nella sezione finale su Regressione, imparerai la Regressione Logistica per determinare le categorie.

---
## 🚀Sfida

Prova diverse variabili in questo notebook per vedere come la correlazione corrisponde all’accuratezza del modello.

## [Quiz post-lezione](https://ff-quizzes.netlify.app/en/ml/)

## Revisione & Studio individuale

In questa lezione abbiamo imparato la regressione lineare. Ci sono altri tipi importanti di regressione. Leggi sulle tecniche Stepwise, Ridge, Lasso e Elasticnet. Un buon corso da studiare per approfondire è il [corso Stanford Statistical Learning](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Compito

[Costruisci un modello](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Disclaimer**:  
Questo documento è stato tradotto utilizzando il servizio di traduzione automatica [Co-op Translator](https://github.com/Azure/co-op-translator). Pur impegnandoci per garantire l'accuratezza, si prega di considerare che le traduzioni automatiche possono contenere errori o inesattezze. Il documento originale nella sua lingua madre deve essere considerato la fonte autorevole. Per informazioni critiche, si raccomanda una traduzione professionale umana. Non ci assumiamo alcuna responsabilità per eventuali incomprensioni o interpretazioni errate derivanti dall'uso di questa traduzione.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->