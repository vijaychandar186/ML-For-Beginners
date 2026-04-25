# Construire un modèle de régression avec Scikit-learn : régression de quatre manières

## Note pour débutants

La régression linéaire est utilisée lorsque nous voulons prédire une **valeur numérique** (par exemple, le prix d'une maison, la température ou les ventes).
Elle fonctionne en trouvant une droite qui représente au mieux la relation entre les caractéristiques d'entrée et la sortie.

Dans cette leçon, nous nous concentrons sur la compréhension du concept avant d'explorer des techniques de régression plus avancées.
![Comparaison entre régression linéaire et polynomiale](../../../../translated_images/fr/linear-polynomial.5523c7cb6576ccab.webp)
> Infographie par [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Quiz pré-lecture](https://ff-quizzes.netlify.app/en/ml/)

> ### [Cette leçon est disponible en R !](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introduction

Jusqu'à présent, vous avez exploré ce qu'est la régression avec des données d'exemple issues du dataset de prix de citrouilles que nous utiliserons tout au long de cette leçon. Vous l'avez également visualisé avec Matplotlib.

Vous êtes maintenant prêt à approfondir la régression en Machine Learning. Alors que la visualisation permet de donner du sens aux données, la véritable puissance du Machine Learning provient de _l'entraînement des modèles_. Les modèles sont entraînés sur des données historiques afin de capturer automatiquement les dépendances dans les données, et ils permettent de prédire les résultats pour de nouvelles données que le modèle n'a jamais vues auparavant.

Dans cette leçon, vous apprendrez davantage sur deux types de régression : la _régression linéaire basique_ et la _régression polynomiale_, ainsi que quelques notions mathématiques sous-jacentes à ces techniques. Ces modèles nous permettront de prédire les prix des citrouilles en fonction de différentes données d'entrée.

[![ML pour débutants - Comprendre la régression linéaire](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Cliquez sur l'image ci-dessus pour une courte vidéo introductive sur la régression linéaire.

> Tout au long de ce parcours, nous partons du principe d’une connaissance mathématique minimale, et cherchons à la rendre accessible aux étudiants venant d’autres domaines, donc surveillez les notes, 🧮 encadrés, diagrammes et autres outils pédagogiques pour faciliter la compréhension.

### Prérequis

Vous devriez maintenant connaître la structure des données des citrouilles que nous examinons. Vous les trouverez préchargées et pré-nettoyées dans le fichier _notebook.ipynb_ de cette leçon. Dans ce fichier, le prix des citrouilles est affiché par boisseau dans un nouveau DataFrame. Assurez-vous de pouvoir exécuter ces notebooks dans des kernels de Visual Studio Code.

### Préparation

Pour rappel, vous chargez ces données afin de pouvoir leur poser des questions.

- Quel est le meilleur moment pour acheter des citrouilles ?  
- Quel prix puis-je attendre pour une caisse de mini citrouilles ?  
- Dois-je les acheter en paniers de demi-boisseau ou par cartons de 1 1/9 boisseau ?  
Continuons à creuser ces données.

Dans la leçon précédente, vous avez créé un DataFrame Pandas et l'avez rempli avec une partie du dataset original, en standardisant les prix par boisseau. Ce faisant, vous avez cependant rassemblé environ 400 points de données uniquement pour les mois d'automne.

Jetez un coup d'œil aux données que nous avons préchargées dans le notebook accompagnant cette leçon. Les données sont préchargées et une première représentation en nuage de points est affichée pour montrer les données par mois. Peut-être pouvons-nous obtenir plus de détails sur la nature des données en les nettoyant davantage.

## Une droite de régression linéaire

Comme vous l'avez appris dans la Leçon 1, le but d'un exercice de régression linéaire est de pouvoir tracer une droite pour :

- **Montrer les relations entre variables**. Montrer la relation entre les variables
- **Faire des prédictions**. Faire des prédictions précises sur la position d’un nouveau point de données par rapport à cette droite.

Il est typique que la **Régression des moindres carrés** dessine ce type de droite. Le terme "moindres carrés" fait référence au processus de minimisation de l'erreur totale dans notre modèle. Pour chaque point de données, nous mesurons la distance verticale (appelée résidu) entre le point réel et notre droite de régression.

Nous mettons au carré ces distances pour deux raisons principales :

1. **Magnitude plutôt que direction :** Nous voulons traiter une erreur de -5 de la même manière qu’une erreur de +5. La mise au carré rend toutes les valeurs positives.

2. **Pénaliser les valeurs extrêmes :** Mettre au carré donne plus de poids aux erreurs importantes, ce qui force la droite à rester plus proche des points éloignés.

Nous ajoutons ensuite toutes ces valeurs mises au carré. Notre objectif est de trouver la droite spécifique pour laquelle cette somme finale est la plus faible (plus petite valeur possible) — d'où le nom "moindres carrés".

> **🧮 Montrez-moi les mathématiques**
>
> Cette droite, appelée _droite d'ajustement_, peut s'exprimer par [une équation](https://en.wikipedia.org/wiki/Simple_linear_regression) :  
> 
> ```
> Y = a + bX
> ```
>
> `X` est la « variable explicative ». `Y` est la « variable dépendante ». La pente de la droite est `b` et `a` est l'ordonnée à l'origine, qui correspond à la valeur de `Y` quand `X = 0`.
>
>![calculer la pente](../../../../translated_images/fr/slope.f3c9d5910ddbfcf9.webp)
>
> D'abord, calculez la pente `b`. Infographie par [Jen Looper](https://twitter.com/jenlooper)
>
> En d’autres termes, et en se référant à la question originale de nos données sur les citrouilles : "prédire le prix d’une citrouille par boisseau selon le mois", `X` se réfèrerait au prix et `Y` au mois de vente.
>
>![compléter l'équation](../../../../translated_images/fr/calculation.a209813050a1ddb1.webp)
>
> Calculez la valeur de Y. Si vous payez environ 4 $, cela doit être avril ! Infographie par [Jen Looper](https://twitter.com/jenlooper)
>
> Les mathématiques qui calculent la droite doivent montrer la pente de la droite, qui dépend aussi de l’ordonnée à l'origine, ou la position de `Y` lorsque `X = 0`.
>
> Vous pouvez observer la méthode de calcul de ces valeurs sur le site [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Visitez également [ce calculateur de moindres carrés](https://www.mathsisfun.com/data/least-squares-calculator.html) pour voir comment les valeurs numériques influencent la droite.

## Corrélation

Un autre terme à comprendre est le **coefficient de corrélation** entre les variables X et Y données. À l’aide d’un nuage de points, vous pouvez rapidement visualiser ce coefficient. Un graphique avec les points de données alignés de façon nette possède une corrélation élevée, mais un graphique avec des points dispersés partout entre X et Y a une faible corrélation.

Un bon modèle de régression linéaire est celui qui a un coefficient de corrélation élevé (plus proche de 1 que de 0) utilisant la méthode des moindres carrés avec une droite de régression.

✅ Exécutez le notebook accompagnant cette leçon et regardez le nuage de points du mois par rapport au prix. Les données associant le mois au prix pour les ventes de citrouilles semblent-elles avoir une corrélation élevée ou faible selon votre interprétation visuelle du nuage de points ? Cela change-t-il si vous utilisez une mesure plus fine au lieu de `Month`, par ex. *le jour de l’année* (c’est-à-dire le nombre de jours écoulés depuis le début de l’année) ?

Dans le code ci-dessous, nous supposons que nous avons nettoyé les données et obtenu un DataFrame appelé `new_pumpkins`, similaire à ce qui suit :

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> Le code pour nettoyer les données est disponible dans [`notebook.ipynb`](notebook.ipynb). Nous avons effectué les mêmes étapes de nettoyage que dans la leçon précédente, et avons calculé la colonne `DayOfYear` en utilisant l'expression suivante :

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Maintenant que vous comprenez les mathématiques derrière la régression linéaire, créons un modèle de régression pour voir si nous pouvons prédire quel emballage de citrouilles aura les meilleurs prix. Quelqu'un achetant des citrouilles pour un patch de citrouilles à l'occasion des fêtes voudrait peut-être cette information pour optimiser ses achats.

## Recherche de corrélation

[![ML pour débutants - Recherche de corrélation : la clé de la régression linéaire](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Cliquez sur l'image ci-dessus pour une courte vidéo introductive sur la corrélation.

D’après la leçon précédente, vous avez probablement vu que le prix moyen pour différents mois ressemble à ceci :

<img alt="Prix moyen par mois" src="../../../../translated_images/fr/barchart.a833ea9194346d76.webp" width="50%"/>

Cela suggère qu’il devrait y avoir une certaine corrélation, et nous pouvons essayer d'entraîner un modèle de régression linéaire pour prédire la relation entre `Month` et `Price`, ou entre `DayOfYear` et `Price`. Voici le nuage de points qui montre cette dernière relation :

<img alt="Nuage de points du prix en fonction du jour de l'année" src="../../../../translated_images/fr/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Voyons s’il existe une corrélation en utilisant la fonction `corr` :

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Il semble que la corrélation soit plutôt faible, -0.15 pour `Month` et -0.17 pour `DayOfMonth`, mais il pourrait y avoir une autre relation importante. Il semble y avoir différents groupes de prix correspondant à différentes variétés de citrouilles. Pour confirmer cette hypothèse, traçons chaque catégorie de citrouilles avec une couleur différente. En passant un paramètre `ax` à la fonction de tracé `scatter`, nous pouvons représenter tous les points sur le même graphique :

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Nuage de points du prix en fonction du jour de l'année coloré par variété" src="../../../../translated_images/fr/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Notre investigation suggère que la variété a plus d’effet sur le prix global que la date réelle de vente. Nous pouvons le voir avec un graphique en barres :

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Graphique en barres du prix selon la variété" src="../../../../translated_images/fr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Concentrons-nous pour l’instant sur une seule variété de citrouille, le type « pie », et voyons l’effet de la date sur le prix :

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Nuage de points du prix en fonction du jour de l'année pour les citrouilles de type pie" src="../../../../translated_images/fr/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Si nous calculons maintenant la corrélation entre `Price` et `DayOfYear` avec la fonction `corr`, nous obtiendrons environ `-0.27` — ce qui signifie que l’entraînement d’un modèle prédictif est pertinent.

> Avant d’entraîner un modèle de régression linéaire, il est important de s’assurer que nos données sont propres. La régression linéaire ne fonctionne pas bien avec des valeurs manquantes, il est donc judicieux de supprimer toutes les cellules vides :

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Une autre approche serait de remplir ces valeurs vides avec la moyenne des valeurs de la colonne correspondante.

## Régression linéaire simple

[![ML pour débutants - Régression linéaire et polynomiale avec Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Cliquez sur l'image ci-dessus pour une courte vidéo introductive sur la régression linéaire et polynomiale.

Pour entraîner notre modèle de régression linéaire, nous utiliserons la bibliothèque **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Nous commençons par séparer les valeurs d'entrée (features) et la sortie attendue (label) dans des tableaux numpy distincts :

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Notez que nous avons dû effectuer un `reshape` sur les données d'entrée pour que le package de régression linéaire les comprenne correctement. La régression linéaire attend un tableau 2D en entrée, où chaque ligne du tableau correspond à un vecteur de caractéristiques d'entrée. Dans notre cas, comme nous avons une seule entrée, nous avons besoin d’un tableau de forme N&times;1, où N est la taille du dataset.

Ensuite, nous devons diviser les données en ensembles d'entraînement et de test, afin de pouvoir valider notre modèle après l’entraînement :

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Enfin, l’entraînement du modèle de régression linéaire réel ne prend que deux lignes de code. Nous définissons l’objet `LinearRegression`, et l'appliquons à nos données avec la méthode `fit` :

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

L'objet `LinearRegression` après avoir été ajusté (`fit`) contient tous les coefficients de la régression, accessibles via la propriété `.coef_`. Dans notre cas, il n'y a qu'un seul coefficient, qui devrait être autour de `-0.017`. Cela signifie que les prix semblent baisser légèrement avec le temps, mais pas trop, d'environ 2 centimes par jour. Nous pouvons également accéder au point d'intersection de la régression avec l'axe des ordonnées en utilisant `lin_reg.intercept_` - il sera autour de `21` dans notre cas, indiquant le prix au début de l'année.

Pour voir la précision de notre modèle, nous pouvons prédire les prix sur un ensemble de test, puis mesurer la proximité de nos prédictions avec les valeurs attendues. Cela peut être fait en utilisant la métrique de l'erreur quadratique moyenne (RMSE), qui est la racine de la moyenne de toutes les différences au carré entre la valeur attendue et la valeur prédite.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Notre erreur semble être autour de 2 points, ce qui est environ 17 %. Pas très bon. Un autre indicateur de la qualité du modèle est le **coefficient de détermination**, que l'on peut obtenir ainsi :

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Si la valeur est 0, cela signifie que le modèle ne prend pas en compte les données d'entrée et agit comme le *pire prédicteur linéaire*, qui est simplement une valeur moyenne du résultat. Une valeur de 1 signifie que nous pouvons prédire parfaitement toutes les sorties attendues. Dans notre cas, le coefficient est autour de 0.06, ce qui est assez faible.

Nous pouvons aussi tracer les données de test avec la droite de régression pour mieux voir comment la régression fonctionne dans notre cas :

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/fr/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Régression Polynomiale

Un autre type de régression linéaire est la régression polynomiale. Bien qu'il existe parfois une relation linéaire entre les variables - plus la citrouille est volumineuse, plus son prix est élevé - parfois ces relations ne peuvent pas être représentées par un plan ou une droite.

✅ Voici [quelques autres exemples](https://online.stat.psu.edu/stat501/lesson/9/9.8) de données pouvant utiliser la régression polynomiale.

Regardez à nouveau la relation entre Date et Prix. Ce nuage de points semble-t-il nécessairement devoir être analysé par une droite ? Les prix ne peuvent-ils pas fluctuer ? Dans ce cas, vous pouvez essayer la régression polynomiale.

✅ Les polynômes sont des expressions mathématiques qui peuvent comporter une ou plusieurs variables et coefficients.

La régression polynomiale crée une courbe pour mieux ajuster des données non linéaires. Dans notre cas, si nous ajoutons une variable `DayOfYear` au carré dans les données d'entrée, nous devrions pouvoir ajuster nos données avec une courbe parabolique, qui aura un minimum à un certain point de l'année.

Scikit-learn inclut une API pratique de [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) pour combiner différentes étapes du traitement des données. Un **pipeline** est une chaîne d'**estimateurs**. Dans notre cas, nous allons créer un pipeline qui ajoute d'abord des caractéristiques polynomiales à notre modèle, puis entraîne la régression :

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Utiliser `PolynomialFeatures(2)` signifie que nous inclurons tous les polynômes de degré 2 issus des données d'entrée. Dans notre cas cela veut dire simplement `DayOfYear`<sup>2</sup>, mais pour deux variables d'entrée X et Y, cela ajouterait X<sup>2</sup>, XY et Y<sup>2</sup>. On peut aussi utiliser des polynômes de degré plus élevé si on le souhaite.

Les pipelines peuvent être utilisés de la même manière que l'objet `LinearRegression` d'origine, c'est-à-dire que nous pouvons `fit` le pipeline, puis utiliser `predict` pour obtenir les résultats de la prédiction. Voici le graphique montrant les données de test et la courbe d'approximation :

<img alt="Polynomial regression" src="../../../../translated_images/fr/poly-results.ee587348f0f1f60b.webp" width="50%" />

Avec la régression polynomiale, nous pouvons obtenir un MSE légèrement plus faible et une détermination plus élevée, mais pas de manière significative. Nous devons prendre en compte d'autres caractéristiques !

> Vous pouvez voir que les prix minimaux des citrouilles sont observés vers Halloween. Comment expliquer cela ?

🎃 Félicitations, vous venez de créer un modèle qui peut aider à prédire le prix des citrouilles pour tarte. Vous pouvez probablement répéter la même procédure pour tous les types de citrouilles, mais cela serait fastidieux. Apprenons maintenant à prendre en compte la variété des citrouilles dans notre modèle !

## Caractéristiques Catégoriques

Dans un monde idéal, nous souhaitons pouvoir prédire les prix pour différentes variétés de citrouilles avec le même modèle. Cependant, la colonne `Variety` est un peu différente des colonnes comme `Month`, car elle contient des valeurs non numériques. Ces colonnes s'appellent **catégoriques**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Cliquez sur l'image ci-dessus pour une courte vidéo présentant l’utilisation des caractéristiques catégoriques.

Ici, vous pouvez voir comment le prix moyen dépend de la variété :

<img alt="Average price by variety" src="../../../../translated_images/fr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Pour prendre la variété en compte, il faut d'abord la convertir en forme numérique, c'est-à-dire **l'encoder**. Plusieurs méthodes existent :

* Un simple **encodage numérique** va construire un tableau des différentes variétés, puis remplacer le nom de la variété par un indice dans ce tableau. Ce n’est pas la meilleure idée pour la régression linéaire, car la régression linéaire prend la valeur numérique réelle de cet indice et l’ajoute au résultat, multipliée par un coefficient. Or dans notre cas, la relation entre le numéro d'indice et le prix est clairement non linéaire, même si on ordonne les indices d'une certaine manière.
* **L'encodage one-hot** remplace la colonne `Variety` par 4 colonnes différentes, une pour chaque variété. Chaque colonne contient `1` si la ligne correspond à cette variété, et `0` sinon. Cela signifie qu'il y aura quatre coefficients dans la régression linéaire, un pour chaque variété de citrouille, correspondant au « prix de départ » (ou plutôt « prix supplémentaire ») pour cette variété particulière.

Le code ci-dessous montre comment appliquer un encodage one-hot à une variété :

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

Pour entraîner une régression linéaire en utilisant la variété encodée one-hot comme entrée, il suffit d'initialiser correctement les données `X` et `y` :

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Le reste du code est identique à ce que nous avons utilisé ci-dessus pour entraîner la régression linéaire. Si vous essayez, vous verrez que l'erreur quadratique moyenne est à peu près la même, mais que le coefficient de détermination est beaucoup plus élevé (~77 %). Pour obtenir des prédictions encore plus précises, on peut prendre en compte plus de caractéristiques catégoriques ainsi que des caractéristiques numériques, telles que `Month` ou `DayOfYear`. Pour obtenir un grand tableau de caractéristiques, on peut utiliser la fonction `join` :

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Ici, nous prenons aussi en compte `City` et le type de `Package`, ce qui nous donne un MSE de 2.84 (10 %) et une détermination de 0.94 !

## Tout mettre ensemble

Pour créer le meilleur modèle, nous pouvons utiliser les données combinées (catégoriques encodées en one-hot + numériques) de l'exemple précédent, avec la régression polynomiale. Voici le code complet pour votre commodité :

```python
# préparer les données d'entraînement
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# effectuer la séparation train-test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# configurer et entraîner le pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prédire les résultats pour les données de test
pred = pipeline.predict(X_test)

# calculer la MSE et le coefficient de détermination
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Cela devrait nous donner le meilleur coefficient de détermination à presque 97 %, et un MSE de 2.23 (~8 % d’erreur de prédiction).

| Modèle | MSE | Détermination |
|-------|-----|---------------|
| Linéaire `DayOfYear` | 2.77 (17,2 %) | 0.07 |
| Polynomial `DayOfYear` | 2.73 (17,0 %) | 0.08 |
| Linéaire `Variety` | 5.24 (19,7 %) | 0.77 |
| Toutes caractéristiques Linéaire | 2.84 (10,5 %) | 0.94 |
| Toutes caractéristiques Polynomial | 2.23 (8,25 %) | 0.97 |

🏆 Bravo ! Vous avez créé quatre modèles de régression en une leçon et amélioré la qualité du modèle à 97 %. Dans la section finale sur la régression, vous apprendrez la régression logistique pour déterminer des catégories.

---
## 🚀Défi

Testez plusieurs variables différentes dans ce notebook pour voir comment la corrélation correspond à la précision du modèle.

## [Quiz post-cours](https://ff-quizzes.netlify.app/en/ml/)

## Revue & Auto-Étude

Dans cette leçon, nous avons appris la régression linéaire. Il existe d'autres types importants de régression. Lisez sur les techniques Stepwise, Ridge, Lasso et Elasticnet. Un bon cours à suivre pour en apprendre davantage est le [cours d’apprentissage statistique de Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Devoir

[Construisez un modèle](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatiques peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant foi. Pour les informations cruciales, une traduction professionnelle humaine est recommandée. Nous ne pouvons être tenus responsables des malentendus ou erreurs d'interprétation résultant de l'utilisation de cette traduction.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->