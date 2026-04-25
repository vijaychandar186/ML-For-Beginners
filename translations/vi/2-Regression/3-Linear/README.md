# Xây dựng mô hình hồi quy sử dụng Scikit-learn: hồi quy theo bốn phương pháp

## Ghi chú cho người mới bắt đầu

Hồi quy tuyến tính được sử dụng khi chúng ta muốn dự đoán một **giá trị số** (ví dụ, giá nhà, nhiệt độ hoặc doanh số).
Nó hoạt động bằng cách tìm một đường thẳng đại diện tốt nhất cho mối quan hệ giữa các đặc trưng đầu vào và đầu ra.

Trong bài học này, chúng ta tập trung vào việc hiểu khái niệm trước khi khám phá các kỹ thuật hồi quy nâng cao hơn.
![Linear vs polynomial regression infographic](../../../../translated_images/vi/linear-polynomial.5523c7cb6576ccab.webp)
> Infographic bởi [Dasani Madipalli](https://twitter.com/dasani_decoded)
## [Bài kiểm tra trước bài giảng](https://ff-quizzes.netlify.app/en/ml/)

> ### [Bài học này cũng có sẵn bằng R!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### Giới thiệu 

Từ trước đến nay bạn đã khám phá khái niệm hồi quy với dữ liệu mẫu thu thập từ bộ dữ liệu giá bí ngô mà chúng ta sẽ sử dụng xuyên suốt bài học này. Bạn cũng đã hình dung dữ liệu bằng Matplotlib.

Bây giờ bạn đã sẵn sàng để đi sâu hơn vào hồi quy trong ML. Trong khi việc trực quan hóa dữ liệu giúp bạn hiểu được dữ liệu, sức mạnh thực sự của Machine Learning đến từ _việc huấn luyện mô hình_. Mô hình được huấn luyện trên dữ liệu lịch sử để tự động nắm bắt các phụ thuộc trong dữ liệu, cho phép bạn dự đoán kết quả cho dữ liệu mới mà mô hình chưa từng thấy trước đó.

Trong bài học này, bạn sẽ học thêm về hai loại hồi quy: _hồi quy tuyến tính cơ bản_ và _hồi quy đa thức_, cùng với một số toán học nền tảng của các kỹ thuật này. Những mô hình đó sẽ giúp chúng ta dự đoán giá bí ngô tùy thuộc vào các dữ liệu đầu vào khác nhau.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 Nhấn vào hình trên để xem video tóm tắt ngắn về hồi quy tuyến tính.

> Xuyên suốt chương trình học này, chúng tôi giả định kiến thức toán học tối thiểu, và cố gắng làm cho nó dễ tiếp cận cho học viên từ các lĩnh vực khác, vì vậy hãy chú ý đến các ghi chú, 🧮 cảnh báo, sơ đồ và các công cụ học tập khác để hỗ trợ tiếp thu.

### Kiến thức nền tảng

Bạn nên đã quen với cấu trúc dữ liệu bí ngô mà chúng ta đang xem xét. Bạn có thể tìm thấy nó được tải sẵn và đã được làm sạch trong tệp _notebook.ipynb_ của bài học này. Trong tệp, giá bí ngô được hiển thị theo mỗi bushel trong một dataframe mới. Đảm bảo bạn có thể chạy các notebook này trong môi trường kernel trên Visual Studio Code.

### Chuẩn bị

Như một lời nhắc, bạn đang tải dữ liệu này để đặt câu hỏi với nó.

- Khi nào là thời điểm tốt nhất để mua bí ngô?
- Giá của một thùng bí ngô tí hon có thể kỳ vọng là bao nhiêu?
- Tôi nên mua chúng trong giỏ nửa bushel hay theo hộp 1 1/9 bushel?
Hãy tiếp tục khai thác dữ liệu này.

Trong bài học trước, bạn đã tạo một Pandas dataframe và điền dữ liệu từ bộ dữ liệu gốc, chuẩn hóa giá theo bushel. Tuy nhiên, bằng cách đó bạn chỉ thu thập được khoảng 400 điểm dữ liệu và chỉ cho các tháng mùa thu.

Hãy xem dữ liệu được tải sẵn trong notebook đi kèm bài học này. Dữ liệu đã được tải sẵn và một biểu đồ điểm ban đầu đã được vẽ để hiển thị dữ liệu theo tháng. Có lẽ chúng ta có thể thu được nhiều chi tiết hơn về bản chất dữ liệu bằng cách làm sạch thêm.

## Đường hồi quy tuyến tính

Như bạn đã học trong Bài 1, mục tiêu của bài tập hồi quy tuyến tính là có thể vẽ một đường để:

- **Hiển thị quan hệ biến số**. Thể hiện mối quan hệ giữa các biến
- **Dự đoán**. Dự đoán chính xác vị trí mà một điểm dữ liệu mới rơi vào tương quan với đường đó.

Dòng thường được sử dụng trong **Hồi quy bình phương tối thiểu**. Thuật ngữ "Bình phương tối thiểu" đề cập đến quá trình giảm thiểu tổng sai số trong mô hình. Với mỗi điểm dữ liệu, ta đo khoảng cách thẳng đứng (gọi là phần dư) giữa điểm thực tế và đường hồi quy của chúng ta.

Chúng ta lấy bình phương các khoảng cách này vì hai lý do chính:

1. **Cường độ hơn hướng:** Chúng ta muốn xem lỗi -5 tương đương với lỗi +5. Việc bình phương làm tất cả giá trị thành số dương.

2. **Phạt các ngoại lệ:** Việc bình phương cho trọng số cao hơn với các lỗi lớn, buộc đường hồi quy phải gần hơn với các điểm dữ liệu xa.

Sau đó chúng ta cộng tất cả các giá trị bình phương lại với nhau. Mục tiêu là tìm ra đường cụ thể nơi tổng này nhỏ nhất có thể — do đó tên gọi "Bình phương tối thiểu".

> **🧮 Cho tôi xem toán học**
> 
> Đường này, gọi là _đường khớp tốt nhất_ có thể được biểu diễn bằng [một phương trình](https://en.wikipedia.org/wiki/Simple_linear_regression):
> 
> ```
> Y = a + bX
> ```
>
> `X` là 'biến giải thích'. `Y` là 'biến phụ thuộc'. Độ dốc của đường là `b` và `a` là điểm giao y, tức là giá trị của `Y` khi `X = 0`.
>
>![calculate the slope](../../../../translated_images/vi/slope.f3c9d5910ddbfcf9.webp)
>
> Trước tiên, tính độ dốc `b`. Infographic bởi [Jen Looper](https://twitter.com/jenlooper)
>
> Nói cách khác, và liên quan đến câu hỏi ban đầu về dữ liệu bí ngô của chúng ta: "dự đoán giá bí ngô theo bushel theo tháng", `X` sẽ là giá và `Y` sẽ là tháng bán.
>
>![complete the equation](../../../../translated_images/vi/calculation.a209813050a1ddb1.webp)
>
> Tính giá trị Y. Nếu bạn trả khoảng $4, chắc hẳn là tháng Tư! Infographic bởi [Jen Looper](https://twitter.com/jenlooper)
>
> Toán học tính toán đường phải biểu thị độ dốc của đường, cũng phụ thuộc vào giao điểm, tức vị trí `Y` khi `X = 0`.
>
> Bạn có thể quan sát phương pháp tính cho những giá trị này trên trang web [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html). Cũng hãy ghé xem [máy tính bình phương tối thiểu này](https://www.mathsisfun.com/data/least-squares-calculator.html) để xem cách giá trị số ảnh hưởng đến đường.

## Tương quan

Một thuật ngữ nữa cần hiểu là **Hệ số Tương quan** giữa các biến X và Y cho trước. Bằng việc sử dụng biểu đồ phân tán, bạn có thể nhanh chóng trực quan hệ số này. Một biểu đồ với các điểm dữ liệu xếp thành một đường thẳng rõ ràng có tương quan cao, còn biểu đồ với điểm dữ liệu rải rác khắp nơi giữa X và Y có tương quan thấp.

Một mô hình hồi quy tuyến tính tốt sẽ có hệ số tương quan cao (gần 1 hơn 0) sử dụng phương pháp Hồi quy bình phương tối thiểu với đường hồi quy.

✅ Chạy notebook đi kèm bài học và xem biểu đồ phân tán Tháng với Giá. Theo quan sát của bạn, dữ liệu liên hệ giữa Tháng và Giá trong bán bí ngô có vẻ tương quan cao hay thấp? Liệu điều này có thay đổi nếu bạn sử dụng đo lường chi tiết hơn thay vì `Month`, ví dụ *ngày trong năm* (tức số ngày kể từ đầu năm)?

Trong đoạn mã dưới đây, ta giả sử đã làm sạch dữ liệu và thu được một dataframe có tên `new_pumpkins`, tương tự như sau:

ID | Tháng | NgàyTrongNăm | ChủngLoại | ThànhPhố | Gói | Giá Thấp | Giá Cao | Giá Trung Bình
---|-------|--------------|-----------|----------|--------|---------|---------|--------------
70 | 9 | 267 | LOẠI BÁNH | BALTIMORE | hộp 1 1/9 bushel | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | LOẠI BÁNH | BALTIMORE | hộp 1 1/9 bushel | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | LOẠI BÁNH | BALTIMORE | hộp 1 1/9 bushel | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | LOẠI BÁNH | BALTIMORE | hộp 1 1/9 bushel | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | LOẠI BÁNH | BALTIMORE | hộp 1 1/9 bushel | 15.0 | 15.0 | 13.636364

> Mã lệnh làm sạch dữ liệu có trong [`notebook.ipynb`](notebook.ipynb). Chúng ta đã tiến hành các bước làm sạch giống như bài học trước, và đã tính toán cột `DayOfYear` theo biểu thức sau:

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

Bây giờ bạn đã hiểu toán học nền tảng của hồi quy tuyến tính, hãy tạo mô hình Hồi quy để xem liệu chúng ta có thể dự đoán gói bí ngô nào sẽ có giá tốt nhất không. Người mua bí ngô cho khu vực trang trí lễ hội có thể muốn thông tin này để tối ưu hóa việc mua hàng.

## Tìm kiếm tương quan

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 Nhấn vào hình trên để xem video tóm tắt ngắn về tương quan.

Từ bài học trước, bạn có thể đã thấy rằng giá trung bình cho các tháng khác nhau trông như sau:

<img alt="Average price by month" src="../../../../translated_images/vi/barchart.a833ea9194346d76.webp" width="50%"/>

Điều này gợi ý rằng có thể có tương quan, và chúng ta có thể thử huấn luyện mô hình hồi quy tuyến tính để dự đoán mối quan hệ giữa `Month` và `Price`, hoặc giữa `DayOfYear` và `Price`. Dưới đây là biểu đồ phân tán thể hiện mối quan hệ sau:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/vi/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

Hãy xem tương quan qua hàm `corr`:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

Có vẻ hệ số tương quan khá nhỏ, -0.15 theo `Month` và -0.17 theo `DayOfYear`, nhưng rất có thể còn mối quan hệ quan trọng khác. Có vẻ như có các cụm điểm giá ứng với các chủng loại bí ngô khác nhau. Để xác nhận giả thuyết này, hãy vẽ mỗi loại bí ngô bằng màu khác nhau. Bằng cách truyền tham số `ax` vào hàm vẽ `scatter` ta có thể vẽ tất cả điểm trong cùng một biểu đồ:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/vi/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

Cuộc điều tra cho thấy chủng loại ảnh hưởng nhiều hơn đến giá chung so với ngày bán thực tế. Ta có thể thấy điều này qua biểu đồ cột:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/vi/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

Tạm thời chúng ta hãy tập trung chỉ vào một chủng loại bí ngô, 'loại bánh', và xem ngày bán ảnh hưởng thế nào đến giá:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/vi/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

Nếu ta tính toán tương quan giữa `Price` và `DayOfYear` bằng hàm `corr`, ta sẽ thu được khoảng `-0.27` - nghĩa là việc huấn luyện mô hình dự đoán là có lý.

> Trước khi đào tạo mô hình hồi quy tuyến tính, quan trọng là phải đảm bảo dữ liệu sạch. Hồi quy tuyến tính không làm việc tốt với các giá trị thiếu, vì vậy nên loại bỏ tất cả ô trống:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

Một cách tiếp cận khác là điền các giá trị thiếu bằng giá trị trung bình của cột tương ứng.

## Hồi quy tuyến tính đơn giản

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 Nhấn vào hình trên để xem video tóm tắt ngắn về hồi quy tuyến tính và đa thức.

Để huấn luyện mô hình Hồi quy tuyến tính, chúng ta sẽ dùng thư viện **Scikit-learn**.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

Đầu tiên ta tách các giá trị đầu vào (đặc trưng) và kết quả mong đợi (nhãn) ra thành các mảng numpy riêng biệt:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> Lưu ý chúng ta phải thực hiện `reshape` trên dữ liệu đầu vào để gói Linear Regression hiểu đúng cách. Hồi quy tuyến tính yêu cầu đầu vào là mảng 2 chiều, trong đó mỗi dòng là một vector đặc trưng. Trong trường hợp của ta, vì chỉ có một đầu vào nên cần mảng có kích thước N&times;1, với N là kích thước bộ dữ liệu.

Sau đó, ta phải chia dữ liệu thành tập huấn luyện và tập kiểm tra để có thể kiểm tra mô hình sau khi huấn luyện:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Cuối cùng, việc huấn luyện mô hình Linear Regression thực tế chỉ mất hai dòng code. Ta định nghĩa đối tượng `LinearRegression`, và gọi phương thức `fit` để phù hợp với dữ liệu:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

Đối tượng `LinearRegression` sau khi được `fit` chứa tất cả các hệ số của hồi quy, có thể truy cập thông qua thuộc tính `.coef_`. Trong trường hợp của chúng ta, chỉ có một hệ số duy nhất, khoảng `-0.017`. Điều này có nghĩa là giá cả có xu hướng giảm nhẹ theo thời gian, nhưng không nhiều, khoảng 2 cent mỗi ngày. Chúng ta cũng có thể truy cập điểm giao của hồi quy với trục Y bằng `lin_reg.intercept_` - nó sẽ khoảng `21` trong trường hợp của chúng ta, biểu thị giá vào đầu năm.

Để xem mô hình của chúng ta chính xác đến mức nào, chúng ta có thể dự đoán giá trên bộ dữ liệu test, và sau đó đo xem các dự đoán có gần với giá trị mong đợi hay không. Điều này có thể được thực hiện bằng cách sử dụng chỉ số lỗi trung bình bình phương căn (RMSE), là căn bậc hai của trung bình tất cả các sai số bình phương giữa giá trị mong đợi và giá trị dự đoán.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

Lỗi của chúng ta có vẻ khoảng 2 điểm, tức là ~17%. Không được tốt lắm. Một chỉ số khác để đánh giá chất lượng mô hình là **hệ số xác định**, có thể lấy như sau:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```

Nếu giá trị là 0, nghĩa là mô hình không xem xét dữ liệu đầu vào, và hoạt động như *bộ dự đoán tuyến tính tệ nhất*, chính là giá trị trung bình của kết quả. Giá trị 1 nghĩa là chúng ta có thể dự đoán chính xác tất cả các đầu ra mong đợi. Trong trường hợp của chúng ta, hệ số khoảng 0.06, khá thấp.

Chúng ta cũng có thể vẽ dữ liệu test cùng với đường hồi quy để thấy rõ hơn hồi quy hoạt động như thế nào trong trường hợp của chúng ta:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/vi/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Hồi quy đa thức

Một loại khác của Hồi quy tuyến tính là Hồi quy đa thức. Mặc dù đôi khi có mối quan hệ tuyến tính giữa các biến - càng to thì giá càng cao - đôi khi các mối quan hệ này không thể biểu diễn bằng một mặt phẳng hoặc đường thẳng.

✅ Đây là [một số ví dụ khác](https://online.stat.psu.edu/stat501/lesson/9/9.8) về dữ liệu có thể sử dụng Hồi quy đa thức

Hãy xem lại mối quan hệ giữa Ngày và Giá. Đồ thị phân tán này có thật sự nên được phân tích bằng đường thẳng không? Không thể có sự dao động về giá sao? Trong trường hợp này, bạn có thể thử hồi quy đa thức.

✅ Đa thức là các biểu thức toán học có thể gồm một hoặc nhiều biến và hệ số

Hồi quy đa thức tạo đường cong để phù hợp hơn với dữ liệu phi tuyến. Trong trường hợp của chúng ta, nếu thêm biến `DayOfYear` bình phương vào dữ liệu đầu vào, chúng ta có thể khớp dữ liệu với đường cong parabol, có điểm cực tiểu ở một thời điểm trong năm.

Scikit-learn có API [pipeline](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) hữu ích để kết hợp các bước xử lý dữ liệu lại với nhau. Một **pipeline** là chuỗi các **estimator**. Trong trường hợp này, chúng ta sẽ tạo pipeline đầu tiên thêm các đặc trưng đa thức vào mô hình, rồi sau đó huấn luyện hồi quy:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```

Sử dụng `PolynomialFeatures(2)` nghĩa là chúng ta sẽ bao gồm tất cả đa thức bậc hai từ dữ liệu đầu vào. Trong trường hợp này chỉ là `DayOfYear`<sup>2</sup>, nhưng với hai biến đầu vào X và Y, sẽ thêm X<sup>2</sup>, XY và Y<sup>2</sup>. Chúng ta cũng có thể dùng đa thức bậc cao hơn nếu muốn.

Pipeline có thể dùng như đối tượng `LinearRegression` ban đầu, tức là ta có thể `fit` pipeline rồi sau đó dùng `predict` để lấy kết quả dự đoán. Dưới đây là đồ thị cho thấy dữ liệu test và đường cong xấp xỉ:

<img alt="Polynomial regression" src="../../../../translated_images/vi/poly-results.ee587348f0f1f60b.webp" width="50%" />

Dùng Hồi quy đa thức, ta có thể có MSE hơi thấp hơn và hệ số xác định cao hơn, nhưng không đáng kể. Ta cần xem xét các đặc trưng khác!

> Bạn có thể thấy giá tối thiểu của bí ngô xuất hiện xung quanh Halloween. Bạn giải thích điều này thế nào?

🎃 Chúc mừng, bạn vừa tạo mô hình có thể giúp dự đoán giá bí ngô làm bánh. Có thể bạn sẽ lặp lại quy trình cho các loại bí khác, nhưng sẽ rất tốn thời gian. Giờ hãy học cách đưa loại bí vào mô hình nhé!

## Đặc trưng phân loại

Trong thế giới lý tưởng, ta muốn dự đoán giá cho các loại bí khác nhau bằng cùng một mô hình. Tuy nhiên, cột `Variety` khá khác so với các cột như `Month` vì nó chứa giá trị không phải số. Các cột như vậy gọi là **phân loại**.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 Nhấn vào hình trên để xem video ngắn về cách dùng các đặc trưng phân loại.

Bạn có thể thấy giá trung bình phụ thuộc vào loại bí như thế nào:

<img alt="Average price by variety" src="../../../../translated_images/vi/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Để đưa loại bí vào mô hình, trước tiên cần chuyển thành dạng số, hay **mã hóa**. Có một số cách để làm điều này:

* **Mã hóa số đơn giản** tạo bảng các loại khác nhau, rồi thay tên loại bằng chỉ số trong bảng đó. Đây không phải ý hay cho hồi quy tuyến tính, vì hồi quy tuyến tính dùng trực tiếp giá trị số của chỉ số và nhân với hệ số. Trong trường hợp này, mối quan hệ giữa số chỉ số và giá không phải là tuyến tính, dù ta cố sắp xếp các chỉ số theo thứ tự nào đó.
* **Mã hóa one-hot** sẽ thay cột `Variety` bằng 4 cột khác, mỗi cột cho một loại. Mỗi cột có giá trị `1` nếu hàng tương ứng thuộc loại đó, `0` nếu không. Điều này dẫn đến 4 hệ số trong hồi quy, mỗi hệ số dành cho một loại bí, thể hiện "giá khởi đầu" (hoặc "giá thêm") cho loại đó.

Đoạn mã dưới đây cho thấy cách mã hóa one-hot cho loại bí:

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

Để huấn luyện hồi quy tuyến tính dùng kiểu mã hóa one-hot, ta chỉ cần khởi tạo dữ liệu `X` và `y` đúng cách:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Phần còn lại của mã giống như trên dùng để huấn luyện hồi quy tuyến tính. Nếu bạn thử, sẽ thấy MSE gần như bằng nhau, nhưng hệ số xác định tăng lên khá nhiều (~77%). Để dự đoán chính xác hơn, ta có thể dùng nhiều đặc trưng phân loại hơn, cũng như các đặc trưng số, ví dụ như `Month` hoặc `DayOfYear`. Để có mảng đặc trưng lớn, dùng `join`:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

Ở đây ta cũng thêm vào `City` và loại `Package`, cho kết quả MSE 2.84 (10%), và hệ số xác định 0.94!

## Tổng hợp lại

Để có mô hình tốt nhất, ta có thể dùng dữ liệu kết hợp (phân loại mã hóa one-hot + số) từ ví dụ trên cùng hồi quy đa thức. Dưới đây là mã đầy đủ cho bạn tiện sử dụng:

```python
# thiết lập dữ liệu đào tạo
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# chia dữ liệu thành tập huấn luyện và kiểm tra
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# thiết lập và huấn luyện pipeline
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# dự đoán kết quả cho dữ liệu kiểm tra
pred = pipeline.predict(X_test)

# tính MSE và hệ số xác định
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

Mô hình này cho hệ số xác định cao nhất gần 97% và MSE=2.23 (~8% lỗi dự đoán).

| Mô hình | MSE | Hệ số xác định |
|-------|-----|---------------|
| `DayOfYear` Tuyến tính | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Đa thức | 2.73 (17.0%) | 0.08 |
| `Variety` Tuyến tính | 5.24 (19.7%) | 0.77 |
| Tất cả đặc trưng Tuyến tính | 2.84 (10.5%) | 0.94 |
| Tất cả đặc trưng Đa thức | 2.23 (8.25%) | 0.97 |

🏆 Làm tốt lắm! Bạn đã tạo bốn mô hình hồi quy trong một bài học, và cải thiện chất lượng mô hình lên 97%. Trong phần cuối về Hồi quy, bạn sẽ học về Hồi quy Logistic để phân loại.

---
## 🚀Thử thách

Thử nghiệm với vài biến khác nhau trong notebook này để xem yếu tố tương quan tương ứng với độ chính xác mô hình như thế nào.

## [Bài kiểm tra sau bài giảng](https://ff-quizzes.netlify.app/en/ml/)

## Ôn tập & Tự học

Trong bài học này chúng ta tìm hiểu về Hồi quy tuyến tính. Còn nhiều loại hồi quy quan trọng khác. Hãy đọc về các kỹ thuật Stepwise, Ridge, Lasso và Elasticnet. Một khóa học hay để học thêm là [khóa học Học thống kê Stanford](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning)

## Bài tập

[Xây dựng mô hình](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tin chính thức. Đối với thông tin quan trọng, nên sử dụng dịch thuật chuyên nghiệp bởi con người. Chúng tôi không chịu trách nhiệm đối với bất kỳ sự hiểu lầm hoặc giải thích sai nào phát sinh từ việc sử dụng bản dịch này.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->