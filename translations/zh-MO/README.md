[![GitHub license](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 多語言支持

#### 透過 GitHub Action 支持（自動化且始終保持最新）

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](../zh-HK/README.md) | [Chinese (Traditional, Macau)](./README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Khmer](../km/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](../th/README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **想要本地端 Clone？**
>
> 本倉庫包含超過 50 種語言的翻譯，會顯著增加下載大小。若只想 Clone 不包含翻譯檔案，可使用稀疏檢出：
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
> 這樣你可以用更快的下載速度獲得完成課程所需的所有內容。
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### 加入我們的社群

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

我們正在進行 Discord 上的 AI 學習系列，請於 2025 年 9 月 18 - 30 日從 [Learn with AI Series](https://aka.ms/learnwithai/discord) 獲得更多資訊並加入。我們將分享使用 GitHub Copilot 於數據科學的技巧與秘訣。

![Learn with AI series](../../translated_images/zh-MO/3.9b58fd8d6c373c20.webp)

# 機器學習初學者課程大綱

> 🌍 隨著我們透過世界文化探索機器學習，一起環遊世界吧 🌍

微軟的 Cloud Advocates 很高興提供這套為期 12 週、共 26 課的 <strong>機器學習</strong> 課程。在本課程中，你將學習所謂的<strong>經典機器學習</strong>，主要使用 Scikit-learn 函式庫，並避開深度學習部分，後者在我們的 [AI 初學者課程](https://aka.ms/ai4beginners) 裡有涵蓋。你也可以同時搭配我們的 [『數據科學初學者課程』](https://aka.ms/ds4beginners) 一起學習！

跟隨我們環遊世界，將這些經典技術應用於來自全球各地的資料。每堂課含課前和課後測驗、書面教學、解答、作業等。我們採用專案導向的教學法，讓你透過實作學習，是讓新技能穩固掌握的有效方式。

**✍️ 衷心感謝我們的作者們** Jen Looper、Stephen Howell、Francesca Lazzeri、Tomomi Imura、Cassie Breviu、Dmitry Soshnikov、Chris Noring、Anirban Mukherjee、Ornella Altunyan、Ruth Yakubu 與 Amy Boyd

**🎨 感謝我們的插畫師們** Tomomi Imura、Dasani Madipalli 與 Jen Looper

**🙏 特別感謝🙏 微軟學生大使的作者、審核者與內容貢獻者**，特別是 Rishit Dagli、Muhammad Sakib Khan Inan、Rohan Raj、Alexandru Petrescu、Abhishek Jaiswal、Nawrin Tabassum、Ioan Samuila 與 Snigdha Agarwal

**🤩 非常感謝微軟學生大使 Eric Wanjau、Jasleen Sondhi 與 Vidushi Gupta 幫助我們的 R 課程！**

# 入門指南

請遵照下列步驟：
1. <strong>分支此倉庫</strong>：點擊頁面右上角的「Fork」按鈕。
2. <strong>克隆此倉庫</strong>：   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [在我們的 Microsoft Learn 集合中找到本課程的所有額外資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **需要幫助？** 查看我們的 [疑難排解指南](TROUBLESHOOTING.md)，了解安裝、設定與執行課程常見問題解決方法。

**[學生們](https://aka.ms/student-page)**，使用此課程時，請將整個倉庫分支到你自己的 GitHub 帳號，然後獨立或與團隊完成練習：

- 從課前小測驗開始。
- 閱讀授課內容並完成活動，於每個知識檢查點暫停反思。
- 嘗試自己建置專案，以理解課程，而非僅執行解答程式碼；每個專案導向課程的 `/solution` 資料夾則提供了程式碼示範。
- 參加課後測驗。
- 完成挑戰題。
- 完成作業。
- 完成一組課程後，造訪 [討論區](https://github.com/microsoft/ML-For-Beginners/discussions) 並透過填寫「PAT」評分表格來「大聲學習」──PAT 是一種進度評估工具，填寫後能加深學習。你也可以對其它人的 PAT 作出回應，大家一起學習。

> 若想深入學習，我們建議你接續以下 [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) 模組和學習路徑。

<strong>教師們</strong>，我們提供了 [一些建議](for-teachers.md) 來協助您使用這套課程。

---

## 影片導覽

部分課程有短影片可看。你可以在課程中直接看到這些影片，或至 [Microsoft Developer YouTube 頻道的 ML for Beginners 播放列表](https://aka.ms/ml-beginners-videos) 觀看，點擊下方圖片即可連結。

[![ML for beginners banner](../../translated_images/zh-MO/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## 團隊介紹

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif 動畫製作者** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 點擊上方圖片觀看有關這個專案及創作者的影片！

---

## 教學理念

我們在建立本課程時選擇了兩項教學原則：確保為動手做的<strong>專案導向</strong>，並包含<strong>頻繁小測驗</strong>。此外，這個課程有一貫的<strong>主題</strong>以增進內容的凝聚力。

透過讓內容與專案對應，能提高學生的參與度，並增強概念的記憶。此外，課前低風險測驗能幫助學生定下學習主題的心態，課後測驗則促進再次記憶與鞏固。此課程設計靈活且有趣，可全部或部分學習。專案從簡單開始，隨著 12 週的推進持續變得更複雜。課程末還包含機器學習在現實世界應用的後記，可作為額外學分或討論基礎。

> 查閱我們的 [行為守則](CODE_OF_CONDUCT.md)、[貢獻指南](CONTRIBUTING.md)、[翻譯](..) 及 [疑難排解](TROUBLESHOOTING.md) 指引。我們歡迎您的建設性回饋！

## 每堂課包含

- 選擇性手繪筆記
- 選擇性補充影片
- 影片導覽（部分課程）
- [課前暖身測驗](https://ff-quizzes.netlify.app/en/ml/)
- 書面教學
- 專案導向課程含建置專案的步驟指引
- 知識檢查
- 挑戰題
- 補充閱讀
- 作業
- [課後測驗](https://ff-quizzes.netlify.app/en/ml/)
> <strong>關於語言的說明</strong>：這些課程主要以 Python 編寫，但也有很多課程可用於 R。要完成 R 課程，請前往 `/solution` 資料夾並尋找 R 課程。這些檔案具有 .rmd 副檔名，代表 **R Markdown** 檔案，簡單來說就是將 `程式碼區塊`（R 或其他語言）及 `YAML 標頭`（用來指示如何格式化輸出，如 PDF）嵌入 `Markdown 文件`。因此，它作為資料科學的典範創作框架，讓你能將程式碼、輸出及筆記以 Markdown 形式結合書寫。此外，R Markdown 文件可轉換為 PDF、HTML 或 Word 等格式。

> <strong>關於測驗的說明</strong>：所有測驗都包含在 [Quiz App folder](../../quiz-app) 中，共 52 個測驗，每個測驗有三題。測驗會從課程中連結，但你也可以在本機執行測驗應用程式；請參照 `quiz-app` 資料夾中的說明在本機託管或部署至 Azure。

| 課程編號 |                             主題                              |                   課程分類                   | 學習目標                                                                                                             |                                                              連結課程                                                               |                        作者                        |
| :-------: | :------------------------------------------------------------: | :------------------------------------------: | --------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|    01     |                機器學習入門                |      [Introduction](1-Introduction/README.md)       | 學習機器學習背後的基本概念                                                                                |                                             [Lesson](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|    02     |                機器學習的歷史                 |      [Introduction](1-Introduction/README.md)       | 了解此領域的歷史基礎                                                                                         |                                            [Lesson](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen and Amy                      |
|    03     |                 公平性與機器學習                  |      [Introduction](1-Introduction/README.md)       | 建立與應用機器學習模型時，學生應考量的公平性相關倫理議題                                                         |                                              [Lesson](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|    04     |                機器學習技術                 |      [Introduction](1-Introduction/README.md)       | 機器學習研究人員用來建立模型的技術                                                                        |                                          [Lesson](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris and Jen                     |
|    05     |                   回歸分析入門                   |        [Regression](2-Regression/README.md)         | 使用 Python 與 Scikit-learn 進行回歸模型入門                                                                   |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|    06     |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 資料視覺化與清理，為機器學習做準備                                                                           |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|    07     |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立線性及多項式回歸模型                                                                                     |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen and Dmitry • Eric Wanjau       |
|    08     |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立邏輯回歸模型                                                                                             |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|    09     |                          網頁應用程式 🔌                          |           [Web App](3-Web-App/README.md)            | 建立一個可使用您訓練模型的網頁應用程式                                                                        |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|    10     |                 分類入門                 |    [Classification](4-Classification/README.md)     | 清理、準備與視覺化資料；分類入門                                                                              | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen and Cassie • Eric Wanjau |
|    11     |             美味的亞洲和印度料理 🍜             |    [Classification](4-Classification/README.md)     | 分類器入門                                                                                                   | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen and Cassie • Eric Wanjau |
|    12     |             美味的亞洲和印度料理 🍜             |    [Classification](4-Classification/README.md)     | 更多分類器                                                                                                   | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen and Cassie • Eric Wanjau |
|    13     |             美味的亞洲和印度料理 🍜             |    [Classification](4-Classification/README.md)     | 使用您的模型建立推薦系統網頁應用程式                                                                          |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|    14     |                   聚類入門                   |        [Clustering](5-Clustering/README.md)         | 清理、準備和視覺化資料；聚類入門                                                                               |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|    15     |              探索奈及利亞音樂喜好 🎧              |        [Clustering](5-Clustering/README.md)         | 探索 K-平均法聚類                                                                                             |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|    16     |        自然語言處理入門 ☕️         |   [Natural language processing](6-NLP/README.md)    | 透過建立簡單機器人來學習自然語言處理基礎                                                                       |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|    17     |                      常見的 NLP 任務 ☕️                      |   [Natural language processing](6-NLP/README.md)    | 進一步了解處理語言結構時所需的常見自然語言處理任務                                                             |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|    18     |             翻譯與情感分析 ♥️              |   [Natural language processing](6-NLP/README.md)    | 與珍·奧斯汀一起進行情感及翻譯分析                                                                               |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|    19     |                  浪漫歐洲飯店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用飯店評論進行情感分析 1                                                                                      |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|    20     |                  浪漫歐洲飯店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用飯店評論進行情感分析 2                                                                                      |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|    21     |            時間序列預測入門             |        [Time series](7-TimeSeries/README.md)        | 時間序列預測入門                                                                                               |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|    22     | ⚡️ 全球用電量 ⚡️ - ARIMA 的時間序列預測 |        [Time series](7-TimeSeries/README.md)        | 使用 ARIMA 進行時間序列預測                                                                                      |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|    23     |  ⚡️ 全球用電量 ⚡️ - SVR 的時間序列預測  |        [Time series](7-TimeSeries/README.md)        | 使用支持向量迴歸進行時間序列預測                                                                                |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|    24     |             強化學習入門             | [Reinforcement learning](8-Reinforcement/README.md) | 以 Q-Learning 介紹強化學習                                                                                      |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|    25     |                 協助彼得躲避狼！🐺                  | [Reinforcement learning](8-Reinforcement/README.md) | 強化學習 Gym                                                                                                   |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  附錄   |            真實世界的機器學習場景與應用            |      [ML in the Wild](9-Real-World/README.md)       | 傳統機器學習在真實世界有趣且具啟發性的應用                                                                       |                                             [Lesson](9-Real-World/1-Applications/README.md)                                              |                         Team                         |
|  附錄   |            使用 RAI 儀表板進行機器學習模型除錯          |      [ML in the Wild](9-Real-World/README.md)       | 使用 Responsible AI 儀表板元件對機器學習模型進行除錯                                                               |                                             [Lesson](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [在我們的 Microsoft Learn 集合中找到本課程的所有額外資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## 離線存取

你可以使用 [Docsify](https://docsify.js.org/#/) 離線執行本文件。請 fork 此倉庫，在本機安裝 [Docsify](https://docsify.js.org/#/quickstart)，然後在此倉庫的根目錄輸入 `docsify serve`。網站將在你的本地主機 3000 端口執行：`localhost:3000`。

## PDF 檔案

在 [這裡](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf) 找到課程綱要的 PDF，內含連結。

## 🎒 其他課程

我們團隊也有其他課程！請查看：

<!-- CO-OP TRANSLATOR OTHER COURSES START -->
### LangChain
[![LangChain4j for Beginners](https://img.shields.io/badge/LangChain4j%20for%20Beginners-22C55E?style=for-the-badge&&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchain4j-for-beginners)
[![LangChain.js for Beginners](https://img.shields.io/badge/LangChain.js%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://aka.ms/langchainjs-for-beginners?WT.mc_id=m365-94501-dwahlin)
[![LangChain for Beginners](https://img.shields.io/badge/LangChain%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=0553D6)](https://github.com/microsoft/langchain-for-beginners?WT.mc_id=m365-94501-dwahlin)
---

### Azure / Edge / MCP / Agents
[![AZD for Beginners](https://img.shields.io/badge/AZD%20for%20Beginners-0078D4?style=for-the-badge&labelColor=E5E7EB&color=0078D4)](https://github.com/microsoft/AZD-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Edge AI for Beginners](https://img.shields.io/badge/Edge%20AI%20for%20Beginners-00B8E4?style=for-the-badge&labelColor=E5E7EB&color=00B8E4)](https://github.com/microsoft/edgeai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![入門 MCP](https://img.shields.io/badge/MCP%20for%20Beginners-009688?style=for-the-badge&labelColor=E5E7EB&color=009688)](https://github.com/microsoft/mcp-for-beginners?WT.mc_id=academic-105485-koreyst)
[![入門 AI 代理人](https://img.shields.io/badge/AI%20Agents%20for%20Beginners-00C49A?style=for-the-badge&labelColor=E5E7EB&color=00C49A)](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### 生成式 AI 系列
[![入門生成式 AI](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![生成式 AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![生成式 AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![生成式 AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### 核心學習
[![入門機器學習](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![入門數據科學](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![入門 AI](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![入門網絡安全](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![入門網頁開發](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![入門物聯網](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![入門 XR 開發](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot 系列
[![AI 配對編程 Copilot](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![C#/.NET Copilot](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot 冒險](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## 尋求幫助

如果你遇到困難或對建立 AI 應用有任何疑問，歡迎加入學習者與經驗豐富的開發者討論 MCP 的群組。這是一個支持性的社群，歡迎提問並自由分享知識。

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

如果你在建立過程中有產品回饋或發現錯誤，請訪問：

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## 額外學習提示

- 每次課後復習筆記本以加深理解。
- 練習自行實作演算法。
- 利用所學概念探索真實世界數據集。

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 翻譯而成。雖然我們致力於翻譯準確，但請注意自動翻譯可能包含錯誤或不準確之處。原始文件以其原文版本為權威資料。對於關鍵資訊，建議採用專業人工翻譯。我們不對因使用本翻譯所引致之任何誤解或誤釋承擔責任。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->