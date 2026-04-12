### 🌐 बहुभाषी समर्थन

#### GitHub क्रियापदमार्फत समर्थन गरिएको (स्वचालित र सँधै अद्यावधिक)

> **स्थानीय रूपमा क्लोन गर्न चाहनुहुन्छ?**
>
> यो रिपोजिटरीले ५० भन्दा बढी भाषा अनुवादहरू समावेश गर्दछ जसले डाउनलोड आकारलाई उल्लेखनीय रूपमा बढाउँछ। अनुवाद बिना क्लोन गर्न, sparse checkout प्रयोग गर्नुहोस्:
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
> यसले तपाईंलाई कोर्स पूरा गर्न आवश्यक सबै कुरा धेरै छिटो डाउनलोडको साथ उपलब्ध गराउँछ।

#### हाम्रो समुदायमा सहभागी हुनुहोस्

हामीसँग एउटा Discord सिकाईसँगै AI श्रृंखला चलिरहेको छ, थप जान्न र हामीसँग जोडिनुहोस् [Learn with AI Series](https://aka.ms/learnwithai/discord) सेप्टेम्बर १८ - ३०, २०२५। तपाईं GitHub Copilot लाई डाटा विज्ञानका लागि प्रयोग गर्ने सुझाव र तरिकाहरू पाउनुहुनेछ।

# शुरुवात गर्दै

यी चरणहरू पछ्याउनुहोस्:
1. **रिपोजिटरी फोर्क गर्नुहोस्**: यस पृष्ठको दायाँ माथि कुनामा रहेको "Fork" बटन थिच्नुहोस्।
2. **रिपोजिटरी क्लोन गर्नुहोस्**: `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [यो कोर्सका लागि सबै अतिरिक्त स्रोतहरू हाम्रो Microsoft Learn संग्रहमा फेला पार्नुहोस्](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **मद्दत चाहिन्छ?** सामान्य स्थापना, सेटअप, र पाठ चलाउने समस्याहरू समाधानका लागि हाम्रो [समस्या समाधान मार्गदर्शिका](TROUBLESHOOTING.md) हेर्नुहोस्।

**[विद्यार्थीहरू](https://aka.ms/student-page)**, यो पाठ्यक्रम प्रयोग गर्न, पूरै रिपो तपाईंको GitHub खातामा फोर्क गर्नुहोस् र व्यायामहरू आफैंले वा समूहसँग पूरा गर्नुहोस्:

- पूर्व-वक्ता क्विजबाट सुरु गर्नुहोस्।
- व्याख्यान पढ्नुहोस् र गतिविधिहरू पूरा गर्नुहोस्, प्रत्येक ज्ञान जाँचमा रोक्नुहोस् र विचार गर्नुहोस्।
- समाधान कोड चलाउनुभन्दा पाठहरू बुझेर परियोजनाहरू बनाउन प्रयास गर्नुहोस्; तथापि त्यो कोड प्रत्येक परियोजना-केन्द्रित पाठका `/solution` फोल्डरहरूमा उपलब्ध छ।
- पश्च-वक्ता क्विज लिनुहोस्।
- चुनौती पूरा गर्नुहोस्।
- असाइनमेन्ट पूरा गर्नुहोस्।
- एक पाठ समूह पूरा गरेपछि, [चर्चा बोर्ड](https://github.com/microsoft/ML-For-Beginners/discussions) मा जानुहोस् र "उच्चारण गरेर सिक्नुहोस्" उपयुक्त PAT रुब्रिक भरि। 'PAT' भनेको प्रगति मूल्यांकन उपकरण हो जुन तपाईंको सिकाइलाई अगाडि बढाउनको लागि रुब्रिक हो। तपाईंले अरू PAT हरूसँग प्रतिक्रिया दिन सक्नुहुन्छ जसबाट हामी सँगै सिक्न सक्छौँ।

> थप अध्ययनका लागि, यी [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) मोड्युल र सिकाइ मार्गहरू पछ्याउन सिफारिस गरिन्छ।

**शिक्षकहरू**, हामीले यस पाठ्यक्रम प्रयोग गर्ने केही सुझावहरू [सहित गरेका छौं](for-teachers.md)।

---

## भिडियो वाकथ्रुहरू

केही पाठहरू छोटो फर्म भिडियोको रूपमा उपलब्ध छन्। तपाईं यी सबैलाई पाठहरूमा इनलाइन वा [Microsoft Developer YouTube च्यानलको ML for Beginners प्लेलिस्ट](https://aka.ms/ml-beginners-videos) मा हेर्न सक्नुहुन्छ तल चित्रमा क्लिक गरेर।

---

## टोलीसँग परिचय

---

## पेडागोकी

हामीले यो पाठ्यक्रम निर्माण गर्दा दुई शैक्षिक सिद्धान्तहरू छानेका छौं: यो हातमा काम गर्ने **प्रोजेक्ट-आधारित** हुनुपर्छ र यसमा **लगातार क्विजहरू** समावेश हुनुपर्छ। साथै, यस पाठ्यक्रमलाई एक साझा **थीम** दिन तयार गरिएको छ।

सामग्री प्रोजेक्टहरूसँग मेल खाने सुनिश्चित गरेर, विद्यार्थीहरूलाई थप संलग्न गरिन्छ र अवधारणाहरूको स्मरण बढ्छ। कक्षाको अघि सानो क्विज विद्यार्थीको मनस्थितिलाई विषय सिक्न प्रेरित गर्छ, जबकि कक्षापछि दोस्रो क्विज यसलाई थप स्मरणीय बनाउँछ। यो पाठ्यक्रम लचिलो र रमाइलो बनाउन डिजाइन गरिएको छ र पूरै वा भागमा लिन सकिन्छ। परियोजनाहरू शुरूमा साना हुन्छन् र १२ हप्ताको अन्त्यतिर जटिल बन्दै जान्छन्। यस पाठ्यक्रममा वास्तविक विश्वका ML आवेदकोंको पोस्टस्क्रिप्ट पनि समावेश छ, जुन अतिरिक्त क्रेडिट वा छलफलको आधारका रूपमा प्रयोग गर्न सकिन्छ।

> हाम्रो [Code of Conduct](CODE_OF_CONDUCT.md), [Contributing](CONTRIBUTING.md), [Translations](..), र [Troubleshooting](TROUBLESHOOTING.md) दिशानिर्देशहरू फेला पार्नुहोस्। हामी तपाईंको रचनात्मक प्रतिक्रिया स्वागत गर्दछौं!

## प्रत्येक पाठले समावेश गर्दछ

- वैकल्पिक स्केचनोट
- वैकल्पिक पूरक भिडियो
- भिडियो वाकथ्रु (केही पाठहरूमा मात्र)
- [पूर्व-वक्ता वार्मअप क्विज](https://ff-quizzes.netlify.app/en/ml/)
- लेखिएको पाठ
- परियोजना-आधारित पाठहरूका लागि, परियोजना निर्माण गर्ने चरण-दर-चरण मार्गनिर्देशन
- ज्ञान परीक्षणहरू
- चुनौती
- पूरक पढाइ
- असाइनमेन्ट
- [पश्च-वक्ता क्विज](https://ff-quizzes.netlify.app/en/ml/)
> **भाषाहरूको बारेमा एउटा नोट**: यी पाठहरू मुख्य रूपमा Python मा लेखिएका हुन्, तर धेरै R मा पनि उपलब्ध छन्। R पाठ पूरा गर्न, `/solution` फोल्डरमा जानुहोस् र R पाठहरूको खोजी गर्नुहोस्। तिनीहरूमा `.rmd` विस्तार हुन्छ जुन एक **R Markdown** फाइल प्रतिनिधित्व गर्छ, जसलाई साधारण रूपमा `code chunks` (R वा अन्य भाषाहरूका) र `YAML header` (जसले PDF जस्ता आउटपुटलाई कसरी फर्म्याट गर्ने दिशानिर्देशन गर्छ) को समावेशीकरणको रूपमा परिभाषित गर्न सकिन्छ `Markdown document` मा। यसकारण, यो डेटा विज्ञानको लागि एउटा उत्कृष्ट लेखन फ्रेमवर्कको रूपमा काम गर्छ किनकि यसले तपाईंलाई तपाईंको कोड, यसको आउटपुट, र तपाईंका विचारहरू Markdown मा लेख्न अनुमति दिँदै तिनीहरूलाई संयोजन गर्न अनुमति दिन्छ। थप रूपमा, R Markdown कागजातहरू PDF, HTML, वा Word जस्ता आउटपुट स्वरूपहरूमा रेंडर गर्न सकिन्छ।

> **कुइजहरूको बारेमा एउटा नोट**: सबै कुइजहरू [Quiz App folder](../../quiz-app) मा समावेश छन्, जम्मा ५२ कुइजहरू जसमा प्रत्येकमा तीन प्रश्नहरू हुन्छन्। ती पाठहरूबाट लिंक गरिएको छ तर कुइज एप्लिकेशन स्थानीय रूपमा चलाउन सकिन्छ; स्थानीय रूपमा होस्ट वा Azure मा वितरण गर्न `quiz-app` फोल्डरमा निर्देशनहरू पालना गर्नुहोस्।

| पाठ संख्या |                              विषय                              |                  पाठ समूह                  | सिकाइ उद्देश्य                                                                                                          |                                                            लिंक गरिएको पाठ                                                            |                  लेखक                  |
| :--------: | :------------------------------------------------------------: | :----------------------------------------: | ---------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------: |
|     ०१     |                मेशिन लर्निंग परिचय                |      [परिचय](1-Introduction/README.md)       | मेशिन लर्निंगका आधारभूत अवधारणाहरू सिक्नुहोस्                                                                                |                                             [पाठ](1-Introduction/1-intro-to-ML/README.md)                                             |                     मुहम्मद                     |
|     ०२     |                मेशिन लर्निंगको इतिहास                 |      [परिचय](1-Introduction/README.md)       | यस क्षेत्रको इतिहास सिक्नुहोस्                                                                                         |                                            [पाठ](1-Introduction/2-history-of-ML/README.md)                                            |                   जेन र एमी                   |
|     ०३     |                 निष्पक्षता र मेशिन लर्निंग                  |      [परिचय](1-Introduction/README.md)       | मेशिन लर्निंग मोडेलहरू बनाउने र लागू गर्ने क्रममा विद्यार्थीले विचार गर्नुपर्ने महत्वपूर्ण दार्शनिक मुद्दाहरू के छन्? |                                              [पाठ](1-Introduction/3-fairness/README.md)                                               |                      तोमोमी                      |
|     ०४     |                मेशिन लर्निंगका प्रविधिहरू                 |      [परिचय](1-Introduction/README.md)       | मेशिन लर्निंग अनुसन्धानकर्ताहरूले मेशिन लर्निंग मोडेलहरू बनाउन कुन प्रविधिहरू प्रयोग गर्छन्?                                                                       |                                          [पाठ](1-Introduction/4-techniques-of-ML/README.md)                                           |                   क्रिस र जेन                    |
|     ०५     |                   रिग्रेसन परिचय                   |        [रिग्रेसन](2-Regression/README.md)         | Python र Scikit-learn सँग रिग्रेसन मोडेलहरू बनाउन सुरु गर्नुहोस्                                                                  |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      जेन • एरिक वान्जाउ       |
|     ०६     |                उत्तर अमेरिका कुम्हडा मूल्य 🎃                |        [रिग्रेसन](2-Regression/README.md)         | मेशिन लर्निंगका लागि डेटा भिजुअलाइज र सफा गर्नुहोस्                                                                                  |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      जेन • एरिक वान्जाउ       |
|     ०७     |                उत्तर अमेरिका कुम्हडा मूल्य 🎃                |        [रिग्रेसन](2-Regression/README.md)         | रेखीय र बहुपद रिग्रेसन मोडेलहरू बनाउनुहोस्                                                                                   |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      जेन र दिमित्री • एरिक वान्जाउ       |
|     ०८     |                उत्तर अमेरिका कुम्हडा मूल्य 🎃                |        [रिग्रेसन](2-Regression/README.md)         | एक लॉजिस्टिक रिग्रेसन मोडेल बनाउनुहोस्                                                                                               |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      जेन • एरिक वान्जाउ       |
|     ०९     |                          वेब एप्लिकेसन 🔌                          |           [वेब एप](3-Web-App/README.md)            | तपाईंको प्रशिक्षित मोडेल प्रयोग गर्न वेब एप बनाउनुहोस्                                                                                       |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         जेन                          |
|     १०     |                 वर्गीकरण परिचय                 |    [वर्गीकरण](4-Classification/README.md)     | तपाईंको डेटा सफा, तयार, र भिजुअलाइज गर्नुहोस्; वर्गीकरण परिचय                                                            | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | जेन र क्यासी • एरिक वान्जाउ |
|     ११     |             स्वादिष्ट एशियाली र भारतीय भान्सा 🍜             |    [वर्गीकरण](4-Classification/README.md)     | वर्गीकर्ताहरूको परिचय                                                                                                     | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | जेन र क्यासी • एरिक वान्जाउ |
|     १२     |             स्वादिष्ट एशियाली र भारतीय भान्सा 🍜             |    [वर्गीकरण](4-Classification/README.md)     | थप वर्गीकर्ताहरू                                                                                                                | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | जेन र क्यासी • एरिक वान्जाउ |
|     १३     |             स्वादिष्ट एशियाली र भारतीय भान्सा 🍜             |    [वर्गीकरण](4-Classification/README.md)     | तपाईंको मोडेल प्रयोग गरी सिफारिस गर्ने वेब एप बनाउनुहोस्                                                                                    |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         जेन                          |
|     १४     |                   क्लस्टरिङ्ग परिचय                   |        [क्लस्टरिङ्ग](5-Clustering/README.md)         | तपाईंको डेटा सफा, तयार, र भिजुअलाइज गर्नुहोस्; क्लस्टरिङ्ग परिचय                                                                |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      जेन • एरिक वान्जाउ       |
|     १५     |              नाइजेरियाली संगीतिक रुचिहरू अन्वेषण 🎧              |        [क्लस्टरिङ्ग](5-Clustering/README.md)         | K-Means क्लस्टरिङ्ग विधि अन्वेषण गर्नुहोस्                                                                                           |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      जेन • एरिक वान्जाउ       |
|     १६     |        प्राकृतिक भाषा प्रशोधन परिचय ☕️         |   [प्राकृतिक भाषा प्रशोधन](6-NLP/README.md)    | सानो बोट निर्माण गरेर NLP का आधारभूत कुरा सिक्नुहोस्                                                                             |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       स्टिफेन                        |
|     १७     |                      सामान्य NLP कार्यहरू ☕️                      |   [प्राकृतिक भाषा प्रशोधन](6-NLP/README.md)    | भाषा संरचनासँग व्यवहार गर्दा आवश्यक सामान्य कार्य बुझेर तपाईंको NLP ज्ञान गहिरो बनाउनुहोस्                          |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       स्टिफेन                        |
|     १८     |             अनुवाद र भावना विश्लेषण ♥️              |   [प्राकृतिक भाषा प्रशोधन](6-NLP/README.md)    | जेन ऑस्टेनसँग गरिएको अनुवाद र भावना विश्लेषण                                                                             |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       स्टिफेन                        |
|     १९     |                  युरोपका रोमान्टिक होटलहरू ♥️                  |   [प्राकृतिक भाषा प्रशोधन](6-NLP/README.md)    | होटल समीक्षासँग भावना विश्लेषण १                                                                                         |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       स्टिफेन                        |
|     २०     |                  युरोपका रोमान्टिक होटलहरू ♥️                  |   [प्राकृतिक भाषा प्रशोधन](6-NLP/README.md)    | होटल समीक्षासँग भावना विश्लेषण २                                                                                         |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       स्टिफेन                        |
|     २१     |            समय श्रृंखला पूर्वानुमान परिचय             |        [समय श्रृंखला](7-TimeSeries/README.md)        | समय श्रृंखला पूर्वानुमान परिचय                                                                                         |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      फ्रान्सेस्का                       |
|     २२     | ⚡️ विश्व ऊर्जा प्रयोग ⚡️ - ARIMA सँग समय श्रृंखला पूर्वानुमान |        [समय श्रृंखला](7-TimeSeries/README.md)        | ARIMA सँग समय श्रृंखला पूर्वानुमान                                                                                              |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      फ्रान्सेस्का                       |
|     २३     |  ⚡️ विश्व ऊर्जा प्रयोग ⚡️ - SVR सँग समय श्रृंखला पूर्वानुमान  |        [समय श्रृंखला](7-TimeSeries/README.md)        | Support Vector Regressor सँग समय श्रृंखला पूर्वानुमान                                                                           |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       अनिर्बान                        |
|     २४     |             सुदृढीकरण शिक्षण परिचय             | [सुदृढीकरण शिक्षण](8-Reinforcement/README.md) | Q-Learning सँग सुदृढीकरण शिक्षण परिचय                                                                          |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        दिमित्री                        |
|     २५     |                 पिटरलाई बाघबाट बचाउन मद्दत गर्नुहोस्! 🐺                  | [सुदृढीकरण शिक्षण](8-Reinforcement/README.md) | सुदृढीकरण शिक्षण जिम                                                                                                      |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        दिमित्री                        |
|  पोस्टस्क्रिप्ट   |            वास्तविक जीवनका ML परिदृश्य र अनुप्रयोगहरू            |      [जंगली ML](9-Real-World/README.md)       | क्लासिकल ML का रोचक र प्रकट गर्ने वास्तविक जीवनका अनुप्रयोगहरू                                                               |                                             [पाठ](9-Real-World/1-Applications/README.md)                                              |                         टिम                         |
|  पोस्टस्क्रिप्ट   |            RAI ड्यासबोर्डको प्रयोग गरेर ML मा मोडेल डिबगिङ          |      [जंगली ML](9-Real-World/README.md)       | जिम्मेवार AI ड्यासबोर्ड कम्पोनेन्टहरू प्रयोग गरेर मेशिन लर्निंगमा मोडेल डिबगिङ                                                              |                                             [पाठ](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         रुथ याकुबु                       |

> [यस कोर्सका लागि सबै अतिरिक्त स्रोतहरू हाम्रो Microsoft Learn संग्रहमा खोज्नुहोस्](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## अफलाइन पहुँच

तपाईं यस दस्तावेजलाई अफलाइन [Docsify](https://docsify.js.org/#/) प्रयोग गरेर चलाउन सक्नुहुन्छ। यो रिपो फोर्क गर्नुहोस्, तपाईँको स्थानीय मेसिनमा [Docsify स्थापना गर्नुहोस्](https://docsify.js.org/#/quickstart), अनि यो रिपोको मूल फोल्डरमा जानुहोस् र `docsify serve` टाइप गर्नुहोस्। यो वेबसाइट तपाईंको स्थानीयहोस्टमा पोर्ट 3000 मा सेवा दिनेछ: `localhost:3000`.

## PDFहरू

पाठ्यक्रमको PDF लिंकसहितको फाइल [यहाँ](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf) पाउनुहोस्।


## 🎒 अन्य कोर्सहरू

हाम्रो टोलीले अन्य कोर्सहरू उत्पादन गर्दछ! जाँच गर्नुहोस्:

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j for Beginners](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js for Beginners](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain for Beginners](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agents
[![AZD for Beginners](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI for Beginners](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
---
 
### जेनेरेटिभ एआई सिरिज

---
 
### कोर सिकाइ

---
 
### कोपिलट सिरिज

## मद्दत प्राप्त गर्दै

यदि तपाईं अड्किनुहुन्छ वा एआई एपहरू बनाउनका बारेमा कुनै प्रश्नहरू छन् भने। सहपाठीहरू र अनुभवी विकासकर्ताहरूसँग MCP सम्बन्धी छलफलहरूमा सहभागी हुनुहोस्। यो एउटा सहायक समुदाय हो जहाँ प्रश्नहरू स्वागतयोग्य छन् र ज्ञान स्वतन्त्र रूपमा साझा गरिन्छ।

## थप सिकाइ सुझावहरू

- हरेक पाठपछि नोटबुकहरू पुनरावृत्ति गर्नुहोस् राम्रो बुझाइका लागि।
- आफैंले एल्गोरिदमहरू अभ्यास गरेर कार्यान्वयन गर्नुहोस्।
- सिकेका अवधारणाहरू प्रयोग गर्दै वास्तविक-विश्वका डाटासेटहरू अन्वेषण गर्नुहोस्।

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**अस्वीकरण**:  
यस दस्तावेजलाई AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) को प्रयोग गरी अनुवाद गरिएको छ। हामी सटीकता को लागि प्रयासरत छौं, तर कृपया जानकार हुनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा गलतिहरू हुनसक्छन्। मूल दस्तावेज यसको स्वदेशी भाषामा अधिकारिक स्रोत मानिनु पर्छ। महत्वपूर्ण जानकारीको लागि, पेशेवर मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार होइनौं।
<!-- CO-OP TRANSLATOR DISCLAIMER END -->