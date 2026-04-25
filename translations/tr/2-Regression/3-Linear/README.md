# Scikit-learn kullanarak regresyon modeli oluşturma: dört farklı regresyon yöntemi

## Yeni Başlayanlar için Not

Doğrusal regresyon, **sayısal bir değeri** (örneğin, ev fiyatı, sıcaklık veya satışlar) tahmin etmek istediğimizde kullanılır.
Bu yöntemde, giriş özellikleri ile çıktı arasındaki ilişkiyi en iyi temsil eden düz bir çizgi bulunur.

Bu derste, daha ileri regresyon tekniklerini keşfetmeden önce temel kavramı anlamaya odaklanacağız.
![Doğrusal ve polinomsal regresyon infografiği](../../../../translated_images/tr/linear-polynomial.5523c7cb6576ccab.webp)
> İnfografik [Dasani Madipalli](https://twitter.com/dasani_decoded) tarafından
## [Ön-ders sınavı](https://ff-quizzes.netlify.app/en/ml/)

> ### [Bu ders R dilinde de mevcuttur!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Giriş

Şimdiye kadar, balkabağı fiyatlandırma veri setinden toplanan örnek verilerle regresyonun ne olduğu hakkında bilgi edindiniz. Ayrıca Matplotlib kullanarak bunu görselleştirdiniz.

Şimdi Makine Öğrenimi için regresyona daha derinlemesine dalmaya hazırsınız. Görselleştirme, veriyi anlamlandırmanıza olanak sağlarken, Makine Öğrenimi'nin gerçek gücü modellerin _eğitilmesinden_ gelir. Modeller geçmiş verilere göre eğitilir ve veri bağımlılıklarını otomatik olarak yakalar, böylece modelin daha önce görmediği yeni veriler için tahmin yapmanızı sağlar.

Bu derste, _temel doğrusal regresyon_ ve _polinomsal regresyon_ olmak üzere iki regresyon türünü ve bu tekniklerin altında yatan bazı matematikleri öğreneceksiniz. Bu modeller, farklı giriş verilerine bağlı olarak balkabağı fiyatlarını tahmin etmemize olanak sağlayacak.

[![Yeni başlayanlar için ML - Doğrusal Regresyonu Anlamak](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "Yeni başlayanlar için ML - Doğrusal Regresyonu Anlamak")

> 🎥 Doğrusal regresyon hakkında kısa bir video özeti için yukarıdaki resme tıklayın.

> Bu müfredat boyunca, matematik bilgimizin minimum düzeyde olduğunu varsayıyoruz ve bu konuyu diğer alanlardan gelen öğrenciler için erişilebilir kılmaya çalışıyoruz. Bu yüzden anlaşılmayı kolaylaştırmak için notlar, 🧮 açıklamalar, diyagramlar ve diğer öğrenme araçlarına dikkat edin.

### Ön Koşul

Artık incelediğimiz balkabağı verisinin yapısına aşina olmalısınız. Bu dersin _notebook.ipynb_ dosyasında önceden yüklenmiş ve önceden temizlenmiş halde bulunmaktadır. Dosyada balkabağı fiyatı bushel başına yeni bir veri çerçevesinde gösterilmektedir. Bu not defterlerini Visual Studio Code'daki çekirdeklerde çalıştırabildiğinizden emin olun.

### Hazırlık

Hatırlatma olarak, bu verileri sorular sormak için yüklüyorsunuz.

- Balkabaklarını satın almak için en iyi zaman ne zamandır?
- Minyatür balkabaklarından bir kutu için ne kadar fiyat bekleyebilirim?
- Onları yarım bushel sepetlerde mi yoksa 1 1/9 bushel kutularda mı almalıyım?
Veriye daha derinlemesine bakalım.

Önceki derste, Pandas veri çerçevesi oluşturdunuz ve fiyatlandırmayı bushel bazında standartlaştırarak orijinal veri setinin bir kısmını doldurdunuz. Ancak bu şekilde sadece yaklaşık 400 veri noktası toplayabildiniz ve sadece sonbahar aylarına ait veriler oldu.

Bu derse eşlik eden not defterinde önceden yüklenmiş veriye bir göz atın. Veri önceden yüklü ve ay verisini göstermek için ilk bir dağılım grafiği çizildi. Belki veriyi daha da temizleyerek verinin doğası hakkında biraz daha detay alabiliriz.

## Doğrusal regresyon çizgisi

Ders 1'de öğrendiğiniz gibi, doğrusal regresyon egzersizinin amacı bir çizgi çizmek ve:

- **Değişken ilişkilerini göstermek**. Değişkenler arasındaki ilişkiyi göstermek
- **Tahmin yapmak**. Yeni bir veri noktasının o çizgiye göre nerede düşeceğini doğru şekilde tahmin etmek

**En Küçük Kareler Regresyonu** genellikle bu tür bir çizgiyi çizer. "En Küçük Kareler" terimi modelimizdeki toplam hatayı minimize etmeyi ifade eder. Her veri noktası için gerçek nokta ile regresyon çizgisi arasındaki dikey mesafe (kalan) ölçülür.

Bu mesafeleri kareye almamızın iki temel sebebi vardır:

1. **Büyüklük, Yönden Önde:** -5 hatasını +5 hatası ile aynı şekilde ele almak istiyoruz. Karekök alma işlemi tüm değerleri pozitif yapar.

2. **Aykırı Değerleri Cezalandırma:** Karekök alma büyük hatalara daha fazla ağırlık verir ve çizgiyi uzak noktalara daha yakın tutmaya zorlar.

Sonra bu kareleri toplarız. Amaç, toplam karenin en küçük olduğu çizgiyi bulmaktır — bu yüzden adı "En Küçük Kareler"dir.

> **🧮 Matematiği göster** 
> 
> En uygun çizgi (line of best fit) şu [denklemle ifade edilir](https://en.wikipedia.org/wiki/Simple_linear_regression): 
> 
> ```
> Y = a + bX
> ```
>
> `X` 'açıklayıcı değişken'dir. `Y` 'bağımlı değişken'dir. Çizginin eğimi `b` ve `a`, `X = 0` iken `Y` değerini ifade eden y-kesişimidir.
>
>![eğimi hesapla](../../../../translated_images/tr/slope.f3c9d5910ddbfcf9.webp)
>
> Öncelikle eğimi `b` hesaplayın. İnfografik [Jen Looper](https://twitter.com/jenlooper) tarafından
>
> Başka bir deyişle, balkabağı verimizin orijinal sorusu olan: "ay bazında bushel başına balkabağı fiyatını tahmin et" durumunda, `X` fiyatı ifade ederken, `Y` satış ayını temsil eder.
>
>![denklem tamamla](../../../../translated_images/tr/calculation.a209813050a1ddb1.webp)
>
> Y değerini hesaplayın. Yaklaşık 4$ ödüyorsanız, Nisan olmalı! İnfografik [Jen Looper](https://twitter.com/jenlooper) tarafından
>
> Düzgün çizgiyi hesaplayan matematik, eğimi ve aynı zamanda `X = 0` iken `Y`'nin konumunu gösteren y-kesişimini içermektedir.
>
> Bu değerlerin hesaplama yöntemini [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) sitesinde görebilirsiniz. Ayrıca [bu En Küçük Kareler hesaplayıcısını](https://www.mathsisfun.com/data/least-squares-calculator.html) ziyaret ederek sayı değerlerinin çizgiye etkisini izleyebilirsiniz.

## Korelasyon

Bir diğer önemli terim de verilen X ve Y değişkenleri arasındaki **Korelasyon Katsayısıdır**. Bir dağılım grafiği kullanarak bu katsayıyı hızlıca görselleştirebilirsiniz. Veriler düzgün bir çizgi üzerinde ise yüksek korelasyon vardır, ama veriler X ve Y arasında rastgele dağılmışsa korelasyon düşüktür.

İyi bir doğrusal regresyon modeli, En Küçük Kareler Regresyon yöntemi ile çizilmiş regresyon çizgisi kullanarak yüksek (0'a değil, 1'e yakın) bir Korelasyon Katsayısına sahip olandır.

✅ Bu derse eşlik eden not defterini çalıştırın ve Ay ile Fiyat arasındaki dağılım grafiğine bakın. Dağınık grafik yorumu ile balkabağı satışlarında Ay ile Fiyat arasında yüksek mi yoksa düşük mü bir korelasyon görüyorsunuz? Ay yerine *yılın günü* gibi daha ince bir ölçüm kullandığınızda değişir mi?

Aşağıdaki kodda, verinin temizlendiğini ve `new_pumpkins` adında aşağıdakine benzer bir veri çerçevesi elde edildiğini varsayacağız:

ID | Ay | YılınGünü | Çeşit | Şehir | Paket | Düşük Fiyat | Yüksek Fiyat | Fiyat
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | TURTA TİPİ | BALTIMORE | 1 1/9 bushel karton | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | TURTA TİPİ | BALTIMORE | 1 1/9 bushel karton | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | TURTA TİPİ | BALTIMORE | 1 1/9 bushel karton | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | TURTA TİPİ | BALTIMORE | 1 1/9 bushel karton | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | TURTA TİPİ | BALTIMORE | 1 1/9 bushel karton | 15.0 | 15.0 | 13.636364

> Veriyi temizlemek için kullanılan kod [`notebook.ipynb`](notebook.ipynb) dosyasında mevcuttur. Önceki derste yapılan aynı temizleme adımları uygulanmıştır ve `DayOfYear` sütunu aşağıdaki ifade ile hesaplanmıştır: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Doğrusal regresyonun matematiğini anladığınıza göre, hangi balkabağı paketinin en iyi fiyatı sağlayacağını tahmin etmek için bir Regresyon modeli oluşturalım. Tatil balkabağı tarlası için balkabağı alan biri, satın alımlarını optimize edebilmek adına bu bilgiye ihtiyaç duyabilir.

## Korelasyon Arayışı

[![Yeni başlayanlar için ML - Korelasyon Arayışı: Doğrusal Regresyonun Anahtarı](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "Yeni başlayanlar için ML - Korelasyon Arayışı: Doğrusal Regresyonun Anahtarı")

> 🎥 Korelasyon hakkında kısa bir video özeti için yukarıdaki resme tıklayın.

Önceki dersten muhtemelen farklı ayların ortalama fiyatının şöyle göründüğünü gördünüz:

<img alt="Aylara göre ortalama fiyat" src="../../../../translated_images/tr/barchart.a833ea9194346d76.webp" width="50%"/>

Bu, bir miktar korelasyon olduğunu düşündürür ve `Ay` ile `Fiyat` veya `YılınGünü` ile `Fiyat` arasındaki ilişkiyi tahmin etmek için doğrusal regresyon modeli eğitebiliriz. Aşağıda sonuncusu gösteren bir dağılım grafiği bulunmaktadır:

<img alt="Yılın Günü ve Fiyat Dağılım Grafiği" src="../../../../translated_images/tr/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

`corr` fonksiyonunu kullanarak korelasyonu kontrol edelim:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Görüldüğü gibi korelasyon oldukça küçük, `Ay` için -0.15, `YılınGünü` için ise -0.17, fakat başka önemli bir ilişki olabilir. Fiyatların farklı balkabağı çeşitlerine göre kümelendiği görünüyor. Bu hipotezi doğrulamak için, her balkabağı kategorisini farklı renkte gösterelim. `scatter` fonksiyonuna bir `ax` parametresi vererek tüm noktaları aynı grafik üzerinde çizebiliriz:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Yılın Günü ve Fiyat Dağılım Grafiği Renkli" src="../../../../translated_images/tr/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

İncelemenize göre, çeşit genel fiyata satış tarihinden daha fazla etki ediyor. Bir çubuk grafik ile de görebiliriz:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Fiyat ve Çeşit Çubuk Grafiği" src="../../../../translated_images/tr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Şimdi sadece bir balkabağı çeşidi olan 'turta tipi' üzerinde duralım ve tarihin fiyat üzerindeki etkisini görelim:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Yılın Günü ve Fiyat Dağılım Grafiği" src="../../../../translated_images/tr/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Şimdi `Price` ve `DayOfYear` arasındaki korelasyonu `corr` fonksiyonu ile hesaplayalım; yaklaşık `-0.27` alacağız — bu, tahmin modelleri eğitmenin mantıklı olduğunu gösteriyor.

> Doğrusal regresyon modeli eğitmeden önce verimizin temiz olduğundan emin olmak önemlidir. Doğrusal regresyon eksik değerlerle iyi çalışmaz, bu yüzden boş hücreleri temizlemek mantıklıdır:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Başka bir yöntem ise o boş değerleri ilgili sütunun ortalama değerleri ile doldurmaktır.

## Basit Doğrusal Regresyon

[![Yeni başlayanlar için ML - Scikit-learn kullanarak Doğrusal ve Polinomsal Regresyon](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "Yeni başlayanlar için ML - Scikit-learn kullanarak Doğrusal ve Polinomsal Regresyon")

> 🎥 Doğrusal ve polinomsal regresyon hakkında kısa video özeti için yukarıdaki resme tıklayın.

Doğrusal Regresyon modelimizi eğitmek için **Scikit-learn** kütüphanesini kullanacağız.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Giriş değerlerini (özellikleri) ve beklenen çıktıyı (etiket) ayrı numpy dizileri olarak ayırarak başlıyoruz:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Giriş verisini Linear Regression paketinin doğru anlaması için `reshape` işlemi yapmamız gerektiğine dikkat edin. Doğrusal Regresyon, girdi olarak her satırı bir özellik vektörü olan 2D bir dizi bekler. Bizim durumumuzda sadece bir girdi olduğundan, array boyutu N&times;1 (N veri seti büyüklüğü) olmalıdır.

Sonra modeli eğitim ve test verisi olarak bölmemiz gerekmektedir, böylece eğitim sonrası modelimizi doğrulayabiliriz:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Son olarak, gerçek Doğrusal Regresyon modelinin eğitilmesi sadece iki satır kod alır. `LinearRegression` nesnesini tanımlıyoruz ve `fit` metodu ile veriye uyduruyoruz:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`fit` işleminden sonra `LinearRegression` nesnesi regresyonun tüm katsayılarını içerir ve bunlara `.coef_` özelliği aracılığıyla erişilebilir. Bizim durumumuzda, yalnızca bir katsayı vardır ve bu yaklaşık `-0.017` civarında olmalıdır. Bu, fiyatların zamanla biraz düşme eğiliminde olduğunu gösterir, ancak çok fazla değil, günde yaklaşık 2 sent kadar. Regresyonun Y eksenini kestiği noktaya `lin_reg.intercept_` ile erişebiliriz - bizim örneğimizde bu yaklaşık `21` olacak ve yılın başındaki fiyatı gösterir.

Modelimizin ne kadar doğru olduğunu görmek için test veri seti üzerinde fiyatları tahmin edebilir ve ardından tahminlerimizin beklenen değerlere ne kadar yakın olduğunu ölçebiliriz. Bu, beklenen ve tahmin edilen değerler arasındaki tüm kare farkların ortalamasının karekökü olan kök ortalama kare hata (RMSE) metriği kullanılarak yapılabilir.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Hatalarımız yaklaşık 2 puan civarında görünüyor, bu da yaklaşık %17. Çok iyi değil. Model kalitesinin diğer bir göstergesi **belirleme katsayısı**dır ve şöyle elde edilir:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```

Eğer değer 0 ise, model giriş verilerini hesaba katmaz ve *en kötü doğrusal tahminci* gibi davranır ki bu sadece sonucun ortalamasıdır. Değer 1 olursa, tüm beklenen çıktıları mükemmel şekilde tahmin edebiliriz. Bizim durumumuzda, katsayı yaklaşık 0.06 civarında, yani oldukça düşük.

Regresyonun nasıl çalıştığını daha iyi görmek için test verilerini regresyon çizgisiyle birlikte de çizebiliriz:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/tr/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polinom Regresyonu

Doğrusal regresyonun bir başka türü Polinom Regresyonudur. Bazen değişkenler arasında doğrusal bir ilişki vardır - hacmi ne kadar büyükse balkabağının fiyatı o kadar yüksek olur - bazen bu ilişkiler düz bir çizgi ya da düzlem olarak çizilemez.

✅ İşte Polinom Regresyon kullanılabilecek [başka örnekler](https://online.stat.psu.edu/stat501/lesson/9/9.8)

Date ve Price arasındaki ilişkiye bir kez daha bakın. Bu saçılım grafiği mutlaka bir doğruyla mı analiz edilmeli gibi görünüyor? Fiyatlar dalgalanamaz mı? Bu durumda polinom regresyonu deneyebilirsiniz.

✅ Polinomlar bir veya daha fazla değişken ve katsayı içerebilen matematiksel ifadelerden oluşur.

Polinom regresyon, doğrusal olmayan verilere daha iyi uyması için eğri bir çizgi oluşturur. Bizim durumumuzda, giriş verisine karesel `DayOfYear` değişkenini dahil edersek, verimizi yıl içinde belirli bir noktada minimuma sahip parabolik bir eğriyle uyarlayabiliriz.

Scikit-learn, veri işleme adımlarını birleştirmek için faydalı bir [pipeline API'si](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) içerir. Bir **pipeline** bir dizi **estimator**dir. Bizim durumumuzda önce modele polinom özellikler ekleyen, ardından regresyon eğiten bir pipeline oluşturacağız:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

`PolynomialFeatures(2)` kullanmak, giriş verisindeki tüm ikinci dereceden polinomları dahil edeceğimiz anlamına gelir. Bizim durumumuzda bu sadece `DayOfYear`<sup>2</sup> anlamına gelir, ancak örneğin iki değişken olan X ve Y için bu X<sup>2</sup>, XY ve Y<sup>2</sup> ekler. İsterseniz daha yüksek dereceli polinomlar da kullanabilirsiniz.

Pipelinelar, orijinal `LinearRegression` nesnesi ile aynı şekilde kullanılabilir, yani pipeline üzerinde `fit` yapabilir ve sonra `predict` ile tahmin sonuçları alabilirsiniz. İşte test verileri ve yaklaşık eğriyi gösteren grafik:

<img alt="Polynomial regression" src="../../../../translated_images/tr/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polinom Regresyon kullanarak MSE'yi biraz daha düşürebilir ve belirleme katsayısını biraz daha yükseltebiliriz, ama çok değil. Diğer özellikleri de hesaba katmamız gerekiyor!

> Kabak fiyatlarının en düşük olduğu yerin Cadılar Bayramı civarı olduğunu görebilirsiniz. Bunu nasıl açıklarsınız?

🎃 Tebrikler, kabak fiyatını tahmin etmeye yardımcı olabilecek bir model yarattınız. Muhtemelen aynı prosedürü tüm kabak çeşitleri için tekrarlayabilirsiniz, ama bu zahmetli olur. Şimdi modelimizde kabak çeşidini nasıl dikkate alacağımızı öğrenelim!

## Kategorik Özellikler

İdeal dünyada, farklı kabak çeşitlerinin fiyatlarını aynı modelle tahmin etmek isteriz. Ancak `Variety` sütunu, `Month` gibi sütunlardan biraz farklıdır çünkü sayısal olmayan değerler içerir. Bu tür sütunlara **kategorik** denir.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Kategorik özelliklerin kullanımına kısa video özetini izlemek için yukarıdaki görsele tıklayın.

Burada ortalama fiyatın çeşide nasıl bağlı olduğunu görebilirsiniz:

<img alt="Average price by variety" src="../../../../translated_images/tr/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Çeşidi dikkate almak için önce onu sayısal forma dönüştürmemiz veya **kodlamamız** gerekir. Bunu yapmanın birkaç yolu vardır:

* Basit **sayısal kodlama** farklı çeşitlerin bir tablosunu oluşturur ve ardından çeşit adını o tablodaki bir indeks ile değiştirir. Bu doğrusal regresyon için en iyi fikir değildir çünkü doğrusal regresyon indeksin gerçek sayısal değerini alır ve sonucu buna göre katsayı ile çarpar. Bizim durumumuzda, indeks numarası ile fiyat arasındaki ilişki açıkça doğrusal değildir, indekslerin belirli bir şekilde sıralandığını varsaysak bile.
* **One-hot kodlama** `Variety` sütununu dört farklı sütunla değiştirir, her biri bir çeşit içindir. Her sütun karşılık gelen satır o çeşide aitse `1`, değilse `0` içerir. Bu, doğrusal regresyonda dört katsayı olacağı anlamına gelir; her kabak çeşidi için biri, o çeşidin "başlangıç fiyatı" (veya "ek fiyat") sorumlusudur.

Aşağıdaki kod kabak çeşidini one-hot kodlama ile nasıl yapabileceğimizi gösterir:

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

One-hot kodlu çeşidi giriş olarak kullanarak doğrusal regresyon eğitmek için sadece `X` ve `y` verilerini doğru başlatmamız gerekir:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Kalan kod, yukarıda doğrusal regresyon eğitmek için kullandığımız ile aynıdır. Denerseniz, ortalama kare hata yaklaşık aynı kalır ama belirleme katsayısı çok daha yüksek olur (~%77). Daha doğru tahminler almak için, daha fazla kategorik özellik ile birlikte `Month` veya `DayOfYear` gibi sayısal özellikleri de dikkate alabiliriz. Tüm özellikleri birleştirmek için `join` kullanılabilir:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Burada ayrıca `City` ve `Package` türü de dikkate alınır, bu da MSE'yi 2.84 (%10) ve belirleme katsayısını 0.94 yapar!

## Hepsini Bir Araya Getirmek

En iyi modeli oluşturmak için, yukarıdaki örnekteki birleşik (one-hot kodlu kategorik + sayısal) verileri Polinom Regresyon ile birlikte kullanabiliriz. İşte kolayınız için tam kod:

```python
# eğitim verilerini ayarla
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# eğitim-test bölünmesi yap
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# işlem hattını kur ve eğit
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# test verisi için sonuçları tahmin et
pred = pipeline.predict(X_test)

# MSE ve kararlılığı hesapla
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Bu, bize neredeyse %97 belirleme katsayısı ve MSE=2.23 (~%8 tahmin hatası) verecektir.

| Model | MSE | Belirleme |
|-------|-----|---------------|
| `DayOfYear` Doğrusal | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polinom | 2.73 (17.0%) | 0.08 |
| `Variety` Doğrusal | 5.24 (19.7%) | 0.77 |
| Tüm özellikler Doğrusal | 2.84 (10.5%) | 0.94 |
| Tüm özellikler Polinom | 2.23 (8.25%) | 0.97 |

🏆 Aferin! Bir derste dört regresyon modeli yarattınız ve model kalitesini %97’ye kadar yükselttiniz. Regresyonun son bölümünde kategorileri belirlemek için Lojistik Regresyondan bahsedeceğiz.

---
## 🚀Meydan Okuma

Bu not defterinde çeşitli değişkenlerle deney yaparak korelasyonun model doğruluğuna nasıl karşılık geldiğini görün.

## [Ders sonrası sınav](https://ff-quizzes.netlify.app/en/ml/)

## Tekrar & Kendi Kendine Çalışma

Bu derste Doğrusal Regresyonu öğrendik. Başka önemli regresyon türleri de vardır. Stepwise, Ridge, Lasso ve Elasticnet teknikleri hakkında okuyun. Daha fazla öğrenmek için iyi bir kurs [Stanford İstatistiksel Öğrenme kursu](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning).

## Ödev

[Model Oluştur](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Feragatnamesi**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba sarf etsek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayınız. Orijinal belge, kendi yerel dilinde yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımı sonucu oluşabilecek herhangi bir yanlış anlama veya yanlış yorumdan sorumlu değiliz.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->