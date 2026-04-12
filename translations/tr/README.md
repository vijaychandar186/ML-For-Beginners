[![GitHub lisansı](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub katkıda bulunanlar](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub sorunları](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub çekme istekleri](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Hoşgeldiniz](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub izleyicileri](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub çatalları](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub yıldızları](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 Çok Dilli Destek

#### GitHub Action ile Desteklenmektedir (Otomatik & Her Zaman Güncel)

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arapça](../ar/README.md) | [Bengalce](../bn/README.md) | [Bulgarca](../bg/README.md) | [Birmanca (Myanmar)](../my/README.md) | [Çince (Basitleştirilmiş)](../zh-CN/README.md) | [Çince (Geleneksel, Hong Kong)](../zh-HK/README.md) | [Çince (Geleneksel, Makao)](../zh-MO/README.md) | [Çince (Geleneksel, Tayvan)](../zh-TW/README.md) | [Hırvatça](../hr/README.md) | [Çekçe](../cs/README.md) | [Danca](../da/README.md) | [Flemenkçe](../nl/README.md) | [Estonca](../et/README.md) | [Fince](../fi/README.md) | [Fransızca](../fr/README.md) | [Almanca](../de/README.md) | [Yunanca](../el/README.md) | [İbranice](../he/README.md) | [Hintçe](../hi/README.md) | [Macarca](../hu/README.md) | [Endonezce](../id/README.md) | [İtalyanca](../it/README.md) | [Japonca](../ja/README.md) | [Kannada](../kn/README.md) | [Kmerce](../km/README.md) | [Korece](../ko/README.md) | [Litvanca](../lt/README.md) | [Malayca](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepalce](../ne/README.md) | [Nijerya Pidgin](../pcm/README.md) | [Norveççe](../no/README.md) | [Farsça (Farsi)](../fa/README.md) | [Lehçe](../pl/README.md) | [Brezilya Portekizcesi](../pt-BR/README.md) | [Portekizce (Portekiz)](../pt-PT/README.md) | [Pencapça (Gurmukhi)](../pa/README.md) | [Rumence](../ro/README.md) | [Rusça](../ru/README.md) | [Sırpça (Kiril)](../sr/README.md) | [Slovakça](../sk/README.md) | [Slovence](../sl/README.md) | [İspanyolca](../es/README.md) | [Svahili](../sw/README.md) | [İsveççe](../sv/README.md) | [Tagalogca (Filipince)](../tl/README.md) | [Tamilce](../ta/README.md) | [Telugu](../te/README.md) | [Tayca](../th/README.md) | [Türkçe](./README.md) | [Ukraynaca](../uk/README.md) | [Urduca](../ur/README.md) | [Vietnamca](../vi/README.md)

> **Yerel olarak klonlamayı mı tercih edersiniz?**
>
> Bu depo, indirme boyutunu önemli ölçüde artıran 50'den fazla dil çevirisi içerir. Çeviriler olmadan klonlamak için sparse checkout kullanın:
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
> Bu, kursu tamamlamak için gereken her şeyi çok daha hızlı indirmenizi sağlar.
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### Topluluğumuza Katılın

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

AI ile öğrenme serimiz devam etmektedir, daha fazla bilgi edinip [AI ile Öğrenme Serisi](https://aka.ms/learnwithai/discord) adresinden 18 - 30 Eylül 2025 tarihleri arasında bize katılabilirsiniz. GitHub Copilot'un Veri Bilimi için kullanımına dair ipuçları ve püf noktaları edineceksiniz.

![AI ile öğrenme serisi](../../translated_images/tr/3.9b58fd8d6c373c20.webp)

# Yeni Başlayanlar için Makine Öğrenmesi - Bir Müfredat

> 🌍 Dünya kültürleri yoluyla Makine Öğrenmesini keşfederken dünyayı gezin 🌍

Microsoft'taki Bulut Savunucuları, tamamen **Makine Öğrenmesi** üzerine 12 haftalık, 26 derslik bir müfredat sunmaktan mutluluk duyar. Bu müfredatta, çoğunlukla Scikit-learn kütüphanesini kullanarak ve derin öğrenmeden kaçınarak, bazen **klasik makine öğrenmesi** olarak adlandırılan konuları öğreneceksiniz; derin öğrenme ise [Yenidoğanlar için AI müfredatımızda](https://aka.ms/ai4beginners) ele alınmaktadır. Ayrıca, bu dersleri ['Yeni Başlayanlar için Veri Bilimi müfredatıyla'](https://aka.ms/ds4beginners) eşleştirebilirsiniz!

Dünya genelindeki birçok bölgeden verilerle bu klasik teknikleri uygularken bizimle seyahat edin. Her ders öncesi ve sonrası sınavları, dersin tamamlanması için yazılı talimatlar, bir çözüm, bir görev ve daha fazlasını içerir. Proje tabanlı öğretim yöntemimiz, yeni becerilerin kalıcı olmasını sağlayan kanıtlanmış bir öğrenme yoludur.

**✍️ Yazarlarımıza içten teşekkürler** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu ve Amy Boyd

**🎨 İllüstratörlerimize teşekkürler** Tomomi Imura, Dasani Madipalli ve Jen Looper

**🙏 Özel teşekkürler 🙏 Microsoft Öğrenci Elçisi yazarlarımıza, inceleyicilerimize ve içerik katkıda bulunanlara**, özellikle Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila ve Snigdha Agarwal

**🤩 R derslerimiz için Microsoft Öğrenci Elçileri Eric Wanjau, Jasleen Sondhi ve Vidushi Gupta’ya ekstra teşekkürler!**

# Başlarken

Şu adımları izleyin:
1. **Depoyu Forklayın**: Bu sayfanın sağ üst köşesindeki "Fork" butonuna tıklayın.
2. **Depoyu Klonlayın**:   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [Bu kurs için tüm ek kaynakları Microsoft Learn koleksiyonumuzda bulun](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **Yardıma mı ihtiyacınız var?** Kurulum, ayar ve ders çalıştırmadaki yaygın sorunlar için [Sorun Giderme Rehberimizi](TROUBLESHOOTING.md) kontrol edin.

**[Öğrenciler](https://aka.ms/student-page)**, bu müfredatı kullanmak için tüm depoyu kendi GitHub hesabınıza fork’layın ve alıştırmaları kendi başınıza ya da bir grupla tamamlayın:

- Ders öncesi sınavla başlayın.
- Dersi okuyun ve her bilgi kontrol noktasında durup düşünerek etkinlikleri tamamlayın.
- Çözüme ait kodu çalıştırmak yerine dersleri anlayarak projeleri oluşturmayı deneyin; bu kod her proje odaklı dersin `/solution` klasörlerinde mevcuttur.
- Ders sonrası sınavı yapın.
- Meydan okumayı tamamlayın.
- Ödevi tamamlayın.
- Bir ders grubunu tamamladıktan sonra [Tartışma Panosunu](https://github.com/microsoft/ML-For-Beginners/discussions) ziyaret edin ve uygun PAT rubriğini doldurarak "yüksek sesle öğrenin". 'PAT', öğrenmeyi ilerletmek için doldurduğunuz bir İlerleme Değerlendirme Aracıdır. Ayrıca diğer PAT’lere tepki vererek birlikte öğrenebiliriz.

> Daha ileri çalışmalar için bu [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) modüllerini ve öğrenme yollarını takip etmenizi öneririz.

**Öğretmenler**, bu müfredatı kullanmanıza dair [bazı öneriler](for-teachers.md) ekledik.

---

## Video anlatımları

Bazı dersler kısa form video olarak mevcuttur. Tüm bunları derslerde satır içinde veya aşağıdaki görsele tıklayarak Microsoft Developer YouTube kanalındaki [Yeni Başlayanlar için Makine Öğrenmesi oynatma listesinde](https://aka.ms/ml-beginners-videos) bulabilirsiniz.

[![Yeni Başlayanlar için ML afişi](../../translated_images/tr/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## Takımımızla Tanışın

[![Tanıtım videosu](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif yapan** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 Proje ve yaratanları hakkında video için yukarıdaki görsele tıklayın!

---

## Pedagoji

Bu müfredatı oluştururken iki pedagojik ilke seçtik: uygulamalı **proje tabanlı** olmasını ve **sık sık sınavlar** içermesini sağlamak. Ayrıca, müfredatın bir bütünlük kazanması için ortak bir **tema** bulunmaktadır.

İçeriğin projelerle uyumlu olmasını sağlayarak süreç öğrenciler için daha ilgi çekici hale getirilir ve kavramların kalıcılığı artırılır. Ayrıca, dersten önceki düşük riskli bir sınav öğrencinin öğrenme niyetini belirlerken, dersten sonraki ikinci sınav öğrenmeyi pekiştirir. Bu müfredat esnek ve eğlenceli olacak şekilde tasarlanmıştır ve tamamı ya da bir kısmı alınabilir. Projeler küçük başlayıp 12 haftalık döngünün sonunda giderek karmaşıklaşır. Müfredat, gerçek dünyadaki ML uygulamaları hakkında ekstra kredi ya da tartışma temeli olarak kullanılabilecek bir son bölüm de içerir.

> [Davranış Kurallarımızı](CODE_OF_CONDUCT.md), [Katkıda Bulunma](CONTRIBUTING.md), [Çevirilerimizi](..) ve [Sorun Giderme](TROUBLESHOOTING.md) rehberlerini bulun. Yapıcı geri bildiriminizi memnuniyetle karşılıyoruz!

## Her ders içerir

- isteğe bağlı çizim notu
- isteğe bağlı destekleyici video
- video anlatımı (sadece bazı derslerde)
- [ders öncesi ısınma sınavı](https://ff-quizzes.netlify.app/en/ml/)
- yazılı ders
- proje tabanlı derslerde, projeyi inşa etmek için adım adım rehberler
- bilgi kontrol noktaları
- bir meydan okuma
- ek okumalar
- ödev
- [ders sonrası sınav](https://ff-quizzes.netlify.app/en/ml/)
> **Diller hakkında bir not**: Bu dersler ağırlıklı olarak Python ile yazılmıştır, ancak birçok ders R dilinde de mevcuttur. Bir R dersini tamamlamak için, `/solution` klasörüne gidip R derslerini arayabilirsiniz. Bunlar, `R Markdown` dosyasını temsil eden .rmd uzantısına sahiptir; bu, basitçe `kod parçacıklarının` (R veya diğer dillerden) ve çıktı formatlarını nasıl şekillendireceğini belirten `YAML başlığının` birleştirilmesiyle oluşturulan bir `Markdown belgesi` olarak tanımlanabilir. Bu nedenle, kodunuzu, çıktılarını ve düşüncelerinizi Markdown ile yazarak birleştirmenizi sağlayan, veri bilimi için örnek teşkil eden bir yazım çerçevesi olarak hizmet eder. Ayrıca, R Markdown belgeleri PDF, HTML veya Word gibi çıktı formatlarına dönüştürülebilir.

> **Quizler hakkında bir not**: Tüm quizler, toplam 52 adet üç soruluk quiz içeren [Quiz App klasöründe](../../quiz-app) bulunmaktadır. Derslerin içinden bağlantı verilmiştir, ancak quiz uygulaması yerel olarak da çalıştırılabilir; `quiz-app` klasöründeki talimatları izleyerek yerel olarak barındırabilir veya Azure'a dağıtabilirsiniz.

| Ders Numarası |                             Konu                              |                   Ders Gruplandırması                   | Öğrenme Hedefleri                                                                                                              |                                                              Bağlantılı Ders                                                               |                        Yazar                        |
| :-----------: | :------------------------------------------------------------: | :-----------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------: |
|      01       |                Makine öğrenimine giriş                         |      [Giriş](1-Introduction/README.md)                   | Makine öğrenmesinin temel kavramlarını öğrenin                                                                                 |                                             [Ders](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|      02       |                Makine öğrenmesinin tarihi                      |      [Giriş](1-Introduction/README.md)                   | Bu alanın arkasındaki tarihi öğrenin                                                                                           |                                            [Ders](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen ve Amy                       |
|      03       |                 Adalet ve makine öğrenmesi                     |      [Giriş](1-Introduction/README.md)                   | ML modelleri oluştururken ve uygularken öğrencilerin dikkate alması gereken önemli felsefi adalet konuları nelerdir?             |                                              [Ders](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|      04       |                Makine öğrenmesi teknikleri                     |      [Giriş](1-Introduction/README.md)                   | ML araştırmacılarının ML modelleri oluşturmak için kullandığı teknikler nelerdir?                                              |                                          [Ders](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris ve Jen                      |
|      05       |                   Regresyona giriş                             |        [Regresyon](2-Regression/README.md)               | Regresyon modelleri için Python ve Scikit-learn ile başlayın                                                                   |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|      06       |                Kuzey Amerika balkabağı fiyatları 🎃            |        [Regresyon](2-Regression/README.md)               | Makine öğrenmesi için veriyi görselleştirin ve temizleyin                                                                      |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|      07       |                Kuzey Amerika balkabağı fiyatları 🎃            |        [Regresyon](2-Regression/README.md)               | Doğrusal ve polinom regresyon modelleri oluşturun                                                                              |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen ve Dmitry • Eric Wanjau       |
|      08       |                Kuzey Amerika balkabağı fiyatları 🎃            |        [Regresyon](2-Regression/README.md)               | Lojistik regresyon modeli oluşturun                                                                                            |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|      09       |                          Bir Web Uygulaması 🔌                 |           [Web Uygulaması](3-Web-App/README.md)           | Eğitilmiş modelinizi kullanmak için bir web uygulaması oluşturun                                                               |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|      10       |                 Sınıflandırmaya giriş                           |    [Sınıflandırma](4-Classification/README.md)           | Verinizi temizleyin, hazırlayın ve görselleştirin; sınıflandırmaya giriş                                                       | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen ve Cassie • Eric Wanjau |
|      11       |             Lezzetli Asya ve Hint mutfakları 🍜                |    [Sınıflandırma](4-Classification/README.md)           | Sınıflandırıcılara giriş                                                                                                      | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen ve Cassie • Eric Wanjau |
|      12       |             Lezzetli Asya ve Hint mutfakları 🍜                |    [Sınıflandırma](4-Classification/README.md)           | Daha fazla sınıflandırıcı                                                                                                      | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen ve Cassie • Eric Wanjau |
|      13       |             Lezzetli Asya ve Hint mutfakları 🍜                |    [Sınıflandırma](4-Classification/README.md)           | Modelinizi kullanarak bir öneri web uygulaması oluşturun                                                                       |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|      14       |                   Kümelemeye giriş                              |        [Kümeleme](5-Clustering/README.md)                 | Verinizi temizleyin, hazırlayın ve görselleştirin; Kümelemeye giriş                                                           |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|      15       |              Nijerya Müzik Zevklerini Keşfetmek 🎧             |        [Kümeleme](5-Clustering/README.md)                 | K-Means kümeleme yöntemini keşfedin                                                                                            |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|      16       |        Doğal dil işleme giriş ☕️                               |   [Doğal Dil İşleme](6-NLP/README.md)                     | Basit bir bot oluşturarak NLP temel bilgileri öğrenin                                                                          |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|      17       |                      Yaygın NLP Görevleri ☕️                  |   [Doğal Dil İşleme](6-NLP/README.md)                     | Dil yapıları ile çalışırken gerekli olan yaygın görevleri anlamak için NLP bilginizi derinleştirin                             |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|      18       |             Çeviri ve duygu analizi ♥️                         |   [Doğal Dil İşleme](6-NLP/README.md)                     | Jane Austen ile çeviri ve duygu analizi                                                                                         |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|      19       |                  Avrupa'nın romantik otelleri ♥️               |   [Doğal Dil İşleme](6-NLP/README.md)                     | Otel yorumları ile duygu analizi 1                                                                                            |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|      20       |                  Avrupa'nın romantik otelleri ♥️               |   [Doğal Dil İşleme](6-NLP/README.md)                     | Otel yorumları ile duygu analizi 2                                                                                            |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|      21       |            Zaman serisi tahminine giriş                        |        [Zaman Serisi](7-TimeSeries/README.md)             | Zaman serisi tahminine giriş                                                                                                   |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|      22       | ⚡️ Dünya Güç Kullanımı ⚡️ - ARIMA ile zaman serisi tahmini     |        [Zaman Serisi](7-TimeSeries/README.md)             | ARIMA ile zaman serisi tahmini                                                                                                |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|      23       |  ⚡️ Dünya Güç Kullanımı ⚡️ - SVR ile zaman serisi tahmini      |        [Zaman Serisi](7-TimeSeries/README.md)             | Destek Vektör Regresörü ile zaman serisi tahmini                                                                             |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|      24       |             Pekiştirmeli öğrenmeye giriş                        | [Pekiştirmeli Öğrenme](8-Reinforcement/README.md)         | Q-Öğrenme ile pekiştirmeli öğrenmeye giriş                                                                                    |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|      25       |                 Peter'ın kurttan kaçmasına yardım edin! 🐺     | [Pekiştirmeli Öğrenme](8-Reinforcement/README.md)         | Pekiştirmeli öğrenme Gym                                                                                                      |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  Postscript   |            Gerçek dünya ML senaryoları ve uygulamaları          |      [Doğada ML](9-Real-World/README.md)                   | Klasik ML'nin ilginç ve aydınlatıcı gerçek dünya uygulamaları                                                                |                                             [Ders](9-Real-World/1-Applications/README.md)                                              |                         Takım                         |
|  Postscript   |            RAI kontrol panelini kullanarak ML modellerini hata ayıklama |      [Doğada ML](9-Real-World/README.md)                   | Responsible AI kontrol paneli bileşenlerini kullanarak Makine Öğrenmesinde model hata ayıklama                                |                                             [Ders](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [Bu kurs için tüm ek kaynakları Microsoft Learn koleksiyonumuzda bulun](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## Çevrimdışı erişim

Bu dokümantasyonu çevrimdışı kullanmak için [Docsify](https://docsify.js.org/#/) kullanabilirsiniz. Bu depoyu çatallayın, yerel makinenize [Docsify kurun](https://docsify.js.org/#/quickstart) ve ardından bu deponun kök klasöründe `docsify serve` yazın. Web sitesi localhost'unuzda 3000 portunda sunulacaktır: `localhost:3000`.

## PDF'ler

Konu anlatımını bağlantılar ile birlikte pdf formatında [burada](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf) bulabilirsiniz.


## 🎒 Diğer Kurslar 

Ekibimiz başka kurslar da üretmektedir! Göz atın:

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j for Beginners](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js for Beginners](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain for Beginners](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agents
[![AZD for Beginners](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI for Beginners](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için MCP](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için AI Ajanları](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Üretken AI Serisi
[![Başlangıç için Üretken AI](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Üretken AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Üretken AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Üretken AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### Temel Öğrenme
[![Başlangıç için ML](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için Veri Bilimi](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için AI](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için Siber Güvenlik](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Başlangıç için Web Geliştirme](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için IoT](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![Başlangıç için XR Geliştirme](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot Serisi
[![Yapay Zekâ Eşli Programlama için Copilot](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![C#/.NET için Copilot](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Macerası](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## Yardım Almak

Yapay zekâ uygulamaları geliştirirken takılırsanız veya herhangi bir sorunuz olursa. MCP hakkında tartışmalara katılmak için diğer öğrenenler ve deneyimli geliştiricilerle bir araya gelin. Sorulara açık ve bilginin özgürce paylaşıldığı destekleyici bir topluluktur.

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Ürün geri bildiriminiz veya geliştirme sırasında karşılaştığınız hatalar için ziyaret edin:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## Ek Öğrenme İpuçları

- Daha iyi anlamak için her dersten sonra not defterlerini gözden geçirin.
- Algoritmaları kendi başınıza uygulayarak pratik yapın.
- Öğrenilen kavramları kullanarak gerçek dünya veri setlerini keşfedin.

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Feragatname**:
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba sarf etsek de, otomatik çevirilerin hatalar veya yanlışlıklar içerebileceğini lütfen göz önünde bulundurun. Orijinal belge, kendi dilinde yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımı sonucu ortaya çıkabilecek herhangi bir yanlış anlama veya yanlış yorumdan dolayı sorumluluk kabul etmiyoruz.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->