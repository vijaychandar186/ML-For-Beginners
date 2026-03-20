[![GitHub license](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 多語言支援

#### 透過 GitHub Action 支援（自動且保持最新）

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](../zh-HK/README.md) | [Chinese (Traditional, Macau)](./README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](../th/README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **想本地克隆？**
>
> 本倉庫包含 50 多種語言翻譯，會大幅增加下載大小。若想克隆但不帶翻譯，請使用稀疏檢出：
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
> 這樣可以讓您以更快速度下載，完成課程所有所需內容。
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### 加入我們的社群

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

我們有一個持續進行的 Discord AI 學習系列，了解更多及加入我們請訪問 [Learn with AI Series](https://aka.ms/learnwithai/discord)（2025年9月18日至30日）。您將學習使用 GitHub Copilot 進行資料科學的技巧與秘訣。

![Learn with AI series](../../translated_images/zh-MO/3.9b58fd8d6c373c20.webp)

# 初學者機器學習課程大綱

> 🌍 跟隨我們透過世界文化探索機器學習之旅 🌍

微軟的雲端倡導者很高興提供一套為期 12 週、共 26 課的 **機器學習** 課程。在這套課程中，您將學習所謂的 **傳統機器學習**，主要使用 Scikit-learn 函式庫，並避開深度學習（深度學習部份收錄於我們的 [初學者人工智能課程](https://aka.ms/ai4beginners)）。同時建議搭配我們的 [初學者資料科學課程](https://aka.ms/ds4beginners)。

跟著我們一起環遊世界，將經典技術應用於來自世界各地的數據。每堂課包含課前與課後小測、書面說明完成課程步驟、解答、作業等。我們以專案為基礎的教學法讓您在建構專案中同時學習，這是讓新技能更穩固的有效方法。

**✍️ 衷心感謝作者** Jen Looper、Stephen Howell、Francesca Lazzeri、Tomomi Imura、Cassie Breviu、Dmitry Soshnikov、Chris Noring、Anirban Mukherjee、Ornella Altunyan、Ruth Yakubu 以及 Amy Boyd

**🎨 同時感謝插畫者** Tomomi Imura、Dasani Madipalli 和 Jen Looper

**🙏 特別感謝 Microsoft 學生大使們的作者、審閱者與內容貢獻者**，特別是 Rishit Dagli、Muhammad Sakib Khan Inan、Rohan Raj、Alexandru Petrescu、Abhishek Jaiswal、Nawrin Tabassum、Ioan Samuila 和 Snigdha Agarwal

**🤩 額外感謝 Microsoft 學生大使 Eric Wanjau、Jasleen Sondhi 與 Vidushi Gupta 協助我們製作 R 課程！**

# 開始之前

請依序執行下列步驟：
1. **Fork 此倉庫**：點擊頁面右上角的「Fork」按鈕。
2. **複製倉庫**：   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [你可在我們的 Microsoft Learn 集合中找到本課程所有額外資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **需要幫忙？** 請查閱我們的 [故障排除指南](TROUBLESHOOTING.md)，了解常見安裝、設定及執行課程問題的解決方案。

**[學生們](https://aka.ms/student-page)**，請將此課程倉庫全部 Fork 至自己的 GitHub 帳號，並自行或與團隊完成練習：

- 先完成課前小測。
- 閱讀課程內容並完成活動，在每個知識點暫停並思考。
- 嘗試自行理解課程內容完成專案，而非直接執行解答程式碼；該解答程式碼可在每個專案主題課程的 `/solution` 資料夾找到。
- 完成課後小測。
- 完成挑戰題。
- 完成作業。
- 完成本組課程後，請到 [討論區](https://github.com/microsoft/ML-For-Beginners/discussions) 填寫 PAT 評量表以「大聲學習」。PAT 是一種你填寫以促進學習的進度評估工具。你也可以對其他人的 PAT 留下回應，大家一起學習。

> 若要深入學習，我們建議參考這些 [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) 模組與學習路徑。

**教師們**，我們提供了關於如何使用此課程的[建議說明](for-teachers.md)。

---

## 影片導覽

部分課程提供短影片說明。您可在課程內內嵌觀看，也可到 [Microsoft 開發者 YouTube 頻道的 ML 初學者播放清單](https://aka.ms/ml-beginners-videos) 點擊下方圖片觀看。

[![ML for beginners banner](../../translated_images/zh-MO/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## 認識團隊

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif 來源** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 點擊上方圖片觀看關於專案和作者們的影片！

---

## 教學理念

我們在構建此課程時選擇了兩大教學原則：確保實作為主的**專案導向**，並加入**頻繁的小測**。此外，本課程具備共同的**主題性**以增強連貫性。

確保內容與專案相符，能讓學生更加投入且增強概念記憶。課前低壓力小測確立學習目標，課後小測則幫助深化記憶。本課程設計靈活且有趣，可全文修讀或部分學習。專案規模由小至大，至 12 週結束達成較複雜程度。此外，課程還包含機器學習現實應用後記，可用作額外學分或討論基礎。

> 請參閱我們的 [行為準則](CODE_OF_CONDUCT.md)、[貢獻指南](CONTRIBUTING.md)、[翻譯](..)與[故障排除](TROUBLESHOOTING.md) 文件。歡迎提供建設性意見！

## 每堂課包含

- 可選手繪筆記
- 可選補充影片
- 影片導覽（部分課程）
- [課前暖身小測](https://ff-quizzes.netlify.app/en/ml/)
- 書面課程說明
- 專案課程逐步指引
- 知識檢核
- 挑戰題
- 補充閱讀資料
- 作業
- [課後小測](https://ff-quizzes.netlify.app/en/ml/)

> **語言說明**：這些課程主要使用 Python 撰寫，但許多也有 R 版本。要完成 R 課程，請前往 `/solution` 資料夾尋找 .rmd 檔案，這是 **R Markdown** 文件，結合了 `R 語言或其他語言代碼區塊` 和一個用來指示如何格式化輸出（如 PDF）的 `YAML 標頭`，內含 Markdown 文件。本格式提供數據科學優秀的撰寫框架，可將程式碼、輸出與想法寫入 Markdown 文件中。此外，R Markdown 文件能編譯輸出成 PDF、HTML 或 Word 等格式。
> **關於小測驗的說明**：所有小測驗皆收錄於[Quiz App folder](../../quiz-app)，共52個小測驗，每個包含三個問題。小測驗會在課程中連結，但你也可以在本地執行小測驗應用程式；請遵循 `quiz-app` 資料夾內的指示進行本地託管或部署到 Azure。

| 課程編號 |                             主題                              |                   課程群組                   | 學習目標                                                                                                                         |                                                              連結課程                                                               |                        作者                        |
| :-------: | :------------------------------------------------------------: | :-------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|    01     |                機器學習介紹                |      [Introduction](1-Introduction/README.md)       | 學習機器學習的基本概念                                                                                 |                                             [Lesson](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|    02     |                機器學習的歷史                 |      [Introduction](1-Introduction/README.md)       | 瞭解此領域的歷史背景                                                                                         |                                            [Lesson](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen and Amy                      |
|    03     |                 公平性與機器學習                  |      [Introduction](1-Introduction/README.md)       | 學生應考慮建構及應用機器學習模型時需注意的重要哲學公平性議題                                            |                                              [Lesson](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|    04     |                機器學習技術                 |      [Introduction](1-Introduction/README.md)       | 機器學習研究者用來建立模型的技術有哪些？                                                                       |                                          [Lesson](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris and Jen                     |
|    05     |                   回歸介紹                   |        [Regression](2-Regression/README.md)         | 開始使用 Python 與 Scikit-learn 進行回歸模型建構                                                                  |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|    06     |                北美地區南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 視覺化並清理資料以準備機器學習                                                                                  |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|    07     |                北美地區南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立線性及多項式回歸模型                                                                                   |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen and Dmitry • Eric Wanjau       |
|    08     |                北美地區南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立邏輯回歸模型                                                                                               |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|    09     |                          網頁應用程式 🔌                          |           [Web App](3-Web-App/README.md)            | 建立使用你訓練好的模型的網頁應用程式                                                                                       |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|    10     |                 分類介紹                 |    [Classification](4-Classification/README.md)     | 清理、準備及視覺化資料；分類介紹                                                            | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen and Cassie • Eric Wanjau |
|    11     |             美味亞洲及印度料理 🍜             |    [Classification](4-Classification/README.md)     | 分類器介紹                                                                                                     | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen and Cassie • Eric Wanjau |
|    12     |             美味亞洲及印度料理 🍜             |    [Classification](4-Classification/README.md)     | 更多分類器                                                                                                                | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen and Cassie • Eric Wanjau |
|    13     |             美味亞洲及印度料理 🍜             |    [Classification](4-Classification/README.md)     | 使用你的模型建立推薦系統網頁應用程式                                                                                    |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|    14     |                   聚類介紹                   |        [Clustering](5-Clustering/README.md)         | 清理、準備及視覺化資料；聚類介紹                                                                |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|    15     |              探索尼日利亞音樂品味 🎧              |        [Clustering](5-Clustering/README.md)         | 探索 K-Means 聚類方法                                                                                           |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|    16     |        自然語言處理介紹 ☕️         |   [Natural language processing](6-NLP/README.md)    | 通過建立簡單的機器人了解 NLP 基礎                                                                             |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|    17     |                      常見 NLP 任務 ☕️                      |   [Natural language processing](6-NLP/README.md)    | 通過理解處理語言結構所需的常見任務來深化你的 NLP 知識                          |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|    18     |             翻譯與情感分析 ♥️              |   [Natural language processing](6-NLP/README.md)    | 使用 Jane Austen 進行翻譯與情感分析                                                                             |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|    19     |                  歐洲浪漫飯店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用旅館評論進行情感分析 1                                                                                         |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|    20     |                  歐洲浪漫飯店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用旅館評論進行情感分析 2                                                                                         |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|    21     |            時間序列預測介紹             |        [Time series](7-TimeSeries/README.md)        | 時間序列預測入門                                                                                         |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|    22     | ⚡️ 全球電力使用 ⚡️ - 使用 ARIMA 進行時間序列預測 |        [Time series](7-TimeSeries/README.md)        | 使用 ARIMA 進行時間序列預測                                                                                              |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|    23     |  ⚡️ 全球電力使用 ⚡️ - 使用 SVR 進行時間序列預測  |        [Time series](7-TimeSeries/README.md)        | 使用支持向量迴歸進行時間序列預測                                                                           |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|    24     |             強化學習介紹             | [Reinforcement learning](8-Reinforcement/README.md) | 使用 Q-Learning 進行強化學習入門                                                                          |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|    25     |                 幫彼得躲避狼！🐺                  | [Reinforcement learning](8-Reinforcement/README.md) | 強化學習 Gym                                                                                                      |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  附錄   |            真實世界的機器學習案例與應用            |      [ML in the Wild](9-Real-World/README.md)       | 有趣且具啟發性的經典機器學習真實應用案例                                                               |                                             [Lesson](9-Real-World/1-Applications/README.md)                                              |                         團隊                         |
|  附錄   |            使用 RAI 儀表板進行機器學習模型調試          |      [ML in the Wild](9-Real-World/README.md)       | 使用 Responsible AI 儀表板組件進行機器學習模型調試                                                              |                                             [Lesson](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [在我們的 Microsoft Learn 集合中找到此課程的所有其他資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## 離線存取

您可以使用 [Docsify](https://docsify.js.org/#/) 離線運行此文件。將本倉庫 fork，並在本地機器上安裝 [Docsify](https://docsify.js.org/#/quickstart)，然後在本倉庫根資料夾鍵入 `docsify serve`。網站將在您本地的 3000 端口提供服務：`localhost:3000`。

## PDF 檔案

請在[這裡](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf)下載帶有連結的課程大綱 PDF。

## 🎒 其他課程

我們團隊還製作其他課程！請參考：

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
 
### 生成式 AI 系列
[![Generative AI for Beginners](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generative AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generative AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generative AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### 核心學習
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot 系列
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## 獲取幫助

如果你遇到困難或有任何關於建立 AI 應用程式的問題，歡迎加入 MCP 的學習者和有經驗開發者討論。這是一個支持性的社群，歡迎提問並自由分享知識。

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

如果你有產品反饋或在開發時遇到錯誤，請訪問：

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## 額外學習提示

- 每課後回顧筆記本以增進理解。
- 練習自行實作演算法。
- 探索使用所學概念的實際數據集。

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：  
本文件係使用AI翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們力求準確，但請注意，自動翻譯可能包含錯誤或不準確之處。文件原文版本應被視為權威依據。對於重要資訊，建議使用專業人工翻譯。我們對因使用此翻譯而導致之任何誤解或誤釋不承擔任何責任。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->