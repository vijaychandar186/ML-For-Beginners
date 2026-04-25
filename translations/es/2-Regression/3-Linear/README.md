# Construir un modelo de regresión usando Scikit-learn: regresión de cuatro formas

## Nota para principiantes

La regresión lineal se usa cuando queremos predecir un **valor numérico** (por ejemplo, precio de una casa, temperatura o ventas). Funciona encontrando una línea recta que mejor representa la relación entre las características de entrada y la salida.

En esta lección, nos enfocamos en entender el concepto antes de explorar técnicas de regresión más avanzadas.
![Infografía de regresión lineal vs polinomial](../../../../translated_images/es/linear-polynomial.5523c7cb6576ccab.webp)
> Infografía por [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Cuestionario previo a la clase](https://ff-quizzes.netlify.app/en/ml/)

> ### [Esta lección está disponible en R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Introducción

Hasta ahora has explorado qué es la regresión con datos de muestra tomados del conjunto de datos de precios de calabazas que usaremos a lo largo de esta lección. También lo has visualizado usando Matplotlib.

Ahora estás listo para profundizar en la regresión para ML. Mientras que la visualización te permite entender los datos, el verdadero poder del Aprendizaje Automático proviene de _entrenar modelos_. Los modelos se entrenan con datos históricos para capturar automáticamente dependencias en los datos, y permiten predecir resultados para datos nuevos, que el modelo no ha visto antes.

En esta lección, aprenderás más sobre dos tipos de regresión: _regresión lineal básica_ y _regresión polinómica_, junto con algo de la matemática subyacente a estas técnicas. Estos modelos nos permitirán predecir precios de calabazas dependiendo de distintas entradas.

[![ML para principiantes – Entendiendo la Regresión Lineal](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML para principiantes – Entendiendo la Regresión Lineal")

> 🎥 Haz clic en la imagen de arriba para un video corto que presenta la regresión lineal.

> A lo largo de este currículum, asumimos un conocimiento mínimo de matemáticas, y buscamos hacerlo accesible para estudiantes de otras áreas, así que presta atención a notas, 🧮 llamadas, diagramas y otras herramientas de aprendizaje que ayudarán en la comprensión.

### Prerrequisito

Ya deberías estar familiarizado con la estructura de los datos de calabazas que estamos examinando. Puedes encontrarlos precargados y pre-limpiados en el archivo _notebook.ipynb_ de esta lección. En el archivo, el precio de las calabazas se muestra por fanega en un nuevo dataframe. Asegúrate de poder ejecutar estos notebooks en kernels en Visual Studio Code.

### Preparación

Como recordatorio, cargas estos datos para poder hacerles preguntas.

- ¿Cuál es el mejor momento para comprar calabazas?  
- ¿Qué precio puedo esperar de una caja de calabazas miniatura?  
- ¿Debería comprarlas en cestas de media fanega o por la caja de 1 1/9 fanegas?  
Sigamos investigando estos datos.

En la lección anterior, creaste un dataframe de Pandas y lo llenaste con parte del conjunto original, estandarizando el precio por fanega. De esa forma, solo pudiste obtener alrededor de 400 puntos de datos y solo para los meses de otoño.

Mira los datos que precargamos en el notebook que acompaña esta lección. Los datos están precargados y un diagrama de dispersión inicial se grafica para mostrar datos por mes. Tal vez podamos obtener un poco más de detalle sobre la naturaleza de los datos limpiándolos más.

## Una línea de regresión lineal

Como aprendiste en la Lección 1, el objetivo de un ejercicio de regresión lineal es poder graficar una línea para:

- **Mostrar relaciones entre variables**. Mostrar la relación entre variables  
- **Hacer predicciones**. Hacer predicciones precisas sobre dónde caería un nuevo punto de datos en relación con esa línea.

Es típico de la **Regresión de Mínimos Cuadrados** dibujar este tipo de línea. El término "Mínimos Cuadrados" se refiere al proceso de minimizar el error total en nuestro modelo. Para cada punto de datos, medimos la distancia vertical (llamada residual) entre el punto real y nuestra línea de regresión.

Elevamos al cuadrado estas distancias por dos razones principales:

1. **Magnitud sobre Dirección:** Queremos tratar un error de -5 igual que un error de +5. Elevar al cuadrado convierte todos los valores en positivos.

2. **Penalizar valores atípicos:** Al elevar al cuadrado se da más peso a errores mayores, forzando a la línea a quedarse más cerca de puntos alejados.

Luego sumamos todos estos valores al cuadrado. Nuestro objetivo es encontrar la línea específica donde esta suma final es la menor (el valor más pequeño posible), de ahí el nombre de "Mínimos Cuadrados".

> **🧮 Muéstrame las matemáticas**  
>  
> Esta línea, llamada _línea de mejor ajuste_, puede expresarse con [una ecuación](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>
> `X` es la 'variable explicativa'. `Y` es la 'variable dependiente'. La pendiente de la línea es `b` y `a` es la intersección en y, que se refiere al valor de `Y` cuando `X = 0`.  
>
>![calcular la pendiente](../../../../translated_images/es/slope.f3c9d5910ddbfcf9.webp)
>
> Primero, se calcula la pendiente `b`. Infografía por [Jen Looper](https://twitter.com/jenlooper)
>
> En otras palabras, y refiriéndonos a la pregunta original de nuestro dato de calabazas: "predecir el precio de una calabaza por fanega según el mes", `X` se referiría al precio y `Y` al mes de venta.
>
>![completar la ecuación](../../../../translated_images/es/calculation.a209813050a1ddb1.webp)
>
> Calcula el valor de Y. Si estás pagando alrededor de $4, ¡debe ser abril! Infografía por [Jen Looper](https://twitter.com/jenlooper)
>
> Las matemáticas que calculan la línea deben mostrar la pendiente de la línea, que también depende de la intersección, o de dónde se sitúa `Y` cuando `X = 0`.
>
> Puedes ver el método de cálculo para estos valores en el sitio [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). También visita [este calculador de mínimos cuadrados](https://www.mathsisfun.com/data/least-squares-calculator.html) para ver cómo el valor de los números impacta la línea.

## Correlación

Un término más para entender es el **Coeficiente de Correlación** entre variables dadas X y Y. Usando un diagrama de dispersión, puedes visualizar rápidamente este coeficiente. Un gráfico con puntos dispersos en una línea ordenada tiene alta correlación, pero uno con puntos dispersos en todas partes entre X y Y tiene baja correlación.

Un buen modelo de regresión lineal será uno que tenga un Coeficiente de Correlación alto (más cercano a 1 que a 0) usando el método de Regresión de Mínimos Cuadrados con una línea de regresión.

✅ Ejecuta el notebook que acompaña esta lección y observa el diagrama de dispersión Mes a Precio. ¿Parece que la asociación entre Mes y Precio para las ventas de calabazas tiene alta o baja correlación, según tu interpretación visual del diagrama de dispersión? ¿Cambia eso si usas una medida más fina en lugar de `Mes`, por ejemplo *día del año* (es decir, número de días desde el inicio del año)?

En el código a continuación, asumiremos que hemos limpiado los datos y obtenido un dataframe llamado `new_pumpkins`, similar al siguiente:

ID | Mes | DíaDelAño | Variedad | Ciudad | Paquete | Precio Bajo | Precio Alto | Precio
---|-----|-----------|----------|--------|---------|-------------|-------------|--------
70 | 9 | 267 | TIPO PARA PAY | BALTIMORE | cajas de 1 1/9 fanegas | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | TIPO PARA PAY | BALTIMORE | cajas de 1 1/9 fanegas | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | TIPO PARA PAY | BALTIMORE | cajas de 1 1/9 fanegas | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | TIPO PARA PAY | BALTIMORE | cajas de 1 1/9 fanegas | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | TIPO PARA PAY | BALTIMORE | cajas de 1 1/9 fanegas | 15.0 | 15.0 | 13.636364

> El código para limpiar los datos está disponible en [`notebook.ipynb`](notebook.ipynb). Hemos realizado los mismos pasos de limpieza que en la lección anterior, y calculamos la columna `DayOfYear` usando la siguiente expresión:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Ahora que entiendes la matemática detrás de la regresión lineal, creemos un modelo de regresión para ver si podemos predecir qué paquete de calabazas tendrá los mejores precios. Alguien que compra calabazas para un huerto navideño podría querer esta información para optimizar sus compras.

## Buscando Correlación

[![ML para principiantes - Buscando Correlación: La Clave para la Regresión Lineal](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML para principiantes - Buscando Correlación: La Clave para la Regresión Lineal")

> 🎥 Haz clic en la imagen de arriba para un video corto que presenta la correlación.

En la lección anterior probablemente viste que el precio promedio por diferentes meses luce así:

<img alt="Precio promedio por mes" src="../../../../translated_images/es/barchart.a833ea9194346d76.webp" width="50%"/>

Esto sugiere que debería haber algo de correlación, y podemos intentar entrenar un modelo de regresión lineal para predecir la relación entre `Mes` y `Precio`, o entre `DíaDelAño` y `Precio`. Aquí está el diagrama de dispersión que muestra esta última relación:

<img alt="Diagrama de dispersión de Precio vs Día del Año" src="../../../../translated_images/es/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Veamos si hay correlación usando la función `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Parece que la correlación es bastante pequeña, -0.15 usando `Mes` y -0.17 usando `DíaDelMes`, pero podría haber otra relación importante. Parece que hay diferentes grupos de precios según las distintas variedades de calabaza. Para confirmar esta hipótesis, graficamos cada categoría de calabaza usando un color diferente. Pasando un parámetro `ax` a la función de graficar `scatter` podemos poner todos los puntos en el mismo gráfico:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Diagrama de dispersión de Precio vs Día del Año" src="../../../../translated_images/es/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Nuestra investigación sugiere que la variedad afecta más el precio final que la fecha de venta real. Podemos ver esto en un gráfico de barras:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Gráfico de barras de precio vs variedad" src="../../../../translated_images/es/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Enfoquémonos por ahora solo en una variedad de calabaza, el 'tipo para pay', y veamos qué efecto tiene la fecha en el precio:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Diagrama de dispersión de Precio vs Día del Año" src="../../../../translated_images/es/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Si ahora calculamos la correlación entre `Precio` y `DíaDelAño` usando la función `corr`, obtendremos algo como `-0.27`, lo que significa que entrenar un modelo predictivo tiene sentido.

> Antes de entrenar un modelo de regresión lineal, es importante asegurarnos que los datos estén limpios. La regresión lineal no funciona bien con valores faltantes, por lo que conviene eliminar todas las celdas vacías:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Otra opción sería llenar esos valores vacíos con el valor medio de la columna correspondiente.

## Regresión Lineal Simple

[![ML para principiantes - Regresión Lineal y Polinomial usando Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML para principiantes - Regresión Lineal y Polinomial usando Scikit-learn")

> 🎥 Haz clic en la imagen de arriba para un video corto que presenta la regresión lineal y polinomial.

Para entrenar nuestro modelo de Regresión Lineal, usaremos la biblioteca **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Comenzamos separando los valores de entrada (características) y la salida esperada (etiqueta) en matrices numpy separadas:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Nota que tuvimos que aplicar `reshape` a los datos de entrada para que el paquete de Regresión Lineal los entienda correctamente. La Regresión Lineal espera un array 2D como entrada, donde cada fila del array corresponde a un vector de características de entrada. En nuestro caso, dado que solo tenemos una entrada, necesitamos un array con forma N&times;1, donde N es el tamaño del conjunto de datos.

Luego, necesitamos dividir los datos en conjuntos de entrenamiento y prueba, para poder validar nuestro modelo después de entrenarlo:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Finalmente, entrenar el modelo de Regresión Lineal real toma solo dos líneas de código. Definimos el objeto `LinearRegression`, y lo ajustamos a nuestros datos usando el método `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

El objeto `LinearRegression` después de ajustar (`fit`) contiene todos los coeficientes de la regresión, a los cuales se puede acceder usando la propiedad `.coef_`. En nuestro caso, hay solo un coeficiente, que debería estar alrededor de `-0.017`. Esto significa que los precios parecen bajar un poco con el tiempo, pero no demasiado, alrededor de 2 centavos por día. También podemos acceder al punto de intersección de la regresión con el eje Y usando `lin_reg.intercept_` - estará alrededor de `21` en nuestro caso, indicando el precio al inicio del año.

Para ver qué tan preciso es nuestro modelo, podemos predecir los precios en un conjunto de datos de prueba, y luego medir qué tan cercanas están nuestras predicciones a los valores esperados. Esto se puede hacer usando la métrica de raíz del error cuadrático medio (RMSE), que es la raíz de la media de todas las diferencias al cuadrado entre el valor esperado y el predicho.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Nuestro error parece estar alrededor de 2 puntos, que es ~17%. No muy bueno. Otro indicador de la calidad del modelo es el **coeficiente de determinación**, que se puede obtener así:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Si el valor es 0, significa que el modelo no toma en cuenta los datos de entrada y actúa como el *peor predictor lineal*, que es simplemente el promedio del resultado. El valor de 1 significa que podemos predecir perfectamente todos los valores esperados. En nuestro caso, el coeficiente es alrededor de 0.06, lo cual es bastante bajo.

También podemos graficar los datos de prueba junto con la línea de regresión para ver mejor cómo funciona la regresión en nuestro caso:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Regresión lineal" src="../../../../translated_images/es/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regresión Polinómica

Otro tipo de Regresión Lineal es la Regresión Polinómica. Aunque a veces existe una relación lineal entre variables - cuanto mayor es el volumen de la calabaza, mayor es el precio - a veces estas relaciones no pueden ser representadas por un plano o línea recta.

✅ Aquí hay [algunos ejemplos más](https://online.stat.psu.edu/stat501/lesson/9/9.8) de datos que podrían usar Regresión Polinómica

Echa otro vistazo a la relación entre Fecha y Precio. ¿Parece este diagrama de dispersión que deba necesariamente analizarse con una línea recta? ¿No pueden los precios fluctuar? En este caso, puedes probar la regresión polinómica.

✅ Los polinomios son expresiones matemáticas que pueden consistir en una o más variables y coeficientes

La regresión polinómica crea una curva para ajustar mejor datos no lineales. En nuestro caso, si incluimos una variable `DayOfYear` al cuadrado en los datos de entrada, deberíamos poder ajustar nuestros datos con una curva parabólica, que tendrá un mínimo en cierto punto del año.

Scikit-learn incluye una útil [API de pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) para combinar diferentes pasos de procesamiento de datos. Un **pipeline** es una cadena de **estimadores**. En nuestro caso, crearemos un pipeline que primero añade características polinómicas a nuestro modelo, y luego entrena la regresión:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Usar `PolynomialFeatures(2)` significa que incluiremos todos los polinomios de segundo grado de los datos de entrada. En nuestro caso solo significa `DayOfYear`<sup>2</sup>, pero dado dos variables de entrada X y Y, esto agregaría X<sup>2</sup>, XY y Y<sup>2</sup>. También podemos usar polinomios de grado superior si queremos.

Los pipelines pueden usarse de la misma manera que el objeto original `LinearRegression`, es decir, podemos `fit` el pipeline y luego usar `predict` para obtener los resultados de la predicción. Aquí está el gráfico que muestra los datos de prueba y la curva de aproximación:

<img alt="Regresión polinómica" src="../../../../translated_images/es/poly-results.ee587348f0f1f60b.webp" width="50%" />

Usando Regresión Polinómica, podemos obtener un MSE ligeramente más bajo y una determinación más alta, pero no significativamente. ¡Necesitamos tomar en cuenta otras características!

> Puedes ver que los precios mínimos de las calabazas se observan alrededor de Halloween. ¿Cómo puedes explicar esto? 

🎃 ¡Felicidades, acabas de crear un modelo que puede ayudar a predecir el precio de las calabazas para pasteles! Probablemente puedas repetir el mismo procedimiento para todos los tipos de calabazas, pero eso sería tedioso. ¡Aprendamos ahora cómo tomar en cuenta la variedad de calabaza en nuestro modelo!

## Características Categóricas

En un mundo ideal, queremos poder predecir precios para diferentes variedades de calabaza usando el mismo modelo. Sin embargo, la columna `Variety` es algo diferente de columnas como `Month`, porque contiene valores no numéricos. Tales columnas se llaman **categóricas**.

[![ML para principiantes - Predicciones con características categóricas usando regresión lineal](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML para principiantes - Predicciones con características categóricas usando regresión lineal")

> 🎥 Haz clic en la imagen arriba para un breve video explicativo sobre el uso de características categóricas.

Aquí puedes ver cómo depende el precio promedio de la variedad:

<img alt="Precio promedio por variedad" src="../../../../translated_images/es/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Para tomar en cuenta la variedad, primero necesitamos convertirla a forma numérica, o **codificarla**. Hay varias maneras de hacerlo:

* La simple **codificación numérica** creará una tabla de diferentes variedades y reemplazará el nombre por un índice en esa tabla. Esto no es la mejor idea para regresión lineal, porque la regresión lineal toma el valor numérico real del índice y lo suma al resultado multiplicado por algún coeficiente. En nuestro caso, la relación entre el número del índice y el precio es claramente no lineal, incluso si aseguramos que los índices están ordenados de alguna forma específica.
* La **codificación one-hot** reemplazará la columna `Variety` por 4 columnas diferentes, una para cada variedad. Cada columna contendrá un `1` si la fila correspondiente es de esa variedad, y `0` si no. Esto significa que habrá cuatro coeficientes en la regresión lineal, uno para cada variedad de calabaza, responsables por el "precio inicial" (o más bien "precio adicional") para esa variedad particular.

El código a continuación muestra cómo podemos hacer codificación one-hot de una variedad:

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

Para entrenar la regresión lineal usando la variedad codificada one-hot como entrada, solo necesitamos inicializar los datos `X` y `y` correctamente:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

El resto del código es el mismo que usamos arriba para entrenar Regresión Lineal. Si lo pruebas, verás que el error cuadrático medio es aproximadamente el mismo, pero obtenemos un coeficiente de determinación mucho más alto (~77%). Para obtener predicciones aún más precisas, podemos tomar en cuenta más características categóricas así como características numéricas como `Month` o `DayOfYear`. Para obtener una matriz grande de características, podemos usar `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Aquí también tomamos en cuenta `City` y tipo de `Package`, lo que nos da un MSE de 2.84 (10%) y una determinación de 0.94!

## Poniéndolo todo junto

Para hacer el mejor modelo, podemos usar datos combinados (categóricos codificados one-hot + numéricos) del ejemplo anterior junto con Regresión Polinómica. Aquí está el código completo para tu conveniencia:

```python
# configurar los datos de entrenamiento
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# hacer la división entrenamiento-prueba
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# configurar y entrenar el pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# predecir resultados para los datos de prueba
pred = pipeline.predict(X_test)

# calcular el error cuadrático medio y la determinación
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Esto debería darnos el mejor coeficiente de determinación de casi 97%, y MSE=2.23 (~8% de error en la predicción).

| Modelo | MSE | Determinación |
|-------|-----|---------------|
| Regresión Lineal con `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Regresión Polinómica con `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Regresión Lineal con `Variety` | 5.24 (19.7%) | 0.77 |
| Regresión Lineal con todas las características | 2.84 (10.5%) | 0.94 |
| Regresión Polinómica con todas las características | 2.23 (8.25%) | 0.97 |

🏆 ¡Buen trabajo! Creaste cuatro modelos de regresión en una lección y mejoraste la calidad del modelo al 97%. En la sección final sobre Regresión, aprenderás sobre Regresión Logística para determinar categorías.

---
## 🚀Desafío

Prueba varias variables diferentes en este cuaderno para ver cómo la correlación corresponde con la precisión del modelo.

## [Cuestionario post-clase](https://ff-quizzes.netlify.app/en/ml/)

## Repaso y Autoestudio

En esta lección aprendimos sobre Regresión Lineal. Hay otros tipos importantes de regresión. Lee sobre las técnicas Stepwise, Ridge, Lasso y Elasticnet. Un buen curso para estudiar y aprender más es el [curso de Aprendizaje Estadístico de Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tarea

[Construye un modelo](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Aunque nos esforzamos por la precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o inexactitudes. El documento original en su idioma nativo debe considerarse la fuente autorizada. Para información crítica, se recomienda una traducción profesional humana. No nos hacemos responsables de ningún malentendido o interpretación errónea que surja del uso de esta traducción.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->