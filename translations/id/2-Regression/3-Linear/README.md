# Bangun model regresi menggunakan Scikit-learn: regresi dengan empat cara

## Catatan Pemula

Regresi linier digunakan ketika kita ingin memprediksi **nilai numerik** (misalnya, harga rumah, suhu, atau penjualan).  
Ini bekerja dengan menemukan garis lurus yang paling mewakili hubungan antara fitur input dan output.

Dalam pelajaran ini, kita fokus pada pemahaman konsep sebelum mengeksplorasi teknik regresi yang lebih maju.  
![Linear vs polynomial regression infographic](../../../../translated_images/id/linear-polynomial.5523c7cb6576ccab.webp)  
> Infografis oleh [Dasani Madipalli](https://twitter.com/dasani_decoded)

## [Kuis Pra-lecture](https://ff-quizzes.netlify.app/en/ml/)

> ### [Pelajaran ini tersedia dalam R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)

### Pendahuluan

Sejauh ini Anda telah mengeksplorasi apa itu regresi dengan data contoh yang dikumpulkan dari dataset harga labu yang akan kita gunakan sepanjang pelajaran ini. Anda juga telah memvisualisasikannya menggunakan Matplotlib.

Sekarang Anda siap untuk menggali lebih dalam regresi untuk ML. Sementara visualisasi memungkinkan Anda memahami data, kekuatan sesungguhnya dari Pembelajaran Mesin datang dari _melatih model_. Model dilatih dengan data historis untuk secara otomatis menangkap ketergantungan data, dan memungkinkan Anda memprediksi hasil untuk data baru, yang belum pernah dilihat model sebelumnya.

Dalam pelajaran ini, Anda akan belajar lebih banyak tentang dua jenis regresi: _regresi linier dasar_ dan _regresi polinomial_, bersama dengan beberapa matematika dasar di balik teknik ini. Model-model itu akan memungkinkan kita memprediksi harga labu tergantung pada data input yang berbeda.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Klik gambar di atas untuk video singkat tentang regresi linier.

> Sepanjang kurikulum ini, kami mengasumsikan pengetahuan matematika yang minimal, dan berusaha agar dapat diakses oleh siswa dari bidang lain, jadi perhatikan catatan, panggilan 🧮, diagram, dan alat pembelajaran lainnya untuk membantu pemahaman.

### Prasyarat

Anda seharusnya sudah familiar dengan struktur data labu yang sedang kita periksa. Anda dapat menemukannya sudah dimuat dan dibersihkan dalam berkas _notebook.ipynb_ pelajaran ini. Dalam berkas tersebut, harga labu ditampilkan per bushel dalam frame data baru. Pastikan Anda dapat menjalankan notebook ini di kernel Visual Studio Code.

### Persiapan

Sebagai pengingat, Anda memuat data ini agar dapat mengajukan pertanyaan tentangnya.

- Kapan waktu terbaik membeli labu?  
- Harga berapa yang bisa saya harapkan untuk satu kotak labu mini?  
- Haruskah saya membelinya dalam keranjang setengah bushel atau dalam kotak 1 1/9 bushel?  
Mari terus gali data ini.

Dalam pelajaran sebelumnya, Anda membuat data frame Pandas dan mengisinya dengan sebagian data asli, menstandarkan harga berdasarkan bushel. Namun dengan cara itu, Anda hanya mengumpulkan sekitar 400 datapoint dan hanya untuk bulan-bulan musim gugur.

Lihatlah data yang sudah kami muat dalam notebook pendamping pelajaran ini. Data dimuat dan scatterplot awal dibuat untuk menunjukkan data bulan. Mungkin kita bisa mendapatkan detail lebih tentang sifat data ini dengan membersihkannya lebih lanjut.

## Garis regresi linier

Seperti yang Anda pelajari di Pelajaran 1, tujuan latihan regresi linier adalah untuk dapat membuat garis yang:

- **Menunjukkan hubungan variabel**. Menunjukkan hubungan antar variabel  
- **Membuat prediksi**. Membuat prediksi yang akurat tentang di mana titik data baru akan jatuh terkait garis tersebut.

Biasanya, **Least-Squares Regression** digunakan untuk menggambar garis jenis ini. Istilah "Least-Squares" mengacu pada proses meminimalkan total kesalahan dalam model kita. Untuk setiap titik data, kita mengukur jarak vertikal (disebut residual) antara titik aktual dan garis regresi kita.

Jarak-jarak ini kita kuadratkan karena dua alasan utama:

1. **Magnitudo lebih penting dari Arah:** Kita ingin menganggap kesalahan -5 sama dengan kesalahan +5. Mengkuadratkan membuat semua nilai menjadi positif.

2. **Memberi Bobot pada Outlier:** Kuadrat memberi bobot lebih besar pada kesalahan yang lebih besar, memaksa garis untuk tetap dekat dengan titik yang jauh.

Kemudian kita jumlahkan semua nilai kuadrat ini. Tujuan kita adalah menemukan garis spesifik di mana jumlah akhir ini paling kecil (nilai terkecil mungkin)—maka namanya "Least-Squares".

> **🧮 Tunjukkan matematikanya**  
>  
> Garis ini, disebut _line of best fit_ dapat dinyatakan dengan [persamaan](https://en.wikipedia.org/wiki/Simple_linear_regression):  
>  
> ```
> Y = a + bX
> ```
>  
> `X` adalah 'variabel penjelas'. `Y` adalah 'variabel dependen'. Kemiringan garis adalah `b` dan `a` adalah intercept-y, yang merujuk pada nilai `Y` ketika `X = 0`.  
>  
>![hitung kemiringan](../../../../translated_images/id/slope.f3c9d5910ddbfcf9.webp)  
>  
> Pertama, hitung kemiringan `b`. Infografis oleh [Jen Looper](https://twitter.com/jenlooper)  
>  
> Dengan kata lain, dan mengacu pada pertanyaan asli data labu kita: "memprediksi harga labu per bushel berdasarkan bulan", `X` akan merujuk pada harga dan `Y` merujuk pada bulan penjualan.  
>  
>![lengkapi persamaan](../../../../translated_images/id/calculation.a209813050a1ddb1.webp)  
>  
> Hitung nilai Y. Jika Anda membayar sekitar $4, pasti bulan April! Infografis oleh [Jen Looper](https://twitter.com/jenlooper)  
>  
> Matematika yang menghitung garis harus menunjukkan kemiringan garis, yang juga bergantung pada intercept, atau di mana `Y` berada ketika `X = 0`.  
>  
> Anda dapat mengamati metode perhitungan nilai-nilai ini di situs [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Juga kunjungi [Kalkulator Least-squares ini](https://www.mathsisfun.com/data/least-squares-calculator.html) untuk melihat bagaimana nilai angka memengaruhi garis.

## Korelasi

Satu istilah lagi yang perlu dipahami adalah **Koefisien Korelasi** antara variabel X dan Y tertentu. Dengan scatterplot, Anda dapat dengan cepat memvisualisasikan koefisien ini. Plot dengan titik data tersebar rapi pada satu garis memiliki korelasi tinggi, tapi plot dengan titik-titik acak di mana-mana antara X dan Y memiliki korelasi rendah.

Model regresi linier yang baik adalah yang memiliki Koefisien Korelasi tinggi (mendekati 1 daripada 0) menggunakan metode Least-Squares Regression dengan garis regresi.

✅ Jalankan notebook pendamping pelajaran ini dan lihat scatterplot Bulan terhadap Harga. Apakah data yang mengasosiasikan Bulan ke Harga penjualan labu tampak memiliki korelasi tinggi atau rendah menurut interpretasi visual Anda terhadap scatterplot? Apakah berubah jika Anda menggunakan ukuran lebih rinci daripada `Month`, misalnya *hari dalam tahun* (jumlah hari sejak awal tahun)?

Dalam kode berikut, kita asumsikan data sudah dibersihkan, dan diperoleh data frame bernama `new_pumpkins`, mirip dengan berikut:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  

> Kode pembersihan data tersedia di [`notebook.ipynb`](notebook.ipynb). Kami sudah melakukan langkah pembersihan yang sama seperti pelajaran sebelumnya, dan menghitung kolom `DayOfYear` menggunakan ekspresi berikut:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Sekarang setelah Anda memahami matematika di balik regresi linier, mari buat model Regresi untuk melihat apakah kita bisa memprediksi paket labu mana yang memiliki harga labu terbaik. Seseorang yang membeli labu untuk patch labu liburan mungkin ingin informasi ini agar dapat mengoptimalkan pembelian paket labu untuk patch tersebut.

## Mencari Korelasi

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Klik gambar di atas untuk video singkat tentang korelasi.

Dari pelajaran sebelumnya Anda mungkin sudah melihat bahwa rata-rata harga untuk bulan yang berbeda tampak seperti ini:

<img alt="Average price by month" src="../../../../translated_images/id/barchart.a833ea9194346d76.webp" width="50%"/>

Ini menunjukkan bahwa seharusnya ada korelasi, dan kita dapat mencoba melatih model regresi linier untuk memprediksi hubungan antara `Month` dan `Price`, atau antara `DayOfYear` dan `Price`. Berikut adalah scatter plot yang menunjukkan hubungan yang terakhir:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/id/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Mari kita lihat apakah ada korelasi menggunakan fungsi `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Tampaknya korelasinya cukup kecil, -0.15 berdasarkan `Month` dan -0.17 berdasarkan `DayOfMonth`, tetapi mungkin ada hubungan penting lain. Tampak ada beberapa kluster harga berbeda yang sesuai dengan varietas labu berbeda. Untuk mengonfirmasi hipotesis ini, mari plot setiap kategori labu menggunakan warna berbeda. Dengan melewatkan parameter `ax` pada fungsi plot `scatter` kita bisa membuat semua titik berada di grafik yang sama:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/id/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Penyelidikan kita menunjukkan bahwa varietas memiliki pengaruh lebih besar pada harga keseluruhan daripada tanggal penjualan sebenarnya. Kita bisa melihat ini dengan grafik batang:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Bar graph of price vs variety" src="../../../../translated_images/id/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Mari kita fokus untuk saat ini hanya pada satu varietas labu, 'pie type', dan lihat pengaruh tanggal pada harga:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/id/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Jika sekarang kita hitung korelasi antara `Price` dan `DayOfYear` menggunakan fungsi `corr`, kita akan mendapat sekitar `-0.27` - yang berarti melatih model prediktif masuk akal.

> Sebelum melatih model regresi linier, penting memastikan data kita bersih. Regresi linier tidak bekerja baik dengan nilai hilang, jadi masuk akal untuk menghapus semua sel kosong:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
Pendekatan lain adalah mengisi nilai kosong dengan nilai rata-rata dari kolom terkait.

## Regresi Linier Sederhana

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Klik gambar di atas untuk video singkat tentang regresi linier dan polinomial.

Untuk melatih model Regresi Linier kita, kita akan menggunakan perpustakaan **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
Kita mulai dengan memisahkan nilai input (fitur) dan output yang diharapkan (label) ke dalam array numpy terpisah:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> Catatan bahwa kita harus melakukan `reshape` pada data input agar paket Linear Regression memahaminya dengan benar. Regresi Linier mengharapkan array 2D sebagai input, di mana setiap baris array sesuai dengan vektor fitur input. Dalam kasus kita, karena kita hanya punya satu input - kita butuh array dengan bentuk N×1, di mana N adalah ukuran dataset.

Kemudian, kita perlu membagi data menjadi dataset latih dan uji, agar kita dapat memvalidasi model setelah pelatihan:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
Akhirnya, melatih model Regresi Linier sebenarnya hanya memerlukan dua baris kode. Kita definisikan objek `LinearRegression`, dan melatihnya dengan data kita menggunakan metode `fit`:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Objek `LinearRegression` setelah di-`fit` berisi semua koefisien regresi, yang dapat diakses menggunakan properti `.coef_`. Dalam kasus kita, hanya ada satu koefisien, yang seharusnya sekitar `-0.017`. Ini berarti harga tampaknya sedikit turun seiring waktu, tapi tidak terlalu banyak, sekitar 2 sen per hari. Kita juga dapat mengakses titik potong regresi dengan sumbu Y menggunakan `lin_reg.intercept_` - yang akan sekitar `21` dalam kasus kita, menunjukkan harga pada awal tahun.

Untuk melihat seberapa akurat model kita, kita dapat memprediksi harga pada dataset uji, kemudian mengukur seberapa dekat prediksi kita dengan nilai yang diharapkan. Ini dapat dilakukan menggunakan metrik root mean square error (RMSE), yaitu akar dari rata-rata semua selisih kuadrat antara nilai yang diharapkan dan nilai yang diprediksi.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Kesalahan kita tampaknya sekitar 2 poin, yaitu sekitar 17%. Tidak terlalu bagus. Indikator lain dari kualitas model adalah **koefisien determinasi**, yang dapat diperoleh seperti ini:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Jika nilainya 0, itu berarti model tidak mempertimbangkan data input, dan bertindak sebagai *prediktor linier terburuk*, yaitu nilai rata-rata dari hasilnya. Nilai 1 berarti kita dapat memprediksi semua output yang diharapkan dengan sempurna. Dalam kasus kita, koefisiennya sekitar 0.06, yang cukup rendah.

Kita juga dapat menggambar data uji bersama dengan garis regresi untuk melihat lebih jelas bagaimana regresi bekerja dalam kasus kita:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/id/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Regresi Polinomial

Jenis lain dari Regresi Linear adalah Regresi Polinomial. Kadang-kadang ada hubungan linier antara variabel - semakin besar volume labu, semakin tinggi harganya - tetapi terkadang hubungan ini tidak bisa dipetakan sebagai bidang atau garis lurus.

✅ Berikut [beberapa contoh lagi](https://online.stat.psu.edu/stat501/lesson/9/9.8) dari data yang dapat menggunakan Regresi Polinomial

Perhatikan lagi hubungan antara Date dan Price. Apakah scatterplot ini harus dianalisis dengan garis lurus? Apakah harga tidak bisa berfluktuasi? Dalam kasus ini, Anda dapat mencoba regresi polinomial.

✅ Polinomial adalah ekspresi matematis yang mungkin terdiri dari satu atau lebih variabel dan koefisien

Regresi polinomial membuat garis melengkung untuk lebih cocok dengan data yang tidak linier. Dalam kasus kita, jika kita memasukkan variabel `DayOfYear` kuadrat ke dalam data input, kita harus dapat memfit data kita dengan kurva parabola, yang akan memiliki titik minimum pada suatu titik dalam tahun.

Scikit-learn menyertakan API [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) yang berguna untuk menggabungkan berbagai langkah pemrosesan data secara bersama-sama. **Pipeline** adalah rantai dari **estimators**. Dalam kasus kita, kita akan membuat pipeline yang pertama menambahkan fitur polinomial ke model, kemudian melatih regresi:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Menggunakan `PolynomialFeatures(2)` berarti kita akan memasukkan semua polinomial derajat dua dari data input. Dalam kasus kita ini hanya berarti `DayOfYear`<sup>2</sup>, tapi jika ada dua variabel input X dan Y, ini akan menambahkan X<sup>2</sup>, XY, dan Y<sup>2</sup>. Kita juga dapat menggunakan polinomial tingkat lebih tinggi jika diinginkan.

Pipeline dapat digunakan dengan cara yang sama seperti objek `LinearRegression` asli, yaitu kita dapat melakukan `fit` pada pipeline, lalu menggunakan `predict` untuk mendapatkan hasil prediksi. Berikut adalah grafik yang menunjukkan data uji dan kurva pendekatan:

<img alt="Polynomial regression" src="../../../../translated_images/id/poly-results.ee587348f0f1f60b.webp" width="50%" />

Dengan Regresi Polinomial, kita bisa mendapatkan MSE yang sedikit lebih rendah dan koefisien determinasi yang lebih tinggi, tapi tidak signifikan. Kita perlu mempertimbangkan fitur lain!

> Anda dapat melihat bahwa harga labu minimum diamati sekitar Halloween. Bagaimana Anda menjelaskan ini?

🎃 Selamat, Anda baru saja membuat model yang dapat membantu memprediksi harga labu pie. Anda mungkin bisa mengulangi prosedur yang sama untuk semua jenis labu, tapi itu akan merepotkan. Mari kita pelajari sekarang bagaimana mempertimbangkan varietas labu dalam model kita!

## Fitur Kategorikal

Dalam dunia ideal, kita ingin bisa memprediksi harga untuk berbagai varietas labu menggunakan model yang sama. Namun, kolom `Variety` agak berbeda dari kolom seperti `Month`, karena berisi nilai non-numerik. Kolom seperti ini disebut **kategorikal**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Klik gambar di atas untuk video singkat tentang penggunaan fitur kategorikal.

Di sini Anda dapat melihat bagaimana harga rata-rata bergantung pada varietas:

<img alt="Average price by variety" src="../../../../translated_images/id/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Untuk mempertimbangkan varietas, pertama kita perlu mengubahnya ke bentuk numerik, atau **mengkodekannya**. Ada beberapa cara kita dapat melakukannya:

* **Encoding numerik sederhana** akan membuat tabel berbagai varietas, lalu mengganti nama varietas dengan indeks di tabel tersebut. Ini bukan ide terbaik untuk regresi linear, karena regresi linear akan mengambil nilai numerik indeks itu dan menambahkannya ke hasil, yang dikalikan dengan suatu koefisien. Dalam kasus kita, hubungan antara nomor indeks dan harga jelas non-linier, walaupun kita memastikan indeks diurutkan dengan cara tertentu.
* **One-hot encoding** akan menggantikan kolom `Variety` dengan 4 kolom berbeda, satu untuk setiap varietas. Masing-masing kolom berisi `1` jika baris terkait adalah varietas tersebut, dan `0` jika tidak. Ini berarti ada empat koefisien pada regresi linear, satu untuk tiap varietas labu, yang bertanggung jawab atas "harga dasar" (atau lebih tepatnya "harga tambahan") untuk varietas tersebut.

Kode di bawah menunjukkan bagaimana kita bisa melakukan one-hot encoding pada varietas:

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

Untuk melatih regresi linear menggunakan varietas yang sudah di-one-hot encode sebagai input, kita hanya perlu menginisialisasi data `X` dan `y` dengan benar:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Sisa kode sama seperti yang kita gunakan sebelumnya untuk melatih Regresi Linear. Jika Anda mencobanya, Anda akan melihat bahwa mean squared error hampir sama, tapi kita mendapatkan koefisien determinasi yang jauh lebih tinggi (~77%). Untuk mendapatkan prediksi yang lebih akurat lagi, kita dapat mempertimbangkan fitur kategorikal lainnya, serta fitur numerik, seperti `Month` atau `DayOfYear`. Untuk mendapatkan satu array fitur gabungan, kita dapat menggunakan `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Di sini kita juga mempertimbangkan `City` dan tipe `Package`, yang memberikan MSE 2.84 (10%), dan determinasi 0.94!

## Menggabungkan Semua

Untuk membuat model terbaik, kita dapat menggunakan data gabungan (kategorikal yang telah di-one-hot encode + numerik) dari contoh di atas bersama dengan Regresi Polinomial. Berikut kode lengkap untuk kemudahan Anda:

```python
# siapkan data pelatihan
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# buat pembagian train-test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# siapkan dan latih pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# prediksi hasil untuk data uji
pred = pipeline.predict(X_test)

# hitung MSE dan determinasi
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Ini seharusnya memberi kita koefisien determinasi terbaik hampir 97%, dan MSE=2.23 (~8% kesalahan prediksi).

| Model | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| Semua fitur Linear | 2.84 (10.5%) | 0.94 |
| Semua fitur Polynomial | 2.23 (8.25%) | 0.97 |

🏆 Bagus sekali! Anda telah membuat empat model Regresi dalam satu pelajaran, dan meningkatkan kualitas model menjadi 97%. Pada bagian terakhir tentang Regresi, Anda akan belajar tentang Regresi Logistik untuk menentukan kategori.

---
## 🚀Tantangan

Uji beberapa variabel berbeda dalam notebook ini untuk melihat bagaimana korelasi berhubungan dengan akurasi model.

## [Kuis pasca kuliah](https://ff-quizzes.netlify.app/en/ml/)

## Tinjauan & Belajar Mandiri

Dalam pelajaran ini kita belajar tentang Regresi Linear. Ada jenis Regresi lain yang penting. Bacalah tentang teknik Stepwise, Ridge, Lasso dan Elasticnet. Kursus yang bagus untuk belajar lebih lanjut adalah [kursus Pembelajaran Statistik Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Tugas 

[Bangun Model](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berupaya untuk akurasi, harap diketahui bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber otoritatif. Untuk informasi penting, disarankan menggunakan terjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau salah interpretasi yang timbul dari penggunaan terjemahan ini.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->