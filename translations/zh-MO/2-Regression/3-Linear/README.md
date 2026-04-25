# 使用 Scikit-learn 建立回歸模型：回歸四種方法

## 初學者筆記

線性回歸用於當我們想預測一個<strong>數值</strong>（例如，房價、溫度或銷售量）。
它通過尋找一條最能代表輸入特徵與輸出之間關係的直線來工作。

在本課程中，我們專注於理解概念，然後進一步探索更進階的回歸技術。
![線性回歸與多項式回歸資訊圖](../../../../translated_images/zh-MO/linear-polynomial.5523c7cb6576ccab.webp)
> 資訊圖由 [Dasani Madipalli](https://twitter.com/dasani_decoded) 製作
## [課前小測驗](https://ff-quizzes.netlify.app/en/ml/)

> ### [本課程亦提供 R 版本！](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### 介紹 

到目前為止，你已經透過南瓜定價資料集（本課程將持續使用）探討了回歸的意義。你也使用 Matplotlib 將其視覺化。

現在你已準備好深入探討機器學習中的回歸。雖然視覺化可以幫助你理解數據，機器學習的真正力量來自於_訓練模型_。模型在歷史數據上訓練，以自動捕捉數據之間的依賴關係，並允許你對模型未見過的新數據進行預測。

本課將介紹兩種回歸：_基本線性回歸_與_多項式回歸_，以及一些這些技術背後的數學原理。這些模型將讓我們根據不同輸入資料預測南瓜價格。

[![初學者機器學習 - 理解線性回歸](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "初學者機器學習 - 理解線性回歸")

> 🎥 點擊上圖觀看線性回歸的短片介紹。

> 整個課程假設對數學知識要求低，並致力於讓來自不同領域的學生都能理解，因此你會看到筆記、🧮 註解、圖解及其他學習工具協助理解。

### 前置知識

你現在應該熟悉我們正在檢視的南瓜數據架構。你可以在本課程的 _notebook.ipynb_ 中找到事先加載並預先清理好的數據。在該檔中，南瓜價格以每蒲式耳計算並顯示於新的資料框架中。確保你能在 Visual Studio Code 中運行這些 notebook。

### 準備工作

提醒你，你正在載入這些數據是為了針對它們提出問題。

- 何時是購買南瓜的最佳時機？  
- 一箱迷你南瓜的價格大約是多少？  
- 我應該買半蒲式耳的南瓜籃，還是一箱1 1/9蒲式耳的箱子？  
讓我們繼續探索這些數據。

在上一課中，你建立了一個 Pandas 資料框架，並以原始資料的一部分填充，將價格標準化為每蒲式耳價格。然而，這樣你只能取得約400筆數據，且只涵蓋秋季月份。

看看我們在本課的 notebook 中預先加載的數據。資料已加載且初步使用散點圖顯示月份數據。也許我們可以透過進一步清理獲得更詳細的資料特性。

## 線性回歸線

如你在第一課中學到，線性回歸的目標是繪製一條線來：

- <strong>展示變量關係</strong>。展示變數間的關係  
- <strong>進行預測</strong>。準確預測新數據點相較該線會落在哪裡  

<strong>最小平方回歸</strong>常用來繪製這類線條。術語「最小平方」指的是我們想最小化模型中總誤差的過程。對每個數據點，我們量度實際點與回歸線之間的垂直距離（稱為殘差）。

我們將這些距離平方，原因有兩個：

1. <strong>大小勝方向</strong>：我們要將-5的誤差與+5的誤差等同對待，平方讓所有值都變成正數。  

2. <strong>懲罰離群值</strong>：平方會給較大誤差更重的權重，迫使線條更貼近遠離的點。

接著將所有平方值加總起來。我們的目標是尋找使該總和最小（可能的最小值）的特定直線——因此稱作「最小平方」。

> **🧮 看數學計算**  
>  
> 這條稱作_最佳擬合線_的直線能用[方程式](https://en.wikipedia.org/wiki/Simple_linear_regression)表示：  
>  
> ```
> Y = a + bX
> ```
>
> `X` 是「解釋變數」，`Y` 是「被解釋變數」。線的斜率是 `b`，`a` 是 y 截距，指的是當 `X = 0` 時的 `Y` 值。  
>
>![計算斜率](../../../../translated_images/zh-MO/slope.f3c9d5910ddbfcf9.webp)
>
> 首先計算斜率 `b`。 資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 製作
>
> 換句話說，對應我們南瓜資料的原始問題：「根據月份預測每蒲式耳南瓜的價格」，`X` 指價格，`Y` 則是銷售月份。  
>
>![完成方程式](../../../../translated_images/zh-MO/calculation.a209813050a1ddb1.webp)
>
> 計算 `Y` 的值。如果你支付約 4 美元，應該是四月！資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 製作
>
> 計算直線的數學必須展示斜率，而斜率也依賴截距，即 `X = 0` 時 `Y` 所在位置。
>
> 你可以到 [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) 網站觀察這些計算方法。也可到[此最小平方計算器](https://www.mathsisfun.com/data/least-squares-calculator.html)觀看數值如何影響直線。

## 相關係數

還有一個需要了解的詞彙是給定 X 與 Y 變數間的<strong>相關係數</strong>。使用散點圖，你可以快速視覺化這個係數。若數據點呈現整齊分布成一條線，代表相關性高；若點散布在 X 與 Y 之間各處，則相關性低。

一個好的線性回歸模型會有一個高（接近1而非0）相關係數，使用最小平方回歸法與回歸線。

✅ 執行本課程附帶 notebook，查看月份對價格的散點圖。根據你對散點圖的視覺判斷，月份與南瓜銷售價格之間的資料關聯是高還是低？如果換成更細緻的度量，例如<em>該年天數</em>（即距離該年開始日的天數），情況會改變嗎？

在以下程式中，假設我們已清理了資料，得到了名為 `new_pumpkins` 的資料框架，結構類似：

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> 清理數據的程式碼在 [`notebook.ipynb`](notebook.ipynb) 中。我們已完成與上一課相同的清理步驟，並利用以下公式計算 `DayOfYear` 欄位： 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

現在你已了解線性回歸背後的數學，讓我們建立一個迴歸模型，看看是否能預測哪種南瓜包裝的南瓜價格會最好。假如有人想購買南瓜以打造節日南瓜園，這資訊會對他們優化包裝購買策略很有幫助。

## 尋找相關性

[![初學者機器學習 - 尋找相關性：線性回歸的關鍵](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "初學者機器學習 - 尋找相關性：線性回歸的關鍵")

> 🎥 點擊上圖觀看相關性短片介紹。

根據上一課，你可能見過不同月份平均價格長這樣：

<img alt="按月平均價格" src="../../../../translated_images/zh-MO/barchart.a833ea9194346d76.webp" width="50%"/>

這表示應該有某種相關性，我們可以嘗試訓練線性回歸模型來預測 `Month` 與 `Price` 或 `DayOfYear` 與 `Price` 之間的關係。以下散點圖顯示後者關係：

<img alt="價格與該年天數散點圖" src="../../../../translated_images/zh-MO/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

讓我們使用 `corr` 函數看看是否存在相關：

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

看起來 `Month` 的相關性大約是 -0.15，`DayOfMonth` 則是 -0.17，都相當小，但可能還有其他重要關係。看來不同南瓜品種的價格形成不同叢集。為證實此假設，我們用不同顏色標示每種南瓜類別。透過傳 `ax` 參數給 `scatter` 繪圖函式，我們可以將所有點畫在同一圖上：

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="價格與該年天數散點圖，依顏色區分" src="../../../../translated_images/zh-MO/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

調查顯示品種比實際銷售日期對整體價格影響更大。我們用長條圖看得更明顯：

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="按品種價格長條圖" src="../../../../translated_images/zh-MO/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

暫時只看一種南瓜品種，稱為「pie type」，來看看日期對價格的影響：

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="價格與該年天數散點圖" src="../../../../translated_images/zh-MO/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

若用 `corr` 函數計算 `Price` 與 `DayOfYear` 相關性，會得到約 `-0.27`，表示訓練預測模型是有意義的。

> 在訓練線性回歸模型前，請確定數據是乾淨的。線性回歸對遺失值表現不佳，因此最好清除所有空白欄位：

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

另一方法是用該欄位的平均值填補空白。

## 簡單線性回歸

[![初學者機器學習 - 使用 Scikit-learn 的線性與多項式回歸](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "初學者機器學習 - 使用 Scikit-learn 的線性與多項式回歸")

> 🎥 點擊上圖觀看線性與多項式回歸短片介紹。

我們將使用 **Scikit-learn** 函式庫訓練線性回歸模型。

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

首先，我們要將輸入值（特徵）和預期輸出（標籤）分別放進 numpy 陣列：

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> 注意，我們必須將輸入資料 `reshape` 以讓線性回歸套件能正確處理。線性回歸預期輸入是 2 維陣列，每列是輸入特徵向量。在本例中因為只有一個輸入，所以需要一個形狀為 N×1 的陣列，N 是資料集大小。

接著，我們需要將資料分成訓練集和測試集，以便在訓練後驗證模型：

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

最後，訓練線性回歸模型只需兩行程式碼。我們定義 `LinearRegression` 物件，然後用 `fit` 方法將其擬合到資料上：

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression` 物件在 `fit` 後會包含迴歸的所有係數，可以透過 `.coef_` 屬性來存取。在我們的例子中，只有一個係數，應該約為 `-0.017`。這表示價格似乎隨時間略微下降，但不多，每天約下降兩仙。我們也可以使用 `lin_reg.intercept_` 來存取迴歸與 Y 軸的交點——在我們的例子中大約是 `21`，表示年初的價格。

為了看看我們的模型有多準確，我們可以在測試資料集上預測價格，然後測量預測值與實際值的接近程度。這可以使用均方根誤差（RMSE）指標來完成，即所有預期與預測值平方差均值的平方根。

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

我們的誤差約為 2 點，約為 17%。不是太好。衡量模型品質的另一個指標是<strong>決定係數（coefficient of determination）</strong>，可以這樣取得：

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
如果值為 0，表示模型不考慮輸入資料，作用如同<em>最差線性預測器</em>，即輸出結果的平均值。值為 1 表示我們可以完美預測所有預期輸出。在我們的例子中，係數約為 0.06，相當低。

我們也可以將測試資料與迴歸線一起繪圖，以更清楚看到迴歸在我們的案例中如何運作：

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/zh-MO/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## 多項式迴歸

另一種線性迴歸是多項式迴歸。雖然有時變數間存在線性關係——例如南瓜體積越大，價格越高——但有時這些關係無法用平面或直線繪製。

✅ 以下是[一些多項式迴歸適用的示例](https://online.stat.psu.edu/stat501/lesson/9/9.8)

再看看日期與價格的關係。這散點圖看起來是否非得用直線分析？價格是否可能波動？這種情況下，可以嘗試多項式迴歸。

✅ 多項式是由一個或多個變數與係數組成的數學表達式

多項式迴歸建立一條曲線，以更好地擬合非線性資料。在我們的例子中，如果將平方的 `DayOfYear` 變數納入輸入，我們應該可以用一個二次曲線擬合資料，該曲線在一年中某點有最小值。

Scikit-learn 提供一個方便的[管道 API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline)來結合多個資料處理步驟。<strong>管道</strong>是由多個<strong>預估器</strong>串連而成。在我們例子中，我們將建構一個管道，先加入多項式特徵，再進行迴歸訓練：

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

使用 `PolynomialFeatures(2)` 表示包含所有二次項多項式。對我們而言，只有 `DayOfYear`<sup>2</sup>，但若有兩個輸入變數 X 和 Y，則會加入 X<sup>2</sup>、XY 與 Y<sup>2</sup>。我們也可以使用更高次多項式。

管道的使用方式與原始的 `LinearRegression` 物件相同，即可以 `.fit` 管道，之後使用 `.predict` 得到預測結果。以下圖顯示測試資料與擬合曲線：

<img alt="Polynomial regression" src="../../../../translated_images/zh-MO/poly-results.ee587348f0f1f60b.webp" width="50%" />

使用多項式迴歸，我們能取得稍低的 MSE 及較高的決定係數，但改善幅度不大。我們需要考慮其他特徵！

> 你可以看到最低價的南瓜出現在萬聖節附近。你如何解釋這現象？

🎃 恭喜，你剛完成一個可幫助預測派用南瓜價格的模型。你可以對其他南瓜種類重複同樣操作，但非常繁瑣。接著讓我們學習如何在模型中考慮南瓜品種！

## 類別特徵

理想狀況下，我們希望同一模型能預測不同南瓜品種的價格。然而，`Variety` 欄位與 `Month` 不同，因它包含非數字值，這類欄位稱為<strong>類別型</strong>。

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 點擊上方圖片觀看使用類別特徵的簡短影片介紹。

這裡展示了平均價格如何依品種變化：

<img alt="Average price by variety" src="../../../../translated_images/zh-MO/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

為了考慮品種，我們首先需要將它轉換為數字形式，或稱<strong>編碼</strong>。有幾種方法：

* 簡單的<strong>數字編碼</strong>會建立一張不同品種的表，然後用該表的索引取代品種名稱。這對線性迴歸不是好方法，因為模型會把索引數字當作數值處理及乘以係數加入結果，但品種索引與價格的關係明顯非線性，即使確保索引有特定順序也會如此。
* <strong>獨熱編碼（one-hot encoding）</strong>會把 `Variety` 欄位換成4個欄位，每個對應一個品種。若該行品種對應該欄位會為 1，否則為 0。如此在迴歸模型有四個係數，分別對應每種南瓜品種，表示該品種的「起價」（或更準確地說「額外價格」）。

以下程式碼示範如何對品種進行獨熱編碼：

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

要用獨熱編碼品種訓練線性迴歸，只需正確初始化 `X` 與 `y` 資料：

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

其他程式碼與前面訓練線性迴歸相同。若嘗試執行，將會發現均方誤差差不多，但決定係數大幅提升（約 77%）。為達更準確預測，我們可以同時考慮更多類別特徵及數值特徵，例如 `Month` 或 `DayOfYear`。若要取得一個完整特徵陣列，可用 `join`：

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

這裡還考慮了 `City` 與 `Package` 類型，得到 MSE 2.84（10%）與決定係數 0.94！

## 綜合應用

為做出最佳模型，我們可以使用上述結合（獨熱編碼類別＋數值）資料，並搭配多項式迴歸。以下是完整程式碼，方便你參考：

```python
# 設置訓練數據
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# 進行訓練-測試劃分
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# 設置並訓練管道
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# 對測試數據進行預測結果
pred = pipeline.predict(X_test)

# 計算均方誤差和決定係數
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

這樣可以取得將近 97% 的最高決定係數，以及 2.23（約 8% 預測誤差）的 MSE。

| 模型 | MSE | 決定係數 |
|-------|-----|---------------|
| `DayOfYear` 線性 | 2.77 (17.2%) | 0.07 |
| `DayOfYear` 多項式 | 2.73 (17.0%) | 0.08 |
| `Variety` 線性 | 5.24 (19.7%) | 0.77 |
| 全特徵線性 | 2.84 (10.5%) | 0.94 |
| 全特徵多項式 | 2.23 (8.25%) | 0.97 |

🏆 做得好！你在一堂課中建立了四個迴歸模型，將模型品質提升至 97%。在迴歸的最後一節中，你將學習用於分類的邏輯斯迴歸。

---
## 🚀挑戰

在這個筆記本中測試不同變數，查看相關性與模型準確度的關係。

## [課後測驗](https://ff-quizzes.netlify.app/en/ml/)

## 複習與自學

本課我們學習了線性迴歸。還有其他重要的迴歸方法。閱讀關於逐步迴歸、Ridge、Lasso 和 Elasticnet 的技術。推薦深入學習的課程是[史丹佛統計學習課程](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## 作業

[建立模型](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於準確性，但請注意自動翻譯可能包含錯誤或不準確之處。原始文件之母語版本應視為權威來源。對於重要資訊，建議採用專業人工翻譯。我們不對因使用本翻譯而引起之任何誤解或錯誤解釋負責。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->