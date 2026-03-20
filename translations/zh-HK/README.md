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
[阿拉伯語](../ar/README.md) | [孟加拉語](../bn/README.md) | [保加利亞語](../bg/README.md) | [緬甸語 (緬甸)](../my/README.md) | [中文 (簡體)](../zh-CN/README.md) | [中文 (繁體, 香港)](./README.md) | [中文 (繁體, 澳門)](../zh-MO/README.md) | [中文 (繁體, 台灣)](../zh-TW/README.md) | [克羅地亞語](../hr/README.md) | [捷克語](../cs/README.md) | [丹麥語](../da/README.md) | [荷蘭語](../nl/README.md) | [愛沙尼亞語](../et/README.md) | [芬蘭語](../fi/README.md) | [法語](../fr/README.md) | [德語](../de/README.md) | [希臘語](../el/README.md) | [希伯來語](../he/README.md) | [印地語](../hi/README.md) | [匈牙利語](../hu/README.md) | [印尼語](../id/README.md) | [義大利語](../it/README.md) | [日語](../ja/README.md) | [卡納達語](../kn/README.md) | [韓語](../ko/README.md) | [立陶宛語](../lt/README.md) | [馬來語](../ms/README.md) | [馬拉雅拉姆語](../ml/README.md) | [馬拉地語](../mr/README.md) | [尼泊爾語](../ne/README.md) | [奈及利亞皮欽語](../pcm/README.md) | [挪威語](../no/README.md) | [波斯語 (法爾西語)](../fa/README.md) | [波蘭語](../pl/README.md) | [葡萄牙語（巴西）](../pt-BR/README.md) | [葡萄牙語（葡萄牙）](../pt-PT/README.md) | [旁遮普語 (古魯穆奇)](../pa/README.md) | [羅馬尼亞語](../ro/README.md) | [俄語](../ru/README.md) | [塞爾維亞語 (西里爾字母)](../sr/README.md) | [斯洛伐克語](../sk/README.md) | [斯洛文尼亞語](../sl/README.md) | [西班牙語](../es/README.md) | [斯瓦希里語](../sw/README.md) | [瑞典語](../sv/README.md) | [塔加洛語 (菲律賓語)](../tl/README.md) | [泰米爾語](../ta/README.md) | [泰盧固語](../te/README.md) | [泰語](../th/README.md) | [土耳其語](../tr/README.md) | [烏克蘭語](../uk/README.md) | [烏爾都語](../ur/README.md) | [越南語](../vi/README.md)

> **偏好本地克隆？**
>
> 此存儲庫包含 50 多種語言的翻譯，會大幅增加下載大小。若想不含翻譯檔，請使用稀疏檢出（sparse checkout）：
>
> **Bash / macOS / Linux：**
> ```bash
> git clone --filter=blob:none --sparse https://github.com/microsoft/ML-For-Beginners.git
> cd ML-For-Beginners
> git sparse-checkout set --no-cone '/*' '!translations' '!translated_images'
> ```
>
> **CMD (Windows)：**
> ```cmd
> git clone --filter=blob:none --sparse https://github.com/microsoft/ML-For-Beginners.git
> cd ML-For-Beginners
> git sparse-checkout set --no-cone "/*" "!translations" "!translated_images"
> ```
>
> 這能讓你快速取得完整課程所需內容，下載速度更快。
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### 加入我們的社群

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

我們正舉行 Discord 的 AI 學習系列活動，詳細內容及加入請見 [Learn with AI Series](https://aka.ms/learnwithai/discord)，活動期間為 2025 年 9 月 18 日至 30 日。你將獲得使用 GitHub Copilot 於資料科學的技巧與秘訣。

![Learn with AI series](../../translated_images/zh-HK/3.9b58fd8d6c373c20.webp)

# 初學者機器學習課程大綱

> 🌍 透過世界文化探索機器學習，一同環遊世界 🌍

微軟的 Cloud Advocates 為大家帶來一個為期 12 週、共 26 課的 **機器學習** 課程。在這課程中，你將學習有時稱為 **經典機器學習** 的內容，主要使用 Scikit-learn 函式庫，並避開深度學習內容，後者已包含於我們的 [AI for Beginners 課程](https://aka.ms/ai4beginners) 中。也可以搭配我們的 [「初學者資料科學」課程](https://aka.ms/ds4beginners) 一起學習。

跟著我們環遊世界，將這些經典技術應用於來自世界各地的數據。每課包含課前與課後的測驗、課文說明、解答、作業和更多。我們採用以專案為基礎的教學法，讓你在實作中學習，這是新技能穩固的有效方法。

**✍️ 衷心感謝我們的作者團隊** Jen Looper、Stephen Howell、Francesca Lazzeri、Tomomi Imura、Cassie Breviu、Dmitry Soshnikov、Chris Noring、Anirban Mukherjee、Ornella Altunyan、Ruth Yakubu 和 Amy Boyd

**🎨 也感謝插畫師** Tomomi Imura、Dasani Madipalli 和 Jen Looper

**🙏 特別感謝 🙏 微軟學生大使作者、審稿和內容貢獻者**，尤其是 Rishit Dagli、Muhammad Sakib Khan Inan、Rohan Raj、Alexandru Petrescu、Abhishek Jaiswal、Nawrin Tabassum、Ioan Samuila 和 Snigdha Agarwal

**🤩 另外感謝微軟學生大使 Eric Wanjau、Jasleen Sondhi 和 Vidushi Gupta 為我們的 R 課程付出！**

# 開始使用

請依照以下步驟操作：
1. **Fork 該儲存庫**：點擊本頁右上角的「Fork」按鈕。
2. **Clone 該儲存庫**：`git clone https://github.com/microsoft/ML-For-Beginners.git`

> [在我們的 Microsoft Learn 集合中找到本課程所有額外資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **需要協助？** 請查看我們的 [故障排解指南](TROUBLESHOOTING.md)，解決一般安裝、設定及執行課程問題。

**[學生](https://aka.ms/student-page)**，使用此課程請 fork 完整儲存庫至你的 GitHub 帳號，並自行或與小組完成練習：

- 先完成課前測驗。
- 閱讀課文並完成活動，每進行一段知識點檢查就暫停並反思。
- 嘗試透過理解課程內容自己做專案，而非直接執行解答程式碼；不過每個專案課程的 `/solution` 資料夾內有完整解答程式碼可參考。
- 做完課後測驗。
- 完成挑戰題。
- 完成作業。
- 完成一組課程後，請到 [討論板](https://github.com/microsoft/ML-For-Beginners/discussions) 分享學習心得，並填寫對應的 PAT 量表。PAT 是進度評估工具，藉由填寫來深化學習。你也可以對其他人的 PAT 進行回應，一同學習。

> 建議參考以下這些 [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott) 模組及學習路線作進一步學習。

**老師們**，我們也有提供一些 [使用建議](for-teachers.md)。

---

## 影片導覽

部分課程可透過短影片學習。可於課程中直接觀看，或至 [Microsoft Developer YouTube 頻道 ML for Beginners 播放清單](https://aka.ms/ml-beginners-videos) 由下方圖片連結進入。

[![ML for beginners banner](../../translated_images/zh-HK/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## 團隊介紹

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**GIF 製作者** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 點擊上方圖片觀看關於該專案及製作者的影片！

---

## 教學理念

我們建立此課程時，選擇兩項教學原則：確保為實作導向 **以專案為本** 且包含 **頻繁測驗**。此外，課程具有統一的 **主題** 以增強連貫性。

透過以專案對應內容，提高學習趣味與概念記憶度。課前低風險的測驗設定學習目標，課後再測則加強記憶。課程設計靈活有趣，可全部或部分修習。專案由淺入深，涵蓋 12 週內容。課程還提供機器學習實務應用的後記，適合作為額外學分或討論基礎。

> 請參考我們的 [行為守則](CODE_OF_CONDUCT.md)、[貢獻指南](CONTRIBUTING.md)、[翻譯說明](..) 及 [故障排解](TROUBLESHOOTING.md) 指南。歡迎提供建設性回饋！

## 各課程皆包含

- 選填手繪筆記
- 選填補充影片
- 影片導覽（部分課程）
- [課前暖身測驗](https://ff-quizzes.netlify.app/en/ml/)
- 課文資料
- 專案課程含逐步專案建置教學
- 知識檢核
- 挑戰題
- 補充閱讀
- 作業
- [課後測驗](https://ff-quizzes.netlify.app/en/ml/)

> **關於語言的說明**：本課程主要採 Python 編寫，但許多內容也有 R 版本。要完成 R 課程，請至 `/solution` 資料夾尋找 R 檔案。這些檔案有 .rmd 副檔名，代表 **R Markdown** 文件，是 Markdown 文件中嵌入 R 或其他程式碼區塊與 YAML 標頭（控制輸出格式如 PDF）的格式。因此 R Markdown 是一個優秀的資料科學撰寫框架，允許你將程式碼、結果與筆記合為一體，並可以輸出成 PDF、HTML 或 Word 等格式。
> **關於小測驗的說明**：所有小測驗均包含在 [Quiz App folder](../../quiz-app) 中，共有 52 個小測驗，每個包含三條問題。這些小測驗在課程中均有連結，但測驗應用程式亦可在本地運行；請按照 `quiz-app` 文件夾中的說明在本地端託管或部署至 Azure。

| Lesson Number |                             Topic                              |                   Lesson Grouping                   | Learning Objectives                                                                                                             |                                                              Linked Lesson                                                               |                        Author                        |
| :-----------: | :------------------------------------------------------------: | :-------------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|      01       |                機器學習簡介                |      [Introduction](1-Introduction/README.md)       | 學習機器學習背後的基本概念                                                                                |                                             [Lesson](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|      02       |                機器學習的歷史                 |      [Introduction](1-Introduction/README.md)       | 學習此領域的歷史                                                                                         |                                            [Lesson](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen and Amy                      |
|      03       |                 公平性與機器學習                  |      [Introduction](1-Introduction/README.md)       | 學生在建構與應用機器學習模型時，應考慮之公平性重要哲學議題為何？ |                                              [Lesson](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|      04       |                機器學習技術                 |      [Introduction](1-Introduction/README.md)       | 機器學習研究者用以建立機器學習模型的技術有哪些？                                                                       |                                          [Lesson](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris and Jen                     |
|      05       |                   回歸簡介                   |        [Regression](2-Regression/README.md)         | 開始使用 Python 及 Scikit-learn 進行回歸模型                                                                  |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|      06       |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 視覺化並清理資料以準備進行機器學習                                                                                  |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|      07       |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立線性與多項式回歸模型                                                                                   |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen and Dmitry • Eric Wanjau       |
|      08       |                北美南瓜價格 🎃                |        [Regression](2-Regression/README.md)         | 建立邏輯回歸模型                                                                                               |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|      09       |                          網頁應用 🔌                          |           [Web App](3-Web-App/README.md)            | 建立一個用以運行你的訓練模型的網頁應用                                                                                       |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|      10       |                 分類簡介                 |    [Classification](4-Classification/README.md)     | 清理、預備和視覺化資料；分類初探                                                            | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen and Cassie • Eric Wanjau |
|      11       |             美味的亞洲與印度料理 🍜             |    [Classification](4-Classification/README.md)     | 分類器入門                                                                                                     | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen and Cassie • Eric Wanjau |
|      12       |             美味的亞洲與印度料理 🍜             |    [Classification](4-Classification/README.md)     | 更多分類器                                                                                                                | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen and Cassie • Eric Wanjau |
|      13       |             美味的亞洲與印度料理 🍜             |    [Classification](4-Classification/README.md)     | 使用你的模型建立推薦系統網頁應用                                                                                    |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|      14       |                   叢集簡介                   |        [Clustering](5-Clustering/README.md)         | 清理、預備及視覺化資料；叢集簡介                                                                |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|      15       |              探索奈及利亞的音樂品味 🎧              |        [Clustering](5-Clustering/README.md)         | 探索 K-Means 叢集方法                                                                                           |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|      16       |        自然語言處理簡介 ☕️         |   [Natural language processing](6-NLP/README.md)    | 透過建立簡易機器人學習 NLP 基礎                                                                             |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|      17       |                      常見 NLP 任務 ☕️                      |   [Natural language processing](6-NLP/README.md)    | 深入理解處理語言結構時所需之常見任務                          |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|      18       |             翻譯與情感分析 ♥️              |   [Natural language processing](6-NLP/README.md)    | 以珍·奧斯汀作品做翻譯與情感分析                                                                             |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|      19       |                  歐洲浪漫酒店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用酒店評論做情感分析 1                                                                                         |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|      20       |                  歐洲浪漫酒店 ♥️                  |   [Natural language processing](6-NLP/README.md)    | 使用酒店評論做情感分析 2                                                                                         |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|      21       |            時間序列預測簡介             |        [Time series](7-TimeSeries/README.md)        | 時間序列預測入門                                                                                         |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|      22       | ⚡️ 世界電力使用量 ⚡️ - ARIMA 時間序列預測 |        [Time series](7-TimeSeries/README.md)        | 使用 ARIMA 進行時間序列預測                                                                                              |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|      23       |  ⚡️ 世界電力使用量 ⚡️ - SVR 時間序列預測  |        [Time series](7-TimeSeries/README.md)        | 使用支持向量回歸（SVR）模型進行時間序列預測                                                                           |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|      24       |             強化學習簡介             | [Reinforcement learning](8-Reinforcement/README.md) | 使用 Q-學習介紹強化學習                                                                          |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|      25       |                 幫助 Peter 避開狼！ 🐺                  | [Reinforcement learning](8-Reinforcement/README.md) | 強化學習 Gym                                                                                                      |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  後記   |            真實世界機器學習應用            |      [ML in the Wild](9-Real-World/README.md)       | 有趣且啟發性十足的傳統機器學習真實案例                                                               |                                             [Lesson](9-Real-World/1-Applications/README.md)                                              |                         Team                         |
|  後記   |            使用 RAI 儀表板進行機器學習模型除錯           |      [ML in the Wild](9-Real-World/README.md)       | 使用 Responsible AI 儀表板元件進行機器學習模型除錯                                                              |                                             [Lesson](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [在我們的 Microsoft Learn 集合中找到此課程所有額外資源](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## 離線存取

你可使用 [Docsify](https://docsify.js.org/#/) 離線運行本文件。叉出這個儲存庫，在本地機器上[安裝 Docsify](https://docsify.js.org/#/quickstart)，然後在本儲存庫的根目錄輸入 `docsify serve`。此網站會在你的本地主機的 3000 埠口提供服務：`localhost:3000`。

## PDF

此課程課綱連結的 pdf 文件 [在此](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf)。


## 🎒 其他課程 

我們團隊製作其他課程！敬請參閱：

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
[![初學者的生成式人工智能](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![生成式人工智能 (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![生成式人工智能 (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![生成式人工智能 (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### 核心學習
[![初學者的機器學習](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![初學者的數據科學](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![初學者的人工智能](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![初學者的網絡安全](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![初學者的網頁開發](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![初學者的物聯網](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![初學者的擴增實境開發](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### Copilot 系列
[![人工智能配對程式設計的 Copilot](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![C#/.NET 的 Copilot](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot 冒險](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## 尋求協助

如果你遇到困難或對建立人工智能應用程式有任何疑問，歡迎加入學習者和經驗豐富開發者的討論。這是一個支持性的社群，歡迎提出問題並自由分享知識。

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

如果你在建構產品時有反饋或錯誤，請訪問：

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## 額外學習提示

- 完成每課後，回顧筆記以加深理解。
- 自行練習實現算法。
- 運用所學概念探索實際的數據集。

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**免責聲明**：
本文件使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於準確性，但請注意自動翻譯可能包含錯誤或不準確之處。原始文件的原文版本應視為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們不對因使用此翻譯而引起的任何誤解或誤釋負責。
<!-- CO-OP TRANSLATOR DISCLAIMER END -->