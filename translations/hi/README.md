### 🌐 बहुभाषी समर्थन

#### GitHub Action के माध्यम से समर्थित (स्वचालित और हमेशा अद्यतित)

> **स्थानीय रूप से क्लोन करना पसंद है?**
>
> इस रिपॉजिटरी में 50+ भाषा अनुवाद शामिल हैं जो डाउनलोड आकार को काफी बढ़ाते हैं। बिना अनुवाद के क्लोन करने के लिए, sparse checkout का उपयोग करें:
>
> **Bash / macOS / Linux:**
> ```bash
> git clone --filter=blob:none --sparse https://github.com/microsoft/ML-For-Beginners.git
> cd ML-For-Beginners
> git sparse-checkout set --no-cone '/*' '!translations' '!translated_images'
> ```
>
> **CMD (Windows):**
> ```cmd
> git clone --filter=blob:none --sparse https://github.com/microsoft/ML-For-Beginners.git
> cd ML-For-Beginners
> git sparse-checkout set --no-cone "/*" "!translations" "!translated_images"
> ```
>
> यह आपको उस सब कुछ देता है जिसकी आपको तेज़ डाउनलोड के साथ कोर्स पूरा करने के लिए ज़रूरत है।

#### हमारे समुदाय में शामिल हों

हमारे पास डिसॉर्ड में AI के साथ सीखने की श्रृंखला चल रही है, अधिक जानने और इसमें शामिल होने के लिए [Learn with AI Series](https://aka.ms/learnwithai/discord) पर जाएं, जो 18 - 30 सितंबर, 2025 को है। आपको GitHub Copilot का डेटा साइंस के लिए उपयोग करने के टिप्स और ट्रिक्स मिलेंगे।

![Learn with AI series](../../translated_images/hi/3.9b58fd8d6c373c20.webp)

# शुरुआती के लिए मशीन लर्निंग - एक पाठ्यक्रम

> 🌍 जब हम दुनिया की संस्कृतियों के माध्यम से मशीन लर्निंग का पता लगाते हैं तो दुनिया की यात्रा करें 🌍

Microsoft के Cloud Advocates एक 12-सप्ताह, 26-लक्षण पाठ्यक्रम प्रदान करते हैं जो पूरी तरह से **मशीन लर्निंग** के बारे में है। इस पाठ्यक्रम में, आप सीखेंगे कि कभी-कभी जिसे **क्लासिक मशीन लर्निंग** कहा जाता है, मुख्य रूप से Scikit-learn पुस्तकालय का उपयोग करके और गहरे लर्निंग से बचते हुए, जिसे हमारे [AI for Beginners' पाठ्यक्रम](https://aka.ms/ai4beginners) में कवर किया गया है। साथ ही, इन पाठों को हमारे ['Data Science for Beginners' पाठ्यक्रम](https://aka.ms/ds4beginners) के साथ जोड़ें।

दुनिया भर के डाटा पर इन क्लासिक तकनीकों को लागू करते हुए हमारे साथ यात्रा करें। प्रत्येक पाठ में पूर्व और पश्चात परीक्षण शामिल हैं, पूरा करने के लिए लिखित निर्देश, समाधान, असाइनमेंट और अधिक। हमारी परियोजना-आधारित शिक्षण विधि आपको निर्माण करते हुए सीखने की अनुमति देती है, जो नई कौशल सीखने का सिद्ध तरीका है।

**✍️ हमारे लेखकों का हार्दिक धन्यवाद** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu और Amy Boyd

**🎨 हमारे चित्रकारों को भी धन्यवाद** Tomomi Imura, Dasani Madipalli, और Jen Looper

**🙏 विशेष धन्यवाद 🙏 हमारे Microsoft Student Ambassador लेखकों, समीक्षकों, और सामग्री योगदानकर्ताओं को**, विशेष रूप से Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila, और Snigdha Agarwal

**🤩 हमारे R पाठों के लिए Microsoft Student Ambassadors Eric Wanjau, Jasleen Sondhi, और Vidushi Gupta को अतिरिक्त आभार!**

# आरंभ करना

इन चरणों का पालन करें:
1. **रिपॉजिटरी को फोर्क करें**: इस पृष्ठ के ऊपर-दाएं कोने में "Fork" बटन पर क्लिक करें।
2. **रिपॉजिटरी क्लोन करें**: `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [इस कोर्स के लिए सभी अतिरिक्त संसाधन हमारे Microsoft Learn संग्रह में खोजें](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **मदद चाहिए?** सामान्य इंस्टॉलेशन, सेटअप, और पाठ चलाने में समस्याओं के समाधान के लिए हमारे [Troubleshooting Guide](TROUBLESHOOTING.md) की जांच करें।


**[छात्रों](https://aka.ms/student-page)**, इस पाठ्यक्रम का उपयोग करने के लिए, पूरी रिपॉजिटरी को अपनी GitHub अकाउंट पर फोर्क करें और स्वयं या समूह के साथ अभ्यास पूर्ण करें:

- पूर्व व्याख्यान क्विज़ से शुरू करें।
- व्याख्यान पढ़ें और गतिविधियों को पूरा करें, प्रत्येक ज्ञान जांच पर रुककर चिंतन करें।
- समाधान कोड चलाने से अधिक, पाठों को समझकर परियोजनाएं बनाने का प्रयास करें; हालांकि यह कोड प्रत्येक परियोजना-केंद्रित पाठ के `/solution` फ़ोल्डरों में उपलब्ध है।
- पश्चात व्याख्यान क्विज़ लें।
- चुनौती पूरी करें।
- असाइनमेंट पूरा करें।
- एक पाठ समूह पूरा करने के बाद, [Discussion Board](https://github.com/microsoft/ML-For-Beginners/discussions) पर जाएं और उपयुक्त PAT रूपरेखा भरकर "उच्चारण से सीखें"। 'PAT' एक प्रगति मूल्यांकन उपकरण है जिसे आप सीखने को आगे बढ़ाने के लिए भरते हैं। आप अन्य PATs पर प्रतिक्रिया भी कर सकते हैं ताकि हम साथ सीख सकें।

> आगे अध्ययन के लिए, हम इन [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) मॉड्यूल और लर्निंग पाथ का अनुसरण करने की सलाह देते हैं।

**शिक्षकों**, हमने इस पाठ्यक्रम का उपयोग कैसे करें इसके लिए [कुछ सुझाव शामिल किए हैं](for-teachers.md)।

---

## वीडियो वॉकथ्रू

कुछ पाठ छोटे वीडियो रूप में उपलब्ध हैं। आप इन्हें पाठों के अंदर पा सकते हैं, या [Microsoft Developer YouTube चैनल पर ML for Beginners प्लेलिस्ट](https://aka.ms/ml-beginners-videos) पर नीचे दी गई छवि पर क्लिक करके देख सकते हैं।

[![ML for beginners banner](../../translated_images/hi/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## टीम से मिलें

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif द्वारा** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 परियोजना और इसे बनाने वाले लोगों के बारे में वीडियो के लिए ऊपर की छवि पर क्लिक करें!

---

## शिक्षणशास्त्र

इस पाठ्यक्रम का निर्माण करते समय हमने दो शिक्षण सिद्धांत चुने हैं: इसे प्रायोगिक **परियोजना-आधारित** बनाना और **बार-बार क्विज़** शामिल करना। इसके अलावा, इस पाठ्यक्रम में एक सामान्य **थीम** शामिल है जो इसे संलग्नता देता है।

सामग्री को परियोजनाओं से संरेखित कर यह प्रक्रिया छात्रों के लिए अधिक व्यस्त और अवधारणाओं के प्रतिधारण को बढ़ावा देने वाली बन जाती है। इसके अतिरिक्त, कक्षा से पहले एक कम जोखिम वाली क्विज़ विद्यार्थी की किसी विषय को सीखने की मंशा निर्धारित करती है, जबकि कक्षा के बाद दूसरी क्विज़ आगे की अवधारण सुनिश्चित करती है। यह पाठ्यक्रम लचीला और मजेदार होने के लिए डिज़ाइन किया गया है और इसे पूरी तरह या आंशिक रूप से लिया जा सकता है। परियोजनाएं छोटी शुरू होती हैं और 12-सप्ताह के चक्र के अंत तक अधिक जटिल हो जाती हैं। इस पाठ्यक्रम में मशीन लर्निंग के वास्तविक विश्व उपयोगों पर एक पोस्टस्क्रिप्ट भी शामिल है, जिसे अतिरिक्त क्रेडिट के रूप में या चर्चा के आधार के रूप में उपयोग किया जा सकता है।

> हमारे [आचार संहिता](CODE_OF_CONDUCT.md), [योगदान](CONTRIBUTING.md), [अनुवाद](..) और [समस्या निवारण](TROUBLESHOOTING.md) दिशा-निर्देश खोजें। हम आपकी रचनात्मक प्रतिक्रिया का स्वागत करते हैं!

## प्रत्येक पाठ में शामिल है

- वैकल्पिक स्केचनोट
- वैकल्पिक सहायक वीडियो
- वीडियो वॉकथ्रू (कुछ पाठों के लिए)
- [पूर्व व्याख्यान वार्मअप क्विज़](https://ff-quizzes.netlify.app/en/ml/)
- लिखित पाठ
- परियोजना-आधारित पाठों के लिए, परियोजना बनाने के चरण-दर-चरण मार्गदर्शक
- ज्ञान जांच
- एक चुनौती
- अतिरिक्त पठन सामग्री
- असाइनमेंट
- [पश्चात व्याख्यान क्विज़](https://ff-quizzes.netlify.app/en/ml/)

> **भाषाओं के बारे में एक नोट**: ये पाठ मुख्य रूप से Python में लिखे गए हैं, लेकिन कई R में भी उपलब्ध हैं। R पाठ पूरा करने के लिए, `/solution` फ़ोल्डर में जाएं और R पाठ देखें। इनमें .rmd एक्सटेंशन शामिल है जो एक **R Markdown** फ़ाइल का प्रतिनिधित्व करता है, जिसे सरलता से परिभाषित किया जा सकता है जैसे कि `कोड खंडों` (R या अन्य भाषाओं के) और एक `YAML हेडर` (जो आउटपुट जैसे PDF के स्वरूपण को निर्देशित करता है) के साथ एक `Markdown दस्तावेज़` एमबेडिंग। इस प्रकार, यह डेटा साइंस के लिए एक आदर्श लेखन ढांचा है क्योंकि यह आपको अपने कोड, उसका आउटपुट, और अपने विचार को Markdown में लिखने की अनुमति देता है। इसके अलावा, R Markdown दस्तावेज़ों को PDF, HTML या Word जैसे आउटपुट स्वरूपों में रेंडर किया जा सकता है।
> **क्विज़ के बारे में एक नोट**: सभी क्विज़ [Quiz App folder](../../quiz-app) में शामिल हैं, प्रत्येक में तीन प्रश्नों के 52 कुल क्विज़ हैं। इन्हें पाठ्यक्रम के भीतर लिंक किया गया है लेकिन क्विज़ ऐप को स्थानीय रूप से चलाया जा सकता है; स्थानीय होस्ट करने या Azure पर डिप्लॉय करने के लिए `quiz-app` फ़ोल्डर में निर्देशों का पालन करें। 

| Lesson Number |                             टॉपिक                              |                   पाठ्य समूह                   | सीखने के उद्देश्य                                                                                                             |                                                              लिंक किया गया पाठ                                                               |                        लेखक                        |
| :-----------: | :------------------------------------------------------------: | :---------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|      01       |                मशीन लर्निंग का परिचय                |      [परिचय](1-Introduction/README.md)       | मशीन लर्निंग के मूलभूत सिद्धांत सीखें                                                                                |                                             [पाठ](1-Introduction/1-intro-to-ML/README.md)                                             |                       मुहम्मद                       |
|      02       |                मशीन लर्निंग का इतिहास                 |      [परिचय](1-Introduction/README.md)       | इस क्षेत्र के पीछे का इतिहास सीखें                                                                                         |                                            [पाठ](1-Introduction/2-history-of-ML/README.md)                                            |                     जेन और एमी                      |
|      03       |                 निष्पक्षता और मशीन लर्निंग                  |      [परिचय](1-Introduction/README.md)       | जब छात्र ML मॉडल बनाते और लागू करते हैं, तो निष्पक्षता के महत्वपूर्ण दार्शनिक मुद्दे क्या हैं? |                                              [पाठ](1-Introduction/3-fairness/README.md)                                               |                        टोमोमी                        |
|      04       |                मशीन लर्निंग की तकनीकें                 |      [परिचय](1-Introduction/README.md)       | ML शोधकर्ता ML मॉडल बनाने के लिए किन तकनीकों का उपयोग करते हैं?                                                                       |                                          [पाठ](1-Introduction/4-techniques-of-ML/README.md)                                           |                    क्रिस और जेन                     |
|      05       |                   प्रतिगमन का परिचय                   |        [प्रतिगमन](2-Regression/README.md)         | प्रतिगमन मॉडल के लिए पाइथन और Scikit-learn के साथ शुरुआत करें                                                                  |         [पाइथन](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      जेन • एरिक वंजीउ       |
|      06       |                उत्तर अमेरिकी कद्दू के दाम 🎃                |        [प्रतिगमन](2-Regression/README.md)         | ML की तैयारी में डेटा को स्वरूपित और साफ़ करें                                                                                  |          [पाइथन](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      जेन • एरिक वंजीउ       |
|      07       |                उत्तर अमेरिकी कद्दू के दाम 🎃                |        [प्रतिगमन](2-Regression/README.md)         | रैखिक और बहुपद प्रतिगमन मॉडल बनाएं                                                                                   |        [पाइथन](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      जेन और दिमित्रि • एरिक वंजीउ       |
|      08       |                उत्तर अमेरिकी कद्दू के दाम 🎃                |        [प्रतिगमन](2-Regression/README.md)         | एक लॉजिस्टिक प्रतिगमन मॉडल बनाएं                                                                                               |     [पाइथन](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      जेन • एरिक वंजीउ       |
|      09       |                          एक वेब ऐप 🔌                          |           [वेब ऐप](3-Web-App/README.md)            | अपने प्रशिक्षित मॉडल का उपयोग करने के लिए एक वेब ऐप बनाएं                                                                                       |                                                 [पाइथन](3-Web-App/1-Web-App/README.md)                                                  |                         जेन                          |
|      10       |                 वर्गीकरण का परिचय                 |    [वर्गीकरण](4-Classification/README.md)     | अपने डेटा को साफ़ करें, तैयार करें और दृष्टिगत करें; वर्गीकरण का परिचय                                                            | [पाइथन](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | जेन और कैसी • एरिक वंजीउ |
|      11       |             स्वादिष्ट एशियाई और भारतीय व्यंजन 🍜             |    [वर्गीकरण](4-Classification/README.md)     | वर्गीकारकों का परिचय                                                                                                     | [पाइथन](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | जेन और कैसी • एरिक वंजीउ |
|      12       |             स्वादिष्ट एशियाई और भारतीय व्यंजन 🍜             |    [वर्गीकरण](4-Classification/README.md)     | और वर्गीकारक                                                                                                                | [पाइथन](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | जेन और कैसी • एरिक वंजीउ |
|      13       |             स्वादिष्ट एशियाई और भारतीय व्यंजन 🍜             |    [वर्गीकरण](4-Classification/README.md)     | अपने मॉडल का उपयोग करके एक अनुशंसा वेब ऐप बनाएं                                                                                    |                                              [पाइथन](4-Classification/4-Applied/README.md)                                              |                         जेन                          |
|      14       |                   क्लस्टरिंग का परिचय                   |        [क्लस्टरिंग](5-Clustering/README.md)         | अपने डेटा को साफ़ करें, तैयारी करें और दृष्टिगत करें; क्लस्टरिंग का परिचय                                                                |         [पाइथन](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      जेन • एरिक वंजीउ       |
|      15       |              नाइजीरियाई संगीत रुचियों की खोज 🎧              |        [क्लस्टरिंग](5-Clustering/README.md)         | K-Means क्लस्टरिंग विधि का अन्वेषण करें                                                                                           |           [पाइथन](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      जेन • एरिक वंजीउ       |
|      16       |        प्राकृतिक भाषा प्रसंस्करण का परिचय ☕️         |   [प्राकृतिक भाषा प्रसंस्करण](6-NLP/README.md)    | एक सरल बोट बनाकर NLP के मूल बातें सीखें                                                                             |                                             [पाइथन](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       स्टीफन                        |
|      17       |                      सामान्य NLP कार्य ☕️                      |   [प्राकृतिक भाषा प्रसंस्करण](6-NLP/README.md)    | भाषा संरचनाओं से निपटने के लिए आवश्यक सामान्य कार्यों को समझकर अपने NLP ज्ञान को गहरा करें                          |                                                    [पाइथन](6-NLP/2-Tasks/README.md)                                                     |                       स्टीफन                        |
|      18       |             अनुवाद और भावना विश्लेषण ♥️              |   [प्राकृतिक भाषा प्रसंस्करण](6-NLP/README.md)    | जेन ऑस्टेन के साथ अनुवाद और भावना विश्लेषण                                                                             |                                            [पाइथन](6-NLP/3-Translation-Sentiment/README.md)                                             |                       स्टीफन                        |
|      19       |                  यूरोप के रोमांटिक होटल ♥️                  |   [प्राकृतिक भाषा प्रसंस्करण](6-NLP/README.md)    | होटल समीक्षाओं के साथ भावना विश्लेषण 1                                                                                         |                                               [पाइथन](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       स्टीफन                        |
|      20       |                  यूरोप के रोमांटिक होटल ♥️                  |   [प्राकृतिक भाषा प्रसंस्करण](6-NLP/README.md)    | होटल समीक्षाओं के साथ भावना विश्लेषण 2                                                                                         |                                               [पाइथन](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       स्टीफन                        |
|      21       |            समय श्रृंखला पूर्वानुमान का परिचय             |        [समय श्रृंखला](7-TimeSeries/README.md)        | समय श्रृंखला पूर्वानुमान का परिचय                                                                                         |                                             [पाइथन](7-TimeSeries/1-Introduction/README.md)                                              |                      फ्रांसेस्का                       |
|      22       | ⚡️ विश्व विद्युत उपयोग ⚡️ - ARIMA के साथ समय श्रृंखला पूर्वानुमान |        [समय श्रृंखला](7-TimeSeries/README.md)        | ARIMA के साथ समय श्रृंखला पूर्वानुमान                                                                                              |                                                 [पाइथन](7-TimeSeries/2-ARIMA/README.md)                                                 |                      फ्रांसेस्का                       |
|      23       |  ⚡️ विश्व विद्युत उपयोग ⚡️ - SVR के साथ समय श्रृंखला पूर्वानुमान  |        [समय श्रृंखला](7-TimeSeries/README.md)        | Support Vector Regressor के साथ समय श्रृंखला पूर्वानुमान                                                                           |                                                  [पाइथन](7-TimeSeries/3-SVR/README.md)                                                  |                       अनिर्बान                        |
|      24       |             सुदृढीकरण अधिगम का परिचय             | [सुदृढीकरण अधिगम](8-Reinforcement/README.md) | Q-लर्निंग के साथ सुदृढीकरण अधिगम का परिचय                                                                          |                                             [पाइथन](8-Reinforcement/1-QLearning/README.md)                                              |                        दिमित्रि                        |
|      25       |                 पीटर को भेड़िये से बचाने में मदद करें! 🐺                  | [सुदृढीकरण अधिगम](8-Reinforcement/README.md) | सुदृढीकरण अधिगम जिम                                                                                                      |                                                [पाइथन](8-Reinforcement/2-Gym/README.md)                                                 |                        दिमित्रि                        |
|  उपसंहार   |            वास्तविक विश्व के ML परिदृश्य और अनुप्रयोग            |      [ML इन द वाइल्ड](9-Real-World/README.md)       | क्लासिकल ML के दिलचस्प और प्रकट करने वाले वास्तविक विश्व अनुप्रयोग                                                               |                                             [पाठ](9-Real-World/1-Applications/README.md)                                              |                         टीम                         |
|  उपसंहार   |            RAI डैशबोर्ड का उपयोग करके ML में मॉडल डीबगिंग          |      [ML इन द वाइल्ड](9-Real-World/README.md)       | जिम्मेदार AI डैशबोर्ड घटकों का उपयोग करके मशीन लर्निंग में मॉडल डीबगिंग                                                              |                                             [पाठ](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         रूथ याकुबू                       |

> [इस कोर्स के लिए हमारे Microsoft Learn संग्रह में सभी अतिरिक्त संसाधन खोजें](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## ऑफ़लाइन पहुँच

आप यह दस्तावेज़ [Docsify](https://docsify.js.org/#/) का उपयोग करके ऑफ़लाइन चला सकते हैं। इस रिपो को फ़ोर्क करें, अपने स्थानीय मशीन पर [Docsify स्थापित करें](https://docsify.js.org/#/quickstart), और फिर इस रिपो के रूट फोल्डर में `docsify serve` टाइप करें। वेबसाइट आपके स्थानीयहोस्ट पर पोर्ट 3000 पर सेवा करेगी: `localhost:3000`।

## पीडीएफ़

लिंक के साथ पाठ्यक्रम की पीडीएफ़ [यहाँ](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf) देखें।


## 🎒 अन्य कोर्स 

हमारी टीम अन्य कोर्स भी बनाती है! देखें:

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j for Beginners](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js for Beginners](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain for Beginners](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agents
[![AZD for Beginners](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI for Beginners](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![MCP for Beginners](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![AI Agents for Beginners](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Generative AI Series
[![Generative AI for Beginners](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generative AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generative AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generative AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### मुख्य शिक्षण
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### कॉपाइलट श्रृंखला
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## सहायता प्राप्त करना

यदि आप अटक जाते हैं या AI ऐप बनाने के बारे में कोई प्रश्न है। एमसीपी के बारे में चर्चा में साथी शिक्षार्थियों और अनुभवी डेवलपर्स से जुड़ें। यह एक सहायक समुदाय है जहां प्रश्नों का स्वागत है और ज्ञान स्वतंत्र रूप से साझा किया जाता है।

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

यदि आपके पास उत्पाद प्रतिपुष्टि या निर्माण के दौरान त्रुटियां हैं तो देखें:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## अतिरिक्त अध्ययन सुझाव

- बेहतर समझ के लिए प्रत्येक पाठ के बाद नोटबुक की समीक्षा करें।
- अपने आप एल्गोरिदम लागू करने का अभ्यास करें।
- सीखे गए सिद्धांतों का उपयोग करके वास्तविक दुनिया के डेटासेट खोजें।

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**अस्वीकरण**:
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। हम सटीकता के लिए प्रयासरत हैं, लेकिन कृपया ध्यान दें कि स्वचालित अनुवादों में त्रुटियाँ या अशुद्धियाँ हो सकती हैं। मूल भाषा में मौलिक दस्तावेज़ ही अधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सलाह दी जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।
<!-- CO-OP TRANSLATOR DISCLAIMER END -->