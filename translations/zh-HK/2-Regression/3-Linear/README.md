# 使用 Scikit-learn 建立迴歸模型：四種迴歸方法

## 初學者注記

線性迴歸用於當我們想要預測<strong>數值</strong>（例如，房價、溫度或銷售額）時。  
線性迴歸透過尋找一條最佳代表輸入特徵和輸出之間關係的直線來運作。

在本課程中，我們著重於先理解概念，再探索更進階的迴歸技術。  
![線性與多項式回歸資訊圖](../../../../translated_images/zh-HK/linear-polynomial.5523c7cb6576ccab.webp)  
> 資訊圖由 [Dasani Madipalli](https://twitter.com/dasani_decoded) 製作

## [課前小測驗](https://ff-quizzes.netlify.app/en/ml/)

> ### [本課程亦有 R 版本！](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)  
### 介紹

到目前為止，您已經使用南瓜價格資料集探索了什麼是迴歸，並且使用 Matplotlib 做了資料視覺化。

現在您已準備深入了解機器學習的迴歸。雖然視覺化可以幫助理解資料，但機器學習的真正威力來自於_訓練模型_。模型是基於歷史資料訓練而成，能自動捕捉資料間的依賴關係，並能對之前沒看過的新資料預測結果。

在本課中，您將學習兩種迴歸：_基本線性迴歸_及_多項式迴歸_，以及其中一些數學原理。這些模型將讓我們根據不同輸入資料預測南瓜價格。

[![機器學習入門 - 理解線性迴歸](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "機器學習入門 - 理解線性迴歸")

> 🎥 點擊上方圖片觀看線性迴歸的簡短影片概述。

> 在整個課程中，我們假設學員的數學知識量少，並力求讓其他領域的學生都能理解，因此會有註解、🧮 重點標註、圖解及其他學習工具協助理解。

### 先備知識

您應該已熟悉我們正在檢視的南瓜資料結構。這份資料已預先載入並清理好，在本課的 _notebook.ipynb_ 檔案中。檔中南瓜價格以每蒲式耳價格顯示於新的資料框中。請確保您能在 Visual Studio Code 的環境中執行這些筆記本。

### 準備工作

提醒您，載入這些資料是為了探究一些問題：

- 何時購買南瓜最划算？  
- 一箱迷你南瓜的價格大約是多少？  
- 應該買半蒲式耳的籃子，還是 1又1/9蒲式耳的箱子？  
讓我們繼續挖掘這些資料。

前一課中，您建立了 Pandas 資料框，並填入原始資料的部分，且將價格以蒲式耳標準化。但如此一來，只收集了約 400 筆資料，且僅涵蓋秋季。

請看看本課附帶筆記本所載入的資料，我們已有初始散點圖繪出月份資料。也許透過更多清理，我們能獲得這資料本質的更多細節。

## 線性迴歸線

如您在第一課學到的，線性迴歸的目標是能繪出一條線，以：

- <strong>展示變數間關係</strong>。展現變數的相互關係  
- <strong>進行預測</strong>。準確預測新資料點在線上的落點

<strong>最小平方法迴歸</strong>通常用於繪製此類線條。所謂「最小平方法」是指最小化模型總誤差的過程。對每個資料點，我們測量該點與迴歸線間的垂直距離（稱為殘差）。

我們將這些距離平方，主要有兩個原因：

1. <strong>重視誤差大小而非方向</strong>：誤差 -5 與誤差 +5 對我們而言應同等重要，平方能將所有誤差轉為正數。

2. <strong>對離群值加重懲罰</strong>：平方會加重較大誤差的權重，促使線條貼近偏遠點。

接著將所有平方後的誤差相加，希望求出誤差和最小的那條線——這即是「最小平方法」的由來。

> **🧮 為我展示數學推導**  
>  
> 這條線稱為_最適合線_，可用[一個方程](https://en.wikipedia.org/wiki/Simple_linear_regression)表示：  
>  
> ```
> Y = a + bX
> ```
>  
> `X` 為「解釋變數」；`Y` 為「應變數」。線的斜率是 `b`，而 `a` 是 y 截距，表示當 `X = 0` 時 `Y` 的數值。  
>  
>![計算斜率](../../../../translated_images/zh-HK/slope.f3c9d5910ddbfcf9.webp)  
>  
> 首先計算斜率 `b`。資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 提供  
>  
> 換句話說，針對南瓜資料的原始問題：「根據月份預測每蒲式耳南瓜價格」，`X` 是指價格而 `Y` 是銷售的月份。  
>  
>![完成等式](../../../../translated_images/zh-HK/calculation.a209813050a1ddb1.webp)  
>  
> 計算 Y 的數值。如果您付約 $4，就應該是四月！資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 提供  
>  
> 計算該線的數學必須展示斜率，也取決於截距，也就是 `X = 0` 時 `Y` 所在位置。  
>  
> 您可參考 [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) 網站來觀察此計算方法；也可使用 [此最小平方法計算器](https://www.mathsisfun.com/data/least-squares-calculator.html) 來觀察數字如何影響迴歸線。

## 相關係數

另一重要詞彙是給定 `X` 與 `Y` 變數間的<strong>相關係數</strong>。透過散點圖，您能快速直觀地看見此係數。若資料點沿著一條整齊的線散佈，代表高度相關；若資料點分佈分散在 `X` 和 `Y` 之間，則代表相關性低。

一個好的線性迴歸模型，其相關係數用最小平方法計算得到的值應該是高的（接近 1，而非 0）。

✅ 執行本課附帶的筆記本並觀察「月份對價格」的散點圖。從這散點圖視覺判斷，與南瓜銷售之月對價格的資料，看起來是高還是低相關？如果改為使用更細緻的時間尺度取代月份，例如「一年中第幾天」（自年初起的天數），結果會改變嗎？

接下來的程式中，我們假設資料已清理完畢，並產生類似以下的 `new_pumpkins` 資料框：

ID | 月份 | 一年中第幾天 | 品種 | 城市 | 包裝 | 最低價 | 最高價 | 價格  
---|-----|--------|------|------|-------|-------|-------|-------  
70 | 9 | 267 | 派用型 | 巴爾的摩 | 1又1/9蒲式耳箱 | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | 派用型 | 巴爾的摩 | 1又1/9蒲式耳箱 | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | 派用型 | 巴爾的摩 | 1又1/9蒲式耳箱 | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | 派用型 | 巴爾的摩 | 1又1/9蒲式耳箱 | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | 派用型 | 巴爾的摩 | 1又1/9蒲式耳箱 | 15.0 | 15.0 | 13.636364  

> 資料清理的程式碼請參見 [`notebook.ipynb`](notebook.ipynb)。我們執行了與上一課相同的清理步驟，並用下式計算出 `DayOfYear` 欄位：  

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
現在您已了解線性迴歸的數學原理，讓我們建立迴歸模型，看看是否能預測出哪種包裝的南瓜價格最划算。想要打造南瓜節慶角落的購買者，會希望知悉這資訊以最佳化南瓜包裝的購買決策。

## 尋找相關性

[![機器學習入門 - 尋找相關性：線性迴歸的關鍵](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "機器學習入門 - 尋找相關性：線性迴歸的關鍵")

> 🎥 點擊上方圖片觀看相關性的簡短影片概述。

在先前的課堂中，您大概已看到不同月份的平均價格如下：

<img alt="各月份平均價格" src="../../../../translated_images/zh-HK/barchart.a833ea9194346d76.webp" width="50%"/>

這顯示應該存在某種相關性，我們可以嘗試訓練線性迴歸模型來預測 `Month` 與 `Price` 或 `DayOfYear` 與 `Price` 間的關係。下圖展示後者的散點圖：

<img alt="價格與一年中第幾天散點圖" src="../../../../translated_images/zh-HK/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

我們用 `corr` 函式來看看有無相關性：

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
看來相關性非常小，使用 `Month` 為 -0.15，使用 `DayOfMonth` 為 -0.17，但可能還有另一個重要的關係。價格在不同南瓜品種間似乎分成不同群聚。為了驗證此假設，我們用不同顏色來繪製各南瓜類別。透過給 `scatter` 函式傳入 `ax` 參數，可以將所有點繪製在同一張圖上：

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="一年中第幾天與價格散點圖（有顏色區分）" src="../../../../translated_images/zh-HK/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

研究顯示品種對價格影響比銷售日期更大。我們用長條圖來說明：

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="品種與價格長條圖" src="../../../../translated_images/zh-HK/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

暫時只聚焦於一種南瓜品種「派用型」，來看看日期對價格的影響：

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="一天中日期與價格散點圖" src="../../../../translated_images/zh-HK/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

如果這時用 `corr` 函式計算 `Price` 與 `DayOfYear` 的相關性，大約是 `-0.27`，意味著訓練預測模型是合理的。

> 在訓練線性迴歸前，務必確保資料乾淨。線性迴歸對缺漏值不友善，因此最好去除所有空值儲存格：

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
另一個作法是使用相對應欄位的平均值填充這些空值。

## 簡單線性迴歸

[![機器學習入門 - 使用 Scikit-learn 線性與多項式迴歸](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "機器學習入門 - 使用 Scikit-learn 線性與多項式迴歸")

> 🎥 點擊上方圖片觀看線性與多項式迴歸的簡短影片概述。

我們將使用 **Scikit-learn** 函式庫來訓練線性迴歸模型。

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
首先將輸入值（特徵）與預期輸出（標籤）分開存成 numpy 陣列：

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> 注意我們必須對輸入資料做 `reshape`，讓線性迴歸模組可正確理解。線性迴歸要求輸入為二維陣列，陣列中每一列代表一組輸入特徵向量。由於我們只有一個輸入特徵，故需為形狀 N×1 的陣列，N 為資料集大小。

接著，需將資料劃分為訓練集和測試集，以便訓練後驗證模型：

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
最後，訓練線性迴歸模型只需兩行程式：定義 `LinearRegression` 物件，並用 `fit` 方法擬合模型：

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`fit` 後的 `LinearRegression` 對象包含了回歸的所有係數，可以通過 `.coef_` 屬性訪問。在我們的情況下，只有一個係數，應該約為 `-0.017`。這意味著價格似乎隨時間略有下降，但不多，大約每天下降 2 分錢。我們還可以使用 `lin_reg.intercept_` 訪問回歸與 Y 軸的交點 — 在我們的情況下將約為 `21`，表示年初的價格。

為了查看我們模型的準確度，我們可以在測試數據集上進行價格預測，然後測量預測值與預期值的接近程度。這可以通過均方根誤差（RMSE）指標完成，該指標是所有預期值與預測值差的平方平均的平方根。

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

我們的誤差約為 2 點，約為 17%。不太理想。另一個模型質量的指標是 <strong>決定係數</strong>，可以如下獲得：

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
 若該值為 0，表示模型未考慮輸入數據，行為就像<em>最差的線性預測器</em>，即結果的均值。值為 1 表示我們可以完美預測所有預期輸出。在我們的情況下，係數約為 0.06，較低。

我們還可以將測試數據與回歸線繪製在一起，以更好地觀察回歸情況：

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/zh-HK/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## 多項式回歸

另一種線性回歸是多項式回歸。有時變量之間呈線性關係——比如體積越大的南瓜價格越高——但有時這種關係無法用平面或直線表示。

✅ 這裡有[一些額外範例](https://online.stat.psu.edu/stat501/lesson/9/9.8)數據適合用多項式回歸

再看看日期和價格的關係。這個散點圖是否一定要用直線分析？價格難道不會波動嗎？這種情況下，可以嘗試多項式回歸。

✅ 多項式是由一個或多個變量及係數構成的數學表達式

多項式回歸產生一條曲線，更好地擬合非線性數據。在我們的案例中，若將平方的 `DayOfYear` 變量加入輸入資料，應能用拋物線曲線擬合數據，曲線在一年中某點處有最小值。

Scikit-learn 提供了方便的[管道 API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline)來將不同的數據處理步驟組合起來。<strong>管道</strong>是一系列的<strong>估計器</strong>。在這裡，我們創建一個管道，先加入多項式特徵，然後進行回歸訓練：

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

使用 `PolynomialFeatures(2)` 表示我們將包含所有二次項多項式。對於一個變量僅為 `DayOfYear` 的平方，但對兩個輸入變量 X 和 Y 則為 X<sup>2</sup>、XY、Y<sup>2</sup>。我們也可以使用更高次多項式。

管道可以像原始的 `LinearRegression` 對象那樣使用，即可 `fit` 管道，然後用 `predict` 獲取預測結果。下面的圖展示了測試數據和擬合的曲線：

<img alt="Polynomial regression" src="../../../../translated_images/zh-HK/poly-results.ee587348f0f1f60b.webp" width="50%" />

使用多項式回歸，我們可以獲得稍低的均方誤差和更高的決定係數，但提升不明顯。需要考慮其他特徵！

> 你可以看到最小南瓜價格出現在萬聖節前後。你如何解釋這種現象？

🎃 恭喜，你剛剛建立了一個能幫助預測派南瓜價格的模型。你也可以用同樣的方法針對所有南瓜品種建立模型，但那會很繁瑣。接下來學習如何將南瓜品種納入模型考慮！

## 類別特徵

理想狀況下，我們希望用同一模型預測不同南瓜品種的價格。但 `Variety` 欄位與 `Month` 不同，因為它包含非數字值。這類欄位稱為<strong>類別特徵（categorical）</strong>。

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 點擊上圖觀看簡短影片，了解如何使用類別特徵。

這裡展示了平均價格與品種的關係：

<img alt="Average price by variety" src="../../../../translated_images/zh-HK/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

要考慮品種，首先要將其轉為數字形式，即<strong>編碼</strong>。有幾種方法：

* 簡單的<strong>數字編碼</strong>會建一個包含各品種的表格，然後用對應索引替換品種名稱。這對線性回歸不是最佳方案，因為線性回歸使用索引的數字值乘以係數再加總，然而指標號碼和價格的關係顯然非線性，即使索引有特定排序也無法保證。
* <strong>獨熱編碼（One-hot encoding）</strong>則把 `Variety` 欄拆成 4 個不同欄位（每個品種一欄）。對應行屬該品種的欄位為 `1`，否則為 `0`。這意味著線性回歸中會有四個係數，分別表示各品種的「起始價格」或「額外價格」。

下面代碼演示如何獨熱編碼品種：

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

要用獨熱編碼的品種作為輸入訓練線性回歸，只要正確初始化 `X` 和 `y` 數據即可：

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

其餘代碼與之前用於訓練線性回歸的相同。試驗後會看到均方誤差約相同，但決定係數大幅提升至約 77%。要想更精確，也可納入更多類別特徵和數值特徵，如 `Month` 或 `DayOfYear`。為了拼成一個大特徵陣列，可使用 `join`：

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

這裡我們還考慮了 `City` 和 `Package` 類型，結果為 MSE 2.84（約 10%），決定係數 0.94！

## 綜合應用

為構建最佳模型，我們可以將上述示例中一熱編碼類別+數值的特徵結合多項式回歸。以下是完整代碼，方便參考：

```python
# 設置訓練數據
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# 進行訓練和測試分割
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# 設置並訓練流程
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# 預測測試數據結果
pred = pipeline.predict(X_test)

# 計算均方誤差和決定係數
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

預計獲得近乎 97% 的最佳決定係數，以及 MSE=2.23（約 8% 預測誤差）。

| 模型 | MSE | 決定係數 |
|-------|-----|---------------|
| `DayOfYear` 線性 | 2.77 (17.2%) | 0.07 |
| `DayOfYear` 多項式 | 2.73 (17.0%) | 0.08 |
| `Variety` 線性 | 5.24 (19.7%) | 0.77 |
| 所有特徵 線性 | 2.84 (10.5%) | 0.94 |
| 所有特徵 多項式 | 2.23 (8.25%) | 0.97 |

🏆 做得好！本課程你建立了四種回歸模型，並將模型質量提升至 97%。最後一節關於回歸，會介紹用於分類的邏輯迴歸。

---
## 🚀挑戰

試驗本筆記本中的多種變數，看看相關性如何影響模型準確度。

## [課後測驗](https://ff-quizzes.netlify.app/en/ml/)

## 複習與自學

本課學習了線性回歸。還有其他重要的回歸類型。請閱讀逐步回歸、嶺回歸、套索回歸和彈性網技術。學習更多可參考[史丹佛統計學習課程](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## 作業

[建立模型](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：  
本文件由 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 翻譯而成。雖然我們致力於準確性，請注意自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於重要資訊，建議聘請專業人工翻譯。對於因使用本翻譯而產生的任何誤解或錯誤詮釋，我們概不負責。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->