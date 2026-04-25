# Scikit-learn ကို သုံးပြီး regression မော်ဒယ်တစ်ခု တည်ဆောက်ခြင်း - regression နည်းလမ်းလေး မျိုး

## အစပြုသူအတွက် မှတ်ချက်

Linear regression ကို **ကိန်းဂဏန်းတန်ဖိုး** (ဥပမာ၊ အိမ်ခြံမြေ စျးနှုန်း၊ အပူချိန်၊ သို့မဟုတ် အရောင်း) ကြိုတင်ခန့်မှန်းလိုသောအခါ အသုံးပြုသည်။  
ဒါဟာ input လက္ခဏာများနှင့် output အချက်အလက်တို့ကြား ဆက်နွယ်မှုကို အကောင်းဆုံးဖော်ပြနိုင်သော လိုင်းတစ်ခုကို ရှာဖွေခြင်းဖြင့် လည်ပတ်သည်။

ဒီသင်ခန်းမှာတော့ မတော်တဆင့် တိုက်ရိုက်ပညာရှင်ကျမ်းများလုပ်ရန်မသိသေးမီ ဆက်စပ် regression နည်းလမ်းများကိုရှာဖွေဖို့မတိုင်မီ အကြောင်းအရာနားလည်မှုအပေါ် အာရုံစိုက်မှာဖြစ်ပါတယ်။  
![Linear vs polynomial regression infographic](../../../../translated_images/my/linear-polynomial.5523c7cb6576ccab.webp)  
> [Dasani Madipalli](https://twitter.com/dasani_decoded) မှ infographic

## [ချဉ်းကပ်ရေးမေးခွန်း](https://ff-quizzes.netlify.app/en/ml/)

> ### [ဒီသင်ခန်းကို R ဖြင့်လည်းရနိုင်ပါသည်!](../../../../2-Regression/3-Linear/solution/R/lesson_3.html)
### မိတ်ဆက်

အခုထိ pumpkin စျေးနှုန်း dataset မှ နမူနာဒေတာများအပေါ် regression အကြောင်း သိရှိဖူးပြီး Matplotlib ဖြင့် အနုညာတစနစ် ကွက်တိ တည်ဆောက်ထားတာကိုကြည့်နိုင်ခဲ့ပါပြီ။  

ယခုမော်ဒယ်သင်ကြားမှုမှာ ML ရဲ့ regression ဆိုတာ ဘယ်လိုလုပ်ဆောင်ကြောင်း နက်ရှိုင်းစွာ လေ့လာမှာဖြစ်ပြီး၊ visualization က ဒေတာကိုနားလည်မှုရဖို့သင့်ကိုကူညီပေးပေမယ့် Machine Learning ရဲ့ အမှန်တကယ် ပြင်းထန်တဲ့အားကို သိမ်းဆည်းထားတဲ့ နေရာက _training models_ ဖြစ်ပါတယ်။ မော်ဒယ်များကို သမိုင်းအချက်အလက်များမှာ လေ့ကျင့်ကာ ဒေတာ ဆက်စပ်မှုများကို အလိုအလျောက် ဖမ်းဆီးနိုင်ပြီး မကြိုက်တတ်နေသေးသော အသစ်သော ဒေတာအတွက် ရလဒ်များခန့်မှန်းနိုင်ပါတယ်။  

ဒီသင်ခန်းမှာတော့ _မူလသော linear regression_ နှင့် _polynomial regression_ ဆိုတဲ့ regression အမျိုးအစား နှစ်မျိုးအကြောင်းကောင်းကောင်း နားလည်ကြမယ်၊ နည်းပညာများကို ဖက်ရှင်နည်းလမ်း တချို့နဲ့အတူ။ ဒီမော်ဒယ်တွေက pumpkin စျေးနှုန်းကို ကွဲပြားတဲ့ input အပေါ်မူတည်၍ ကြိုတင်ခန့်မှန်းပေးနိုင်ပါတယ်။  

[![ML for beginners - Understanding Linear Regression](https://img.youtube.com/vi/CRxFT8oTDMg/0.jpg)](https://youtu.be/CRxFT8oTDMg "ML for beginners - Understanding Linear Regression")

> 🎥 အပေါ်က ဓာတ်ပုံကို နှိပ်ပြီး linear regression အကြောင်းအကျဉ်းချုပ် ဗွီဒီယို မျှဝေကြည့်ပါ။

> ဒီသင်လမ်းညွှန်တစ်ခုလုံးမှာ နည်းနည်းသောသင်္ချာအသိပညာရှိသူ တွေအတွက်နဲ့ အခြားနယ်ပယ်မှလာသော ကျောင်းသားတွေအလွယ်တကူနားလည်စေချင်သောကြောင့် မှတ်ချက်များ၊ 🧮 သင်္ချာခေါ်ဆိုချက်များ၊ ပုံဆွဲနှင့် သင်ယူမှုကိရိယာများ ပါဝင်ပါတယ်။

### အဆင်သင့်ဖြစ်မှု

ယခုအချိန်မှာ pumpkin ဒေတာဖွဲ့စည်းမှုနှင့် မိတ်ဆက်ထားသင့်ပါတယ်။ ဒေတာကို ဒီသင်ခန်း ရဲ့ _notebook.ipynb_ ဖိုင်ထဲမှာ ရှိပြီး ရှင်းလင်းပြီးသား ဖြစ်ပါတယ်။ ဖိုင်ထဲမှာ pumpkin စျေးနှုန်းကို bushel တစ်ခုခုအလိုက် အသစ်သော ဒေတာဇယားတစ်ခုအဖြစ် ပြထားပါသည်။ Visual Studio Code ၏ kernel များမှာ ဒီ notebook များကို ပြေးနိုင်ခြင်းကို သေချာစေရပါ။

### ပြင်ဆင်မှု

အသိပေးခြင်းအနေဖြင့် ဒီဒေတာကို ဖတ်ယူရခြင်းသည် ဒေတာကို ဖြေရှင်းရန် ရည်ရွယ်သည်ကို သတိပြုပါ။  

- Pumpkin များဝယ်ရောက်ရန် အကောင်းဆုံးအချိန်က ဘယ်အချိန်လဲ?  
- မိသားစုတွေအတွက် ထုပ်ပိုးထားတဲ့ အသေးစား pumpkin တစ်အိတ် စျေးနှုန်း ဘယ်လောက်လဲ?  
- ထုတ်ပိုးမှု များကို half-bushel basket သို့မဟုတ် 1 1/9 bushel ဘောက်စ်ဖြင့် ဝယ်သင့်ပါသလား?  
ဒီဒေတာကို ဆက်လက်စူးစမ်းကြည့်ရအောင်။  

ပြီးခဲ့သည့်သင်ခန်းတွင် Pandas ဒေတာဖွဲ့စည်းမှု တစ်ခုကို ဖန်တီးပြီး မူရင်း dataset မှ အပိုင်းတစ်ပိုင်းဖြင့် ပြည့်စုံစွာ ပြင်ဆင်ပြီး စျေးနှုန်းကို bushel တစ်ခုအလိုက် စံပြန်းပြုလုပ်ခဲ့သည်။ သို့သော်၊ ဒီလိုလုပ်ခြင်းမကြောင့် datapoint ၄၀၀ ခန့် သာစုစည်းနိုင်ခဲ့ပြီး ရာသီဥတု ရာသီကာလများအတွက်သာ ဖြစ်ပါသည်။  

ဒီသင်ခန်းတွင် ပါဝင်သည့် notebook သို့ လေ့လာကြည့်ပါ။ ဒေတာကို အကြိုဖတ်ထားပြီး စတင် scatterplot တစ်ခုကို month အချက်အလက်များ ဖော်ပြထားပါတယ်။ နောက်ထပ်သန့်ရှင်းစင်ကြယ်မှုများအားဖြင့် ဒေတာ၏ သဘာဝအကြောင်းအရာ များကို အသေးစိတ် သိရှိနိုင်ဖို့ ကြိုးစားကြည့်ရအောင်။

## Linear regression လိုင်း

သင်သိရှိခဲ့သည့် Lesson 1 မှာ၊ linear regression ရဲ့ ရည်ရွယ်ချက်မှာ အောက်ပါအချက်များအတွက် လိုင်းတစ်ခု အကောင်းဆုံး ဆွဲဆောင်နိုင်ခြင်း ဖြစ်သည် #

- **အပြောင်းအလဲဆက်စပ်မှုကို ဖော်ပြခြင်း**။ အပြောင်းအလဲများကြား ဆက်သွယ်မှု ဖော်ပြရန်  
- **ခန့်မှန်းချက်လုပ်ခြင်း**။ ဒေတာသစ်အချက်များ အတွင်း ဒီလိုင်းနှင့် ဆက်စပ်နေမည့်နေရာကို တိကျစွာ ခန့်မှန်းရန်  

**Least-Squares Regression** ကိုသုံး၍ ဒီလိုင်းဆွဲခြင်း ပုံမှန်ဖြစ်သည်။ "Least-Squares" ဆိုသည်မှာ မော်ဒယ်အတွင်း စုစုပေါင်း အမှား(အချက်အလွဲ) များအား လျော့နည်းအောင်လုပ်ခြင်းလုပ်ငန်းစဉ်ဖြစ်သည်။ တစ်ခုချင်းစီသော ဒေတာအချက်များအတွက် ရှိနေသည့် စစ်မှန်သော အချက်နှင့် regression လိုင်းအကြား အလျားလိုင်းအကွာအဝေး (residual လို့ခေါ်သည်) ကိုတိုင်းတာသည်။  

အဆိုပါကွာခြားမှုများကို squared (ချယောင်းခြင်း) ကျင့်သုံးစို့ခုနှစ်ကြောင်းမှာ -  

1. **ကြီးသေးမှုကို ဦးစားပေးရန်**။ ကွာခြားချက် -၅ ကို +၅ နှင့်တူညီစေရန်လိုသည်။ squared သောကြောင့် အဖေါ်အဖြစ်မှ အားလုံးကို အပလာတန်ဖိုးပြောင်းလဲသည်။  

2. **အထူးကွာခြားချက်များကို ပိုဆိုးစေခြင်း**။ squared ခြင်းမျိုးက လွယ်ပေါ့ကွန်ယက်အမှားများအားပိုမိုထိခိုက်စေပြီး လိုင်းကို အလွဲကြီးနေသော ဒေတာအချက်များနီးစပ်ရန် မျှော်လင့်စေသည်။  

ပြီးမှ အားလုံးကို စုပေါင်းသည်။ ကျွန်ုပ်တို့ရည်မှန်းတဲ့လိုင်းက ဖော်ပြထားတဲ့ စုစုပေါင်း 성ရေမှာ အနည်းဆုံးဖြစ်မည့် လိုင်းဖြစ်ရမည်။ ဒါကြောင့် "Least-Squares" လို့ ခေါ်ပါတယ်။  

> **🧮 သင်္ချာပြပါ**  
>  
> ဒီလိုင်းကို _line of best fit_ လို့ခေါ်ပြီး [သင်္ချာဆိုင်ရာ ပုံစံဖြင့်](https://en.wikipedia.org/wiki/Simple_linear_regression) ဖော်ပြနိုင်သည် -  
>  
> ```
> Y = a + bX
> ```
>  
> `X` မှာ 'ရှင်းလင်းပြဿနာ ပြသသူ' (explanatory variable) ဖြစ်ပြီး `Y` ဟာ 'တာဝန်ခံပြဿနာ' (dependent variable) ဖြစ်သည်။ လိုင်း၏ စေ့ကွက် (slope) ကို `b` ဟုခေါ်ပြီး `a` သည် y-intercept ဖြစ်ပြီး `X=0` ဖြစ်စဉ်အတွင်း `Y` ရဲ့တန်ဖိုးကို ဆိုလိုသည်။
>
>![calculate the slope](../../../../translated_images/my/slope.f3c9d5910ddbfcf9.webp)
>
> ပထမဆုံး slope `b` ကိုတွက်ပါ။ [Jen Looper](https://twitter.com/jenlooper) ရေး infographic
>
> တခြားစကားများဖြင့် ပြောရမယ်ဆိုရင်၊ ကျွန်ုပ်တို့၏ pumpkin ဒေတာ မူလ မေးခွန်းအား "လစဉ် bushel တစ်ခုအတွက် pumpkin စျေးနှုန်းကို ခန့်မှန်းပါ" ဆိုပါက `X` သည်စျေးနှုန်းကို ကိုယ်စားပြုပြီး `Y` သည် အရောင်းလကို ကိုယ်စားပြုပါသည်။
>
>![complete the equation](../../../../translated_images/my/calculation.a209813050a1ddb1.webp)
>
> Y ကို တွက်ချက်ပါ။ $4 လောက်ပေးဝယ်ရင် April လို့ မှတ်ပါ! [Jen Looper](https://twitter.com/jenlooper) infographic
>
> ဒီလိုင်း တွက်ချက်ရာမှာ slope အပြင် y-intercept (ဆိုလိုသည်မှာ `X=0` ဖြစ်ဆုံးသော အချိန် `Y` တည်ရှိရာ နေရာ) ကို အလေးပေးဆင်ခြင်း လိုအပ်သည်။
>
> [Math is Fun](https://www.mathsisfun.com/data/least-squares-regression.html) ဝက်ဘ်ဆိုက်တွင် တန်ဖိုးများ တွက်ချက်နည်းကို ကြည့်ရှုနိုင်ပါတယ်။ နံပါတ်များ၏ တန်ဖိုးအစုံ မျိုး မျက်နှာပြင်ပေါ် မျဉ်းတွေလမ်းကြောင်းကို ရှုမျက် မိတ်ဆက်ရန် [Least-squares calculator](https://www.mathsisfun.com/data/least-squares-calculator.html) ကိုလည်း သွားကြည့်ပါ။

## Correlation

နောက်တစ်ခု နားလည်ရန် လိုအပ်သော စကားလုံးမှာ X နဲ့ Y တန်ဖိုးများအတွက် **Correlation Coefficient** ဖြစ်သည်။ scatterplot တစ်ခုမှာ ချက်ချင်း ဒီ coefficient ကို မြင်တွေ့နိုင်သည်။ points များ စည်းရုံး၍ စစ်မှန်တဲ့တိုင်းဟာ correlation မြင့်ပြီး ၊ scatter များမရှိပဲ ရှုပ်ထွေးသော scatter က correlation နည်းသည်။  

ကောင်းမွန်သော linear regression မော်ဒယ် အနေနဲ့ Least-Squares Regression နည်းဖြင့် correlation coefficient တန်ဖိုးဟာ 0 ထက် 1 အနီးကပ် ဖြစ်သည်။

✅ ဒီသင်ခန်းထောက်ခံ notebook ကို run ပြီး Month နှင့် Price scatterplot ကို ကြည့်ပါ။ Pumpkin အရောင်းအတွက် Month နှင့် Price အချက်များတွင် သင့်ရဲ့ scatterplot တွင် အမြင်ဖြင့် correlation မြင့်မမှန်သလဲ? `Month` အစား *day of the year* (နှစ်အစဥ်က လနေ့ရေ) သုံးပါက ပြောင်းလဲမှုရှိပါသလား?  

အောက်က code မှာ `new_pumpkins` ဆိုတဲ့ data frame တစ်ခုရရှိထားတယ်ဆိုပြီး ထပ်မံယူဆမယ် -  

ID | Month | DayOfYear | Variety | City | Package | Low Price | High Price | Price  
---|-------|-----------|---------|------|---------|-----------|------------|-------  
70 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  
71 | 9 | 267 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
72 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 18.0 | 18.0 | 16.363636  
73 | 10 | 274 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 17.0 | 17.0 | 15.454545  
74 | 10 | 281 | PIE TYPE | BALTIMORE | 1 1/9 bushel cartons | 15.0 | 15.0 | 13.636364  

> ဒေတာတိုက်ရိုက် သန့်ရှင်းဖို့ code ကို [`notebook.ipynb`](notebook.ipynb) မှာတွေ့နိုင်ပါတယ်။ ယခင်သင်ခန်းတွင် အတူတူ သန့်ရှင်းခြင်း လုပ်ဆောင်ပြီးပြီး၊ `DayOfYear` ကော်လံကို အောက်ပါ ဖော်ပြချက်အတိုင်း တွက်ချက်ထားပါတယ် -  

```python
day_of_year = pd.to_datetime(pumpkins['Date']).apply(lambda dt: (dt-datetime(dt.year,1,1)).days)
```
  
Linear regression ရဲ့ သင်္ချာနောက်ခံကို နားလည်ပြီးရင်တော့ ဟုတ်တယ် Regression မော်ဒယ်တစ်ခုဖန်တီးပြီး ဘယ် package က pumpkin ရဲ့ စျေးနှုန်းအကောင်းဆုံးမျိုး ဖြစ်မလဲ ခန့်မှန်းကြည့်မယ်။ လူတစ်ယောက် holiday pumpkin patch အတွက် ရောင်းဝယ်တဲ့ အချိန်မှာ package များကို မှန်ကန်စွာ ဝယ်ယူဖို့ အကြံပေးရန်လိုလိမ့်မယ်။

## Correlation ကို ရှာဖွေရန်

[![ML for beginners - Looking for Correlation: The Key to Linear Regression](https://img.youtube.com/vi/uoRq-lW2eQo/0.jpg)](https://youtu.be/uoRq-lW2eQo "ML for beginners - Looking for Correlation: The Key to Linear Regression")

> 🎥 အပေါ်ဓာတ်ပုံကိုနှိပ်၍ correlation အကြောင်းအကျဉ်းဗွီဒီယိုကြည့်ပါ။

ယခင်သင်ခန်းမှာ အသိပညာရထားတဲ့အတိုင်း တစ်လလျှင် စျေးနှုန်းပျမ်းမျှက ဒီလိုပုံစံဖြစ်သည် -  

<img alt="Average price by month" src="../../../../translated_images/my/barchart.a833ea9194346d76.webp" width="50%"/>

ဒါက correlation ရှိကြောင်း အဆိုပြုရာ၊ `Month` နဲ့ `Price` သို့မဟုတ် `DayOfYear` နဲ့ `Price` ဆက်နွယ်မှု ထောက်ထားရန် linear regression မော်ဒယ် လေ့ကျင့်ကြည့်နိုင်ပါတယ်။ အောက်မှာ scatterplot တစ်ခု ရှိပြီး "Day of Year" နှင့် "Price" ဆက်နွယ်မှုကို ဖေါ်ပြထားပါတယ် -  

<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/my/scatter-dayofyear.bc171c189c9fd553.webp" width="50%" />  

`corr` function ကိုသုံးပြီး correlation ရှိ/မရှိ စစ်ဆေးကြည့်ပါ -  

```python
print(new_pumpkins['Month'].corr(new_pumpkins['Price']))
print(new_pumpkins['DayOfYear'].corr(new_pumpkins['Price']))
```
  
Correlation က အသေးစားဖြစ်ပြီး `Month` အပေါ်မှာ -0.15, `DayOfMonth` အပေါ်မှာ -0.17 ဖြစ်သော်လည်း ခိုင်မာသော ဆက်နွယ်မှုတစ်ခုရှိနိုင်သည်။ Pumpkin အမျိုးအစားနှင့် သက်ဆိုင်သော စျေးနှုန်း အုပ်စုကွဲများရှိပါသည်။ အဲ့ဒီအကြောင်းကို မူတည်ပြီး pumpkin အမျိုးအစားတွေ မတူညီတဲ့အရောင်နဲ့ scatterplot ချထားကြည့်ပါ။ `scatter` function ကို `ax` parameter ဖြင့် အသုံးပြု၍ တစ်ခုတည်းရေးကွက်ပေါ်မှာ အချက်အားလုံးကို ပုံဖော်နိုင်သည် -  

```python
ax=None
colors = ['red','blue','green','yellow']
for i,var in enumerate(new_pumpkins['Variety'].unique()):
    df = new_pumpkins[new_pumpkins['Variety']==var]
    ax = df.plot.scatter('DayOfYear','Price',ax=ax,c=colors[i],label=var)
```
  
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/my/scatter-dayofyear-color.65790faefbb9d54f.webp" width="50%" />  

စုံစမ်းတွေ့ရှိချက်အရ အမျိုးအစားဟာ စျေးနှုန်းမှာ နေရာအများကြီးသက်ရောက်စေပြီး အရောင်းရက်စွဲထက် ပိုအရေးကြီးသည်။ Bar graph ဖြင့် ထောက်ပြထားသည် -  

```python
new_pumpkins.groupby('Variety')['Price'].mean().plot(kind='bar')
```
  
<img alt="Bar graph of price vs variety" src="../../../../translated_images/my/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />  

ယခုအချိန်မှာ pumpkin အမျိုးအစားတစ်မျိုးဖြစ်တဲ့ 'pie type' မှာ ကန်တော့လိုက်ပြီး အရောင်းရက်စွဲက စျေးနှုန်းမှာ သက်ရောက်မှု သိရှိကြည့်ပါ -  

```python
pie_pumpkins = new_pumpkins[new_pumpkins['Variety']=='PIE TYPE']
pie_pumpkins.plot.scatter('DayOfYear','Price') 
```
<img alt="Scatter plot of Price vs. Day of Year" src="../../../../translated_images/my/pie-pumpkins-scatter.d14f9804a53f927e.webp" width="50%" />  

`Price` နဲ့ `DayOfYear` အကြား correlation တွက်ချက်ရာ `corr` function သုံး၍ -0.27 ခန့်ရပြီး predictive model လေ့ကျင့်ရန် သေချာသည့် နေရာဖြစ်သည်။

> Linear regression မော်ဒယ် လေ့ကျင့်မှုမတိုင်ခင် ဒေတာ အပြည့်အဝ သန့်ရှင်းထားတာ အရေးကြီးသည်။ Missing values တွေ အနေနှင့် မရှိမဖြစ်လိုအပ်သည်။  
> ထို့ကြောင့် ဟိုခွက်ကွက်တွေ ပယ်ဖျက်သင့်ပါတယ် -

```python
pie_pumpkins.dropna(inplace=True)
pie_pumpkins.info()
```
  
အခြားနည်းလမ်းအနေနှင့် အလွတ်ရှိနေသောတန်ဖိုးများကို အဲဒီကော်လံရဲ့ ပျမ်းမျှတန်ဖိုးနဲ့ ဖြည့်စွက်နိုင်ပါတယ်။

## Simple Linear Regression

[![ML for beginners - Linear and Polynomial Regression using Scikit-learn](https://img.youtube.com/vi/e4c_UP2fSjg/0.jpg)](https://youtu.be/e4c_UP2fSjg "ML for beginners - Linear and Polynomial Regression using Scikit-learn")

> 🎥 အပေါ်ဓာတ်ပုံကို နှိပ်ပြီး Linear နှင့် Polynomial Regression အကြောင်း အကျဉ်းဗွီဒီယို ကြည့်ပါ။

Linear Regression မော်ဒယ် လေ့ကျင့်ရန် **Scikit-learn** ကို အသုံးပြုမည်ဖြစ်သည်။

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split
```
  
input တန်ဖိုးများ (features) နဲ့ output ရလဒ် (label ကို) များကို numpy array များအဖြစ် သီးခြားခွဲသည် -  

```python
X = pie_pumpkins['DayOfYear'].to_numpy().reshape(-1,1)
y = pie_pumpkins['Price']
```
  
> input data ကို Linear Regression package သဘောကျစေရန် `reshape` လုပ်ရန် ဖြစ်သည်။ Linear Regression ဟာ 2D-array အနေဖြင့် input လက်ခံပြီး array ၏ တန်းတစ်တန်းစီမှာ input feature တစ်ခုစီ ပါဝင်ရမည်။ ကျွန်ုပ်တို့မှာ input တစ်ခုသာရှိသဖြင့် N×1 အမျိုးအစား array လိုအပ်သည်။

ပြီးနောက် train နှင့် test data များ ခွဲရန် လိုအပ်သည်။ မော်ဒယ်ကို train ပြီးနောက် ဝင်ရောက် စစ်ဆေးနိုင်စေရန်ဖြစ်ပါသည်။  

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```
  
နောက်ဆုံး အမှန်တကယ် Linear Regression မော်ဒယ် လေ့ကျင့်ခြင်း code နှစ်ကြောင်းသာ လိုအပ်သည်။ `LinearRegression` သို့ အသင့်သတ်မှတ်ပြီး `fit` method ဖြင့် လေ့ကျင့်သည်။  

```python
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
```

`fit`-ပြီးပြီးနောက် `LinearRegression` အရာဝတ္ထုတွင် regression ၏ coefficients အားလုံးပါရှိပြီး၊ ထို coefficients များကို `.coef_` ပိုင်ဆိုင်မှုမှတဆင့် access လုပ်နိုင်သည်။ ကျွန်ုပ်တို့အခြေအနေတွင် coefficient တစ်ခုသာရှိပြီး၊ လျှင် `-0.017` အနားအနီးရှိသင့်သည်။ ၎င်းသည် စျေးနှုန်းများသည် အချိန်အလိုက် တစ်နေ့လျှင် လက်မ ၂ စင့်ခန့် ပျော့မှုတစ်ခုခုရှိသည့်အတိုင်း ပြသနေသည်။ `lin_reg.intercept_` ကို သုံးကာ regression ၏ Y-axis နှင့် အစပ်ကိုလည်း access လုပ်နိုင်ပြီး ကျွန်ုပ်တို့အတွက်နှစ်အစတွင်စျေးနှုန်းအနီး `21` ခန့်ရှိမည်ဖြစ်သည်။

မော်ဒယ်၏တိကျမှုကို ကြည့်ရန် မဟာဗျူဟာ dataset တွင် စျေးနှုန်းများကို ခန့်မှန်းပြီး ထိုခန့်မှန်းချက်များနှင့် မျှော်မှန်းထားသည့်တန်ဖိုးများ မည်မျှနီးကပ်သည်ကို ရှာဖွေရမည်။ ဤကို root mean square error (RMSE) မှ အသုံးပြု၍ တိုင်းတာနိုင်ပြီး၊ မျှော်မှန်းထားသည့်တန်ဖိုးနှင့် ခန့်မှန်းထားသည့်တန်ဖိုးတို့၏ ကွာခြားချက်များ၏ စတုရန်းပျားများ၏ ပျမ်းမျှ ၏ မျိုးကို ရွေ့လျား စတုရန်းမှောက်တန်ဖိုးဖြစ်သည်။

```python
pred = lin_reg.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test,pred))
print(f'RMSE: {rmse:3.3} ({rmse/np.mean(pred)*100:3.3}%)')
```

ကျွန်ုပ်တို့ error သည် ၂ ခန့်ရှိပြီး ဒါဟာ ~၁၇% ဖြစ်သည်။ မလွန်စွာကောင်းမှု မရှိပါ။ မော်ဒယ်အရည်အသွေး၏ အခြားပြသနာတစ်ခုမှာ **coefficient of determination** ဖြစ်ပြီး အောက်ပါအတိုင်း ရနိုင်သည်-

```python
score = lin_reg.score(X_train,y_train)
print('Model determination: ', score)
```
Value သည် 0 ဖြစ်ပါက မော်ဒယ်သည် input ဒေတာကို ထည့်သွင်းစဉ်းစားမှုမရှိပါ၊ အဲ့ဒါဟာ *အဆိုးဆုံး linear predictor* အဖြစ် အလုပ်လုပ်ပြီး ရလဒ်၏ ပျမ်းမျှတန်ဖိုးကို ပြသသည်။ 1 ဆိုသည်မှာ မျှော်မှန်းထားသည့် output များအားလုံးကို တိကျစွာ ခန့်မှန်းနိုင်သည်ကို ကိုယ်စားပြုသည်။ ကျွန်ုပ်တို့အတွက် coefficient သည် 0.06 အနည်းငယ်၏ နီးပါးဖြစ်ပြီး၊ အလွန်နိမ့်ပါသည်။

test dataset နှင့် regression လိုင်းကို တွဲ၍ ဖော်ပြနိုင်ပါတယ် မော်ဒယ်အလုပ်လုပ်ပုံကို ပိုမိုရှင်းလင်းစေရန်-

```python
plt.scatter(X_test,y_test)
plt.plot(X_test,pred)
```

<img alt="Linear regression" src="../../../../translated_images/my/linear-results.f7c3552c85b0ed1c.webp" width="50%" />

## Polynomial Regression

Linear Regression ၏ အမျိုးအစားတစ်ခုမှာ Polynomial Regression ဖြစ်သည်။ ကွဲပြားခြားနားသောအချိန်များတွင် variables များအကြားလိုင်းတူဆက်နွယ်မှုရှိနိုင်ပေမယ့် - ပန်းကန်၏ အရွယ်အစား များလာသည်နှင့်အမျှ စျေးနှုန်းမြင့်တက်သည် - တချို့အခြေအနေတွင် ဤဆက်နွယ်မှုများကို ပြင်သစ်လမ်းကြောင်း သို့မဟုတ် သတ်မှတ်ထားသောတန်းတူ အနားများဖြင့် ဖော်ပြ၍ မရနိုင်ပါ။

✅ [Polynomial Regression အသုံးပြုနိုင်သည့် အခြား ဥပမာများ](https://online.stat.psu.edu/stat501/lesson/9/9.8)

Date နှင့် Price အချက်အလက်တို့ ညီမျှမှုကို ထပ်မံကြည့်ပါ။ Scatterplot သည် လိုင်းတစ်လမ်းဖြင့် အသေးစိတ် သုံးသပ်ရန် လိုအပ်သည် ဟုတ်သလား? စျေးနှုန်းများ မပြေပဲ ကွဲပြားခြားနားနိုင်အောင်။ ဤအဖြစ်တွင် polynomial regression ကို စမ်းသပ်နိုင်သည်။

✅ Polynomial များမှာ တစ်ခု သို့မဟုတ် ၎င်းထက်ပိုသော variables နှင့် coefficients ပါဝင်သည့် သင်္ချာရေးသားချက်များဖြစ်သည်။

Polynomial regression သည် nonlinear data ကို ပိုပိုက်ကာစွာသင့်တော်အောင် curved လိုင်း တစ်ခု ဖန်တီးသည်။ ကျွန်ုပ်တို့အတွက် squared `DayOfYear` variable ကို input data ထဲသို့ ထည့်သွင်းပါက parabolic curve အမျိုးအစားဖြင့် data ကို လိုက်ဖက်နိုင်ပြီး နှစ်အတွင်း တစ်နေရာတည်းတွင် အနည်းဆုံးရှိမည်။

Scikit-learn တွင် [pipeline API](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.make_pipeline.html?highlight=pipeline#sklearn.pipeline.make_pipeline) ကိုများသည် data processing အဆင့်ခွဲခြားမှုများကို တွဲဖက် အသုံးပြုနိုင်ရန်အတွက် ပါဝင်သည်။ **pipeline** သည် **estimators** များ၏ လွှဲစရာဖြစ်သည်။ ကျွန်ုပ်တို့အနေဖြင့် ပထမဆုံး polynomial features များကို မော်ဒယ်ထဲသို့ ထည့်သွင်းပြီး regression သင်ကြားမှုလုပ်မည့် pipeline တစ်ခုဖန်တီးမည်။

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())

pipeline.fit(X_train,y_train)
```
  
`PolynomialFeatures(2)` ကိုသုံးခြင်းဖြင့် input data ထဲမှ ဒုတိယကုန်လီပေါ်မီယနယ်များအားလုံး ပါဝင်သည်။ ကျွန်ုပ်တို့အတွက် သည်မှာ `DayOfYear`<sup>2</sup> တစ်ခုသာဖြစ်မည်၊ ဒါပေမယ့် X နှင့် Y တို့ရှိပါက X<sup>2</sup>, XY နှင့် Y<sup>2</sup> ကိုလည်း ထည့်သွင်းသည်။ ပိုမိုမြင့်မားသောကုန်လီပေါ်မီယနယ်များကိုလည်း အသုံးပြုနိုင်သည်။

Pipeline များကို မူရင်း `LinearRegression` object များနှင့်တူညီစွာ အသုံးပြုနိုင်၍၊ pipeline ကို `fit` ပြီး `predict` ဖြင့် ခန့်မှန်းချက်များ ရနိုင်သည်။ ဤနေရာတွင် test data နှင့် approximation curve ကို ဖော်ပြထားသည်-

<img alt="Polynomial regression" src="../../../../translated_images/my/poly-results.ee587348f0f1f60b.webp" width="50%" />

Polynomial Regression ဖြင့် MSE သာနည်းနည်းချိုသာ၍ determination မြင့်တက်သည်၊ သို့သော် ထူးခြားမှုမရှိသေးပါ။ အခြား features များကိုလည်း ပေါင်းစပ်စဉ်းစားရမည်။

> မျက်နှာတစ်ခုအနေဖြင့် အနည်းဆုံး pumpkin စျေးနှုန်းများသည် Halloween အားအနီးတွင် တွေ့ရှိနေရသည်။ ၎င်းအကြောင်း ဘယ်လိုရှင်းလင်းမည်နည်း? 

🎃 ဂုဏ်ယူပါတယ်၊ သင်သည် pumpkin မှာ pie အမျိုးအစား စျေးနှုန်းခန့်မှန်းနိုင်သည့် မော်ဒယ်တစ်ခု ဖန်တီးနိုင်လိုက်ပြီ။ Pumpkin အမျိုးအစားအားလုံးအတွက် ထပ်မံပြုလုပ်ပါက ပင်ပန်းနွမ်းနယ်လိမ့်မည်။ ယခု Pumpkin အမျိုးအစားအား မော်ဒယ်တွင် ထည့်သွင်းစဥ်းစားမည့် နည်းလမ်းကို လေ့လာကြမည်။

## Categorical Features

ကောင်းမွန်သောကမ္ဘာကြီးထဲ၌ pumpkin အမျိုးအစားအလိုက် စျေးနှုန်းများကို တစ်ခုတည်းသောမော်ဒယ်ဖြင့် ခန့်မှန်းနိုင်ရန် ဆန္ဒရှိကြသည်။ သို့ပေမယ့် `Variety` ကော်လမ်သည် `Month` ကဲ့သို့ ကော်လမ်များနှင့် မတူဘဲ နံပါတ်မဟုတ်သော တန်ဖိုးများပါရှိသည်။ ဒီလိုကော်လမ်များကို **categorical** ဟုခေါ်သည်။

[![ML for beginners - Categorical Feature Predictions with Linear Regression](https://img.youtube.com/vi/DYGliioIAE0/0.jpg)](https://youtu.be/DYGliioIAE0 "ML for beginners - Categorical Feature Predictions with Linear Regression")

> 🎥 အပေါ်ရှိ ဇာတ်ပုံကို နှိပ်၍ categorical features အသုံးပြုခြင်း၏ အကျဉ်းချုပ် ဗီဒီယိုကို ကြည့်ရှုနိုင်ပါသည်။

Variety အလိုက် စျေးနှုန်းပျမ်းမျှသည် ဤအတိုင်း ဖြစ်ပါသည်-

<img alt="Average price by variety" src="../../../../translated_images/my/price-by-variety.744a2f9925d9bcb4.webp" width="50%" />

Variety ကို စဉ်းစားရန်အတွက် ပထမဦးစွာ နံပါတ်တန်ဖိုးသို့ သို့မဟုတ် **encode** ပြုလုပ်ရန် လိုအပ်သည်။ လုပ်နည်းများမှာ-

* ရိုးရိုး **နံပါတ်အမှတ်ပေးခြင်း** သည် variété များကို စာရင်းတစ်ခုဖန်တီးပြီး variety နာမည်ကို စာရင်းအတွင်းရှိ အညွှန်းနံပါတ်ဖြင့် အစားထိုးသည်။ အကြောင်းက linear regression အတွက် အကောင်းဆုံးမဟုတ်ပါ၊ မကြာခဏ linear regression သည် index နံပါတ်၏ နံပါတ်တန်ဖိုးကို အသုံးပြုပြီး ရလဒ်ထဲ ထည့်သွင်းခြင်းဖြင့် coefficient တစ်ခုနှင့် မြှောက်သည်။ ကျွန်ုပ်တို့အနေဖြင့် index နံပါတ်နှင့် စျေးနှုန်းအကြား ဆက်စပ်မှုသည် ရိုးရှင်း linear မဟုတ်ပေ။
* **One-hot encoding** သည် `Variety` ကော်လမ်ကို စားကြီးသုံးကော်လမ်အစားထိုးပေးပြီး၊ ကြိုက်သော variety အတန်းတစ်ခုစီအတွက် ကော်လမ်တစ်ခုစီဖန်တီးသည်။ အတန်းအလိုက် အဆိုပါ variety ရှိပါက ကော်လမ်တွင် `1`၊ မရှိပါက `0` ပါဝင်သည်။ ထို့ကြောင့် linear regression တွင် pumpkin variety တစ်ခုစီအတွက် coefficient ၄ ခုရှိပြီး၊ ၎င်းတွင် အစောပိုင်းစျေးနှုန်း(သို့မဟုတ် "အပိုစျေး") အတွက် တာဝန်ရှိသည်။

Variety ကို one-hot encode ပြုလုပ်သည့်နည်းလမ်းကို အောက်ပါကုဒ်က ဖော်ပြထားသည်-

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

One-hot encoded variety ကို input အဖြစ်သုံးပြီး linear regression ကို သင်ကြားရာတွင် `X` နှင့် `y` ဒေတာများကို မှန်မှန်ကန်ကန် သတ်မှတ်ရုံဖြစ်သည်-

```python
X = pd.get_dummies(new_pumpkins['Variety'])
y = new_pumpkins['Price']
```

Linear Regression သင်ကြားခြင်းတွက် အခြားကုဒ်ပိုင်းများထက်မတူဘဲမဟုတ်ပါ၊ မူလသင်ကြားထားသည့်ပုံစံနှင့် တူညီသည်။ စမ်းသပ်ပါက mean squared error ပြောင်းလဲမှုမပြင်းထန်ပေ၊ determination coefficient သည် ၀.၇၇ ခန့် ရရှိမည်။ ပိုမိုတိကျသော ခန့်မှန်းချက်များ ရယူရန် categorical features များနှင့် numeric features များ (ဥပမာ- `Month`, `DayOfYear`) ကိုပါ သွင်းစဉ်းစားနိုင်သည်။ feature များကို တစ်စုစည်း array တစ်ခုတွင် ပေါင်းစပ်ဖို့ `join` ကို အသုံးပြုနိုင်သည်-

```python
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']
```

ဤတွင် `City` နှင့် `Package` အမျိုးအစားများလည်း သွင်းစဉ်းစားပြီး၊ MSE 2.84 (၁၀%) နှင့် determination 0.94 ထိရရှိပါသည်။

## စုပေါင်းပြီး မော်ဒယ်ကို ဖန်တီးခြင်း

အကောင်းဆုံးမော်ဒယ်ဖန်တီးရန် အပေါ်ပါ ဥပမာမှ Categorical (one-hot encoded) နှင့် numeric ဒေတာများကို Polynomial Regression နှင့် တွဲဖက်၍ အသုံးပြုနိုင်သည်။ အဆင်ပြေစေရန် မူလကုဒ် here ပါ-

```python
# လေ့ကျင့်ရေးဒေတာကို စီစဉ်ပါ
X = pd.get_dummies(new_pumpkins['Variety']) \
        .join(new_pumpkins['Month']) \
        .join(pd.get_dummies(new_pumpkins['City'])) \
        .join(pd.get_dummies(new_pumpkins['Package']))
y = new_pumpkins['Price']

# လေ့ကျင့်မှုနှင့် စမ်းသပ်မှု ခွဲခြားပါ
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# ပိုင်းလိုင်းကို အသင့်ပြင်ပြီး လေ့ကျင့်ပါ
pipeline = make_pipeline(PolynomialFeatures(2), LinearRegression())
pipeline.fit(X_train,y_train)

# စမ်းသပ်ဒေတာအတွက် ဖော်ထုတ်ဆောင်ရွက်မှု
pred = pipeline.predict(X_test)

# MSE နှင့် သတ်မှတ်ချက်ကို ချည်းကပ်ပါ
mse = np.sqrt(mean_squared_error(y_test,pred))
print(f'Mean error: {mse:3.3} ({mse/np.mean(pred)*100:3.3}%)')

score = pipeline.score(X_train,y_train)
print('Model determination: ', score)
```

ဒါမှတစ်ပါး determination coefficient ကို ၉၇% ခန့်၊ MSE=2.23 (~၈%ခန့် မျှော်မှန်းချက် အချက်အလက်အမှား) ရရှိမည်။

| Model | MSE | Determination |
|-------|-----|---------------|
| `DayOfYear` Linear | 2.77 (17.2%) | 0.07 |
| `DayOfYear` Polynomial | 2.73 (17.0%) | 0.08 |
| `Variety` Linear | 5.24 (19.7%) | 0.77 |
| All features Linear | 2.84 (10.5%) | 0.94 |
| All features Polynomial | 2.23 (8.25%) | 0.97 |

🏆 အလုပ်ကောင်းပါတယ်! သင်သည် သင်ခန်းစာတစ်ခုအတွင်း Regression မော်ဒယ် (၄) များ ဖန်တီးပြီး မော်ဒယ်အရည်အသွေးကို ၉၇% ဆုတ်ခဲ့ပြီ။ Regression ၏ နောက်ဆုံးပိုင်းတွင် Logistic Regression အကြောင်း လေ့လာ၍ ကဏ္ဍ သတ်မှတ်ခြင်းကို သင်ယူမည်ဖြစ်သည်။

---
## 🚀စိန်ခေါ်မှု

ဤ notebook တွင် မတူညီသော variable များစမ်းသပ်၍ correlation နှင့် မော်ဒယ်တိကျမှု ဆက်စပ်မှုကို တွေ့ပါ။

## [သင်ခန်းစာ အပေါ်တွင် စစ်တမ်း](https://ff-quizzes.netlify.app/en/ml/)

## ပြန်လည်သုံးသပ်ရန် နှင့် ကိုယ်တိုင်လေ့လာရန်

ဤသင်ခန်းစာတွင် Linear Regression အကြောင်း သင်ယူခဲ့သည်။ အခြား အရေးကြီးသော Regression အမျိုးအစားများလည်းရှိပါသည်။ Stepwise, Ridge, Lasso, နှင့် Elasticnet နည်းများကို အသေးစိတ်လေ့လာပါ။ ပိုမိုသိရှိရန် [Stanford Statistical Learning course](https://online.stanford.edu/courses/sohs-ystatslearning-statistical-learning) ကို အကြံပြုသည်။

## အလုပ်လက်တွေ့

[Model တစ်ခု တည်ဆောက်ရန်](assignment.md)

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**ကာကွယ်ချက်**  
ဤစာရွက်စာတမ်းကို AI ဘာသာပြန် စနစ်ဖြစ်သော [Co-op Translator](https://github.com/Azure/co-op-translator) မှ အသုံးပြု၍ ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှန်ကန်မှုအတွက် ကြိုးစားသော်လည်း အလိုအလျှောက်ဘာသာပြန်ခြင်းများတွင် အမှားများ သို့မဟုတ် မှားယွင်းချက်များ ပါဝင်နိုင်ခြင်းကို ကျေးဇူးပြုပြီး သိရှိထားရပါမည်။ စာရွက်စာတမ်းပိုင်ဆိုင်ခြင်းနှင့် အခိုင်အမာအချက်အလက်အဖြစ် မူလစာရွက်စာတမ်းကို သတ်မှတ်သည်။ အရေးကြီးသော အချက်အလက်များအတွက် အတတ်ပညာရှင် လူသား ဘာသာပြန်ခြင်းကို အကြံပြုပါသည်။ ဤဘာသာပြန်ချက်ကို အသုံးပြုရာအတွင်း ဖြစ်ပေါ်လာသော လွဲမှားခြင်းများ သို့မဟုတ် သဘောနားလည်မှုမှားယွင်းမှုများအတွက် ကျွန်ုပ်တို့မှာ တာဝန်မရှိပါ။
<!-- CO-OP TRANSLATOR DISCLAIMER END -->