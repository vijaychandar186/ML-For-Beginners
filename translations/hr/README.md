### 🌐 Podrška za više jezika

#### Podržano putem GitHub akcije (automatizirano i uvijek ažurno)

> **Želite li radije klonirati lokalno?**
>
> Ovaj repozitorij uključuje prijevode na više od 50 jezika što značajno povećava veličinu preuzimanja. Za kloniranje bez prijevoda, koristite sparse checkout:
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
> Time dobivate sve što vam je potrebno za završetak tečaja s mnogo bržim preuzimanjem.

#### Pridružite se našoj zajednici

Imamo Discord serijal učenja s AI-jem, saznajte više i pridružite nam se na [Learn with AI Series](https://aka.ms/learnwithai/discord) od 18. do 30. rujna 2025. Dobit ćete savjete i trikove za korištenje GitHub Copilota za znanost o podacima.

# Strojno učenje za početnike – Nastavni program

> 🌍 Putujte svijetom dok istražujemo strojno učenje kroz kulture svijeta 🌍

Cloud Advocates u Microsoftu s veseljem vam predstavljaju 12-tjedni nastavni program od 26 lekcija posvećenih **strojnome učenju**. U ovom ćete nastavnom programu naučiti o onome što se ponekad naziva **klasično strojno učenje**, koristeći uglavnom Scikit-learn kao biblioteku i izbjegavajući duboko učenje, koje je obuhvaćeno u našem [nastavnom programu AI za početnike](https://aka.ms/ai4beginners). Spojite ove lekcije sa našim [nastavnim programom 'Znanost o podacima za početnike'](https://aka.ms/ds4beginners).

Putujte s nama širom svijeta dok primjenjujemo ove klasične tehnike na podatke iz različitih dijelova svijeta. Svaka lekcija sadrži kviz prije i poslije lekcije, pisane upute za dovršetak lekcije, rješenje, zadatak i više. Naša poduka temeljena na projektima omogućuje vam učenje kroz izgradnju, što je dokazano učinkovit način da nove vještine ostanu.

**✍️ Srdačna zahvala našim autorima** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu i Amy Boyd

**🎨 Zahvala i našim ilustratorima** Tomomi Imura, Dasani Madipalli i Jen Looper

**🙏 Posebna zahvala 🙏 našim Microsoft Student Ambassador autorima, recenzentima i suradnicima na sadržaju**, posebice Rishitu Dagliju, Muhammadu Sakibu Khan Inanu, Rohanu Raju, Alexandru Petrescuu, Abhisheku Jaiswalu, Nawrin Tabassumu, Ioanu Samuili i Snigdhi Agarwalu

**🤩 Posebna zahvalnost Microsoft Student Ambassadorima Ericu Wanjauu, Jasleen Sondhi i Vidushi Gupti za naše R lekcije!**

# Početak

Slijedite ove korake:
1. **Forkajte repozitorij**: Kliknite na gumb "Fork" u gornjem desnom kutu ove stranice.
2. **Klonirajte repozitorij**:   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [pronađite sve dodatne resurse za ovaj tečaj u našoj Microsoft Learn kolekciji](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **Trebate pomoć?** Pogledajte naš [Vodič za rješavanje problema](TROUBLESHOOTING.md) za rješenja uobičajenih problema s instalacijom, postavljanjem i izvođenjem lekcija.


**[Studenti](https://aka.ms/student-page)**, da biste koristili ovaj nastavni program, forkjajte cijeli repozitorij na svoj GitHub račun i rješavajte vježbe samostalno ili u grupi:

- Započnite s kvizom prije predavanja.
- Pročitajte predavanje i dovršite aktivnosti, zastajući i razmišljajući na svakom provjeru znanja.
- Pokušajte kreirati projekte razumijevanjem lekcija umjesto samo pokretanja rješenja; međutim, taj je kod dostupan u /solution mapama svake lekcije orijentirane na projekt.
- Napravite kviz nakon predavanja.
- Dovršite izazov.
- Dovršite zadatak.
- Nakon dovršetka skupine lekcija, posjetite [Discussion Board](https://github.com/microsoft/ML-For-Beginners/discussions) i "naučite naglas" popunjavanjem odgovarajućeg PAT obrasca. 'PAT' je alat za procjenu napretka koji popunjavate kako biste dodatno usavršili svoje znanje. Također možete reagirati na druge PAT-ove kako bismo svi zajedno učili.

> Za daljnje proučavanje preporučamo praćenje ovih [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) modula i putanja učenja.

**Nastavnici**, dali smo [neke prijedloge](for-teachers.md) za korištenje ovog nastavnog programa.

---

## Video vodiči

Neke lekcije dostupne su u obliku kratkih videa. Sve ih možete pronaći u lekcijama ili na [ML for Beginners playlisti na Microsoft Developer YouTube kanalu](https://aka.ms/ml-beginners-videos) klikom na sliku ispod.

---

## Upoznajte tim

> 🎥 Kliknite na gornju sliku za video o projektu i ljudima koji su ga stvorili!

---

## Pedagogija

Odabrali smo dva pedagoška načela za izradu ovog nastavnog programa: da bude praktičan i **temeljen na projektima** te da uključuje **učestale kvizove**. Osim toga, ovaj nastavni program ima zajedničku **temu** koja mu daje koheziju.

Osiguravajući usklađenost sadržaja s projektima, proces je zanimljiviji studentima i povećava se zadržavanje pojmova. Također, lagani kviz prije predavanja usmjerava pažnju studenta na učenje teme, dok kviz poslije predavanja dodatno osigurava zadržavanje naučenog. Ovaj nastavni program je dizajniran da bude fleksibilan i zabavan te se može pohađati u cijelosti ili djelomično. Projekti počinju jednostavno i postaju sve složeniji do kraja 12-tjednog ciklusa. Nakon toga slijedi postscript o stvarnim primjenama strojnog učenja koji se može koristiti kao dodatni zadatak ili kao osnova za raspravu.

> Pronađite naš [Kodeks ponašanja](CODE_OF_CONDUCT.md), [Upute za pridonošenje](CONTRIBUTING.md), [Prijevode](..) i [Vodič za rješavanje problema](TROUBLESHOOTING.md). Pozdravljamo vaše konstruktivne povratne informacije!

## Svaka lekcija uključuje

- neobavezna skicna bilješka
- neobavezni dodatni video
- video vodič (samo za neke lekcije)
- [pred-predavački zagrijavajući kviz](https://ff-quizzes.netlify.app/en/ml/)
- pisane upute za lekciju
- za lekcije temeljene na projektima, korak-po-korak vodiče za izgradnju projekta
- provjere znanja
- izazov
- dodatno čitanje
- zadatak
- [post-predavački kviz](https://ff-quizzes.netlify.app/en/ml/)

> **Napomena o jezicima**: Lekcije su uglavnom napisane u Pythonu, ali mnoge su dostupne i u R-u. Za dovršetak R lekcije, posjetite mapu `/solution` i potražite R lekcije. One uključuju ekstenziju .rmd što predstavlja **R Markdown** datoteku, koja se može jednostavno definirati kao umetanje `kodnih blokova` (iz R ili drugih jezika) i `YAML zaglavlja` (koje određuje format izlaza poput PDF-a) u `Markdown dokument`. Kao takav, on služi kao izvrsni okvir za pisanje za znanost o podacima jer omogućuje kombiniranje koda, njegovih rezultata i vaših razmišljanja pisanjem u Markdownu. Nadalje, R Markdown dokumenti mogu se prikazivati u izlaznim formatima poput PDF-a, HTML-a ili Worda.
> **Napomena o kvizovima**: Svi kvizovi nalaze se u [Quiz App folderu](../../quiz-app), ukupno 52 kviza s po tri pitanja. Povezani su iz lekcija, ali quiz app se može pokrenuti lokalno; pratite upute u mapi `quiz-app` za lokalno hostanje ili deploy na Azure.

| Broj lekcije |                             Tema                              |                   Grupiranje lekcija                   | Ciljevi učenja                                                                                                             |                                                              Povezana lekcija                                                               |                        Autor                        |
| :-----------: | :------------------------------------------------------------: | :-------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|      01       |                Uvod u strojno učenje                |      [Uvod](1-Introduction/README.md)       | Naučite osnovne pojmove iza strojnog učenja                                                                                |                                             [Lekcija](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|      02       |                Povijest strojnog učenja                 |      [Uvod](1-Introduction/README.md)       | Naučite povijest tog područja                                                                                         |                                            [Lekcija](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen i Amy                      |
|      03       |                 Pravednost i strojarstvo                  |      [Uvod](1-Introduction/README.md)       | Koja su važna filozofska pitanja o pravednosti koja učenici trebaju razmotriti kod izrade i primjene ML modela? |                                              [Lekcija](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|      04       |                Tehnike strojnog učenja                 |      [Uvod](1-Introduction/README.md)       | Koje tehnike istraživači strojnog učenja koriste za izgradnju ML modela?                                                                       |                                          [Lekcija](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris i Jen                     |
|      05       |                   Uvod u regresiju                   |        [Regresija](2-Regression/README.md)         | Počnite s Python i Scikit-learn za regresijske modele                                                                  |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|      06       |                Cijene bundeva u Sjevernoj Americi 🎃                |        [Regresija](2-Regression/README.md)         | Vizualizirajte i očistite podatke u pripremi za ML                                                                                  |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|      07       |                Cijene bundeva u Sjevernoj Americi 🎃                |        [Regresija](2-Regression/README.md)         | Izgradite linearne i polinomne regresijske modele                                                                                   |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen i Dmitry • Eric Wanjau       |
|      08       |                Cijene bundeva u Sjevernoj Americi 🎃                |        [Regresija](2-Regression/README.md)         | Izgradite logistički regresijski model                                                                                               |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|      09       |                          Web aplikacija 🔌                          |           [Web App](3-Web-App/README.md)            | Izgradite web aplikaciju za korištenje vašeg treniranog modela                                                                                       |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|      10       |                 Uvod u klasifikaciju                 |    [Klasifikacija](4-Classification/README.md)     | Očistite, pripremite i vizualizirajte podatke; uvod u klasifikaciju                                                            | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen i Cassie • Eric Wanjau |
|      11       |             Ukusna azijska i indijska jela 🍜             |    [Klasifikacija](4-Classification/README.md)     | Uvod u klasifikatore                                                                                                     | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen i Cassie • Eric Wanjau |
|      12       |             Ukusna azijska i indijska jela 🍜             |    [Klasifikacija](4-Classification/README.md)     | Više klasifikatora                                                                                                                | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen i Cassie • Eric Wanjau |
|      13       |             Ukusna azijska i indijska jela 🍜             |    [Klasifikacija](4-Classification/README.md)     | Izgradite preporučiteljsku web aplikaciju koristeći vaš model                                                                                    |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|      14       |                   Uvod u klasteriranje                   |        [Klasteriranje](5-Clustering/README.md)         | Očistite, pripremite i vizualizirajte podatke; uvod u klasteriranje                                                                |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|      15       |              Istraživanje glazbenih ukusa Nigerije 🎧              |        [Klasteriranje](5-Clustering/README.md)         | Istražite K-Sredina metodu klasteriranja                                                                                           |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|      16       |        Uvod u obradu prirodnog jezika ☕️         |   [Obrada prirodnog jezika](6-NLP/README.md)    | Naučite osnove NLP-a izradom jednostavnog bota                                                                             |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|      17       |                      Uobičajeni NLP zadaci ☕️                      |   [Obrada prirodnog jezika](6-NLP/README.md)    | Produbite znanje NLP-a razumijevanjem uobičajenih zadataka potrebnih pri radu s jezičnim strukturama                          |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|      18       |             Prevođenje i analiza sentimenta ♥️              |   [Obrada prirodnog jezika](6-NLP/README.md)    | Prevođenje i analiza sentimenta s Jane Austen                                                                             |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|      19       |                  Romantični hoteli Europe ♥️                  |   [Obrada prirodnog jezika](6-NLP/README.md)    | Analiza sentimenta na osnovu recenzija hotela 1                                                                                         |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|      20       |                  Romantični hoteli Europe ♥️                  |   [Obrada prirodnog jezika](6-NLP/README.md)    | Analiza sentimenta na osnovu recenzija hotela 2                                                                                         |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|      21       |            Uvod u vremenske serije i predviđanje             |        [Vremenske serije](7-TimeSeries/README.md)        | Uvod u predviđanje vremenskih serija                                                                                         |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|      22       | ⚡️ Svjetska potrošnja električne energije ⚡️ - predviđanje vremenskih serija s ARIMA |        [Vremenske serije](7-TimeSeries/README.md)        | Predviđanje vremenskih serija s ARIMA                                                                                              |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|      23       |  ⚡️ Svjetska potrošnja električne energije ⚡️ - predviđanje vremenskih serija sa SVR  |        [Vremenske serije](7-TimeSeries/README.md)        | Predviđanje vremenskih serija sa Support Vector Regressor                                                                           |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|      24       |             Uvod u učenje s potkrepljenjem             | [Učenje s potkrepljenjem](8-Reinforcement/README.md) | Uvod u učenje s potkrepljenjem koristeći Q-Learning                                                                          |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|      25       |                 Pomozi Petru da izbjegne vuka! 🐺                  | [Učenje s potkrepljenjem](8-Reinforcement/README.md) | Učenje s potkrepljenjem u Gym okruženju                                                                                                      |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  Postscript   |            Scenariji i primjene ML u stvarnom svijetu            |      [ML u stvarnom svijetu](9-Real-World/README.md)       | Zanimljive i otkrivajuće stvarne primjene klasičnog ML-a                                                               |                                             [Lekcija](9-Real-World/1-Applications/README.md)                                              |                         Tim                         |
|  Postscript   |            Debugiranje modela u ML koristeći RAI nadzornu ploču          |      [ML u stvarnom svijetu](9-Real-World/README.md)       | Debugiranje modela u strojnog učenja koristeći Responsible AI nadzornu ploču                                                              |                                             [Lekcija](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [pronađite sve dodatne resurse za ovaj tečaj u našoj Microsoft Learn kolekciji](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## Offline pristup

Ovu dokumentaciju možete pokrenuti offline koristeći [Docsify](https://docsify.js.org/#/). Forkajte ovaj repozitorij, [installirajte Docsify](https://docsify.js.org/#/quickstart) na vašem lokalnom računalu, te u korijenskoj mapi ovog repozitorija unesite `docsify serve`. Web stranica će biti dostupna na portu 3000 na vašem localhostu: `localhost:3000`.

## PDF-ovi

Pronađite pdf nastavnog plana s poveznicama [ovdje](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf).


## 🎒 Ostali tečajevi

Naš tim proizvodi i druge tečajeve! Pogledajte:

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j za početnike](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js za početnike](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain za početnike](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agenti
[![AZD za početnike](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI za početnike](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![MCP za početnike](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![AI Agenti za početnike](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Serija generativne umjetne inteligencije
[![Generative AI for Beginners](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generative AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generative AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generative AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---

### Osnovno učenje
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---

### Serija Copilot
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## Dobivanje pomoći

Ako zapnete ili imate pitanja o izradi AI aplikacija. Pridružite se kolegama polaznicima i iskusnim programerima u raspravama o MCP-u. To je podržavajuća zajednica gdje su pitanja dobrodošla i znanje se slobodno dijeli.

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

Ako imate povratne informacije o proizvodu ili greške tijekom izrade posjetite:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## Dodatni savjeti za učenje

- Pregledajte bilježnice nakon svake lekcije za bolje razumijevanje.
- Vježbajte implementaciju algoritama sami.
- Istražujte stvarne skupove podataka koristeći naučene koncepte.

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**Odricanje od odgovornosti**:
Ovaj je dokument preveden pomoću AI usluge za prijevod [Co-op Translator](https://github.com/Azure/co-op-translator). Iako težimo točnosti, molimo imajte na umu da automatizirani prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku smatra se službenim i najpouzdanijim izvorom. Za kritične informacije preporučuje se profesionalni ljudski prijevod. Ne preuzimamo odgovornost za bilo kakve nesporazume ili pogrešna tumačenja koja proizlaze iz korištenja ovog prijevoda.
<!-- CO-OP TRANSLATOR DISCLAIMER END -->