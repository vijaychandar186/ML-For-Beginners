# Scikit-learn பயன்படுத்தி ஒரு பகுப்பாய்வு மாதிரியை உருவாக்குதல்: regression நான்கு வழிகள்

## ஆரம்பக்காரர் குறிப்பு

எண் மதிப்பை (உதாரணமாக, வீட்டு விலை, வெப்ப நிலை அல்லது விற்பனை) கணிக்க linear regression பயன்படுத்தப்படுகிறது.
இது உள்ளீட்டு அம்சங்களுக்கும் வெளியீட்டு மதிப்பிற்குமான தொடர்பை சிறந்த முறையில் பிரதிநிதித்துவப்படுத்தும் நேர்கைக்கோவை கண்டுபிடிப்பதன் மூலம் செயல்படுகிறது.

இந்த பாடத்தில், நாம் regression முறைகளை புரிந்து கொள்வதில் கவனம் செலுத்தி இன்னும் மேம்பட்ட regression நுட்பங்களை ஆராய்வதற்கு முன் இத்தொடர்பை புரிந்து கொள்கிறோம்.
![Linear vs polynomial regression infographic](../../../../translated_images/ta/linear-polynomial.5523c7cb6576ccab.webp)
> [Dasani Madipalli](https://twitter.com/dasani_decoded) என்பவரின் தகவல்காட்சி
## [பாடமுன் வினாத்தாளி](https://ff-quizzes.netlify.app/en/ml/)

> ### [இந்த பாடம் R இல் கிடைக்கும்!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### அறிமுகம்

இதுவரை நீங்கள் regression என்பது என்ன என்பதை pumpkin விலை தரவுத்தொகுப்பிலிருந்து எடுத்துக்காட்டுக் கூரிய தரவுடன் ஆராய்ந்துள்ளீர்கள், இதை இந்த பாடத்துடன் முழுமையாக பயன்படுத்த உள்ளோம். Matplotlib பயன்படுத்தி அதனை காண்பித்துள்ளீர்கள்.

இப்போது நீங்கள் ML க்கான regression இல் மேலும் நுழைய தயாராக உள்ளீர்கள். தரவுகளை காண்பிப்பது அவற்றை புரிந்துகொள்ள உதவுகிறது, ஆனாலும் இயந்திரக் கற்றல் மாட்சிமை என்பது _மாதிரிகளை பயிற்சி செய்வதில்_ உள்ளது. மாதிரிகள் கடந்த தரவுகளில் பயிற்சி பெற்று தரவு சார்புகளை தானாக பறைசெய்கின்றன, மேலும் புதிய தரவிற்கான முடிவுகளை கணிக்க உதவுகின்றன, இந்த மாதிரி பழைய தரவுகளை காட்டியதில்லை.

இந்த பாடத்தில், நீங்கள் இரண்டு regression வகைகள், _அடிப்படை நேரியல் regression_ மற்றும் _பல்கோண regression_ கொஞ்சம் கணிதத்துடன் பற்றி கற்றுக்கொள்வீர்கள். அவை pumpkin விலை கணிக்க உதவும், உள்ளீட்டு தரவை பொருத்து.

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 மேலே உள்ள படத்தை கிளிக் செய்து நேரியல் regression குறித்த சிறு வீடியோ சர்போட்டைப் பெறவும்.

> இந்த பாடத்திட்டத்தில், கணிதத்தில் மிகக் குறைந்த அறிவுப்பார்வையை மதிப்பிடுகிறோம், மற்றும் வேறு துறையிலிருந்து வரும் மாணவர்களுக்கு சோதனை செய்யிறோம், ஆகையால் குறிப்பு, 🧮 அழைப்புகள், வரைபடங்கள் மற்றும் பிற கற்றல் கருவிகளை கவனியுங்கள்.

### முன் அறிவு

இப்போது நாம் பார்க்கும் pumpkin தரவின் அமைப்புக்குப் பழகியிருக்க வேண்டும். இந்த பாடத்தில் முன்னமே preloaded மற்றும் pre-cleaned செய்யப்பட்டுள்ளது. இதில் pumpkin விலை புதிய தரவு பெட்டியில் bushel வீதம் காட்டப்பட்டுள்ளது. Visual Studio Codeல் இந்த notebook இனை கெர்னல்களில் இயக்கு என்பது உறுதியாக்கொள்ள வேண்டும்.

### தயாரிப்பு

நீங்கள் இந்த தரவை ஏற்று அதில் கேள்விகள் கேட்கப் போகிறீர்கள் என்பதைக் நினைவுக்கொள்ளுங்கள்.

- pumpkins வாங்க எந்த நேரம் சிறந்தது?
- குறுந்துண்டு pumpkins ஒரு பெட்டிக்கு என்ன விலை எதிர்பார்க்கலாம்?
- பால்-bushel தொட்டிகளில் வாங்க மறுப்பதா அல்லது 1 1/9 bushel பெட்டியில் வாங்குமா?
நாம் இந்த தரவை ஆராய்வு செய்கிறோம்.

கடந்த பாடத்தில், நீங்கள் Pandas data frame உருவாக்கி அதனை ஆரம்ப தரவின் ஒரு பகுதியுடன் நிரப்பி, விலையை bushel கூறு விகிதத்தால் சீரமைத்துள்ளீர்கள். ஆனால், இதனால் நீங்கள் சுமார் 400 தரவு புள்ளிகளை மட்டுமே மற்றும் இறறுநீண்ட காலங்களுக்குப் பொருந்தி சேகரித்துள்ளீர்கள்.

இந்த பாடத் தொடர்பாக உள்ள notebook இல் முன்னதாக ஏற்றப்பட்ட தரவைக் கவனியுங்கள். அங்கு ஆரம்ப scatterplot வரைபடம் மாத தரவை காட்டுகிறது. கூடுதலான தரவின் இயல்பைப் புரிந்துகொள்ள, மேலும் சுத்திகரிப்பது வாய்ப்பு உள்ளது.

## ஒரு நேரியல் regression கோடு

பாடம் 1ல் கற்றுக்கொண்டது போல, linear regression பயிற்சியின் நோக்கம் கோடை வரைபடத்தைக் கடைப்பிடிப்பதற்குள் இருக்கிறது:

- **மாற்றியமை கடத்தியவை** ஓர் மாறில்களுக்கு இடையேயான தொடர்பை காட்ட
- **பரிந்துரைகள் செய்ய** புதிய தரவு புள்ளி அந்தக் கோட்டிற்கு எங்கிருக்கும் என்பதில் துல்லியமான கணிப்பை செய்ய

**Least-Squares Regression** இல் இந்த வகையான கோடு வரைபடம் கிட்டத்தட்ட வழக்கம். Least-Squares என்பது, மாதிரியின் மொத்த பிழையை குறைத்துக் கொள்ளும் செயல்முறையை குறிக்கும். ஒவ்வொரு தரவு புள்ளிக்கும், நாங்கள் உண்மையான புள்ளி மற்றும் கோடி இடையே நேரடி தொலைவான (residual என்று அழைக்கப்படும்) அளவை அளவிடுகிறோம்.

இதைக் مربع முறையில் மதிப்பீடு செய்வதற்குக் காரணங்கள் இரண்டு:

1. **திசை சாரா அளவு:** -5 என்ற பிழையை +5 பிழை போலவே கையாள்வது தேவை. مربع செய்வதால் அனைத்து மதிப்புகளும் நேர்மறை ஆனவை ஆகின்றன.

2. **விலகிய தரவுகளுக்கு அதிகம் போக்குதல்:** பெரிய பிழைகள் இல் مربع அதிக மதிப்பளிக்கிறது, அதனால் கோடு அந்த புள்ளிகளுக்கு நெருக்கம் படுகிறது.

பிறகு அனைத்து مربع மதிப்புகளையும் கூட்டுகிறோம். குறைந்தபட்சமான மொத்தம் (சிறந்த துல்லியத்துடன்) உள்ள கோட்டை கண்டுபிடிப்பதே நோக்கம்— அதனால் இது "Least-Squares" எனப்படும்.

> **🧮 எண்கணிதம் காட்டவும்**  
> இது _சிறந்த பொருந்தக்கூடிய கோடு_ என அழைக்கப்படுகின்றது மற்றும் [ஒரு சமன்பாடால்](https://en.wikipedia.org/wiki/Simple_linear_regression) வெளிப்படுகிறது:  
> 
> ```
> Y = a + bX
> ```
>
> `X` என்பது ‘விளக்க மாறி’. `Y` என்பது ‘மாறாக உள்ள மாறி’. கோட்டின் சாய்வு `b` ஆகும் மேலும் `a` என்பது y-இலக்கு, இது `X = 0` ஆகும் போது `Y`ன் மதிப்பை குறிக்கிறது.  
>
>![calculate the slope](../../../../translated_images/ta/slope.f3c9d5910ddbfcf9.webp)  
>
> முதலில், சாய்வு `b`-ஐ கணக்கிடவும். தகவல்காட்சி [Jen Looper](https://twitter.com/jenlooper) என்பவருடையது  
>
> மற்றொரு வழியில் கூறுவதில், pumpkin தரவின் ஆரம்ப கேள்வியை கூறும் போது: "ஒரு pumpkin விலையை மாத வாரியாக predict செய்ய", `X` விலை மற்றும் `Y` விற்பனை மாதமாக இருக்கும்.  
>
>![complete the equation](../../../../translated_images/ta/calculation.a209813050a1ddb1.webp)  
>
> Y இன் மதிப்பை கணக்கிடுங்கள். நீங்கள் $4 ஆல் பாவிக்கிறீர்கள் எனில் அது ஏப்ரல் மாதம் என்பதுதான்! தகவல்காட்சி [Jen Looper](https://twitter.com/jenlooper) என்பவருடையது  
>
> கோட்டின் சாய்வும், இப்படியே மதிப்பிடும் கோட்டின் இடைச்சேதம் (intercept) கூட Y இடம் நிரந்தரப்படுத்தும் இடமும் கணிதத்தில் அடங்கியிருக்க வேண்டும்.  
>
> இந்த மதிப்பீட்டுக்கான முறைகளை [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) இணையதளத்தில் பார்க்கலாம். மேலும் [Least-squares calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) இல் எண்களின் மதிப்புகள் கோட்டிற்கு எப்படி பாதகம் செய்கின்றன என காணலாம்.

## தொடர்பு (Correlation)

இன்னொரு முக்கியமான மாறி என்பது கொடுக்கப்பட்டு X மற்றும் Y மாறில்களுக்கு இடையேயான **Correlation Coefficient** ஆகும். scatterplot பயன்படுத்தி இதை விரைவாக காட்சி படுத்தலாம். தரவு புள்ளிகள் ஓர் நேரடி கோட்டில் சீராக பரவியிருந்தால் அதிக தொடர்பு, அந்நிலையை வாயிலாக புள்ளிகள் எங்கெங்கும் பரவியிருந்தாலும் குறைந்த தொடர்பு.

சிறந்த linear regression மாதிரி, Least-Squares Regression முறையிலும் regression கோட்டுடன் Correlation Coefficient 1க்கு அருகிலும் (0க்கு அல்ல) இருப்பதே.

✅ இந்த பாடத்திற்கான notebook இனை இயக்கு, Month மற்றும் Price இடையேயான scatterplot பார்க்கவும். Month மற்றும் Price இடையே தாவரவியல் தொடர்பு அதிகமாக இருக்கிறதா, குறைவா என்ற விவரமளித்துக் கொள்ளவும். இதை Month பதிலாக வருடத்தின் நாட்கள் (day of the year) போன்ற சுருக்கமான அளவீட்டுடன் மாற்றியால் நிலைமைகள் மாறுமா?

கீழே உள்ள குறியீட்டில், தரவை சுத்திகரித்து, `new_pumpkins` எனும் data frame உருவாக்கிவிட்டோம், இதோ அதர்வானது:

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price
---|-------|-----------|---------|------|---------|-----------|------------|-------
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364

> தரவை சுத்திகரிக்கும் குறியீடு [`notebook.ipynb`](notebook.ipynb) இல் உள்ளது. கடந்த பாடத்தில் செய்த அதே சுத்திகரிப்பு நடவடிக்கைகள் கையாண்டோம். `DayOfYear` பத்தியை பின்வரும் வெளிப்பாட்டின் மூலம் உருவாக்கியுள்ளோம்: 

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```

இப்போது linear regression மேலான கணிதம் புரிந்திருக்கிறது; pumpkin விலையில் எது சிறந்தது என்று predict செய்ய Regression மாதிரி உருவாக்குவோம். ஓர் pumpkin கிளப்புக்காக pumpkins வாங்கும் நபர், வாங்கும் தொகுதிகளை முறையாக தேர்ந்தெடுக்க இதன் உதவிச்செய்யலாம்.

## தொடர்பை தேடுதல்

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 மேலே உள்ள படத்தை கிளிக் செய்து தொடர்பு குறித்த சிறிய காணொளி பெறவும்.

கடந்த பாடத்தில், விதிவிலக்கு, மாதத்திற்கு பேராசை விலை இப்படியே இருந்தது என்று பார்த்திருப்பீர்கள்:

<img alt="Average price by month" src="../../../../translated_images/ta/barchart.a833ea9194346d76.webp" width="50%"/>

இதன் மூலம் தொடர்பு இருக்கவேண்டும் என்றும், நாங்கள் linear regression மாதிரியை பயிற்சி செய்து `Month` மற்றும் `Price`, அல்லது `DayOfYear` மற்றும் `Price` இடையேயான தொடர்பை கணிக்கலாம். கீழே உடன் வரும் scatter plot, அந்த இரண்டாவது தொடர்பை காட்டுகிறது:

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ta/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" /> 

`corr` function பயன்படுத்தி தொடர்பு சரிபார்ப்போம்:

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```

மாதத்தில் -0.15 மற்றும் தினத்தில் -0.17 ஆகியவை போன்ற குறைந்த தொடர்புகள் இருப்பதாக தெரிகிறது, ஆனால் வேறு முக்கியமான தொடர்பு இருக்கலாம். pumpkin வகைகள் விலை ஒருங்கிணைப்பின் வேறுபாடு இருப்பதாக தோன்றுகிறது. இதில் நம்பிக்கை பெற pumpkin வகைகளுக்கு வெவ்வேறு வண்ணங்களில் பரவியானது காட்டுவோம். `scatter` வரைபட செயல்பாட்டுக்கு `ax` அளவுருவை கொடுத்து அனைத்து புள்ளிகளையும் ஒரே வரைபடத்தில் காட்டலாம்:

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ta/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" /> 

மாத இறுதியில் pumpkin வகை விலை மீது விடுவிக்கப்படும் விளைவுகள் தேதி விட அதிகமானது என்பதை மாதிரியாக்கலாம்:

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```

<img alt="Bar graph of price vs variety" src="../../../../translated_images/ta/price-by-variety.744a2f9925d9bcb4.webp" width="50%" /> 

நாம் 'pie type' pumpkin வகையில் மட்டும் கவனம் செலுத்தி நாளில் விலை மீது விலை விளைவுகளை பார்க்கலாம்:

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/ta/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" /> 

இப்போது `Price` மற்றும் `DayOfYear` இடையேயான தொடர்பை `corr` மூலம் கணக்கிடினால், `-0.27` போன்ற மதிப்பை பெறுவீர்கள் – அதாவது கணிப்புத் தன்மைக்கான மாதிரியின் பயிற்சி அர்த்தமுள்ளதாகும்.

> linear regression பயிற்சி செய்யும் முன், தரவு சுத்தமாக இருப்பதை உறுதி செய்வது அவசியம். linear regression காணாமல் போன மதிப்புகளுடன் நல்ல செயல்பாட்டைத் தராது; ஆகையால் வெறும் காலியான செல்களை அகற்றுவது நன்றானது:

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```

மற்றொரு வழி காலியான மதிப்புகளை கோலத்தின் சராசரி மதிப்புகளால் நிரப்புவது.

## எளிமையான நேரியல் Regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 மேலே உள்ள படத்தை கிளிக் செய்து linear மற்றும் polynomial regression குறித்த சிறு வீடியோ பார்வை பெறவும்.

நாம் Linear Regression மாதிரியை பயிற்சியிட Scikit-learn நூலகத்தை பயன்படுத்துவோம்.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```

முதல் நிலையாக உள்ளீட்டு மதிப்புகள் (அம்சங்கள்) மற்றும் எதிர்பார்க்கப்படும் வெளியீடு (குறி) பிரித்து numpy arrays ஆக மாற்றுவோம்:

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```

> எச்சரிக்கை: Linear Regression தொகுப்பை சரியாக புரிந்துகொள்ள,input தரவுகள் `reshape` செய்யப்பட்டு 2D array ஆக மாற்ற வேண்டியது அவசியம். Linear Regression 2D array (ஒரு வரி ஒரு அம்ச குறியீடு) வடிவம் எதிர்பார்க்கிறது. நமது வழியில், உள்ளீடு ஒன்றை மட்டும் கொண்டு இருப்பதால், வடிவம் N×1 ஆக வேண்டும், இதில் N என்பது தரவு அளவு.

பின்னர், பயிற்சி மற்றும் சோதனை தரவுதொகுதிகளை பிரித்து, பயிற்சியில் மாதிரியை சரிபார்க்க வேண்டும்:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

இறுதியில், Linear Regression மாதிரியை தவிர்க்க இரண்டு வரிகளிலேயே பயிற்சி செய்கிறது. `LinearRegression` பொருளை வரையறுக்கி, அதை `fit` முறையால் தரவுக்கு பொருத்துவோம்:

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`LinearRegression` பொருள் `fit` செய்த பிறகு, அனைத்து ரெגרெஷன் коэффициентுகளை `.coef_` சொத்தைப் பயன்படுத்தி அணுக முடியும். எங்கள் நிலையில், ஒரு коэффициентே உள்ளது, அது `-0.017` கிட்டத்தட்ட இருக்க வேண்டும். இதன் பொருள், விலைகள் காலத்தோடு சிறிது குறையும் போலும், ஆனால் அதிகமாக அல்ல, ஒரு நாளுக்கு சுமார் 2 சென்ட். ரெגרெஷன் வையின் Y அச்சுடன் கட்டாயிடும் புள்ளியை `lin_reg.intercept_` மூலம் அணுகலாம் - இது எங்கள் நிலையில் சுமார் `21` இருக்கும், அதாவது வருடத்தின் தொடக்கத்தில் விலை.

எங்கள் மாதிரி எவ்வளவு நுட்பமாக உள்ளது என்று பார்க்க, நாம் ஒரு சோதனை தரவுத்தொகுப்பில் விலை கணிக்கலாம், பிறகு எவ்வளவு நமது கணிப்புகள் எதிர்பார்க்கப்பட்ட மதிப்புகளுக்கு அருகில் உள்ளது என்பதை மதிப்பிடலாம். இது root mean square error (RMSE) அளவுகோலை பயன்படுத்தி செய்ய முடியும், இது எதிர்பார்க்கப்படும் மற்றும் கணிக்கப்பட்ட மதிப்புகளுக்கிடையேயான அனைத்து சதுர வேறுபாடுகளின் சராசரி வேர் ஆகும்.

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```
  
எமது பிழை சுமார் 2 புள்ளிகள் இருக்குமென தெரிகிறது, இது ~17% ஆகும். மிகவும் நன்றாக இல்லை. மாதிரி தரத்தின் மற்றொரு குறியீடு **coefficient of determination** ஆகும், இதைப் பின்வருமாறு பெறலாம்:

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
  
மதிப்பு 0 என்றால், மாதிரி உள்ளீட்டு தரவை எடுத்துக்கொள்வதில்லை என்றும், *மிக மோசமான நேர்காணல் முன்மாதிரி* போல செயல்படுகிறது என்றும் பொருள், இது வெறும் முடிவின் சராசரி மதிப்பாகும். மதிப்பு 1 என்றால், நாம் எதிர்பார்க்கப்படும் அனைத்து வெளியீடுகளையும் முற்றிலும் கணிக்க முடியும் என்று பொருள். எங்கள் நிலையில், коэффициент சுமார் 0.06, இது மிகவும் குறைவாக உள்ளது.

சோதனை தரவுத்தொகுப்பைக் கூட்டி ரெเกஸ்ஸனின் கோட்டுடன் வரைபடம் வரைதல் மூலம் எமது மாதிரி எவ்வாறு செயல்படுகிறது என்பதை தெளிவாக பார்க்கலாம்:

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```
  
<img alt="Linear regression" src="../../../../translated_images/ta/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

Linear Regression இன் மற்றொரு வகை Polynomial Regression ஆகும். சில நேரங்களில், மாறிலிகளுக்கு நேர்காணல் தொடர்பு உள்ளது - ஒரு பூசணிக்காய் அதிக அளவில் இருந்தால் விலை உயர்ந்திருக்கும் - ஆனால் சில சமயங்களில் இத்தகைய தொடர்புகளை சமத்துவமான அல்லது நேரியல் கோட்டாக வரைய முடியாது.

✅ இங்கு [இன்னும் சில எடுத்துக்காட்டுகள்](https://online.stat.psu.edu/stat501/lesson/9/9.8) உள்ளன, Polynomial Regression பயன்படும் தரவுக்கு

Date மற்றும் Price இடையேயான தொடர்பை மறுபடியும் பாருங்கள். இந்த scatterplot நேர்காணல் கோட்டால் பகுப்பாய்வு செய்ய வேண்டுமா? விலை மாற்றமடைய முடியாது என்றாய்? இவ்வாறு இருந்தால், polynomial regression முயற்சி செய்யலாம்.

✅ Polynomial என்பது ஒரு அல்லது அதற்கு மேற்பட்ட மாறிலிகள் மற்றும் коэффициентுகள் கொண்ட கணித வெளிப்பாடுகள் ஆகும்

Polynomial regression ஒரு வளைந்த கோட்டைக் உருவாக்கி, நேரியல் அல்லாத தரவுக்கு சிறந்த பொருத்தத்தை அளிக்கிறது. எங்கள் நிலைமையில், வகையான `DayOfYear²` மாறியை உள்ளீடு தரவில் சேர்த்தால், நாம் ஒரு பரபோலிக் வளைவை பொருத்த முடியும், அதில் வருடத்தின் ஒரு குறிப்பிட்ட இடத்தில் குறைந்தபட்சம் இருக்கும்.

Scikit-learn ஆல் ஒரு பயனுள்ள [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) உள்ளது, இது தரவு செயலாக்க பல படிகளை ஒன்றிணைக்க உதவுகிறது. **pipeline** என்பது பல **estimators** வரிசையாகும். எங்கள் நிலையில், முதலில் polynomial பண்புகளை மாதிரிக்கு சேர்த்து, பிறகு ரெக்ரெஷன் பயிற்சி பெறும் pipeline ஒன்றை உருவாக்குவோம்:

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```
  
`PolynomialFeatures(2)` பயன்படுத்துவது, உள்ளீடு தரவின் இரண்டாம் நிலை அனைத்து polynomial யையும் சேர்த்துக் கொள்வதை 의미ம். எங்கள் நிலைமையில் இது `DayOfYear²` ஆகும், ஆனால் இரண்டு மாறிலிகள் X மற்றும் Y என்றால், இது X², XY, Y² ஆகியவற்றை சேர்க்கும். மேல் நிலை polynomial களை நாங்கள் விரும்பினால் பயன்படுத்தலாம்.

Pipelines ஐ இயல்பான `LinearRegression` பொருளின் மாதிரியே பயன்படுத்தலாம், அதாவது pipeline ஐ `fit` செய்து, பிறகு `predict` மூலம் கணிப்புகளை பெறலாம். கீழே சோதனை தரவும், பரபோலிக் பரப்பையும் காட்டியுள்ளோம்:

<img alt="Polynomial regression" src="../../../../translated_images/ta/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polynomial Regression பயன்படுத்தி சில அளவிற்கு குறைந்த MSE மற்றும் அதிகமாகும் determination பெற முடியும், ஆனால் அதிக மாறுபாடு இல்லை. மற்ற பண்புகளையும் கவனிக்க வேண்டும்!

> பீ பதங்களை அதிகரிக்கும் மிகக் குறைந்த விலைகள் ஹாலோவீன் சுற்றிலும் உள்ளது என்று நீங்கள் கவனித்தீர்களா? இதனை எப்படி விளக்கமுடியும்?

🎃 வாழ்த்துக்கள், நீங்கள் பை பீற்கூடிய பீ விலையை கணிக்க உதவும் மாதிரியை உருவாக்கினீர்கள். இதே சீரியல் முறையை அனைத்து பீ வகைகளுக்கும் பயன்படுத்தலாம், ஆனால் அது களைப்பானதாக இருக்கும். இப்போது உங்கள் மாதிரியில் பீ விதத்தை மாற்றுவது எப்படி என்று கற்றுக் கொள்வோம்!

## Categorical Features

சரியான உலகில், நம்முடைய மாதிரி பல பீ விதங்களுக்கு விலை கணிக்க முடியும். ஆனால், `Variety` நெடுவரிசை `Month` போன்ற எண் சார்ந்த அல்லாத மதிப்புகளை கொண்டுள்ளது. இந்த நெடுவரிசைகள் **categorical** என அழைக்கப்படுகின்றன.

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 தெரிந்துகொள்ள முக்கிய வீடியோ - categorical பண்புகளை எப்படி பயன்படுத்துவது.

இங்கு விதத்தின் அடிப்படையில் சராசரி விலை எப்படி உள்ளது பார்க்கலாம்:

<img alt="Average price by variety" src="../../../../translated_images/ta/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

விதத்தை எண்ணிக்கையாக மாற்ற, அதாவது **encode** செய்ய முதலில் அதை எண்கள் வடிவத்திற்குப் பதிக்க வேண்டும். இதற்குள் பல வழிகள் உள்ளன:

* எளிய **எண்ணியல் எண்கோவை** விதங்களின் பட்டியலை நோக்கி அமைத்து, பெயரை அந்த பட்டியலில் உள்ள இடமான எண்ணுடன் மாற்றும். இது linear regression க்கு நல்லதல்ல, ஏனெனில் linear regression அந்த எண்ணை நேரடி மதிப்பாக எடுத்துக்கொண்டு, சில коэффициентுகளுடன் கூடிய கூட்டலைச் செய்கிறது. எங்கள் நிலைகளில், இந்த எண்ணும் விலை இடையேயான தொடர்பு நேர்காணல் அல்ல என்பதுவரை, இத்தெரிவு நல்லது அல்ல.
* **One-hot encoding** என்பது `Variety` நெடுவரிசையை 4 வித்தியாசமான நெடுவரிசைகளாக மாற்றும், ஒவ்வொரு விதத்திற்கும் ஒரு நெடுவரிசை இருக்கும். அந்த வரி அந்த வகையாக இருந்தால் 1, இல்லையெனில் 0 ஆகும். இதனால் linear regression-ல் நான்கு коэффициентுகள் இருப்பார்கள், ஒவ்வொரு மாதியன் விதத்திற்கும் "தொடங்கு விலை" அல்லது "மேலதிக விலை" என பொறுப்பாக இருக்கும்.

எப்படி வகையை one-hot encode செய்வது என்று கீழே காணலாம்:

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

one-hot encoded variety ஐ உள்ளீடு கொண்டு linear regression பயிற்சி பெற `X` மற்றும் `y` தரவை சரியாக தயார் செய்யவேண்டும்:

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```
  
மீதியானக் குறியிடல் மேலே பயன்படுத்திய Linear Regression பயிற்சிக்குத் தன்னோடே அதே மாதிரியானது. முயற்சி செய்தால், சராசரி சதுர பிழை சுமார் அதே அளவில் இருக்கும், ஆனால் coefficient of determination அதிக வேகம் (~77%) பெறப்படும். மேலும் நுட்பமான கணிப்புகள் பெற, பல categorical பண்புகளை மேலும் எண்ணிக்கையான பண்புகளுடன் (`Month` அல்லது `DayOfYear` போன்ற) சேர்த்து, `join` உபயோகித்து ஒன்றாக கூட்டலாம்:

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```
  
இங்கு மேலும் `City` மற்றும் `Package` வகையும் சேர்த்து, MSE 2.84 (10%), determination 0.94 கிடைத்துள்ளது!

## அனைத்தையும் ஒருங்கிணைத்தல்

சிறந்த மாதிரியை உருவாக்க, மேலே கொடுக்கப்பட்ட இணைந்த (one-hot encoded categorical + numeric) தரவை Polynomial Regression உடன் பயன்படுத்தலாம். இங்கே முழுமையான குறியீடு உள்ளது:

```python
# பயிற்சி தரவுகளை அமைக்கவும்
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# பயிற்சி மற்றும் சோதனை பாகங்களை பிரிக்கவும்
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# குழாய்க்குழியை அமைத்து பயிற்சி செய்யவும்
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# சோதனை தரவுகளுக்கான முன்னறிவிப்பை செய்யவும்
pred = pipeline.predict(X_test)

# MSE மற்றும் தீர்மானத்தை கணக்கிடவும்
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```
  
இது சுமார் 97% determination коэффициентுடன் மற்றும் MSE=2.23 (~8% பிழை) தர வேண்டும்.

| Model | MSE | Determination |  
|-------|-----|---------------|  
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |  
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |  
| `Variety` Linear | 5.24 (19.7%) | 0.77 |  
| All features Linear | 2.84 (10.5%) | 0.94 |  
| All features Polynomial | 2.23 (8.25%) | 0.97 |

🏆 நன்றாக செய்தீர்கள்! நீண்ட பாடத்தில் நான்கு Regression மாதிரிகள் உருவாக்கித் தேர்வு தரத்தை 97% வரை மேம்படுத்தினீர்கள். Regression இறுதி பகுதியில் நீங்கள் Logistic Regression பற்றி கற்றுக் கொண்டு வகைகளை தீர்மானிப்பீர்கள்.

---
## 🚀சவால்

இந்த நோட்புக்கில் பல மாறிலிகளை சோதித்து, பொறுத்து மாதிரி நுட்பத்திற்கு எப்படி ஏற்படுகிறது என்று காண்க.

## [பாட முடிந்த பிறகு விடைத் தேர்வு](https://ff-quizzes.netlify.app/en/ml/)

## பார்வை & சுயபடிப்பு

இந்த பாடத்தில் Linear Regression பற்றி கற்றோம். மற்ற முக்கியமான Regression வகைகளும் உள்ளன. Stepwise, Ridge, Lasso மற்றும் Elasticnet தொழில்நுட்பங்களைப் பற்றிக் கற்றுக்கொள்ளுங்கள். இன்னும் அதிகமாக கற்க விரும்புவோருக்கு [Stanford Statistical Learning பாடநெறி](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning) சாத்தியமாகும்.

## பணியாளர் வேலை

[Model உருவாக்குக](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**எச்சரிக்கை**:  
இந்த ஆவணம் AI மொழிபெயர்ப்பு சேவை [Co-op Translator](https://github.com/Azure/co-op-translator) மூலம் மொழிபெயர்க்கப்பட்டுள்ளது. நாங்கள் சரியான தன்மையை உறுதிப்படுத்த முயலுகிறோம், எனினும் தானியங்கி மொழிபெயர்ப்புகளில் தவறுகள் அல்லது பிழைகள் இருக்கக்கூடும் என்பதைக் கவனத்தில் கொள்ளவும். அசல் ஆவணம் அதன் சொந்த மொழியில் அதிகாரப்பூர்வ மூலமாகக் கருதப்பட வேண்டும். முக்கியமான தகவல்களுக்கு, தொழில்முறை மனித மொழிபெயர்ப்பு பரிந்துரைக்கப்படுகிறது. இந்த மொழிபெயர்ப்பை பயன்படுத்துவதால் ஏற்படும் தவறான புரிதல்கள் அல்லது தவறான விளக்கங்களுக்கு நாங்கள் பொறுப்பாக மாறமாட்டோம்.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->