[![GitHub licencia](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub prispievatelia](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub problémy](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub žiadosti o zlúčenie](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub pozorovatelia](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forky](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub hviezdy](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 Podpora viacerých jazykov

#### Podporované cez GitHub Action (Automatizované a vždy aktuálne)

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabčina](../ar/README.md) | [Bengálčina](../bn/README.md) | [Bulharčina](../bg/README.md) | [Barmčina (Myanmar)](../my/README.md) | [Čínština (zjednodušená)](../zh-CN/README.md) | [Čínština (tradičná, Hong Kong)](../zh-HK/README.md) | [Čínština (tradičná, Macao)](../zh-MO/README.md) | [Čínština (tradičná, Taiwan)](../zh-TW/README.md) | [Chorvátčina](../hr/README.md) | [Čeština](../cs/README.md) | [Dánčina](../da/README.md) | [Holandčina](../nl/README.md) | [Estónčina](../et/README.md) | [Fínčina](../fi/README.md) | [Francúzština](../fr/README.md) | [Nemčina](../de/README.md) | [Gréčtina](../el/README.md) | [Hebrejčina](../he/README.md) | [Hindčina](../hi/README.md) | [Maďarčina](../hu/README.md) | [Indonézčina](../id/README.md) | [Taliančina](../it/README.md) | [Japončina](../ja/README.md) | [Kannadčina](../kn/README.md) | [Khmérčina](../km/README.md) | [Kórejčina](../ko/README.md) | [Litovčina](../lt/README.md) | [Malajčina](../ms/README.md) | [Malayalam](../ml/README.md) | [Maráthčina](../mr/README.md) | [Nepálčina](../ne/README.md) | [Nigérijský pidžin](../pcm/README.md) | [Nórčina](../no/README.md) | [Perzština (Farsi)](../fa/README.md) | [Poľština](../pl/README.md) | [Portugalčina (Brazília)](../pt-BR/README.md) | [Portugalčina (Portugalsko)](../pt-PT/README.md) | [Pandžábčina (Gurmukhí)](../pa/README.md) | [Rumunčina](../ro/README.md) | [Ruština](../ru/README.md) | [Srbčina (cyrilika)](../sr/README.md) | [Slovenčina](./README.md) | [Slovinčina](../sl/README.md) | [Španielčina](../es/README.md) | [Svahilčina](../sw/README.md) | [Švédčina](../sv/README.md) | [Tagalog (Filipínčina)](../tl/README.md) | [Tamilčina](../ta/README.md) | [Telugčina](../te/README.md) | [Thajčina](../th/README.md) | [Turečtina](../tr/README.md) | [Ukrajinčina](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamčina](../vi/README.md)

> **Radšej klonujete lokálne?**
>
> Tento repozitár obsahuje viac ako 50 jazykových prekladov, čo výrazne zvyšuje veľkosť sťahovania. Ak chcete klonovať bez prekladov, použite sparse checkout:
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
> Toto vám zabezpečí všetko potrebné na dokončenie kurzu s oveľa rýchlejším sťahovaním.
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### Pridajte sa k našej komunite

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Máme prebiehajúcu sériu Learn with AI na Discorde, dozviete sa viac a pripojte sa k nám na [Learn with AI Series](https://aka.ms/learnwithai/discord) od 18. do 30. septembra 2025. Získate tipy a triky na používanie GitHub Copilot pre Data Science.

![Séria Learn with AI](../../translated_images/sk/3.9b58fd8d6c373c20.webp)

# Strojové učenie pre začiatočníkov - Učebný plán

> 🌍 Cestujte po svete a objavujte Strojové učenie cez svetové kultúry 🌍

Cloud Advocates v Microsoftu s radosťou ponúkajú 12-týždňový učebný plán s 26 lekciami o **Strojovom učení**. V tomto učebnom pláne sa naučíte, čo sa niekedy nazýva **klasické strojové učenie**, pričom primárne používame knižnicu Scikit-learn a vyhýbame sa hlbokému učeniu, ktoré je pokryté v našom [učebnom pláne AI pre začiatočníkov](https://aka.ms/ai4beginners). Tieto lekcie skombinujte aj s našim [učebným plánom Data Science pre začiatočníkov](https://aka.ms/ds4beginners)!

Cestujte s nami po svete a aplikujte tieto klasické techniky na dáta z rôznych oblastí sveta. Každá lekcia obsahuje kvízy pred a po lekcii, písomné inštrukcie na dokončenie lekcie, riešenie, zadanie a ďalšie. Naša projektovo orientovaná pedagogika vám umožňuje učiť sa priamo počas tvorby, čo je osvedčený spôsob, ako si nové vedomosti udržať.

**✍️ Srdečné poďakovanie našim autorom** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu a Amy Boyd

**🎨 Poďakovanie tiež našim ilustrátorom** Tomomi Imura, Dasani Madipalli a Jen Looper

**🙏 Špeciálne poďakovanie 🙏 našim autorom, recenzentom a prispievateľom z Microsoft Student Ambassadors**, najmä Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila a Snigdha Agarwal

**🤩 Zvláštne poďakovanie Microsoft Student Ambassadors Eric Wanjau, Jasleen Sondhi a Vidushi Gupta za naše lekcie R!**

# Začíname

Postupujte podľa týchto krokov:
1. **Vytvorte si fork repozitára**: Kliknite na tlačidlo „Fork“ v pravom hornom rohu tejto stránky.
2. **Klonujte repozitár**: `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [nájdite všetky ďalšie zdroje pre tento kurz v našej kolekcii Microsoft Learn](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **Potrebujete pomoc?** Pozrite si náš [Návod na riešenie problémov](TROUBLESHOOTING.md) pre riešenia bežných problémov s inštaláciou, nastavením a spúšťaním lekcií.

**[Študenti](https://aka.ms/student-page)**, používanie tohto učebného plánu spočíva vo forknutí celého repozitára do svojho GitHub účtu a samostatnom alebo skupinovom plnení cvičení:

- Začnite kvízom pred lekciou.
- Prečítajte si lekciu a dokončite aktivity, pri každej kontrole vedomostí sa zastavte a zamyslite.
- Pokúste sa vytvoriť projekty pochopením lekcií namiesto spúšťania riešení; kód riešení je však k dispozícii v priečinkoch `/solution` v každej lekcii orientovanej na projekt.
- Absolvujte test po lekcii.
- Splňte výzvu.
- Dokončite zadanie.
- Po dokončení skupiny lekcií navštívte [Diskusnú dosku](https://github.com/microsoft/ML-For-Beginners/discussions) a „učte sa nahlas“ vyplnením príslušného PAT hodnotiaceho formulára. 'PAT' je Nástroj hodnotenia pokroku, ktorý vyplníte, aby ste si prehĺbili vedomosti. Môžete tiež reagovať na ďalšie PAT, aby sme sa učili spoločne.

> Na ďalšie štúdium odporúčame sledovať tieto [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) moduly a vzdelávacie cesty.

**Učitelia**, pripravili sme [niekoľko odporúčaní](for-teachers.md) na využitie tohto učebného plánu.

---

## Video návody

Niektoré lekcie sú dostupné ako krátke videá. Nájdete ich priamo v lekciách alebo v [playliste ML for Beginners na Microsoft Developer YouTube kanáli](https://aka.ms/ml-beginners-videos) kliknutím na obrázok nižšie.

[![ML for beginners banner](../../translated_images/sk/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## Spoznajte tím

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif od** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 Kliknite na obrázok vyššie pre video o projekte a jeho tvorcoch!

---

## Pedagogika

Pri tvorbe tohto učebného plánu sme si vybrali dva pedagogické princípy: zabezpečiť, aby bol **prakticky projektovo orientovaný** a aby obsahoval **časté kvízy**. Okrem toho má tento učebný plán spoločnú **tému**, ktorá mu dodáva súdržnosť.

Zabezpečením súladu obsahu s projektmi je proces pre študentov zaujímavejší a upevňuje sa zapamätanie si konceptov. Nízko-rizikový kvíz pred triedou nastavia zámer študenta naučiť sa tému, zatiaľ čo druhý kvíz po lekcii zabezpečuje ďalšie upevnenie vedomostí. Tento učebný plán je navrhnutý tak, aby bol flexibilný a zábavný, a možno ho absolvovať celý alebo čiastočne. Projekty začínajú malé a do konca 12-týždňového cyklu získavajú zložitosť. Učebný plán tiež obsahuje pospis o praktických využitiach ML, ktorý možno použiť ako extra kredit alebo ako základ diskusie.

> Nájdete tu naše [Pravidlá správania](CODE_OF_CONDUCT.md), [Príspevky](CONTRIBUTING.md), [Preklady](..) a [Návody na riešenie problémov](TROUBLESHOOTING.md). Radi prijmeme vašu konštruktívnu spätnú väzbu!

## Každá lekcia obsahuje

- voliteľnú skicu poznámok
- voliteľné doplnkové video
- video návod (len niektoré lekcie)
- [kvíz na rozcvičenie pred lekciou](https://ff-quizzes.netlify.app/en/ml/)
- písomnú lekciu
- pre projektové lekcie, krok za krokom návody na vybudovanie projektu
- kontroly vedomostí
- výzvu
- doplnkové čítanie
- zadanie
- [kvíz po lekcii](https://ff-quizzes.netlify.app/en/ml/)
> **Poznámka o jazykoch**: Tieto lekcie sú primárne napísané v Pythone, ale mnohé sú dostupné aj v R. Ak chcete dokončiť lekciu v R, prejdite do priečinka `/solution` a vyhľadajte lekcie v R. Obsahujú príponu .rmd, ktorá predstavuje **R Markdown** súbor, čo možno jednoducho definovať ako vkladanie `kódových blokov` (v R alebo iných jazykoch) a `YAML hlavičky` (ktorá usmerňuje, ako formátovať výstupy, napr. PDF) v `Markdown dokumente`. Takto slúži ako príkladný rámec pre tvorbu dokumentov v dátovej vede, pretože vám umožňuje kombinovať váš kód, jeho výstup a vaše poznámky tým, že ich môžete zaznamenať v Markdown. Navyše, dokumenty R Markdown môžu byť vyrenderované do výstupných formátov ako PDF, HTML alebo Word.

> **Poznámka o kvízoch**: Všetky kvízy sú uložené v [priečinku Quiz App](../../quiz-app), celkovo 52 kvízov so štruktúrou troch otázok každý. Sú prepojené v jednotlivých lekciách, ale aplikáciu na kvízy možno spustiť lokálne; postupujte podľa inštrukcií v priečinku `quiz-app` pre lokálne hosťovanie alebo nasadenie do Azure.

| Číslo lekcie |                              Téma                               |                 Zoskupenie lekcie                  | Ciele učenia                                                                                                                  |                                                                Prepojená lekcia                                                                |                      Autor                      |
| :----------: | :------------------------------------------------------------: | :------------------------------------------------: | ----------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------: |
|      01      |             Úvod do strojového učenia                         |      [Úvod](1-Introduction/README.md)               | Naučte sa základné pojmy strojového učenia                                                                                   |                                         [Lekcia](1-Introduction/1-intro-to-ML/README.md)                                               |                   Muhammad                     |
|      02      |             História strojového učenia                        |      [Úvod](1-Introduction/README.md)               | Spoznajte históriu tohto odboru                                                                                              |                                        [Lekcia](1-Introduction/2-history-of-ML/README.md)                                              |                  Jen a Amy                      |
|      03      |              Spravodlivosť a strojové učenie                  |      [Úvod](1-Introduction/README.md)               | Aké sú dôležité filozofické otázky spravodlivosti, ktoré by študenti mali zvážiť pri vývoji a použití ML modelov?               |                                            [Lekcia](1-Introduction/3-fairness/README.md)                                               |                    Tomomi                      |
|      04      |             Techniky strojového učenia                        |      [Úvod](1-Introduction/README.md)               | Aké techniky používajú výskumníci ML na tvorbu modelov?                                                                       |                                      [Lekcia](1-Introduction/4-techniques-of-ML/README.md)                                           |                 Chris a Jen                    |
|      05      |                Úvod do regresie                               |        [Regresia](2-Regression/README.md)           | Začnite s Pythonom a Scikit-learn pre regresné modely                                                                        |       [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)       |                 Jen • Eric Wanjau              |
|      06      |              Ceny tekvíc v Severnej Amerike 🎃                |        [Regresia](2-Regression/README.md)           | Vizualizujte a očistite dáta na prípravu ML                                                                                   |        [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)       |                 Jen • Eric Wanjau              |
|      07      |              Ceny tekvíc v Severnej Amerike 🎃                |        [Regresia](2-Regression/README.md)           | Postavte lineárne a polynomiálne regresné modely                                                                              |      [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)      |           Jen a Dmitry • Eric Wanjau           |
|      08      |              Ceny tekvíc v Severnej Amerike 🎃                |        [Regresia](2-Regression/README.md)           | Vybudujte logistický regresný model                                                                                           |   [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)   |                 Jen • Eric Wanjau              |
|      09      |                      Webová aplikácia 🔌                      |           [Web App](3-Web-App/README.md)             | Vybudujte webovú aplikáciu na použitie vášho natrénovaného modelu                                                             |                                                    [Python](3-Web-App/1-Web-App/README.md)                                                 |                        Jen                     |
|      10      |                  Úvod do klasifikácie                        |    [Klasifikácia](4-Classification/README.md)        | Očistite, pripravte a vizualizujte svoje dáta; úvod do klasifikácie                                                           | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html) | Jen a Cassie • Eric Wanjau                      |
|      11      |            Lahodné ázijské a indické kuchyne 🍜               |    [Klasifikácia](4-Classification/README.md)        | Úvod do klasifikátorov                                                                                                        | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen a Cassie • Eric Wanjau                      |
|      12      |            Lahodné ázijské a indické kuchyne 🍜               |    [Klasifikácia](4-Classification/README.md)        | Viac klasifikátorov                                                                                                          | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen a Cassie • Eric Wanjau                      |
|      13      |            Lahodné ázijské a indické kuchyne 🍜               |    [Klasifikácia](4-Classification/README.md)        | Postavte odporúčaciu webovú aplikáciu pomocou vášho modelu                                                                    |                                             [Python](4-Classification/4-Applied/README.md)                                              |                        Jen                      |
|      14      |                   Úvod do zhlukovania                          |        [Zhlukovanie](5-Clustering/README.md)          | Očistite, pripravte a vizualizujte svoje dáta; úvod do zhlukovania                                                             |        [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)        |                 Jen • Eric Wanjau              |
|      15      |             Preskúmanie nigerijských hudobných chutí 🎧       |        [Zhlukovanie](5-Clustering/README.md)          | Preskúmajte K-Means zhlukovaciu metódu                                                                                        |         [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)         |                 Jen • Eric Wanjau              |
|      16      |           Úvod do spracovania prirodzeného jazyka ☕️          |   [Spracovanie prirodzeného jazyka](6-NLP/README.md)   | Naučte sa základy NLP vytvorením jednoduchého bota                                                                             |                                          [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                   Stephen                       |
|      17      |                  Bežné úlohy NLP ☕️                          |   [Spracovanie prirodzeného jazyka](6-NLP/README.md)   | Prehĺbte svoje poznatky o NLP pochopením bežných úloh pri práci s jazykovými štruktúrami                                        |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                   Stephen                       |
|      18      |            Preklad a analýza sentimentu ♥️                     |   [Spracovanie prirodzeného jazyka](6-NLP/README.md)   | Preklad a analýza sentimentu s Jane Austen                                                                                     |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                   Stephen                       |
|      19      |           Romantické hotely v Európe ♥️                        |   [Spracovanie prirodzeného jazyka](6-NLP/README.md)   | Sentimentálna analýza s hotelovými recenziami 1                                                                                |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                   Stephen                       |
|      20      |           Romantické hotely v Európe ♥️                        |   [Spracovanie prirodzeného jazyka](6-NLP/README.md)   | Sentimentálna analýza s hotelovými recenziami 2                                                                                |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                   Stephen                       |
|      21      |            Úvod do predikcie časových radov                   |        [Časové rady](7-TimeSeries/README.md)           | Úvod do predikcie časových radov                                                                                              |                                        [Python](7-TimeSeries/1-Introduction/README.md)                                              |                  Francesca                      |
|      22      | ⚡️ Svetová spotreba energie ⚡️ - predikcia časových radov pomocou ARIMA |        [Časové rady](7-TimeSeries/README.md)           | Predikcia časových radov pomocou ARIMA                                                                                        |                                            [Python](7-TimeSeries/2-ARIMA/README.md)                                              |                  Francesca                      |
|      23      |  ⚡️ Svetová spotreba energie ⚡️ - predikcia časových radov pomocou SVR  |        [Časové rady](7-TimeSeries/README.md)           | Predikcia časových radov pomocou Support Vector Regressora                                                                    |                                             [Python](7-TimeSeries/3-SVR/README.md)                                              |                   Anirban                       |
|      24      |            Úvod do posilňovacieho učenia                      | [Posilňovacie učenie](8-Reinforcement/README.md)       | Úvod do posilňovacieho učenia pomocou Q-Learning                                                                               |                                        [Python](8-Reinforcement/1-QLearning/README.md)                                              |                   Dmitry                        |
|      25      |             Pomôžte Petrovi vyhnúť sa vlkovi! 🐺               | [Posilňovacie učenie](8-Reinforcement/README.md)       | Posilňovacie učenie pomocou Gym                                                                                                |                                        [Python](8-Reinforcement/2-Gym/README.md)                                                 |                   Dmitry                        |
|   Postscript |             Skutočné scenáre a aplikácie ML                   |      [ML vo svete](9-Real-World/README.md)             | Zaujímavé a odhaľujúce reálne aplikácie klasického ML                                                                          |                                         [Lekcia](9-Real-World/1-Applications/README.md)                                              |                     Tím                       |
|   Postscript |               Ladenie modelov ML pomocou RAI dashboardu       |      [ML vo svete](9-Real-World/README.md)             | Ladenie modelov v strojovom učení pomocou komponentov Responsible AI dashboardu                                                 |                                        [Lekcia](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                     Ruth Yakubu                |

> [nájdite všetky ďalšie materiály k tomuto kurzu v našej kolekcii Microsoft Learn](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## Prístup offline

Túto dokumentáciu môžete používať offline pomocou [Docsify](https://docsify.js.org/#/). Naklonujte si tento repozitár, [nainštalujte Docsify](https://docsify.js.org/#/quickstart) na svoj lokálny počítač a potom v koreňovom priečinku repozitára spustite príkaz `docsify serve`. Webstránka bude sprístupnená na porte 3000 na vašom localhoste: `localhost:3000`.

## PDF súbory

Nájdite pdf učebného plánu s odkazmi [tu](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf).


## 🎒 Ďalšie kurzy

Náš tím vytvára aj iné kurzy! Pozrite si:

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j pre začiatočníkov](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js pre začiatočníkov](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain pre začiatočníkov](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agentov
[![AZD pre začiatočníkov](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI pre začiatočníkov](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![MCP pre začiatočníkov](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![AI Agenti pre začiatočníkov](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Séria Generatívnej AI
[![Generatívna AI pre začiatočníkov](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generatívna AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generatívna AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generatívna AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### Základné učenie
[![Strojové učenie pre začiatočníkov](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Dátová veda pre začiatočníkov](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI pre začiatočníkov](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Kyberbezpečnosť pre začiatočníkov](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Webový vývoj pre začiatočníkov](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT pre začiatočníkov](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR vývoj pre začiatočníkov](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Séria Copilot
[![Copilot pre AI párované programovanie](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot pre C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Dobrodružstvo](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## Získanie pomoci

Ak uviaznete alebo máte akékoľvek otázky týkajúce sa tvorby AI aplikácií, pripojte sa k ostatným študentom a skúseným vývojárom v diskusiách o MCP. Je to podporujúca komunita, kde sú otázky vítané a poznatky sa zdieľajú slobodne.

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Ak máte spätnú väzbu na produkt alebo narazíte na chyby počas tvorby, navštívte:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## Dodatočné tipy na učenie

- Po každej lekcii si prezrite poznámkové bloky pre lepšie pochopenie.
- Precvičujte implementáciu algoritmov samostatne.
- Preskúmajte reálne dátové súbory využitím naučených konceptov.

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Zrieknutie sa zodpovednosti**:  
Tento dokument bol preložený pomocou AI prekladateľskej služby [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Originálny dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie odporúčame profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->