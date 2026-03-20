[![GitHub license](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 Monikielinen tuki

#### Tuettu GitHub Actionin kautta (automaattinen ja aina ajan tasalla)

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](../zh-HK/README.md) | [Chinese (Traditional, Macau)](../zh-MO/README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](./README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](../th/README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **Haluatko mieluummin kloonata paikallisesti?**
>
> Tämä arkisto sisältää yli 50 käännöstä, mikä lisää merkittävästi lataustiedoston kokoa. Jos haluat kloonata ilman käännöksiä, käytä sparse checkout -toimintoa:
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
> Tämä antaa sinulle kaiken tarvittavan kurssin suorittamiseen paljon nopeammalla latauksella.
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### Liity yhteisöömme

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Meillä on käynnissä Discordin opi tekoälyn kanssa -sarja, lisätietoja ja liittymään pääset osoitteesta [Learn with AI Series](https://aka.ms/learnwithai/discord) ajalla 18. - 30. syyskuuta 2025. Saat vinkkejä ja niksejä GitHub Copilotin käyttämiseen Data Sciencessä.

![Learn with AI series](../../translated_images/fi/3.9b58fd8d6c373c20.webp)

# Koneoppiminen aloittelijoille - Opetussuunnitelma

> 🌍 Matkustetaan ympäri maailmaa tutkien koneoppimista maailman kulttuurien näkökulmasta 🌍

Microsoftin Cloud Advocates tarjoaa 12 viikon ja 26 oppitunnin opetussuunnitelman, joka keskittyy kokonaan **koneoppimiseen**. Tässä opetussuunnitelmassa opit siitä, mitä joskus kutsutaan **klassikoksi koneoppimiseksi**, pääasiassa Scikit-learn-kirjastoa käyttäen ja välttäen syväoppimista, joka on käsitelty [tekoälyn aloittelijoille -opetussuunnitelmassamme](https://aka.ms/ai4beginners). Yhdistä nämä oppitunnit myös ['Data Science aloittelijoille' -opetussuunnitelmamme](https://aka.ms/ds4beginners) kanssa!

Matkusta kanssamme ympäri maailmaa soveltaen näitä klassisia menetelmiä dataan monilta maailman alueilta. Jokainen oppitunti sisältää ennakko- ja jälkikokeet, kirjalliset ohjeet oppitunnin suorittamiseen, ratkaisun, tehtävän ja paljon muuta. Projektipohjainen opetusmenetelmä antaa sinun oppia samalla kun rakennat, mikä on todistettu tapa uusien taitojen omaksumiseen.

**✍️ Sydämellinen kiitos tekijöillemme** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu ja Amy Boyd

**🎨 Kiitos myös kuvittajillemme** Tomomi Imura, Dasani Madipalli ja Jen Looper

**🙏 Erityiskiitos 🙏 Microsoft Student Ambassador -tekijöille, tarkistajille ja sisältöjen tekijöille**, erityisesti Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila ja Snigdha Agarwal

**🤩 Erityiskiitos Microsoft Student Ambassadors Eric Wanjau, Jasleen Sondhi ja Vidushi Gupta R-oppitunneistamme!**

# Aloittaminen

Noudata näitä vaiheita:
1. **Haarauta arkisto**: Napsauta "Fork" -painiketta tämän sivun oikeassa yläkulmassa.
2. **Kloonaa arkisto**:   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [löydät kaikki lisäresurssit tälle kurssille Microsoft Learn -kokoelmastamme](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **Tarvitsetko apua?** Katso [vianmääritysohjeistuksemme](TROUBLESHOOTING.md) yleisimpiä asennukseen, käyttöönottoon ja oppituntien suorittamiseen liittyviä ongelmia varten.


**[Opiskelijat](https://aka.ms/student-page)**, käyttääksenne tätä opetussuunnitelmaa, haarauttakaa koko arkisto omaan GitHub-tiliinne ja tehkää harjoitukset itseksenne tai ryhmässä:

- Aloita ennakkotestillä.
- Lue luento ja tee tehtävät, pysähdy tarkistamaan osaaminen aina kun on tietotarkistus.
- Yritä luoda projektit ymmärtämällä oppitunnit sen sijaan, että suoritat ratkaisukoodit; nämä koodit ovat kuitenkin saatavilla `/solution`-kansioissa kussakin projektipainotteisessa oppitunnissa.
- Tee jälkitesti.
- Suorita haaste.
- Tee kotitehtävä.
- Kun olet suorittanut oppituntiryhmän, käy [Keskustelualueella](https://github.com/microsoft/ML-For-Beginners/discussions) ja "opiskele ääneen" täyttämällä sopiva PAT-arviointilomake. 'PAT' tarkoittaa Progress Assessment Toolia, jolla arvioit osaamistasi. Voit myös kommentoida muiden PAT:eja, niin opimme yhdessä.

> Jatko-opiskeluun suosittelemme seuraamaan näitä [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) moduuleja ja oppimispolkuja.

**Opettajat**, olemme sisällyttäneet [joitakin ehdotuksia](for-teachers.md) opetussuunnitelman käyttöön.

---

## Videokävelyt

Jotkin oppitunneista ovat saatavilla lyhytmuotoisina videoina. Löydät ne kaikki oppitunnin yhteydessä, tai [ML for Beginners -soittolistalta Microsoft Developer YouTube -kanavalla](https://aka.ms/ml-beginners-videos) klikkaamalla alla olevaa kuvaa.

[![ML for beginners banner](../../translated_images/fi/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## Tutustu tiimiin

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif:** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 Klikkaa kuvaa yllä nähdäksesi videon projektista ja sen tekijöistä!

---

## Pedagogiikka

Olemme valinneet kaksi opetuksellista periaatetta rakentaessamme tätä opetussuunnitelmaa: varmistaa, että se on käytännönläheinen ja **projektipohjainen**, ja että siinä on **usein myös tietotestauksia**. Lisäksi tällä opetussuunnitelmalla on yhteinen **teema** sen yhtenäisyyden vuoksi.

Sisällön liittäminen projekteihin tekee prosessista opiskelijoille kiinnostavamman ja käsitteiden muistaminen tehostuu. Lisäksi matalan panoksen koe ennen luentoa asettaa opiskelijan oppimistavoitteen, ja toinen koe luennon jälkeen varmistaa lisämuistin. Tämä opetussuunnitelma on suunniteltu joustavaksi ja hauskaksi, ja se voidaan suorittaa kokonaan tai osittain. Projektit alkavat yksinkertaisina ja muuttuvat yhä monimutkaisemmiksi 12 viikon aikana. Opetussuunnitelmaan sisältyy myös loppusanat koneoppimisen todellisista sovelluksista, joita voi käyttää lisäpisteisiin tai keskustelun pohjaksi.

> Löydät [käyttäytymissääntömme](CODE_OF_CONDUCT.md), [osallistumisohjeet](CONTRIBUTING.md), [käännökset](..) ja [vianmääritysohjeet](TROUBLESHOOTING.md). Otamme mielellämme vastaan rakentavaa palautetta!

## Jokainen oppitunti sisältää

- valinnaisen muistiinpanokuvan
- valinnaisen lisävideon
- videokävelyn (vain osassa oppitunteja)
- [ennakko-oppimisen lämmittelykokeen](https://ff-quizzes.netlify.app/en/ml/)
- kirjallisen oppitunnin
- projektilähtöisissä oppitunneissa vaiheittaiset ohjeet projektin rakentamiseen
- tietotarkistuksia
- haasteen
- lisälukemista
- kotitehtävän
- [jälkitestin](https://ff-quizzes.netlify.app/en/ml/)

> **Huomio kielistä**: Näitä oppitunteja kirjoitetaan pääasiassa Pythonilla, mutta monet ovat myös saatavilla R:llä. R-oppitunnin suorittamiseksi mene `/solution`-kansioon ja etsi R-oppitunnit. Niissä on .rmd-tiedostopääte, joka tarkoittaa **R Markdown** -tiedostoa, joka voidaan yksinkertaisesti määritellä R- tai muiden kielten `koodilohkojen` ja `YAML-otsikon` (ohjeistaa tulosteiden kuten PDF:n muotoilua) upotuksena `Markdown`-dokumenttiin. Täten se toimii esimerkillisenä kirjoitusalustana data tieteessä, koska sen avulla voit yhdistää koodisi, sen tulokset ja ajatuksesi kirjoittamalla ne Markdownilla. Lisäksi R Markdown -dokumentteja voidaan renderöidä tulostusmuodoiksi kuten PDF, HTML tai Word.
> **Muistutus visailuista**: Kaikki visailut löytyvät [Quiz App -kansiosta](../../quiz-app), yhteensä 52 visailua, joissa jokaisessa on kolme kysymystä. Ne linkitetään oppitunneilta, mutta visailusovelluksen voi myös ajaa paikallisesti; noudata `quiz-app`-kansion ohjeita paikalliseen isännöintiin tai Azureen käyttöönottoon.

| Oppitunnin numero |                             Aihe                             |                   Oppituntiryhmittely                 | Oppimistavoitteet                                                                                                              |                                                               Linkitetty oppitunti                                                               |                        Tekijä                        |
| :---------------: | :----------------------------------------------------------: | :---------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|        01         |                Johdatus koneoppimiseen                      |      [Introduction](1-Introduction/README.md)         | Opettele koneoppimisen peruskäsitteet                                                                                        |                                             [Oppitunti](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|        02         |                Koneoppimisen historia                       |      [Introduction](1-Introduction/README.md)         | Tutustu koneoppimisen alaan liittyvään historiaan                                                                             |                                            [Oppitunti](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen ja Amy                        |
|        03         |                 Oikeudenmukaisuus ja koneoppiminen          |      [Introduction](1-Introduction/README.md)         | Mitkä ovat tärkeimmät oikeudenmukaisuuteen liittyvät filosofiset kysymykset, joita opiskelijoiden tulisi pohtia rakentaessaan ja käyttäessään ML-malleja? |                                              [Oppitunti](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                         |
|        04         |                Koneoppimisen menetelmät                     |      [Introduction](1-Introduction/README.md)         | Mitä menetelmiä ML-tutkijat käyttävät rakentaessaan ML-malleja?                                                               |                                          [Oppitunti](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris ja Jen                       |
|        05         |                   Johdatus regressioon                      |        [Regression](2-Regression/README.md)           | Aloita Pythonin ja Scikit-learnin käytöllä regressiomallien rakentamisessa                                                    |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |       Jen • Eric Wanjau       |
|        06         |                Pohjois-Amerikan kurpitsahinnat 🎃           |        [Regression](2-Regression/README.md)           | Visualisoi ja puhdista data koneoppimista varten                                                                              |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |       Jen • Eric Wanjau       |
|        07         |                Pohjois-Amerikan kurpitsahinnat 🎃           |        [Regression](2-Regression/README.md)           | Rakenna lineaariset ja polynomiset regressiomallit                                                                           |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |       Jen ja Dmitry • Eric Wanjau       |
|        08         |                Pohjois-Amerikan kurpitsahinnat 🎃           |        [Regression](2-Regression/README.md)           | Rakenna logistinen regressiomalli                                                                                            |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |       Jen • Eric Wanjau       |
|        09         |                          Web-sovellus 🔌                     |           [Web App](3-Web-App/README.md)               | Rakenna verkkosovellus koulutetun mallisi käyttöön                                                                            |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|        10         |                 Johdatus luokitteluun                        |    [Classification](4-Classification/README.md)       | Puhdista, valmistele ja visualisoi data; johdatus luokitteluun                                                                | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen ja Cassie • Eric Wanjau |
|        11         |             Herkulliset aasialaiset ja intialaiset ruuat 🍜  |    [Classification](4-Classification/README.md)       | Johdatus luokittelijoihin                                                                                                     | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen ja Cassie • Eric Wanjau |
|        12         |             Herkulliset aasialaiset ja intialaiset ruuat 🍜  |    [Classification](4-Classification/README.md)       | Lisää luokittelijoita                                                                                                         | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen ja Cassie • Eric Wanjau |
|        13         |             Herkulliset aasialaiset ja intialaiset ruuat 🍜  |    [Classification](4-Classification/README.md)       | Rakenna suositteleva verkkosovellus mallisi avulla                                                                            |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|        14         |                   Johdatus klusterointiin                    |        [Clustering](5-Clustering/README.md)           | Puhdista, valmistele ja visualisoi data; johdatus klusterointiin                                                               |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |       Jen • Eric Wanjau       |
|        15         |              Nigerialainen musiikkimaku 🎧                   |        [Clustering](5-Clustering/README.md)           | Tutustu K-Means-klusterointimenetelmään                                                                                       |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |       Jen • Eric Wanjau       |
|        16         |        Johdatus luonnollisen kielen käsittelyyn ☕️          |   [Natural language processing](6-NLP/README.md)      | Opi NLP:n perusteet rakentamalla yksinkertainen botti                                                                          |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|        17         |                      Yleiset NLP-tehtävät ☕️                |   [Natural language processing](6-NLP/README.md)      | Syvennä NLP-tietämystäsi ymmärtämällä yleisiä kielellisten rakenteiden käsittelyssä tarvittavia tehtäviä                       |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|        18         |             Kääntäminen ja mielipiteiden analyysi ♥️         |   [Natural language processing](6-NLP/README.md)      | Kääntäminen ja mielipiteiden analyysi Jane Austenin avulla                                                                     |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|        19         |                  Euroopan romanttiset hotellit ♥️            |   [Natural language processing](6-NLP/README.md)      | Mielipiteiden analyysi hotelliarvosteluilla 1                                                                                  |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|        20         |                  Euroopan romanttiset hotellit ♥️            |   [Natural language processing](6-NLP/README.md)      | Mielipiteiden analyysi hotelliarvosteluilla 2                                                                                  |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|        21         |            Johdatus aikasarjaennusteisiin                    |        [Time series](7-TimeSeries/README.md)          | Johdatus aikasarjaennusteisiin                                                                                                |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|        22         | ⚡️ Maailman sähkönkulutus ⚡️ - aikasarjaennuste ARIMA:lla    |        [Time series](7-TimeSeries/README.md)          | Aikasarjaennuste ARIMA-mallilla                                                                                                |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|        23         |  ⚡️ Maailman sähkönkulutus ⚡️ - aikasarjaennuste SVR:llä    |        [Time series](7-TimeSeries/README.md)          | Aikasarjaennuste tukivektoriregressoriin (SVR) avulla                                                                         |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|        24         |             Johdatus vahvistusoppimiseen                     | [Reinforcement learning](8-Reinforcement/README.md)   | Johdatus vahvistusoppimiseen Q-Learningin avulla                                                                               |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|        25         |                 Auta Peteriä välttämään susi! 🐺             | [Reinforcement learning](8-Reinforcement/README.md)   | Vahvistusoppimisen Gym                                                                                                         |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  Jälkikirjoitus   |            Todelliset ML-skenaariot ja sovellukset          |      [ML in the Wild](9-Real-World/README.md)         | Mielenkiintoisia ja valaisevia todellisen maailman sovelluksia klassisesta ML:stä                                               |                                             [Oppitunti](9-Real-World/1-Applications/README.md)                                              |                         Tiimi                         |
|  Jälkikirjoitus   |            Mallin virheenkorjaus ML:ssä RAI-dashboardilla   |      [ML in the Wild](9-Real-World/README.md)         | Mallin virheenkorjaus koneoppimisessa Responsible AI -dashboard-komponenttien avulla                                            |                                             [Oppitunti](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                     |

> [löydä kaikki tämän kurssin lisäresurssit Microsoft Learn -kokoelmassamme](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## Offline-käyttö

Voit käyttää tätä dokumentaatiota offline-tilassa käyttämällä [Docsify](https://docsify.js.org/#/). Haarauta tämä repo, [asenna Docsify](https://docsify.js.org/#/quickstart) paikallisesti ja sen jälkeen tämän repokansion juurikansiossa kirjoita `docsify serve`. Sivusto toimii portissa 3000 paikallisessa koneessasi: `localhost:3000`.

## PDF:t

Löydät opetussuunnitelman pdf-muodossa linkkeineen [täältä](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf).


## 🎒 Muut kurssit

Tiimimme tuottaa muita kursseja! Tutustu:

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
 
### Keskeinen oppiminen
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot-sarja
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## Apua saamaan

Jos jumitut tai sinulla on kysyttävää tekoälysovellusten rakentamisesta, liity muiden oppijoiden ja kokeneiden kehittäjien keskusteluihin MCP:stä. Se on tukeva yhteisö, jossa kysymykset ovat tervetulleita ja tieto jaetaan vapaasti.

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Jos sinulla on palautetta tuotteesta tai virheitä rakentamisen aikana, käy:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## Lisäoppimisvinkkejä

- Käy läpi muistikirjat jokaisen oppitunnin jälkeen paremman ymmärryksen saamiseksi.
- Harjoittele algoritmien toteuttamista itse.
- Tutustu tosielämän aineistoihin oppimiesi käsitteiden avulla.

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Vastuuvapauslauseke**:  
Tämä asiakirja on käännetty käyttämällä tekoälypohjaista käännöspalvelua [Co-op Translator](https://github.com/Azure/co-op-translator). Pyrimme tarkkuuteen, mutta huomioithan, että automaattikäännöksissä saattaa esiintyä virheitä tai epätarkkuuksia. Alkuperäistä asiakirjaa sen alkuperäiskielellä tulee pitää virallisena lähteenä. Tärkeiden tietojen osalta suositellaan ammattimaista ihmiskäännöstä. Emme ole vastuussa tämän käännöksen käytöstä mahdollisesti aiheutuvista väärinkäsityksistä tai tulkinnoista.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->