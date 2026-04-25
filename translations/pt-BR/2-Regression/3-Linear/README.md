# Construir um modelo de regressão usando Scikit-learn: regressão de quatro formas

## Nota para iniciantes

A regressão linear é usada quando queremos prever um **valor numérico** (por exemplo, preço de casa, temperatura ou vendas). Funciona encontrando uma linha reta que melhor representa a relação entre as variáveis de entrada e a saída.

Nesta lição, focamos em entender o conceito antes de explorar técnicas mais avançadas de regressão.
![Infográfico regressão linear vs polinomial](../../../../translated_images/pt-BR/linear-polynomial.5523c7cb6576ccab.webp)
> Infográfico por [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Quiz pré-aula](https://ff-quizzes.netlify.app/en/ml/)

> ### [Esta lição está disponível em R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introdução

Até agora, você explorou o que é regressão com dados de exemplo coletados do conjunto de dados de preços de abóboras que usaremos durante esta lição. Você também os visualizou usando Matplotlib.

Agora você está pronto para se aprofundar em regressão para ML. Enquanto a visualização permite entender os dados, o verdadeiro poder do Machine Learning vem do _treinamento de modelos_. Modelos são treinados em dados históricos para capturar automaticamente dependências dos dados, permitindo prever resultados para novos dados, que o modelo ainda não viu.

Nesta lição, você aprenderá mais sobre dois tipos de regressão: _regressão linear básica_ e _regressão polinomial_, junto com um pouco da matemática subjacente a essas técnicas. Esses modelos permitirão prever preços de abóboras dependendo de diferentes dados de entrada.

[![ML para iniciantes - Entendendo Regressão Linear](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Clique na imagem acima para uma breve visão geral em vídeo da regressão linear.

> Ao longo deste currículo, assumimos conhecimento mínimo de matemática, e buscamos torná-lo acessível para estudantes de outras áreas, portanto fique atento a notas, 🧮 chamadas, diagramas e outras ferramentas de aprendizado para ajudar na compreensão.

### Pré-requisito

Você já deve estar familiarizado com a estrutura dos dados de abóboras que estamos analisando. Eles estão pré-carregados e pré-limpos no arquivo _notebook.ipynb_ desta lição. No arquivo, o preço da abóbora é exibido por alqueire em um novo dataframe. Certifique-se de que consegue executar esses notebooks em kernels no Visual Studio Code.

### Preparação

Como lembrete, você está carregando esses dados para poder fazer perguntas sobre eles.

- Quando é a melhor época para comprar abóboras?  
- Qual preço posso esperar para uma caixa de abóboras miniatura?  
- Devo comprá-las em cestas de meio alqueire ou por caixa de 1 1/9 alqueire?  
Vamos continuar investigando esses dados.

Na lição anterior, você criou um dataframe Pandas e o preencheu com parte do conjunto de dados original, padronizando os preços por alqueire. Fazendo isso, porém, você conseguiu apenas cerca de 400 pontos de dados e somente dos meses de outono.

Veja os dados que pré-carregamos no notebook que acompanha esta lição. Os dados estão pré-carregados e um gráfico de dispersão inicial foi criado para mostrar os dados por mês. Talvez possamos obter mais detalhes sobre a natureza dos dados limpando-os melhor.

## Uma linha de regressão linear

Como você aprendeu na Lição 1, o objetivo de um exercício de regressão linear é ser capaz de traçar uma linha para:

- **Mostrar relações entre variáveis**. Mostrar a relação entre variáveis  
- **Fazer previsões**. Fazer previsões precisas de onde um novo ponto de dados cairia em relação a essa linha.

É típico da **Regressão dos Mínimos Quadrados** traçar esse tipo de linha. O termo "Mínimos Quadrados" refere-se ao processo de minimizar o erro total em nosso modelo. Para cada ponto de dados, medimos a distância vertical (chamada resíduo) entre o ponto real e nossa linha de regressão.

Elevamos essas distâncias ao quadrado por duas razões principais:

1. **Magnitude sobre Direção:** Queremos tratar o erro de -5 da mesma forma que o erro de +5. Elevar ao quadrado torna todos os valores positivos.

2. **Penalizar Outliers:** Elevar ao quadrado dá mais peso a erros maiores, fazendo a linha ficar mais próxima dos pontos que estão distantes.

Depois somamos todos esses valores ao quadrado. Nosso objetivo é encontrar a linha específica onde essa soma final seja a menor possível—daí o nome "Mínimos Quadrados".

> **🧮 Mostre a matemática**  
>  
> Essa linha, chamada _linha de melhor ajuste_, pode ser expressa por [uma equação](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` é a 'variável explicativa'. `Y` é a 'variável dependente'. A inclinação da linha é `b` e `a` é o intercepto em y, que se refere ao valor de `Y` quando `X = 0`.  
>  
>![calcular a inclinação](../../../../translated_images/pt-BR/slope.f3c9d5910ddbfcf9.webp)  
>  
> Primeiro, calcule a inclinação `b`. Infográfico por [Jen Looper](https://twitter.com/jenlooper)  
>  
> Em outras palavras, e referindo-se à nossa questão original dos dados de abóbora: "prever o preço de uma abóbora por alqueire por mês", `X` se referiria ao preço e `Y` seria o mês da venda.  
>  
>![complete a equação](../../../../translated_images/pt-BR/calculation.a209813050a1ddb1.webp)  
>  
> Calcule o valor de Y. Se você está pagando em torno de $4, deve ser abril! Infográfico por [Jen Looper](https://twitter.com/jenlooper)  
>  
> A matemática que calcula a linha deve demonstrar a inclinação da linha, que também depende do intercepto, ou onde `Y` está situado quando `X = 0`.  
>  
> Você pode observar o método de cálculo destes valores no site [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Também visite [este calculador de Mínimos Quadrados](https://www.mathsisfun.com/data/least-squares-calculator.html) para ver como os valores dos números impactam a linha.

## Correlação

Mais um termo para entender é o **Coeficiente de Correlação** entre as variáveis X e Y dadas. Usando um gráfico de dispersão, você pode visualizar rapidamente esse coeficiente. Um gráfico com pontos de dados alinhados em uma linha nítida tem alta correlação, mas um gráfico com pontos dispersos entre X e Y tem baixa correlação.

Um bom modelo de regressão linear terá um Coeficiente de Correlação alto (próximo de 1 e não de 0) usando o método de Regressão dos Mínimos Quadrados com uma linha de regressão.

✅ Execute o notebook que acompanha esta lição e olhe o gráfico de dispersão de Mês para Preço. Os dados associando Mês ao Preço nas vendas de abóbora parecem ter alta ou baixa correlação, de acordo com sua interpretação visual do gráfico? Isso muda se você usar uma medida mais detalhada em vez de `Month`, por exemplo, *dia do ano* (ou seja, número de dias desde o começo do ano)?

No código abaixo, assumiremos que limpamos os dados e obtivemos um dataframe chamado `new_pumpkins`, semelhante ao seguinte:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> O código para limpar os dados está disponível em [`notebook.ipynb`](notebook.ipynb). Realizamos as mesmas etapas de limpeza da lição anterior e calculamos a coluna `DayOfYear` usando a expressão a seguir: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Agora que você entendeu a matemática por trás da regressão linear, vamos criar um modelo de regressão para ver se podemos prever qual embalagem de abóboras terá os melhores preços. Alguém comprando abóboras para um patch de abóboras de feriado pode querer essa informação para otimizar suas compras dos pacotes.

## Procurando correlação

[![ML para iniciantes - Procurando correlação: a chave para regressão linear](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML para iniciantes - Procurando correlação: a chave para regressão linear")

> 🎥 Clique na imagem acima para uma breve visão geral em vídeo sobre correlação.

Da lição anterior, você provavelmente viu que o preço médio para diferentes meses parece assim:

<img alt="Preço médio por mês" src="../../../../translated_images/pt-BR/barchart.a833ea9194346d76.webp" width="50%"/>

Isso sugere que deve haver alguma correlação, e podemos tentar treinar um modelo de regressão linear para prever a relação entre `Month` e `Price`, ou entre `DayOfYear` e `Price`. Aqui está o gráfico de dispersão que mostra a última relação:

<img alt="Gráfico de dispersão de preço vs dia do ano" src="../../../../translated_images/pt-BR/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Vamos ver se há correlação usando a função `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Parece que a correlação é pequena, -0,15 pelo `Month` e -0,17 pelo `DayOfMonth`, mas pode haver outra relação importante. Parece que existem diferentes clusters de preços correspondentes a diferentes variedades de abóboras. Para confirmar essa hipótese, vamos plotar cada categoria de abóbora usando uma cor diferente. Passando um parâmetro `ax` para a função `scatter`, podemos plotar todos os pontos no mesmo gráfico:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Gráfico de dispersão de preço vs dia do ano colorido" src="../../../../translated_images/pt-BR/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Nossa investigação sugere que a variedade tem mais efeito no preço geral que a data real de venda. Podemos ver isso com um gráfico de barras:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Gráfico de barras preço vs variedade" src="../../../../translated_images/pt-BR/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Vamos focar momentaneamente apenas em uma variedade de abóbora, o 'tipo torta', e ver qual efeito a data tem no preço:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
  
<img alt="Gráfico de dispersão de preço vs dia do ano para abóboras tipo torta" src="../../../../translated_images/pt-BR/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Se agora calcularmos a correlação entre `Price` e `DayOfYear` usando a função `corr`, obteremos algo como `-0.27` — o que significa que treinar um modelo preditivo faz sentido.

> Antes de treinar um modelo de regressão linear, é importante garantir que nossos dados estejam limpos. Regressão linear não funciona bem com valores faltantes, portanto faz sentido eliminar todas as células vazias:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Outra abordagem seria preencher esses valores vazios com a média da coluna correspondente.

## Regressão Linear Simples

[![ML para iniciantes - Regressão Linear e Polinomial usando Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML para iniciantes - Regressão Linear e Polinomial usando Scikit-learn")

> 🎥 Clique na imagem acima para uma breve visão geral em vídeo da regressão linear e polinomial.

Para treinar nosso modelo de Regressão Linear, usaremos a biblioteca **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Começamos separando os valores de entrada (recursos) e a saída esperada (rótulo) em arrays numpy separados:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Note que tivemos que realizar o `reshape` nos dados de entrada para que o pacote de Regressão Linear os entenda corretamente. Regressão Linear espera uma matriz 2D como entrada, onde cada linha da matriz corresponde a um vetor de recursos de entrada. No nosso caso, já que temos apenas uma entrada, precisamos de uma matriz com formato N&times;1, onde N é o tamanho do conjunto de dados.

Depois, precisamos dividir os dados em conjuntos de treino e teste para que possamos validar nosso modelo após o treinamento:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Finalmente, o treinamento do modelo de Regressão Linear real leva apenas duas linhas de código. Definimos o objeto `LinearRegression`, e ajustamos ele aos nossos dados usando o método `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

O objeto `LinearRegression` após o ajuste (`fit`) contém todos os coeficientes da regressão, que podem ser acessados usando a propriedade `.coef_`. No nosso caso, há apenas um coeficiente, que deve estar em torno de `-0.017`. Isso significa que os preços parecem cair um pouco com o tempo, mas não muito, cerca de 2 centavos por dia. Também podemos acessar o ponto de interseção da regressão com o eixo Y usando `lin_reg.intercept_` - será cerca de `21` no nosso caso, indicando o preço no início do ano.

Para ver quão preciso nosso modelo é, podemos prever preços em um conjunto de dados de teste e então medir quão próximas estão nossas previsões dos valores esperados. Isso pode ser feito usando a métrica de erro quadrático médio da raiz (RMSE), que é a raiz da média de todas as diferenças ao quadrado entre o valor esperado e o previsto.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Nosso erro parece estar em torno de 2 pontos, o que é ~17%. Não muito bom. Outro indicador de qualidade do modelo é o **coeficiente de determinação**, que pode ser obtido assim:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Se o valor for 0, isto significa que o modelo não leva em conta os dados de entrada, e atua como o *pior preditor linear*, que é simplesmente um valor médio do resultado. O valor 1 significa que podemos prever perfeitamente todas as saídas esperadas. No nosso caso, o coeficiente está em torno de 0.06, o que é bem baixo.

Também podemos plotar os dados de teste junto com a linha de regressão para ver melhor como a regressão funciona no nosso caso:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/pt-BR/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regressão Polinomial

Outro tipo de Regressão Linear é a Regressão Polinomial. Embora às vezes haja uma relação linear entre variáveis - quanto maior a abóbora em volume, maior o preço - às vezes essas relações não podem ser plotadas como um plano ou linha reta.

✅ Aqui estão [mais alguns exemplos](https://online.stat.psu.edu/stat501/lesson/9/9.8) de dados que poderiam usar Regressão Polinomial

Observe novamente a relação entre Data e Preço. Este gráfico de dispersão parece que deveria necessariamente ser analisado por uma linha reta? Os preços não podem flutuar? Nesse caso, você pode tentar a regressão polinomial.

✅ Polinômios são expressões matemáticas que podem consistir de uma ou mais variáveis e coeficientes

A regressão polinomial cria uma linha curva para ajustar melhor dados não lineares. No nosso caso, se incluirmos a variável ao quadrado `DayOfYear` nos dados de entrada, deveremos ser capazes de ajustar nossos dados com uma curva parabólica, que terá um mínimo em um certo ponto ao longo do ano.

O Scikit-learn inclui uma útil [API de pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) para combinar diferentes etapas do processamento de dados. Um **pipeline** é uma cadeia de **estimadores**. No nosso caso, criaremos um pipeline que primeiro adiciona características polinomiais ao nosso modelo, e então treina a regressão:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Usar `PolynomialFeatures(2)` significa que vamos incluir todos os polinômios de segundo grau a partir dos dados de entrada. No nosso caso, isso significará apenas `DayOfYear`<sup>2</sup>, mas dado duas variáveis de entrada X e Y, isso adicionará X<sup>2</sup>, XY e Y<sup>2</sup>. Podemos também usar polinômios de grau maior, se quisermos.

Pipelines podem ser usados da mesma forma que o objeto original `LinearRegression`, ou seja, podemos `fit`ar o pipeline, e então usar `predict` para obter os resultados da predição. Aqui está o gráfico mostrando os dados de teste, e a curva de aproximação:

<img alt="Polynomial regression" src="../../../../translated_images/pt-BR/poly-results.ee587348f0f1f60b.webp" width="50%" />

Usando Regressão Polinomial, podemos obter erros quadráticos médios ligeiramente menores e coeficientes de determinação maiores, mas não significativamente. Precisamos levar em conta outras características!

> Você pode ver que os preços mínimos das abóboras são observados em algum momento próximo ao Halloween. Como você pode explicar isso?

🎃 Parabéns, você acaba de criar um modelo que pode ajudar a prever o preço de abóboras para torta. Você provavelmente pode repetir o mesmo procedimento para todos os tipos de abóbora, mas isso seria trabalhoso. Vamos aprender agora como levar em conta a variedade de abóbora em nosso modelo!

## Características Categóricas

No mundo ideal, queremos ser capazes de prever preços para diferentes variedades de abóbora usando o mesmo modelo. No entanto, a coluna `Variety` é um pouco diferente de colunas como `Month`, pois contém valores não numéricos. Essas colunas são chamadas de **categóricas**.

[![ML para iniciantes - Predições de Características Categóricas com Regressão Linear](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML para iniciantes - Predições de Características Categóricas com Regressão Linear")

> 🎥 Clique na imagem acima para um breve vídeo sobre o uso de características categóricas.

Aqui você pode ver como o preço médio depende da variedade:

<img alt="Average price by variety" src="../../../../translated_images/pt-BR/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Para levar a variedade em conta, primeiro precisamos convertê-la para forma numérica, ou **codificá-la**. Há várias formas para isso:

* A simples **codificação numérica** constrói uma tabela das diferentes variedades, e depois substitui o nome da variedade por um índice nessa tabela. Isso não é a melhor ideia para regressão linear, porque a regressão linear pega o valor numérico real do índice, e o adiciona ao resultado, multiplicando por algum coeficiente. No nosso caso, a relação entre o número do índice e o preço é claramente não linear, mesmo que asseguremos que os índices estejam ordenados de alguma maneira específica.
* O **one-hot encoding** substituirá a coluna `Variety` por 4 colunas diferentes, uma para cada variedade. Cada coluna conterá `1` se a linha correspondente for de uma determinada variedade, e `0` caso contrário. Isso significa que haverá quatro coeficientes na regressão linear, um para cada variedade de abóbora, responsável pelo "preço inicial" (ou melhor, "preço adicional") para aquela variedade específica.

O código abaixo mostra como podemos fazer o one-hot encoding da variedade:

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

Para treinar a regressão linear usando a variedade codificada por one-hot encoding como entrada, só precisamos inicializar corretamente os dados `X` e `y`:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

O resto do código é o mesmo que usamos acima para treinar a Regressão Linear. Se você tentar, verá que o erro quadrático médio fica mais ou menos o mesmo, mas obtemos um coeficiente de determinação muito maior (~77%). Para obter previsões ainda mais precisas, podemos levar mais características categóricas em conta, bem como características numéricas, como `Month` ou `DayOfYear`. Para obter uma grande matriz de características, podemos usar `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Aqui também levamos em conta `City` e tipo de `Package`, o que nos dá MSE 2.84 (10%), e determinação 0.94!

## Combinando tudo

Para fazer o melhor modelo, podemos usar dados combinados (categóricos codificados one-hot + numéricos) do exemplo acima junto com a Regressão Polinomial. Aqui está o código completo para sua conveniência:

```python
# configurar dados de treinamento
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

Isso deve nos dar o melhor coeficiente de determinação de quase 97%, e MSE=2.23 (~8% de erro de previsão).

| Modelo | MSE | Determinação |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polinomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| Todas as características Linear | 2.84 (10.5%) | 0.94 |
| Todas as características Polinomial | 2.23 (8.25%) | 0.97 |

🏆 Muito bem! Você criou quatro modelos de regressão em uma lição, e melhorou a qualidade do modelo para 97%. Na seção final sobre Regressão, você aprenderá sobre Regressão Logística para determinar categorias.

---
## 🚀Desafio

Teste várias variáveis diferentes neste notebook para ver como a correlação corresponde à precisão do modelo.

## [Questionário pós-aula](https://ff-quizzes.netlify.app/en/ml/)

## Revisão & Estudo Autônomo

Nesta lição aprendemos sobre Regressão Linear. Existem outros tipos importantes de Regressão. Leia sobre as técnicas Stepwise, Ridge, Lasso e Elasticnet. Um bom curso para estudar e aprender mais é o [curso de Aprendizado Estatístico de Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tarefa

[Construa um Modelo](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos empenhemos pela precisão, por favor, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original em seu idioma nativo deve ser considerado a fonte autorizada. Para informações críticas, recomenda-se tradução profissional humana. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações errôneas decorrentes do uso desta tradução.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->