# 使用 Scikit-learn 建立迴歸模型：四種迴歸方式

## 初學者說明

線性迴歸用於我們想預測<strong>數值型</strong>結果（例如房價、溫度或銷售額）時。它透過尋找一條最能代表輸入特徵與輸出之間關係的直線來工作。

本課程重點放在理解概念，稍後會探討更進階的迴歸技術。
![Linear vs polynomial regression infographic](../../../../translated_images/zh-TW/linear-polynomial.5523c7cb6576ccab.webp)
> 資訊圖由 [Dasani Madipalli](https://twitter.com/dasani_decoded) 製作
## [課前測驗](https://ff-quizzes.netlify.app/en/ml/)

> ### [本課程也提供 R 版本！](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### 介紹

到目前為止，你已經了解了迴歸是什麼，並使用了本課程中將持續使用的南瓜價格資料集進行了範例資料的探索。你也使用 Matplotlib 進行了視覺化。

現在，你已經準備好更深入了解機器學習的迴歸。雖然視覺化可以幫助你理解資料，但機器學習的真正強大之處在於_訓練模型_。模型在歷史資料上訓練，能自動捕捉資料間的相依關係，並能為模型沒見過的新資料做出預測。

本課將學習兩種迴歸：_基本線性迴歸_與_多項式迴歸_，並了解這些技術背後的一些數學原理。這些模型將允許我們依據不同的輸入資料預測南瓜價格。

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 點擊上方圖片看關於線性迴歸的短影片概述。

> 在整個課程中，我們假設數學知識最小，並致力於讓來自其他領域的學生也能理解，因此請留意筆記、🧮 註解、圖表及其他學習工具以協助理解。

### 先備知識

你現在應該已熟悉我們所研究的南瓜資料結構。資料已在本課的 _notebook.ipynb_ 檔中預先載入並清理過。該檔案中，南瓜價格已按每蒲式耳顯示。請確保你能在 Visual Studio Code 的 kernel 中執行這些筆記本。

### 準備工作

提醒你，我們載入此資料是為了提出問題：

- 什麼時候買南瓜最划算？
- 一箱迷你南瓜的大致價格是多少？
- 我該買半蒲式耳籃裝還是 1 1/9 蒲式耳箱裝？
讓我們繼續深入這份資料。

上一課中，你建了一個 Pandas 資料框，並填入原始資料部分內容，統一以蒲式耳價格化。這樣你只蒐集到約 400 筆資料，且只有秋季月份。

看看本課附帶筆記本預先載入的資料。資料已準備好，並繪製了最初的散點圖以顯示月份資料。也許我們可以透過更進一步清理，獲得關於資料性質的更多細節。

## 線性迴歸線

如你在第一課學習的，線性迴歸的目標是能夠繪製出一條線，用以：

- <strong>顯示變數關係</strong>。展示變數間的關聯
- <strong>做出預測</strong>。準確預測新數據點相較於該線的位置

通常使用<strong>最小平方回歸</strong>繪製這類線條。名詞「最小平方」指的是我們在模型中將誤差總和降到最低的過程。對每個資料點，我們測量該點與回歸線間的垂直距離（稱為殘差）。

我們會將這些距離平方的原因有兩個：

1. <strong>大小勝於方向</strong>：希望把誤差 -5 與 +5 視為同樣大小，平方能將所有數值轉為正值。

2. <strong>重懲離群值</strong>：平方對較大誤差給予更多權重，促使線條更接近偏離較遠的點。

接著，我們將所有平方值相加。目標是找到使這個總和最小的那條線，因此稱為「最小平方」。

> **🧮 給我數學公式**  
> 
> 這條稱為_最佳擬合線_的直線可以透過[方程式](https://en.wikipedia.org/wiki/Simple_linear_regression)表示：
> 
> ```
> Y = a + bX
> ```
>
> `X` 是「自變數」，`Y` 是「應變數」。直線的斜率為 `b`，`a` 是截距，指當 `X = 0` 時的 `Y` 值。
>
>![計算斜率](../../../../translated_images/zh-TW/slope.f3c9d5910ddbfcf9.webp)
>
> 首先計算斜率 `b`。資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 製作
>
> 換句話說，回到我們南瓜資料的初始問題：「按月份預測南瓜每蒲式耳價格」，`X` 代表價格，`Y` 代表銷售月份。
>
>![完成方程式](../../../../translated_images/zh-TW/calculation.a209813050a1ddb1.webp)
>
> 計算 Y 值。如果你付了約 4 美元，那一定是四月！資訊圖由 [Jen Looper](https://twitter.com/jenlooper) 製作
>
> 計算直線的公式必須呈現斜率，同時也取決於截距，即當 `X=0` 時 `Y` 落在哪裡。
>
> 你可以參考 [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) 網站中這些值的計算方法。也可利用 [this Least-squares calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) 觀察數值如何影響直線。

## 相關性

另一個要理解的概念是給定 X 和 Y 變數之間的<strong>相關係數</strong>。利用散點圖可快速視覺化此係數。若數據點呈現整齊的線狀排列，代表高度相關；若散佈在 X 與 Y 間各處，則相關性低。

良好的線性迴歸模型會在最小平方迴歸線中擁有高（較接近 1）相關係數。

✅ 執行本課附帶的筆記本，觀察「月份對價格」的散點圖。根據你對散點圖的視覺理解，南瓜銷售中月份和價格的相關性是高還是低？若改用較細緻的衡量標準，像是<em>一年中的第幾天</em>（即從年初算起的天數）情況會有改變嗎？

以下程式碼假設資料已清理，並取得名為 `new_pumpkins` 的資料框，如下所示：

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> 清理資料的程式碼可在 [`notebook.ipynb`](notebook.ipynb) 找到。我們執行了與前一課相同的清理步驟，並使用下列表達式計算 `DayOfYear` 欄位：

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

了解線性迴歸的數學後，接著建立一個迴歸模型，看看是否能預測哪種南瓜包裝會有最佳價格。想在南瓜節使用南瓜的人，可能想利用這些資訊優化購買方案。

## 探索相關性

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 點擊上方圖片看相關性的短影片介紹。

你可能已在前一課看到，不同月份的平均價格大致如下：

<img alt="Average price by month" src="../../../../translated_images/zh-TW/barchart.a833ea9194346d76.webp" width="50%"/>

這暗示應該存在某種相關關係，我們可以嘗試用線性迴歸模型來預測 `Month` 與 `Price`，或 `DayOfYear` 與 `Price` 間的關係。下方散點圖展示後者：

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/zh-TW/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

來看看我們用 `corr` 函數測試相關性結果：

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

「月份」的相關係數大約是 -0.15，「年份中的某天」約是 -0.17，相關性看起來不大，不過可能還存在其他重要關係。似乎價格分成幾個群集，對應著不同南瓜品種。為驗證此假設，我們用不同顏色繪製南瓜分類。傳入 `ax` 參數給 `scatter` 函數，把所有點繪在同一張圖：

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/zh-TW/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

調查顯示品種對價格整體影響遠大於銷售日期。條形圖更明顯說明：

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/zh-TW/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

暫且只看「派用型」南瓜，觀察日期對價格的影響：

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/zh-TW/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

此時如果用 `corr` 計算 `Price` 與 `DayOfYear` 的相關係數，會是約 `-0.27`，代表訓練預測模型是可行的。

> 在訓練線性迴歸模型前，確保數據乾淨很重要。線性迴歸對缺失值敏感，通常會把空值剔除：

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

另一種做法是用對應欄的平均值填補缺失值。

## 簡單線性迴歸

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 點擊上方圖片看簡單線性及多項式迴歸的短影片介紹。

我們將用 **Scikit-learn** 函式庫訓練線性迴歸模型。

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

起初，我們將輸入值（特徵）與期望輸出（標籤）分別放入兩個 numpy 陣列：

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> 注意我們對輸入資料做了 `reshape`，讓線性迴歸套件正確識別。它預期輸入為 2 維陣列，每列為一組特徵向量。此處只有一個輸入，故需求是 N×1 形狀，其中 N 是資料集大小。

接下來，我們要將資料分割成訓練集和測試集，以利驗證模型表現：

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

最後，訓練線性迴歸モデル僅需兩行程式碼。我們先建立 `LinearRegression` 物件，再用 `fit` 方法對資料進行擬合：

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression` 物件在 `fit` 後包含了回歸的所有係數，可以使用 `.coef_` 屬性存取。在我們這個例子中，只有一個係數，約為 `-0.017`。這意味著價格似乎隨時間略微下降，但幅度不大，大約是每天下降兩分錢。我們也可以使用 `lin_reg.intercept_` 存取回歸線與 Y 軸的交點——在我們的例子中會約為 `21`，代表年初的價格。

為了檢視模型的準確性，我們可以在測試資料集上預測價格，然後衡量預測值與實際值的接近程度。這可以透過均方根誤差（RMSE）指標完成，其為所有實際值與預測值平方差的平均數的平方根。

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

我們的誤差約為 2 點，約佔 ~17%。不是非常理想。模型品質的另一指標是 <strong>判定係數</strong>，可以用以下方法取得：

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
 若值為 0，表示模型未考慮輸入資料，表現為 <em>最差的線性預測器</em>，即結果的平均值。值為 1 表示可以完美預測所有目標輸出。在我們的例子中，判定係數約為 0.06，屬於相當低。

我們也可以繪製測試資料與回歸線，以更清楚觀看回歸效果：

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/zh-TW/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## 多項式回歸（Polynomial Regression）

另一類線性回歸是多項式回歸。雖然變數間有時呈線性關係——例如南瓜體積越大，價格越高——有時這些關係無法用平面或直線來描繪。

✅ 這裡有[更多的例子](https://online.stat.psu.edu/stat501/lesson/9/9.8)適用於多項式回歸的資料

再看一次日期與價格的關係。這個散佈圖看起來一定得用直線分析嗎？價格不會波動嗎？此時可以嘗試多項式回歸。

✅ 多項式是可能包含一個或多個變數及係數的數學表達式

多項式回歸會產生曲線以更好擬合非線性資料。我們若在輸入資料中加入平方的 `DayOfYear` 變數，應該能用拋物線曲線擬合資料，且該曲線在某年內的某點有極小值。

Scikit-learn 提供了方便的 [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) 將不同的資料處理步驟串聯起來。**pipeline** 是一連串的 **estimators**。在我們例子中，建立一個首先加入多項式特徵，接著訓練回歸模型的 pipeline：

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

使用 `PolynomialFeatures(2)` 意味著會包含所有二階多項式。我們的例子為 `DayOfYear`<sup>2</sup>，如果有兩個輸入變數 X 與 Y，會加入 X<sup>2</sup>、XY 與 Y<sup>2</sup>。當然也可以用更高階多項式。

Pipeline 使用方式與原本的 `LinearRegression` 物件相同，可以 `fit` 來訓練，然後用 `predict` 預測。下圖展示測試資料與擬合曲線：

<img alt="Polynomial regression" src="../../../../translated_images/zh-TW/poly-results.ee587348f0f1f60b.webp" width="50%" />

使用多項式回歸，我們能獲得稍微更低的 MSE 與更高的判定係數，但差異不大。還是要加入其他特徵考量！

> 你可以看到南瓜價格的最低點出現在萬聖節左右。你如何解釋這個現象？

🎃 恭喜，你已建立了可協助預測派用南瓜價格的模型。你可以用同樣流程為所有南瓜種類建立模型，但會很繁瑣。接著讓我們學習如何將南瓜品種納入模型中！

## 類別變數（Categorical Features）

理想狀況下，我們希望能用同一個模型預測不同南瓜品種的價格。但 `Variety` 欄位與 `Month` 等欄位不同，因為它包含非數值資料。這種欄位稱為 **類別變數（categorical）**。

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 點擊上方圖片，可觀看使用類別特徵的簡短說明影片。

這裡展示了平均價格與品種的關係：

<img alt="Average price by variety" src="../../../../translated_images/zh-TW/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

要考慮品種，我們必須先將它轉成數字形式，或叫做<strong>編碼</strong>。有幾種方法：

* 簡單的<strong>數字編碼</strong>會建立不同品種的編號表，然後用編號替換品種名稱。對線性回歸來說這不佳，因為數字編碼會被視為數值並乘以係數，造成明顯的非線性關係，尤其即便我們嘗試排序編號仍然不合適。
* <strong>One-hot 編碼</strong>會把 `Variety` 欄拆成四個欄位，分別代表四種品種。每欄包含 1 或 0，表示該行是否屬於此品種。線性回歸有四個係數，各自代表各品種的“基本價格”或“額外價格”。

以下程式碼示範如何對品種做 one-hot 編碼：

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

若要用 one-hot 編碼的品種訓練線性回歸，只要正確建立 `X` 和 `y` 即可：

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

其餘程式碼與之前線性回歸訓練過程相同。嘗試執行後會看到均方誤差大致相同，但判定係數明顯提升到約 77%。若要更準確的預測，可以將更多類別特徵和數值特徵（如 `Month` 或 `DayOfYear`）納入。用 `join` 合併成一個大特徵陣列：

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

這裡也將 `City` 與 `Package` 類型納入，得到的 MSE 降至 2.84（10%），判定係數提升至 0.94！

## 綜合建模

為了取得最佳模型，我們可以將前面例子中合併（one-hot 編碼類別 + 數值）資料與多項式回歸結合。以下是完整範例程式碼供您方便使用：

```python
# 設置訓練資料
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# 進行訓練-測試資料切割
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# 設定並訓練流程
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# 預測測試資料的結果
pred = pipeline.predict(X_test)

# 計算均方誤差和決定係數
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

這會讓我們得到接近 97% 的判定係數，以及 MSE = 2.23（約 8% 預測誤差）。

| 模型 | MSE | 判定係數 |
|-------|-----|----------------|
| `DayOfYear` 線性 | 2.77 (17.2%) | 0.07 |
| `DayOfYear` 多項式 | 2.73 (17.0%) | 0.08 |
| `Variety` 線性 | 5.24 (19.7%) | 0.77 |
| 所有特徵 線性 | 2.84 (10.5%) | 0.94 |
| 所有特徵 多項式 | 2.23 (8.25%) | 0.97 |

🏆 做得好！你在這一課建立了四個迴歸模型，並將模型品質提升到 97%。在迴歸的最後一節，我們會學習羅吉斯迴歸（Logistic Regression）來判斷類別。

---
## 🚀挑戰

在此筆記本中測試不同變數，看看其相關度與模型準確率的關係。

## [課後測驗](https://ff-quizzes.netlify.app/en/ml/)

## 複習與自學

本課程學習了線性回歸。還有其他重要的迴歸類型，像是逐步回歸、Ridge、Lasso 與 Elasticnet 技術。推薦研讀的優良課程為 [史丹佛統計學習課程](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## 作業

[建立模型](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於確保翻譯準確，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件之母語版本應視為權威來源。對於重要資訊，建議採用專業人工翻譯。因使用本翻譯所產生之任何誤解或誤用，我們概不負責。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->