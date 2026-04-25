# Construir um modelo de regressão usando Scikit-learn: regressão de quatro formas

## Nota para iniciantes

A regressão linear é usada quando queremos prever um **valor numérico** (por exemplo, preço da casa, temperatura ou vendas). Funciona encontrando uma linha reta que melhor representa a relação entre as características de entrada e o resultado.

Nesta lição, focamos em entender o conceito antes de explorar técnicas de regressão mais avançadas.
![Infográfico de regressão linear vs polinomial](../../../../translated_images/pt-PT/linear-polynomial.5523c7cb6576ccab.webp)
> Infográfico por [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Questionário pré-aula](https://ff-quizzes.netlify.app/en/ml/)

> ### [Esta lição está disponível em R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introdução

Até agora explorou o que é regressão com dados de exemplo recolhidos do conjunto de dados de preços de abóboras que iremos usar ao longo desta lição. Também visualizou esses dados usando Matplotlib.

Agora está pronto para mergulhar mais fundo na regressão para ML. Enquanto a visualização permite dar sentido aos dados, o verdadeiro poder do Machine Learning vem do _treino de modelos_. Os modelos são treinados em dados históricos para captar automaticamente as dependências dos dados, e permitem prever resultados para novos dados, que o modelo ainda não viu.

Nesta lição, irá aprender mais sobre dois tipos de regressão: _regressão linear básica_ e _regressão polinomial_, juntamente com alguma da matemática subjacente a estas técnicas. Esses modelos permitirão prever preços de abóboras dependendo de diferentes dados de entrada.

[![ML para iniciantes - Compreender Regressão Linear](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML para iniciantes - Compreender Regressão Linear")

> 🎥 Clique na imagem acima para uma curta visão geral em vídeo da regressão linear.

> Ao longo deste currículo, assumimos um conhecimento matemático mínimo, buscando tornar acessível para estudantes de outras áreas, por isso esteja atento a notas, 🧮 destaques, diagramas e outras ferramentas de aprendizagem para ajudar na compreensão.

### Pré-requisitos

Deve estar agora familiarizado com a estrutura dos dados de abóboras que estamos a examinar. Pode encontrá-los pré-carregados e pré-limpados no ficheiro _notebook.ipynb_ desta lição. No ficheiro, o preço da abóbora está apresentado por alqueire num novo data frame. Certifique-se de que pode executar estes notebooks em núcleos (kernels) no Visual Studio Code.

### Preparação

Como lembrete, está a carregar estes dados para fazer perguntas a eles.

- Qual é a melhor altura para comprar abóboras?  
- Que preço posso esperar por uma caixa de pequenas abóboras?  
- Devo comprá-las em cestos de meio alqueire ou numa caixa de 1 1/9 alqueire?  
Vamos continuar a aprofundar estes dados.

Na lição anterior, criou um data frame do Pandas e preencheu-o com parte do conjunto de dados original, padronizando os preços por alqueire. Ao fazer isso, no entanto, conseguiu recolher cerca de 400 pontos de dados e apenas para os meses de outono.

Veja os dados que pré-carregámos no notebook que acompanha esta lição. Os dados vêm pré-carregados e um gráfico de dispersão inicial foi traçado para mostrar os dados do mês. Talvez possamos obter um pouco mais de detalhe sobre a natureza dos dados fazendo uma limpeza maior.

## Uma linha de regressão linear

Como aprendeu na Lição 1, o objetivo de um exercício de regressão linear é conseguir traçar uma linha para:

- **Mostrar relações entre variáveis**. Mostrar a relação entre variáveis  
- **Fazer previsões**. Fazer previsões precisas sobre onde um novo ponto de dados cairia em relação a essa linha.  

É típico da **Regressão pelo Método dos Mínimos Quadrados** desenhar este tipo de linha. O termo "Mínimos Quadrados" refere-se ao processo de minimizar o erro total no nosso modelo. Para cada ponto de dados, medimos a distância vertical (chamada resíduo) entre o ponto real e a nossa linha de regressão.

Elevamos ao quadrado essas distâncias por duas razões principais:

1. **Magnitude sobre direção:** Queremos tratar um erro de -5 da mesma forma que um erro de +5. Elevar ao quadrado torna todos os valores positivos.

2. **Penalização de outliers:** Elevar ao quadrado dá mais peso a erros maiores, obrigando a linha a ficar mais próxima dos pontos distantes.

Depois somamos todos esses valores ao quadrado. O nosso objetivo é encontrar a linha específica onde essa soma final é a menor possível—daí o nome "Mínimos Quadrados".

> **🧮 Mostre-me a matemática**  
>  
> Esta linha, chamada de _linha de melhor ajuste_, pode ser expressa por [uma equação](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` é a 'variável explicativa'. `Y` é a 'variável dependente'. O declive da linha é `b` e `a` é o intercepto em y, que se refere ao valor de `Y` quando `X = 0`.  
>  
>![calcular o declive](../../../../translated_images/pt-PT/slope.f3c9d5910ddbfcf9.webp)  
>  
> Primeiro, calcule o declive `b`. Infográfico por [Jen Looper](https://twitter.com/jenlooper)  
>  
> Por outras palavras, e referindo-nos à pergunta original dos dados das abóboras: "prever o preço por alqueire da abóbora por mês", `X` referir-se-ia ao preço e `Y` ao mês da venda.  
>  
>![completar a equação](../../../../translated_images/pt-PT/calculation.a209813050a1ddb1.webp)  
>  
> Calcule o valor de Y. Se está a pagar cerca de 4 dólares, deve ser abril! Infográfico por [Jen Looper](https://twitter.com/jenlooper)  
>  
> A matemática que calcula a linha deve demonstrar o declive da linha, que também depende do intercepto, ou de onde `Y` está situado quando `X = 0`.  
>  
> Pode observar o método de cálculo destes valores no site [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Visite também [esta calculadora de mínimos quadrados](https://www.mathsisfun.com/data/least-squares-calculator.html) para ver como os valores numéricos impactam a linha.

## Correlação

Mais um termo a compreender é o **Coeficiente de Correlação** entre as variáveis X e Y dadas. Usando um gráfico de dispersão, pode visualizar rapidamente este coeficiente. Um gráfico com pontos de dados dispersos numa linha limpa tem alta correlação, mas um gráfico com pontos dispersos por todo o lado entre X e Y tem baixa correlação.

Um bom modelo de regressão linear será aquele que tem um Coeficiente de Correlação alto (mais próximo de 1 do que de 0) usando o método dos mínimos quadrados com uma linha de regressão.

✅ Execute o notebook que acompanha esta lição e observe o gráfico de dispersão Mês versus Preço. Os dados que associam Mês a Preço para vendas de abóboras parecem ter alta ou baixa correlação, segundo a sua interpretação visual do gráfico de dispersão? Isso muda se usar uma medida mais pormenorizada em vez de `Mês`, por exemplo *dia do ano* (isto é, número de dias desde o início do ano)?

No código abaixo, vamos assumir que limpámos os dados e obtivemos um data frame chamado `new_pumpkins`, semelhante ao seguinte:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> O código para limpar os dados está disponível em [`notebook.ipynb`](notebook.ipynb). Realizámos os mesmos passos de limpeza da lição anterior e calculámos a coluna `DayOfYear` usando a seguinte expressão:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Agora que compreende a matemática por trás da regressão linear, vamos criar um modelo de regressão para ver se conseguimos prever que pacote de abóboras terá os melhores preços. Alguém a comprar abóboras para uma decoração de abóboras para o feriado pode querer esta informação para optimizar as suas compras de pacotes de abóboras para a decoração.

## Procurar correlação

[![ML para iniciantes - Procurar correlação: a chave para regressão linear](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML para iniciantes - Procurar correlação: a chave para regressão linear")

> 🎥 Clique na imagem acima para uma breve visão geral em vídeo da correlação.

Na lição anterior provavelmente viu que o preço médio para diferentes meses se parece com isto:

<img alt="Preço médio por mês" src="../../../../translated_images/pt-PT/barchart.a833ea9194346d76.webp" width="50%"/>

Isto sugere que deve haver alguma correlação, e podemos tentar treinar um modelo de regressão linear para prever a relação entre `Month` e `Price`, ou entre `DayOfYear` e `Price`. Aqui está o gráfico de dispersão que mostra esta última relação:

<img alt="Gráfico de dispersão do preço vs dia do ano" src="../../../../translated_images/pt-PT/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />  

Vamos ver se existe correlação usando a função `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Parece que a correlação é bastante pequena, -0.15 pelo `Month` e -0.17 pelo `DayOfMonth`, mas pode haver outra relação importante. Parece que há diferentes agrupamentos de preços correspondendo a diferentes variedades de abóbora. Para confirmar esta hipótese, vamos representar cada categoria de abóboras com uma cor diferente. Ao passar o parâmetro `ax` para a função de plotagem `scatter` podemos plotar todos os pontos no mesmo gráfico:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Gráfico de dispersão do preço vs dia do ano com cores" src="../../../../translated_images/pt-PT/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" />  

A nossa investigação sugere que a variedade tem mais efeito no preço global do que a data real de venda. Podemos ver isso num gráfico de barras:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Gráfico de barras do preço por variedade" src="../../../../translated_images/pt-PT/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />  

Vamos focar-nos para já apenas numa variedade de abóboras, a do tipo 'pie', e ver que efeito a data tem no preço:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Gráfico de dispersão do preço vs dia do ano para abóboras 'pie'" src="../../../../translated_images/pt-PT/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" />  

Se agora calcularmos a correlação entre `Price` e `DayOfYear` usando a função `corr`, obteremos algo como `-0.27` - o que significa que treinar um modelo preditivo faz sentido.

> Antes de treinar um modelo de regressão linear, é importante garantir que os nossos dados estão limpos. A regressão linear não funciona bem com valores em falta, portanto faz sentido livrar-se de todas as células vazias:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Outra abordagem seria preencher esses valores vazios com a média da coluna correspondente.

## Regressão Linear Simples

[![ML para iniciantes - Regressão Linear e Polinomial usando Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML para iniciantes - Regressão Linear e Polinomial usando Scikit-learn")

> 🎥 Clique na imagem acima para uma breve visão geral em vídeo da regressão linear e polinomial.

Para treinar o nosso modelo de Regressão Linear, vamos usar a biblioteca **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Começamos por separar os valores de entrada (características) e a saída esperada (rótulo) em arrays numpy separados:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Repare que tivemos de fazer um `reshape` nos dados de entrada para que o pacote de Regressão Linear os compreendesse corretamente. A Regressão Linear espera uma matriz 2D como entrada, onde cada linha da matriz corresponde a um vetor de características de entrada. No nosso caso, como temos apenas uma entrada, precisamos de uma matriz com forma N&times;1, onde N é o tamanho do conjunto de dados.

Depois, é necessário dividir os dados nos conjuntos de treino e de teste, para que possamos validar o modelo após o treino:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Finalmente, treinar o modelo de Regressão Linear propriamente dito leva apenas duas linhas de código. Definimos o objeto `LinearRegression` e ajustamo-lo aos nossos dados usando o método `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

O objeto `LinearRegression` após o treino (`fit`) contém todos os coeficientes da regressão, que podem ser acedidos através da propriedade `.coef_`. No nosso caso, há apenas um coeficiente, que deverá ser cerca de `-0.017`. Isto significa que os preços parecem diminuir um pouco com o tempo, mas não demasiado, cerca de 2 cêntimos por dia. Também podemos aceder ao ponto de interseção da regressão com o eixo Y usando `lin_reg.intercept_` - será cerca de `21` no nosso caso, indicando o preço no início do ano.

Para ver quão preciso é o nosso modelo, podemos prever preços num conjunto de dados de teste, e depois medir quão próximas estão as nossas previsões dos valores esperados. Isto pode ser feito usando a métrica root mean square error (RMSE), que é a raiz da média de todas as diferenças quadráticas entre o valor esperado e o previsto.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

O nosso erro parece ser cerca de 2 pontos, o que é ~17%. Nada muito bom. Outro indicador da qualidade do modelo é o **coeficiente de determinação**, que pode ser obtido assim:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Se o valor for 0, significa que o modelo não tem em conta os dados de entrada, e atua como o *pior preditor linear*, que é simplesmente o valor médio do resultado. O valor 1 significa que podemos prever perfeitamente todas as saídas esperadas. No nosso caso, o coeficiente é cerca de 0.06, o que é bastante baixo.

Também podemos desenhar os dados de teste juntamente com a linha de regressão para vermos melhor como funciona a regressão no nosso caso:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/pt-PT/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regressão Polinomial

Outro tipo de Regressão Linear é a Regressão Polinomial. Embora por vezes haja uma relação linear entre variáveis - quanto maior a abóbora em volume, maior o preço - por vezes essas relações não podem ser representadas por um plano ou linha reta.

✅ Aqui estão [mais alguns exemplos](https://online.stat.psu.edu/stat501/lesson/9/9.8) de dados que poderiam usar Regressão Polinomial

Veja outra vez a relação entre Data e Preço. Este gráfico de dispersão parece que deve necessariamente ser analisado por uma linha reta? Será que os preços não podem flutuar? Neste caso, pode tentar a regressão polinomial.

✅ Os polinómios são expressões matemáticas que podem consistir em uma ou mais variáveis e coeficientes

A regressão polinomial cria uma linha curva para melhor ajustar dados não lineares. No nosso caso, se incluirmos uma variável ao quadrado `DayOfYear` nos dados de entrada, deveremos ser capazes de ajustar os nossos dados com uma curva parabólica, que terá um mínimo em certo ponto dentro do ano.

O Scikit-learn inclui uma API útil de [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) para combinar diferentes passos do processamento de dados. Um **pipeline** é uma cadeia de **estimadores**. No nosso caso, vamos criar um pipeline que primeiro adiciona características polinomiais ao nosso modelo, e depois treina a regressão:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Usar `PolynomialFeatures(2)` significa que vamos incluir todos os polinómios de segundo grau a partir dos dados de entrada. No nosso caso, isso significará apenas `DayOfYear`<sup>2</sup>, mas dado duas variáveis de entrada X e Y, isso adicionaria X<sup>2</sup>, XY e Y<sup>2</sup>. Também podemos usar polinómios de grau superior se quisermos.

Os pipelines podem ser usados da mesma forma que o objeto original `LinearRegression`, ou seja, podemos `fit` o pipeline e depois usar `predict` para obter os resultados da previsão. Aqui está o gráfico mostrando os dados de teste e a curva de aproximação:

<img alt="Polynomial regression" src="../../../../translated_images/pt-PT/poly-results.ee587348f0f1f60b.webp" width="50%" />

Usando Regressão Polinomial, podemos obter um MSE ligeiramente inferior e um coeficiente de determinação mais alto, mas não de forma significativa. Precisamos de ter em conta outras características!

> Pode ver que os preços mínimos das abóboras ocorrem por volta do Halloween. Como pode explicar isso? 

🎃 Parabéns, acabou de criar um modelo que pode ajudar a prever o preço de abóboras para torta. Provavelmente poderá repetir o mesmo procedimento para todos os tipos de abóbora, mas isso seria aborrecido. Vamos aprender agora como ter em conta a variedade de abóbora no nosso modelo!

## Características Categóricas

No mundo ideal, queremos ser capazes de prever preços para diferentes variedades de abóbora usando o mesmo modelo. No entanto, a coluna `Variety` é um pouco diferente das colunas como `Month`, porque contém valores não numéricos. Essas colunas são chamadas **categóricas**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Clique na imagem acima para um breve vídeo explicativo sobre o uso de características categóricas.

Aqui pode ver como o preço médio depende da variedade:

<img alt="Average price by variety" src="../../../../translated_images/pt-PT/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Para ter a variedade em conta, primeiro precisamos convertê-la para forma numérica, ou **codificá-la**. Existem várias maneiras de o fazer:

* A simples **codificação numérica** constrói uma tabela de diferentes variedades, e depois substitui o nome da variedade por um índice nessa tabela. Isto não é a melhor ideia para regressão linear, porque a regressão linear toma o valor numérico real do índice, e adiciona-o ao resultado, multiplicando por algum coeficiente. No nosso caso, a relação entre o número do índice e o preço é claramente não linear, mesmo se assegurarmos que os índices estão ordenados de alguma forma específica.
* A **codificação one-hot** vai substituir a coluna `Variety` por 4 colunas diferentes, uma para cada variedade. Cada coluna terá `1` se a linha correspondente for de uma dada variedade, e `0` caso contrário. Isto significa que haverá quatro coeficientes na regressão linear, um para cada variedade de abóbora, responsável pelo "preço inicial" (ou antes "preço adicional") para aquela variedade particular.

O código abaixo mostra como podemos codificar uma variedade usando one-hot:

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

Para treinar a regressão linear usando variedade codificada one-hot como entrada, só precisamos inicializar os dados `X` e `y` corretamente:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

O resto do código é igual ao que usamos anteriormente para treinar a regressão linear. Se tentar, verá que o erro quadrático médio é mais ou menos o mesmo, mas obtemos um coeficiente de determinação muito mais alto (~77%). Para obter previsões ainda mais precisas, podemos levar mais características categóricas em conta, bem como características numéricas, como `Month` ou `DayOfYear`. Para obter um grande array de características, podemos usar `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Aqui também levamos em conta `City` e tipo de `Package`, o que nos dá MSE 2.84 (10%), e determinação 0.94!

## Juntando tudo

Para fazer o melhor modelo, podemos usar dados combinados (categóricos codificados one-hot + numéricos) do exemplo acima juntamente com a Regressão Polinomial. Aqui está o código completo para sua conveniência:

```python
# configurar dados de treino
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# fazer divisão treino-teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# configurar e treinar o pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prever resultados para os dados de teste
pred = pipeline.predict(X_test)

# calcular MSE e determinação
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Isto deverá dar-nos o melhor coeficiente de determinação de quase 97%, e MSE=2.23 (~8% de erro de previsão).

| Modelo | MSE | Determinação |
|-------|-----|---------------|
| Linear `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Polinomial `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Linear `Variety` | 5.24 (19.7%) | 0.77 |
| Linear com todas as características | 2.84 (10.5%) | 0.94 |
| Polinomial com todas as características | 2.23 (8.25%) | 0.97 |

🏆 Muito bem! Criou quatro modelos de regressão numa lição, e melhorou a qualidade do modelo para 97%. Na secção final de Regressão, vai aprender sobre Regressão Logística para determinar categorias. 

---
## 🚀Desafio

Teste várias variáveis diferentes neste notebook para ver como a correlação corresponde à precisão do modelo.

## [Questionário pós-aula](https://ff-quizzes.netlify.app/en/ml/)

## Revisão & Auto-estudo

Nesta lição aprendemos sobre Regressão Linear. Existem outros tipos importantes de Regressão. Leia sobre as técnicas Stepwise, Ridge, Lasso e Elasticnet. Um bom curso para estudar e aprender mais é o [curso de Aprendizagem Estatística de Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tarefa

[Construa um Modelo](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Aviso Legal**:
Este documento foi traduzido utilizando o serviço de tradução automática [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos pela precisão, por favor tenha em conta que traduções automáticas podem conter erros ou imprecisões. O documento original, no seu idioma nativo, deve ser considerado a fonte oficial. Para informação crítica, recomenda-se a tradução profissional por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes da utilização desta tradução.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->