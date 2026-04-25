# Membina model regresi menggunakan Scikit-learn: regresi empat cara

## Nota Pemula

Regresi linear digunakan apabila kita ingin meramalkan **nilai berangka** (contohnya, harga rumah, suhu, atau jualan).
Ia berfungsi dengan mencari satu garis lurus yang paling mewakili hubungan antara ciri input dan output.

Dalam pelajaran ini, kita memberi tumpuan kepada memahami konsep terlebih dahulu sebelum meneroka teknik regresi yang lebih maju.
![Linear vs polynomial regression infographic](../../../../translated_images/ms/linear-polynomial.5523c7cb6576ccab.webp)
> Infografik oleh [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Kuiz pra-ceramah](https://ff-quizzes.netlify.app/en/ml/)

> ### [Pelajaran ini tersedia dalam R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Pengenalan

Sejauh ini anda telah meneroka apa itu regresi dengan data contoh yang dikumpulkan daripada set data harga labu yang akan kita gunakan sepanjang pelajaran ini. Anda juga telah memvisualisasikannya menggunakan Matplotlib.

Kini anda bersedia untuk menyelami lebih lanjut tentang regresi untuk ML. Walaupun visualisasi membolehkan anda memahami data, kuasa sebenar Pembelajaran Mesin datang daripada _melatih model_. Model dilatih menggunakan data sejarah untuk secara automatik menangkap kebergantungan data, dan membolehkan anda meramalkan keputusan untuk data baru, yang belum pernah dilihat oleh model.

Dalam pelajaran ini, anda akan mempelajari lebih lanjut tentang dua jenis regresi: _regresi linear asas_ dan _regresi polinomial_, bersama dengan beberapa matematik asas yang mendasari teknik-teknik ini. Model-model tersebut akan membolehkan kita meramalkan harga labu bergantung pada data input yang berbeza.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klik imej di atas untuk video ringkas gambaran keseluruhan regresi linear.

> Sepanjang kurikulum ini, kami menganggap pengetahuan matematik adalah minimum, dan berusaha menjadikannya mudah diakses bagi pelajar yang datang dari bidang lain, jadi perhatikan nota, 🧮 panggilan keluar, rajah, dan alat pembelajaran lain untuk membantu pemahaman.

### Prasyarat

Anda kini sepatutnya sudah biasa dengan struktur data labu yang kita periksa. Anda boleh menjumpainya sudah dimuatkan dan dibersihkan dalam fail _notebook.ipynb_ pelajaran ini. Dalam fail tersebut, harga labu dipaparkan setiap bushel dalam bingkai data baru. Pastikan anda boleh menjalankan notebook ini dalam kernel di Visual Studio Code.

### Persediaan

Sebagai peringatan, anda memuatkan data ini supaya boleh bertanya soalan mengenainya.

- Bila masa terbaik untuk membeli labu?
- Berapakah harga yang boleh saya jangkakan untuk satu kotak labu mini?
- Perlukah saya membelinya dalam bakul separuh bushel atau dalam kotak 1 1/9 bushel?
Mari terus gali data ini.

Dalam pelajaran sebelum ini, anda telah mencipta bingkai data Pandas dan mengisinya dengan sebahagian daripada set data asal, menstandardkan harga mengikut bushel. Dengan melakukan itu, walau bagaimanapun, anda hanya dapat mengumpul kira-kira 400 titik data dan hanya untuk bulan musim luruh.

Lihat data yang telah kami pra-muatkan di notebook yang disertakan dalam pelajaran ini. Data dipra-muat dan plot taburan awal telah dilakar untuk menunjukkan data bulan. Mungkin kita boleh dapatkan lebih banyak maklumat tentang sifat data dengan membersihkannya dengan lebih lanjut.

## Garis regresi linear

Seperti yang anda pelajari dalam Pelajaran 1, tujuan latihan regresi linear adalah untuk dapat melakar garis yang:

- **Menunjukkan hubungan pemboleh ubah**. Menunjukkan hubungan antara pemboleh ubah
- **Membuat ramalan**. Membuat ramalan tepat mengenai di mana titik data baru akan jatuh berbanding garis tersebut.

Biasanya, **Regresi Kuasa Dua Terkecil (Least-Squares Regression)** digunakan untuk melukis jenis garis ini. Istilah "Kuasa Dua Terkecil" merujuk kepada proses meminimumkan jumlah ralat dalam model kita. Untuk setiap titik data, kita mengukur jarak menegak (dipanggil residual) antara titik sebenar dan garis regresi kita.

Kita kuasakan kuadrat jarak ini atas dua sebab utama:

1. **Magnitud melebihi Arah:** Kita mahu memperlakukan ralat -5 sama seperti ralat +5. Menguaskan kuadrat menjadikan semua nilai positif.

2. **Menghukum Titik Luar Normal (Outliers):** Menguasakan kuadrat memberi lebih berat kepada ralat yang lebih besar, memaksa garis kekal lebih dekat dengan titik yang jauh.

Kemudian kita menjumlahkan semua nilai kuasa dua ini. Matlamat kita adalah untuk mencari garis tertentu di mana jumlah akhir ini adalah paling kecil (nilai terkecil yang mungkin)—justeru nama "Kuasa Dua Terkecil".

> **🧮 Tunjukkan saya matematiknya**  
>  
> Garis ini, dipanggil _garis kesesuaian terbaik_ boleh dinyatakan melalui [persamaan](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` adalah 'pemboleh ubah penerang'. `Y` adalah 'pemboleh ubah bergantung'. Kecerunan garis ialah `b` dan `a` adalah pintasan-y, yang merujuk kepada nilai `Y` apabila `X = 0`.  
>  
>![kira kecerunan](../../../../translated_images/ms/slope.f3c9d5910ddbfcf9.webp)  
>  
> Pertama, kira kecerunan `b`. Infografik oleh [Jen Looper](https://twitter.com/jenlooper)  
>  
> Dengan kata lain, dan merujuk kepada soalan asal data labu kita: "meramalkan harga labu setiap bushel mengikut bulan", `X` merujuk kepada harga dan `Y` merujuk kepada bulan jualan.  
>  
>![lengkapkan persamaan](../../../../translated_images/ms/calculation.a209813050a1ddb1.webp)  
>  
> Kira nilai Y. Jika anda membayar sekitar $4, sudah pasti April! Infografik oleh [Jen Looper](https://twitter.com/jenlooper)  
>  
> Matematik yang mengira garis itu mesti menunjukkan kecerunan garis, yang juga bergantung pada pintasan, atau di mana `Y` berada apabila `X = 0`.  
>  
> Anda boleh melihat kaedah pengiraan untuk nilai-nilai ini di laman web [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Lawati juga [kalkulator Least-squares](https://www.mathsisfun.com/data/least-squares-calculator.html) untuk lihat bagaimana nilai nombor mempengaruhi garis.

## Korelasi

Satu lagi istilah untuk difahami ialah **Pekali Korelasi** antara pemboleh ubah X dan Y yang diberi. Dengan menggunakan scatterplot, anda boleh dengan cepat memvisualisasikan pekali ini. Plot dengan titik data bertaburan dalam garis yang kemas mempunyai korelasi tinggi, tetapi plot dengan titik data bertaburan di mana-mana antara X dan Y mempunyai korelasi rendah.

Model regresi linear yang baik adalah yang mempunyai Pekali Korelasi tinggi (lebih hampir kepada 1 berbanding 0) menggunakan kaedah Regresi Kuasa Dua Terkecil dengan garis regresi.

✅ Jalankan notebook yang disertakan dalam pelajaran ini dan lihat scatterplot Bulan ke Harga. Adakah data yang mengaitkan Bulan dengan Harga untuk jualan labu nampaknya mempunyai korelasi tinggi atau rendah, menurut tafsiran visual anda terhadap scatterplot? Adakah ia berubah jika anda menggunakan ukuran yang lebih terperinci sebagai ganti `Month`, contohnya *hari dalam setahun* (iaitu bilangan hari sejak awal tahun)?

Dalam kod di bawah, kita akan menganggap bahawa kita telah membersihkan data, dan memperoleh bingkai data bernama `new_pumpkins`, serupa dengan yang berikut:

ID | Bulan | DayOfYear | Jenis | Bandar | Pembungkusan | Harga Rendah | Harga Tinggi | Harga
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | JENIS PIE | BALTIMORE | kotak 1 1/9 bushel | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | JENIS PIE | BALTIMORE | kotak 1 1/9 bushel | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | JENIS PIE | BALTIMORE | kotak 1 1/9 bushel | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | JENIS PIE | BALTIMORE | kotak 1 1/9 bushel | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | JENIS PIE | BALTIMORE | kotak 1 1/9 bushel | 15.0 | 15.0 | 13.636364

> Kod untuk membersihkan data tersedia dalam [`notebook.ipynb`](notebook.ipynb). Kami telah melaksanakan langkah pembersihan yang sama seperti dalam pelajaran sebelumnya, dan telah mengira lajur `DayOfYear` menggunakan ungkapan berikut:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Sekarang anda sudah faham matematik di belakang regresi linear, mari bina model Regresi untuk melihat sama ada kita boleh meramalkan pakej labu mana yang akan mempunyai harga labu terbaik. Seseorang yang membeli labu untuk tapak labu perayaan mungkin mahukan maklumat ini untuk mengoptimumkan pembelian pakej labu mereka untuk tapak tersebut.

## Mencari Korelasi

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klik imej di atas untuk video ringkas gambaran keseluruhan korelasi.

Daripada pelajaran sebelumnya anda mungkin telah melihat bahawa harga purata untuk bulan yang berbeza kelihatan seperti ini:

<img alt="Average price by month" src="../../../../translated_images/ms/barchart.a833ea9194346d76.webp" width="50%"/>

Ini mencadangkan bahawa wujud beberapa korelasi, dan kita boleh cuba melatih model regresi linear untuk meramalkan hubungan antara `Month` dan `Price`, atau antara `DayOfYear` dan `Price`. Berikut ialah plot taburan yang menunjukkan hubungan kedua:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ms/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Mari lihat sama ada terdapat korelasi menggunakan fungsi `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Nampaknya korelasinya agak kecil, -0.15 mengikut `Month` dan -0.17 mengikut `DayOfMonth`, tetapi mungkin ada hubungan penting lain. Nampaknya terdapat kluster harga yang berbeza berhubung dengan varieti labu yang berbeza. Untuk mengesahkan hipotesis ini, mari plot setiap kategori labu menggunakan warna yang berbeza. Dengan memberikan parameter `ax` kepada fungsi plot `scatter` kita boleh plot semua titik pada graf yang sama:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ms/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Siasatan kami mencadangkan bahawa varieti mempunyai kesan lebih ke atas harga keseluruhan berbanding tarikh jualan sebenar. Kita boleh lihat ini dengan graf bar:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/ms/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Marilah kita fokus buat masa ini hanya pada satu varieti labu, iaitu 'jenis pai', dan lihat kesan tarikh ke atas harga:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ms/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Jika kita kira korelasi antara `Price` dan `DayOfYear` menggunakan fungsi `corr`, kita akan mendapat nilai sekitar `-0.27` - yang bermakna melatih model ramalan adalah wajar.

> Sebelum melatih model regresi linear, adalah penting untuk memastikan data kita bersih. Regresi linear tidak berfungsi dengan baik dengan nilai kosong, maka adalah wajar untuk membuang semua sel kosong:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Pendekatan lain ialah mengisi nilai kosong tersebut dengan nilai purata daripada lajur berkenaan.

## Regresi Linear Mudah

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klik imej di atas untuk video ringkas gambaran keseluruhan regresi linear dan polinomial.

Untuk melatih model Regresi Linear kita, kita akan menggunakan perpustakaan **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Kita mulakan dengan memisahkan nilai input (ciri) dan output yang dijangka (label) ke dalam array numpy yang berasingan:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Perhatikan bahawa kita perlu melakukan `reshape` ke atas data input supaya pakej Regresi Linear memahaminya dengan betul. Regresi Linear menjangka input dalam bentuk array 2D, di mana setiap baris array mewakili vektor ciri input. Dalam kes kita, kerana kita hanya ada satu input - kita perlukan array berbentuk N&times;1, di mana N adalah saiz dataset.

Kemudian, kita perlu membahagikan data kepada dataset latihan dan ujian, supaya kita boleh mengesahkan model kita selepas latihan:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Akhir sekali, melatih model Regresi Linear sebenar hanya mengambil dua baris kod. Kita mentakrif objek `LinearRegression`, dan melatihnya pada data kita menggunakan kaedah `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objek `LinearRegression` selepas `fit`-ting mengandungi semua koefisien regresi, yang boleh diakses menggunakan sifat `.coef_`. Dalam kes kami, terdapat hanya satu koefisien, yang sepatutnya sekitar `-0.017`. Ini bermakna harga kelihatan turun sedikit dengan masa, tetapi tidak terlalu banyak, sekitar 2 sen sehari. Kita juga boleh mengakses titik persilangan regresi dengan paksi Y menggunakan `lin_reg.intercept_` - ia akan sekitar `21` dalam kes kami, menunjukkan harga pada permulaan tahun.

Untuk melihat sejauh mana ketepatan model kami, kita boleh meramalkan harga pada set data ujian, dan kemudian mengukur sejauh mana ramalan kami dekat dengan nilai yang dijangkakan. Ini boleh dilakukan menggunakan metrik galat kuasa dua purata punca (RMSE), iaitu punca bagi purata semua perbezaan kuasa dua antara nilai yang dijangkakan dan diramalkan.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Galat kami kelihatan sekitar 2 mata, iaitu ~17%. Tidak terlalu baik. Penunjuk lain bagi kualiti model ialah **koefisien penentuan**, yang boleh diperoleh seperti berikut:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Jika nilai adalah 0, ini bermakna model tidak mengambil kira data input, dan berfungsi sebagai *peramal linear yang paling teruk*, iaitu nilai purata hasil sahaja. Nilai 1 bermakna kita boleh meramalkan semua output yang dijangkakan dengan sempurna. Dalam kes kami, koefisien adalah sekitar 0.06, yang agak rendah.

Kita juga boleh plot data ujian bersama dengan garis regresi untuk melihat dengan lebih baik bagaimana regresi berfungsi dalam kes kami:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/ms/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regresi Polinomial

Satu lagi jenis Regresi Linear ialah Regresi Polinomial. Walaupun kadang-kadang terdapat hubungan linear antara pembolehubah - semakin besar labu dari segi isi padu, semakin tinggi harga - kadang-kadang hubungan ini tidak boleh digambarkan sebagai satah atau garis lurus.

✅ Berikut adalah [beberapa contoh lagi](https://online.stat.psu.edu/stat501/lesson/9/9.8) data yang boleh menggunakan Regresi Polinomial

Lihat sekali lagi hubungan antara Tarikh dan Harga. Adakah plot taburan ini semestinya perlu dianalisis menggunakan garis lurus? Bukankah harga boleh berubah-ubah? Dalam kes ini, anda boleh cuba regresi polinomial.

✅ Polinomial adalah ekspresi matematik yang mungkin terdiri daripada satu atau lebih pembolehubah dan koefisien

Regresi polinomial menghasilkan garis melengkung untuk menyesuaikan data bukan linear dengan lebih baik. Dalam kes kami, jika kami memasukkan pembolehubah kuasa dua `DayOfYear` ke dalam data input, kami sepatutnya dapat menyesuaikan data kami dengan lengkung parabola, yang akan mempunyai nilai minimum pada suatu titik dalam tahun.

Scikit-learn termasuk API [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) yang berguna untuk menggabungkan langkah-langkah pemprosesan data yang berbeza bersama-sama. Sebuah **pipeline** adalah rantai **penganggar**. Dalam kes kami, kami akan membuat pipeline yang pertama menambah ciri polinomial ke model kami, kemudian melatih regresi:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Menggunakan `PolynomialFeatures(2)` bermakna kami akan memasukkan semua polinomial darjah kedua dari data input. Dalam kes kami ia hanya bermaksud `DayOfYear`<sup>2</sup>, tetapi jika diberikan dua pembolehubah input X dan Y, ini akan menambah X<sup>2</sup>, XY dan Y<sup>2</sup>. Kami juga boleh menggunakan polinomial darjah lebih tinggi jika mahu.

Pipeline boleh digunakan dengan cara yang sama seperti objek `LinearRegression` asal, iaitu kami boleh `fit` pipeline, dan kemudian menggunakan `predict` untuk mendapatkan hasil ramalan. Berikut adalah graf yang menunjukkan data ujian dan lengkung anggaran:

<img alt="Polynomial regression" src="../../../../translated_images/ms/poly-results.ee587348f0f1f60b.webp" width="50%" />

Dengan menggunakan Regresi Polinomial, kami boleh mendapatkan MSE yang sedikit lebih rendah dan koefisien penentuan yang lebih tinggi, tetapi tidak secara signifikan. Kami perlu mengambil kira ciri-ciri lain!

> Anda boleh melihat bahawa harga labu minima diperhatikan sekitar Halloween. Bagaimana anda boleh menerangkannya?

🎃 Tahniah, anda baru sahaja mencipta model yang boleh membantu meramalkan harga labu pai. Anda mungkin boleh mengulangi prosedur yang sama untuk semua jenis labu, tetapi itu akan memenatkan. Mari kita pelajari sekarang cara mengambil kira varieti labu dalam model kita!

## Ciri Kategori

Dalam dunia ideal, kami mahu dapat meramalkan harga untuk varieti labu yang berbeza menggunakan model yang sama. Namun, lajur `Variety` agak berbeza daripada lajur seperti `Month`, kerana ia mengandungi nilai bukan angka. Lajur sebegini dipanggil **kategori**.

[![ML untuk pemula - Ramalan Ciri Kategori dengan Regresi Linear](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML untuk pemula - Ramalan Ciri Kategori dengan Regresi Linear")

> 🎥 Klik imej di atas untuk video ringkas mengenai penggunaan ciri kategori.

Di sini anda boleh lihat bagaimana harga purata bergantung pada varieti:

<img alt="Average price by variety" src="../../../../translated_images/ms/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Untuk mengambil kira varieti, pertama kita perlu menukarnya ke bentuk nombor, atau **mengekod**nya. Terdapat beberapa cara kita boleh lakukannya:

* Pengekodan **nombor mudah** akan membina jadual varieti yang berbeza, kemudian menggantikan nama varieti dengan indeks dalam jadual tersebut. Ini bukan idea terbaik untuk regresi linear, kerana regresi linear mengambil nilai nombor sebenar indeks, dan menambahkannya ke hasil, dengan darab koefisien tertentu. Dalam kes kami, hubungan antara nombor indeks dan harga jelas bukan linear, walaupun jika kami memastikan indeks disusun dalam cara tertentu.
* **Pengekodan one-hot** akan menggantikan lajur `Variety` dengan 4 lajur berbeza, satu untuk setiap varieti. Setiap lajur akan mengandungi `1` jika baris berkenaan adalah varieti tertentu, dan `0` jika tidak. Ini bermakna ada empat koefisien dalam regresi linear, satu untuk setiap varieti labu, yang bertanggungjawab untuk "harga permulaan" (atau lebih tepat "harga tambahan") bagi varieti berkenaan.

Kod di bawah menunjukkan bagaimana kita boleh mengekod varieti secara one-hot:

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

Untuk melatih regresi linear menggunakan varieti yang telah dienkod one-hot sebagai input, kita hanya perlu inisialisasi data `X` dan `y` dengan betul:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Selepas itu, kod adalah sama seperti yang kami gunakan sebelum ini untuk melatih Regresi Linear. Jika anda mencubanya, anda akan lihat galat kuasa dua purata hampir sama, tetapi koefisien penentuan jauh lebih tinggi (~77%). Untuk mendapatkan ramalan yang lebih tepat, kita boleh mengambil lebih banyak ciri kategori serta ciri numerik, seperti `Month` atau `DayOfYear`. Untuk mendapatkan satu tatasusunan besar ciri, kita boleh menggunakan `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Di sini kami juga mengambil kira `City` dan jenis `Package`, yang menghasilkan MSE 2.84 (10%), dan penentuan 0.94!

## Menggabungkan semuanya

Untuk membuat model terbaik, kita boleh menggunakan data gabungan (kategori yang dienkod one-hot + numerik) dari contoh di atas bersama Regresi Polinomial. Berikut adalah kod lengkap untuk kemudahan anda:

```python
# sediakan data latihan
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# buat pembahagian latih-uji
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# sediakan dan latih saluran paip
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# ramalan keputusan untuk data ujian
pred = pipeline.predict(X_test)

# kira MSE dan penentuan
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Ini sepatutnya memberikan koefisien penentuan terbaik hampir 97%, dan MSE=2.23 (~8% galat ramalan).

| Model | MSE | Penentuan |
|-------|-----|-----------|
| Linear `DayOfYear` | 2.77 (17.2%) | 0.07 |
| Polinomial `DayOfYear` | 2.73 (17.0%) | 0.08 |
| Linear `Variety` | 5.24 (19.7%) | 0.77 |
| Linear Semua ciri | 2.84 (10.5%) | 0.94 |
| Polinomial Semua ciri | 2.23 (8.25%) | 0.97 |

🏆 Tahniah! Anda telah mencipta empat model Regresi dalam satu pelajaran, dan meningkatkan kualiti model kepada 97%. Dalam bahagian akhir mengenai Regresi, anda akan belajar mengenai Regresi Logistik untuk menentukan kategori.

---
## 🚀Cabaran

Uji beberapa pembolehubah berbeza dalam buku nota ini untuk melihat bagaimana korelasi berkaitan dengan ketepatan model.

## [Kuiz selepas kuliah](https://ff-quizzes.netlify.app/en/ml/)

## Ulasan & Belajar Sendiri

Dalam pelajaran ini kita belajar tentang Regresi Linear. Terdapat jenis Regresi penting lain. Baca tentang teknik Stepwise, Ridge, Lasso dan Elasticnet. Kursus yang baik untuk dipelajari ialah [Kursus Pembelajaran Statistik Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tugasan 

[Membina Model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Walaupun kami berusaha untuk ketepatan, sila maklum bahawa terjemahan automatik mungkin mengandungi ralat atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang sahih. Untuk maklumat penting, terjemahan manusia profesional adalah disyorkan. Kami tidak bertanggungjawab atas sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->