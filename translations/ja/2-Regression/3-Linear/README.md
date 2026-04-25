# Scikit-learnを使った回帰モデルの構築：4つの回帰手法

## 初心者向けノート

線形回帰は、<strong>数値的な値</strong>（例えば、家の価格、気温、売上高）を予測したいときに使われます。
入力特徴量と出力の関係を最もよく表す直線を見つけることで動作します。

このレッスンでは、より高度な回帰手法に進む前に、概念の理解に重点を置きます。
![線形回帰と多項式回帰のインフォグラフィック](../../../../translated_images/ja/linear-polynomial.5523c7cb6576ccab.webp)
> インフォグラフィック作成者：[Dasani Madipalli](https://twitter.com/dasani_decoded)
## [事前講義クイズ](https://ff-quizzes.netlify.app/en/ml/)

> ### [このレッスンはRでも利用可能です！](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### はじめに

これまで、かぼちゃの価格設定データセットから収集したサンプルデータを使って回帰とは何かを探りました。このレッスン全体でこのデータセットを使用します。また、Matplotlibを使って可視化も行いました。

いよいよ機械学習の回帰をより深く掘り下げる準備ができました。可視化によりデータの内容を理解することはできますが、機械学習の真の強みは_モデルのトレーニング_にあります。モデルは過去のデータで学習し、自動的にデータの依存関係を捉え、新しいデータに対して予測を行うことができます。

このレッスンでは、_基本的な線形回帰_と_多項式回帰_の2種類の回帰について詳しく学び、それらの手法の背後にある数学も一部扱います。これらのモデルを利用して、さまざまな入力データに基づいたかぼちゃの価格を予測します。

[![初心者のための機械学習 - 線形回帰の理解](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "初心者のための機械学習 - 線形回帰の理解")

> 🎥 上の画像をクリックすると線形回帰の簡単な動画概要が見られます。

> このカリキュラム全体を通じて、数学の知識は最小限に抑え、他分野から来た学生でも理解しやすいよう工夫しています。メモ、🧮 コールアウト、図解などの学習支援も随所にあります。

### 前提条件

かぼちゃデータの構造に既に慣れているはずです。このレッスンの_notebook.ipynb_に前処理済みの状態で組み込まれています。ファイル内ではバッシェル単位のかぼちゃ価格が新しいデータフレームに表示されています。Visual Studio Codeのカーネルでこれらのノートブックが動作するか必ず確認してください。

### 準備

念のために言えば、このデータを読み込み、そこから質問を立てることが目的です。

- かぼちゃを買うベストな時期はいつか？
- ミニかぼちゃのケースの価格はいくらか？
- 半バッシェルのバスケットと1 1/9バッシェルの箱、どちらで買うべきか？
さらにデータを深掘りしていきましょう。

前回のレッスンで、Pandasのデータフレームを作成し、元のデータセットの一部を抽出、バッシェル単位で価格を標準化しました。しかしその際、約400件のデータポイントしか得られず、対象は秋の月だけでした。

このレッスンのノートブックにプリロードされたデータを見てみましょう。データは既に読み込まれ、月ごとの散布図が作成されています。データの性質をもう少し詳しく理解するため、データをさらにクリーニングすることができるかもしれません。

## 線形回帰直線

レッスン1で学んだように、線形回帰の目的は直線をプロットして、

- <strong>変数間の関係を示すこと</strong>。変数間の関係を表現する
- <strong>予測を行うこと</strong>。新しいデータ点がその直線に対してどこに位置するかを正確に予測する

ことです。

この種の直線を引くのは通常、<strong>最小二乗回帰</strong>と呼ばれる手法です。「最小二乗」はモデル内の誤差（残差）を最小化するプロセスを指します。各データポイントに対して、実際の点と回帰直線との垂直距離（残差）を測ります。

二乗和を使う理由は主に2つです：

1. <strong>大きさを重視し方向は無視</strong>：誤差の-5も+5も同じ扱いにしたいため、全て正の値にするために二乗します。

2. <strong>外れ値へのペナルティ</strong>：大きな誤差により大きな重みを与えることで、遠く離れた点に線が近づくようにします。

これらの二乗値の合計を計算し、その合計が最小となる直線を探します。これが「最小二乗法」の名前の由来です。

> **🧮 数学を見てみましょう**  
>  
> この直線は_最適適合直線_と呼ばれ、[次の式](https://en.wikipedia.org/wiki/Simple_linear_regression)で表されます:  
>  
> ```
> Y = a + bX
> ```
>
> `X`は「説明変数」、`Y`は「目的変数」です。直線の傾きは`b`、`a`は切片で、`X=0`のときの`Y`の値を指します。  
>
>![傾きの計算](../../../../translated_images/ja/slope.f3c9d5910ddbfcf9.webp)
>
> まず傾き`b`を計算します。インフォグラフィックは [Jen Looper](https://twitter.com/jenlooper) さん作成
>
> 言い換えれば、「月ごとのかぼちゃ価格を予測する」というオリジナルの問題に関連するとき、`X`が価格、`Y`が販売月を表します。
>
>![計算の完成](../../../../translated_images/ja/calculation.a209813050a1ddb1.webp)
>
> `Y`の値を計算します。価格が約4ドルなら4月と推測！インフォグラフィックは [Jen Looper](https://twitter.com/jenlooper) さん作成
>
> 直線計算の数学は、切片（`X=0`の場合の`Y`の値）に依存する傾きを示す必要があります。
>
> これらの値の算出方法は [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) のサイトで説明されています。また [この最小二乗計算機](https://www.mathsisfun.com/data/least-squares-calculator.html) で数値が直線に与える影響を確認できます。

## 相関

理解すべきもう一つの用語は、与えられたXとY変数間の<strong>相関係数</strong>です。散布図を使えば、この係数を素早く視覚的に把握できます。データ点がきれいに一直線上に散らばっている場合は高い相関があり、XとYの間で点がバラバラに散らばっていれば相関は低いです。

良い線形回帰モデルとは、最小二乗法の回帰直線で高い（0より1に近い）相関係数を持つモデルです。

✅ このレッスンのノートブックを実行して、月と価格の散布図を見てください。かぼちゃの月と価格の関連は、散布図の視覚的解釈から見ると高い相関でしょうか？それとも低いでしょうか？また、`Month`ではなく、より細かい指標（例えば、年始からの通算日数）を使うとどう変わるか確認してください。

以下のコードでは、データがクリーニングされ、`new_pumpkins`という名前のデータフレームが得られていると仮定します。以下のようなデータです：

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> データクリーニングのコードは[`notebook.ipynb`](notebook.ipynb)にあります。前回のレッスンと同様のクリーニング手順を行い、`DayOfYear`カラムは以下の式で算出しています：

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

線形回帰の数学的背景を理解したので、回帰モデルを作成し、どのかぼちゃパッケージが最も価格的に有利か予測できるか試してみましょう。かぼちゃパッチのためにかぼちゃを買う人にとって、この情報はパッチ用のかぼちゃ購入最適化に役立つでしょう。

## 相関を探す

[![初心者のための機械学習 - 相関関係の探求：線形回帰の鍵](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "初心者のための機械学習 - 相関関係の探求：線形回帰の鍵")

> 🎥 上の画像をクリックすると相関関係の簡単な動画概要が見られます。

前回のレッスンでは月ごとの平均価格は以下のようでした：

<img alt="月ごとの平均価格" src="../../../../translated_images/ja/barchart.a833ea9194346d76.webp" width="50%"/>

これは一定の相関関係があることを示唆しています。そこで、`Month`と`Price`間、もしくは`DayOfYear`と`Price`間の関係性を予測する線形回帰モデルのトレーニングを試みます。以下がその後者の散布図です：

<img alt="価格と年初からの日数の散布図" src="../../../../translated_images/ja/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

`corr`関数で相関を見てみましょう：

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

月を使った場合-0.15、日数を使った場合-0.17と相関は小さいように見えますが、別の重要な関係もありそうです。どうやら価格のクラスターはかぼちゃの品種によって異なっているようです。この仮説を確かめるため、品種ごとに色分けしてプロットします。`scatter`関数に`ax`パラメータを渡すことで全ての点を同じグラフ上に描画できます：

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="価格と年初からの日数の散布図（色分けあり）" src="../../../../translated_images/ja/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

調査の結果、品種が販売日の影響よりも総価格に影響を与えていることが示されました。棒グラフでもわかります：

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="品種ごとの価格の棒グラフ" src="../../../../translated_images/ja/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

ここでは一旦、かぼちゃ品種の一つである「パイタイプ」に焦点を当て、日付が価格に与える影響を見てみましょう：

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="価格と年初からの日数の散布図（パイタイプのみ）" src="../../../../translated_images/ja/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

ここで`Price`と`DayOfYear`の相関を`corr`関数で計算すると、約`-0.27`となります。つまり予測モデルを学習する価値があると言えます。

> 線形回帰モデルをトレーニングする前に、データがクリーンかどうか確認しましょう。線形回帰は欠損値に弱いため、空のセルを削除するのが有効です：

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

別の方法としては、空のセルを対応する列の平均値で埋める方法もあります。

## 単純線形回帰

[![初心者のための機械学習 - Scikit-learnによる線形回帰と多項式回帰](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "初心者のための機械学習 - Scikit-learnによる線形回帰と多項式回帰")

> 🎥 上の画像をクリックすると線形回帰と多項式回帰の簡単な動画概要が見られます。

線形回帰モデルのトレーニングには<strong>Scikit-learn</strong>ライブラリを使用します。

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

まず入力値（特徴量）と期待される出力（ラベル）を別々のnumpy配列に分けます：

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> 入力データに`reshape`を施した理由は、線形回帰パッケージが正しく理解するためです。線形回帰は2次元配列を入力として期待しており、配列の各行は入力特徴量のベクトルに対応します。今回は入力がひとつだけなので、形状はN×1となります（Nはデータセットのサイズ）。

次に、トレーニング用データとテスト用データに分割し、学習後にモデルの検証ができるようにします：

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

最後に、線形回帰モデルのトレーニングはたった2行のコードです。`LinearRegression`オブジェクトを定義し、その`fit`メソッドでデータにフィットさせます：

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`fit` 後の `LinearRegression` オブジェクトには回帰のすべての係数が含まれており、`.coef_` プロパティを使ってアクセスできます。今回の場合、係数はひとつだけで、約 `-0.017` です。これは価格が時間とともに少しずつ下がる傾向があることを示しており、1日あたり約2セントの減少を意味します。また、回帰直線のY軸との交点には `lin_reg.intercept_` を使ってアクセスでき、今回の場合は約 `21` で、年初の価格を示しています。

モデルの精度を確認するために、テストデータセットで価格を予測し、その予測値が期待値にどれだけ近いかを測定できます。これは二乗平均平方根誤差（RMSE）という指標を使って行い、期待値と予測値のすべての二乗差の平均の平方根を計算します。

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```
  
誤差は約2ポイント、すなわち約17%となり、あまり良くありません。モデル品質の別の指標として <strong>決定係数</strong> があります。これは次のように取得できます：

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
  
値が0の場合、モデルは入力データを考慮せず、結果の単純な平均値として振る舞う「最悪の線形予測子」となります。値が1の場合、すべての期待出力を完全に予測できることを意味します。今回の決定係数は約0.06で、かなり低い値です。

テストデータと回帰直線を一緒にプロットすると、回帰の仕組みがよりわかりやすくなります：

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```
  
<img alt="Linear regression" src="../../../../translated_images/ja/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## 多項式回帰

線形回帰の別のタイプとして多項式回帰があります。変数間に必ずしも線形関係があるとは限らず、たとえばカボチャの体積が大きいほど価格が高くなる場合でも、それが平面や直線として表現できないことがあります。

✅ こちらに [多項式回帰が有効な他の例](https://online.stat.psu.edu/stat501/lesson/9/9.8) があります

再度、日付と価格の関係を見てみましょう。この散布図は必ずしも直線で分析すべきものに見えますか？価格が変動することはありませんか？この場合、多項式回帰を試すことができます。

✅ 多項式は一つまたは複数の変数と係数からなる数学的表現です

多項式回帰は非線形データにより適合するカーブを作ります。今回の場合、入力データに二乗した `DayOfYear` 変数を含めれば、パラボラカーブによりデータを近似でき、年のある時点で最小値を持つ曲線ができます。

Scikit-learn にはデータ処理の複数ステップを結合できる便利な [パイプラインAPI](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) があります。<strong>パイプライン</strong>は一連の<strong>推定器</strong>から構成されます。ここでは最初に多項式特徴を追加し、その後回帰の学習を行うパイプラインを作成します：

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```
  
`PolynomialFeatures(2)` を使うと、入力データからすべての2次多項式を含めます。今回の場合は `DayOfYear`<sup>2</sup> だけですが、X と Y という2つの入力変数があれば X<sup>2</sup>、XY、Y<sup>2</sup> が追加されます。より高次の多項式も使えます。

パイプラインは元の `LinearRegression` オブジェクトと同様に使えるので、`fit` で学習し `predict` で予測結果を得られます。以下の図はテストデータと近似曲線です：

<img alt="Polynomial regression" src="../../../../translated_images/ja/poly-results.ee587348f0f1f60b.webp" width="50%" />

多項式回帰を使うことで、わずかにMSEは下がり、決定係数は上がりますが、大きな変化ではありません。他の特徴量も考慮する必要があります！

> 最低のカボチャ価格がハロウィーン付近に現れることがわかります。これはどう説明できますか？

🎃 おめでとうございます。パイ用カボチャの価格を予測できるモデルを作成できました。同じ手順をすべてのカボチャの種類に繰り返せるはずですが、それは面倒でしょう。次は品種をモデルに組み込む方法を学びましょう！

## カテゴリカル特徴量

理想的には、同じモデルで異なるカボチャの品種の価格を予測したいです。ただし `Variety` 列は `Month` のように数値ではなく、数値以外の値を含みます。このような列は <strong>カテゴリカル</strong> と呼ばれます。

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 カテゴリカル特徴を使う方法を簡単に解説した動画は上の画像をクリックしてください。

ここでは種類ごとの平均価格がどう違うかがわかります：

<img alt="Average price by variety" src="../../../../translated_images/ja/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

品種を考慮するには、まず数値形式に変換（<strong>エンコード</strong>）する必要があります。方法はいくつかあります：

* 単純な <strong>数値エンコード</strong> は異なる品種の一覧を作り、その品種名をインデックスに置き換えます。線形回帰ではこれはあまりよくありません。なぜなら線形回帰がインデックスの数値を実際の値として使い、それに係数を掛けて結果に加えるからです。今回の場合、インデックス番号と価格の関係は明らかに非線形で、インデックスの順序をどう決めてもそうです。
* <strong>ワンホットエンコード</strong> は `Variety` 列を4つの別列に置き換え、それぞれが品種の一つを表します。各列には該当品種なら `1`、そうでなければ `0` が入ります。これにより、線形回帰は4つの係数を持ち、それぞれが特定品種の「基準価格」（より正確には「追加価格」）を表します。

以下のコードはワンホットエンコードのサンプルです：

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

ワンホットエンコードした品種を入力にして線形回帰を学習するには、適切に `X` と `y` データを初期化すればよいです：

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```
  
それ以外のコードはこれまでの線形回帰の学習時と同じです。これを試すと平均二乗誤差はほぼ同じながら、決定係数はかなり高く（約77%）なります。さらに精度を上げるには、ほかのカテゴリカル特徴や数値特徴（例：`Month` や `DayOfYear`）も考慮します。特徴量をひとつの大きな配列にまとめるには `join` を使います：

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```
  
ここでは `City` と `Package` の種類も考慮し、MSEは2.84（10%）、決定係数は0.94となりました！

## 総合的なモデル作成

最高のモデルを作るため、上記の組み合わせ（ワンホットエンコードしたカテゴリカル＋数値）データを多項式回帰と組み合わせます。以下はその完全なコードです：

```python
# トレーニングデータを設定する
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# トレイン・テスト分割を行う
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# パイプラインを設定し、トレーニングする
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# テストデータの結果を予測する
pred = pipeline.predict(X_test)

# MSEと決定係数を計算する
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```
  
これで決定係数は約97%、MSEは2.23（予測誤差約8%）となります。

| モデル | MSE | 決定係数 |
|-------|-----|----------|
| `DayOfYear` 線形 | 2.77 (17.2%) | 0.07 |
| `DayOfYear` 多項式 | 2.73 (17.0%) | 0.08 |
| `Variety` 線形 | 5.24 (19.7%) | 0.77 |
| 全特徴量 線形 | 2.84 (10.5%) | 0.94 |
| 全特徴量 多項式 | 2.23 (8.25%) | 0.97 |

🏆 お疲れ様でした！このレッスンで4つの回帰モデルを作り、モデル精度を97%まで高めました。回帰の最後のセクションでは、ロジスティック回帰について学びカテゴリ分類を行います。

---
## 🚀チャレンジ

このノートブックで異なる変数をいくつか試し、相関がモデル精度にどう影響するかを調べてみましょう。

## [講義後のクイズ](https://ff-quizzes.netlify.app/en/ml/)

## 復習と自主学習

本レッスンでは線形回帰について学びました。ほかにも重要な回帰手法があります。Stepwise、Ridge、Lasso、Elasticnet などの手法を調べてみましょう。深く学びたい場合は [スタンフォード大学の統計学習コース](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning) が良い教材です。

## 課題

[モデル構築](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責事項**:  
本書類は AI 翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性の向上に努めていますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知おきください。原文の原語版が正式な情報源として優先されます。重要な情報については、専門の人間による翻訳を推奨します。本翻訳の使用により生じた誤解や誤訳について、当方は一切の責任を負いかねます。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->