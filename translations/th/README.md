[![GitHub license](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 การสนับสนุนหลายภาษา

#### สนับสนุนผ่าน GitHub Action (อัตโนมัติและอัปเดตอยู่เสมอ)

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](../zh-HK/README.md) | [Chinese (Traditional, Macau)](../zh-MO/README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](./README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **ชอบที่จะโคลนในเครื่องมั้ย?**
>
> โครงการนี้มีการแปลในมากกว่า 50 ภาษา ซึ่งจะเพิ่มขนาดไฟล์ดาวน์โหลดอย่างมาก หากต้องการโคลนโดยไม่รวมการแปล ให้ใช้ sparse checkout:
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
> นี้จะให้ทุกอย่างที่คุณต้องการเพื่อเรียนจบหลักสูตรด้วยการดาวน์โหลดที่รวดเร็วมากขึ้น
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### เข้าร่วมชุมชนของเรา

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

เรามีซีรีส์เรียนรู้กับ AI บน Discord ดำเนินการอยู่ เรียนรู้เพิ่มเติมและเข้าร่วมกับเราที่ [Learn with AI Series](https://aka.ms/learnwithai/discord) ตั้งแต่วันที่ 18 - 30 กันยายน 2025 คุณจะได้รับเคล็ดลับและกลเม็ดการใช้ GitHub Copilot สำหรับด้าน Data Science

![Learn with AI series](../../translated_images/th/3.9b58fd8d6c373c20.webp)

# การเรียนรู้เครื่องสำหรับผู้เริ่มต้น - หลักสูตร

> 🌍 เที่ยวรอบโลกในขณะที่เราค้นพบการเรียนรู้เครื่องผ่านวัฒนธรรมโลก 🌍

Cloud Advocates ของ Microsoft มีความยินดีที่จะเสนอกหลักสูตร 12 สัปดาห์ 26 บทเรียนเกี่ยวกับ **Machine Learning** ในหลักสูตรนี้ คุณจะได้เรียนรู้เกี่ยวกับบางสิ่งที่เรียกว่า **classic machine learning** ใช้ Scikit-learn เป็นหลักและหลีกเลี่ยงการเรียนรู้เชิงลึกซึ่งมีการสอนในหลักสูตร [AI for Beginners ของเรา](https://aka.ms/ai4beginners) จับคู่บทเรียนเหล่านี้กับหลักสูตร ['Data Science for Beginners' ของเรา](https://aka.ms/ds4beginners) ด้วย!

เดินทางไปกับเราไปรอบโลกขณะที่เราประยุกต์ใช้เทคนิคคลาสสิกเหล่านี้กับข้อมูลจากหลายพื้นที่ของโลก แต่ละบทเรียนมีแบบทดสอบก่อนและหลังเรียน คำแนะนำเป็นลายลักษณ์อักษรเพื่อทำบทเรียนให้เสร็จสมบูรณ์ โซลูชัน งานมอบหมาย และอื่นๆ การสอนโดยมีโครงการเป็นฐานช่วยให้คุณเรียนรู้ไปพร้อมกับการสร้าง ซึ่งเป็นวิธีพิสูจน์แล้วว่าสำหรับการเรียนรู้ทักษะใหม่จะ 'ติด' 

**✍️ ขอขอบคุณอย่างจริงใจต่อผู้เขียนของเรา** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu และ Amy Boyd

**🎨 ขอบคุณนักวาดภาพประกอบ** Tomomi Imura, Dasani Madipalli และ Jen Looper

**🙏 ขอบคุณเป็นพิเศษ 🙏 ต่อตัวแทนนักศึกษาของ Microsoft ผู้เขียน ผู้ทบทวน และผู้ร่วมเนื้อหา** โดยเฉพาะอย่างยิ่ง Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila และ Snigdha Agarwal

**🤩 ขอบคุณพิเศษสำหรับ Microsoft Student Ambassadors Eric Wanjau, Jasleen Sondhi และ Vidushi Gupta สำหรับบทเรียน R ของเรา!**

# เริ่มต้น

ทำตามขั้นตอนเหล่านี้:
1. **Fork โครงการนี้**: คลิกที่ปุ่ม "Fork" ที่มุมบนขวาของหน้านี้
2. **โคลนโครงการนี้**:   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [ค้นหาทรัพยากรเพิ่มเติมทั้งหมดสำหรับหลักสูตรนี้ในคอลเลกชัน Microsoft Learn ของเรา](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **ต้องการความช่วยเหลือ?** ตรวจสอบ [คู่มือแก้ปัญหา](TROUBLESHOOTING.md) สำหรับวิธีแก้ปัญหาทั่วไปเกี่ยวกับการติดตั้ง การตั้งค่า และการรันบทเรียน

**[นักเรียน](https://aka.ms/student-page)** เพื่อใช้หลักสูตรนี้ ให้ฟอร์กรีโพทั้งหมดไปยังบัญชี GitHub ของคุณเองและทำแบบฝึกหัดด้วยตัวเองหรือกับกลุ่ม:

- เริ่มด้วยแบบทดสอบก่อนบรรยาย
- อ่านบทเรียนและทำกิจกรรมให้เสร็จสมบูรณ์ หยุดเพื่อสะท้อนความรู้ในแต่ละจุดตรวจสอบความเข้าใจ
- พยายามสร้างโครงการโดยเข้าใจบทเรียนแทนการรันโค้ดตัวอย่าง อย่างไรก็ตาม โค้ดนั้นมีอยู่ในโฟลเดอร์ `/solution` ในแต่ละบทเรียนที่เน้นโครงการ
- ทำแบบทดสอบหลังบรรยาย
- ทำความท้าทายให้เสร็จ
- ทำงานมอบหมายให้เสร็จ
- หลังจากจบบทเรียนแต่ละกลุ่ม ให้ไปที่ [กระดานอภิปราย](https://github.com/microsoft/ML-For-Beginners/discussions) และ "พูดออกเสียง" โดยกรอกแบบประเมิน PAT ที่เหมาะสม 'PAT' คือเครื่องมือประเมินความก้าวหน้าที่คุณกรอกเพื่อส่งเสริมการเรียนรู้ของคุณ คุณยังสามารถโต้ตอบกับ PAT ของคนอื่นเพื่อเรียนรู้ไปด้วยกัน

> สำหรับการศึกษาต่อ เราแนะนำให้ทำตามโมดูลและเส้นทางการเรียนรู้เหล่านี้ของ [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott)

**คุณครู** เรามี [คำแนะนำบางส่วน](for-teachers.md) เกี่ยวกับวิธีการใช้หลักสูตรนี้

---

## วิดีโอสอน

บทเรียนบางบทมีในรูปแบบวิดีโอสั้น คุณสามารถหาวิดีโอทั้งหมดนี้ในบทเรียน หรือ ที่ [เพลย์ลิสต์ ML for Beginners ในช่อง Microsoft Developer YouTube](https://aka.ms/ml-beginners-videos) โดยคลิกที่ภาพด้านล่าง

[![ML for beginners banner](../../translated_images/th/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## รู้จักทีมงาน

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**GIF โดย** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 คลิกที่ภาพด้านบนเพื่อดูวิดีโอเกี่ยวกับโครงการและทีมผู้สร้าง!

---

## วิธีการสอน

เราเลือกหลักการสอน 2 ประการขณะสร้างหลักสูตรนี้: การทำให้เป็นแบบ **project-based** ที่เน้นปฏิบัติ และการมี **แบบทดสอบบ่อยๆ** นอกจากนี้ หลักสูตรนี้มี **ธีม** ร่วมกันเพื่อให้มีความต่อเนื่อง

โดยการทำเนื้อหาให้สอดคล้องกับโครงการ เทคนิคนี้ทำให้นักเรียนมีส่วนร่วมมากขึ้นและช่วยเสริมการจดจำแนวคิด นอกจากนี้ แบบทดสอบที่ไม่มีแรงกดดันก่อนเรียนช่วยกำหนดเจตนารมณ์ของนักเรียนในการเรียนรู้หัวข้อ ขณะที่แบบทดสอบหลังเรียนช่วยเสริมการจำอีกครั้ง หลักสูตรนี้ออกแบบมาให้ยืดหยุ่นและสนุก และสามารถเรียนทั้งหลักสูตรหรือเลือกบางส่วนได้ โครงการเริ่มเล็กและซับซ้อนเพิ่มขึ้นเรื่อยๆ ภายใน 12 สัปดาห์ หลักสูตรนี้ยังรวมเนื้อหาด้านโลกจริงเกี่ยวกับแอปพลิเคชันของ ML ซึ่งสามารถใช้เป็นเครดิตพิเศษหรือฐานสำหรับการอภิปราย

> ค้นหา [จรรยาบรรณการปฏิบัติ](CODE_OF_CONDUCT.md), [การมีส่วนร่วม](CONTRIBUTING.md), [การแปล](..), และ [คู่มือแก้ปัญหา](TROUBLESHOOTING.md) ของเรา เราขอต้อนรับคำติชมที่สร้างสรรค์ของคุณ!

## แต่ละบทเรียนประกอบด้วย

- สเก็ตช์โน้ต (ไม่บังคับ)
- วิดีโอเสริม (ไม่บังคับ)
- วิดีโอสอน (เฉพาะบทเรียนบางบท)
- [แบบทดสอบวอร์มอัพก่อนบรรยาย](https://ff-quizzes.netlify.app/en/ml/)
- บทเรียนลายลักษณ์อักษร
- สำหรับบทเรียนแบบโปรเจค มีคำแนะนำทีละขั้นตอนในการสร้างโปรเจค
- การตรวจสอบความรู้
- ความท้าทาย
- การอ่านเสริม
- งานมอบหมาย
- [แบบทดสอบหลังบรรยาย](https://ff-quizzes.netlify.app/en/ml/)

> **หมายเหตุเกี่ยวกับภาษา**: บทเรียนเหล่านี้เขียนเป็นหลักในภาษา Python แต่หลายบทเรียนมีให้ใน R ด้วย เพื่อทำบทเรียน R ให้ไปที่โฟลเดอร์ `/solution` และมองหาบทเรียน R ซึ่งจะมีนามสกุล .rmd ซึ่งหมายถึง **R Markdown** ที่เป็นการผสมผสานของ `code chunks` (ของ R หรือภาษาอื่นๆ) และ `YAML header` (ที่กำหนดการฟอร์แมตผลลัพธ์ เช่น PDF) ภายในเอกสาร Markdown ด้วยเหตุนี้ R Markdown จึงเป็นกรอบการเขียนตัวอย่างที่ยอดเยี่ยมสำหรับ data science เพราะช่วยให้คุณรวมโค้ด ผลลัพธ์ และความคิดของคุณโดยเขียนลงใน Markdown นอกจากนี้ เอกสาร R Markdown ยังสามารถแปลงเป็นรูปแบบผลลัพธ์ เช่น PDF, HTML หรือ Word ได้อีกด้วย
> **หมายเหตุเกี่ยวกับแบบทดสอบ**: แบบทดสอบทั้งหมดถูกจัดเก็บอยู่ใน [โฟลเดอร์ Quiz App](../../quiz-app) รวมทั้งหมด 52 แบบทดสอบ แต่ละแบบประกอบด้วยสามคำถาม สามารถเข้าถึงได้จากบทเรียนต่างๆ แต่แอปแบบทดสอบสามารถรันได้ในเครื่อง; ทำตามคำแนะนำในโฟลเดอร์ `quiz-app` เพื่อโฮสต์ในเครื่องหรือนำไปใช้งานบน Azure

| Lesson Number |                             หัวข้อ                             |                   กลุ่มบทเรียน                   | วัตถุประสงค์การเรียนรู้                                                                                                       |                                                              บทเรียนที่เชื่อมโยง                                                               |                        ผู้แต่ง                        |
| :-----------: | :------------------------------------------------------------: | :----------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------: |
|      01       |            บทนำสู่การเรียนรู้ของเครื่อง (machine learning)             |      [Introduction](1-Introduction/README.md)       | เรียนรู้แนวคิดพื้นฐานของการเรียนรู้ของเครื่อง                                                                                   |                                             [Lesson](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                       |
|      02       |                ประวัติศาสตร์ของการเรียนรู้ของเครื่อง                 |      [Introduction](1-Introduction/README.md)       | เรียนรู้ประวัติศาสตร์เบื้องหลังสาขานี้                                                                                         |                                            [Lesson](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen and Amy                      |
|      03       |                 ความเป็นธรรมและการเรียนรู้ของเครื่อง                  |      [Introduction](1-Introduction/README.md)       | ปัญหาทางปรัชญาสำคัญเกี่ยวกับความเป็นธรรมที่นักเรียนควรพิจารณาเมื่อสร้างและนำแบบจำลอง ML ไปใช้                                |                                              [Lesson](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                        |
|      04       |                เทคนิคสำหรับการเรียนรู้ของเครื่อง                 |      [Introduction](1-Introduction/README.md)       | เทคนิคที่นักวิจัย ML ใช้ในการสร้างแบบจำลอง ML มีอะไรบ้าง                                                                       |                                          [Lesson](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris and Jen                     |
|      05       |                   บทนำสู่การถดถอย (regression)                   |        [Regression](2-Regression/README.md)         | เริ่มต้นกับ Python และ Scikit-learn สำหรับแบบจำลองถดถอย                                                                          |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)         |      Jen • Eric Wanjau       |
|      06       |                ราคาฟักทองในอเมริกาเหนือ 🎃                |        [Regression](2-Regression/README.md)         | การแสดงผลและทำความสะอาดข้อมูลเตรียมสำหรับ ML                                                                                   |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|      07       |                ราคาฟักทองในอเมริกาเหนือ 🎃                |        [Regression](2-Regression/README.md)         | สร้างแบบจำลองถดถอยเชิงเส้นและพหุนาม                                                                                           |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen and Dmitry • Eric Wanjau       |
|      08       |                ราคาฟักทองในอเมริกาเหนือ 🎃                |        [Regression](2-Regression/README.md)         | สร้างแบบจำลองถดถอยโลจิสติก                                                                                                   |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|      09       |                          เว็บแอป 🔌                          |           [Web App](3-Web-App/README.md)            | สร้างเว็บแอปเพื่อใช้แบบจำลองที่ฝึกฝน                                                                                           |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                          |
|      10       |                 บทนำสู่การจัดประเภท                 |    [Classification](4-Classification/README.md)     | ทำความสะอาด เตรียมข้อมูล และแสดงข้อมูล; บทนำสู่การจัดประเภท                                                                   | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen and Cassie • Eric Wanjau |
|      11       |             อาหารอร่อยของเอเชียและอินเดีย 🍜             |    [Classification](4-Classification/README.md)     | บทนำสู่ตัวจัดประเภท                                                                                                            | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen and Cassie • Eric Wanjau |
|      12       |             อาหารอร่อยของเอเชียและอินเดีย 🍜             |    [Classification](4-Classification/README.md)     | ตัวจัดประเภทเพิ่มเติม                                                                                                           | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen and Cassie • Eric Wanjau |
|      13       |             อาหารอร่อยของเอเชียและอินเดีย 🍜             |    [Classification](4-Classification/README.md)     | สร้างเว็บแอปแนะนำโดยใช้แบบจำลองของคุณ                                                                                        |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                          |
|      14       |                   บทนำสู่การจัดกลุ่ม (clustering)                   |        [Clustering](5-Clustering/README.md)         | ทำความสะอาด เตรียม และแสดงข้อมูล; บทนำสู่การจัดกลุ่ม                                                                          |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|      15       |              สำรวจรสนิยมทางดนตรีของไนจีเรีย 🎧              |        [Clustering](5-Clustering/README.md)         | สำรวจวิธีการจัดกลุ่มด้วย K-Means                                                                                              |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|      16       |        บทนำสู่การประมวลผลภาษาธรรมชาติ ☕️         |   [Natural language processing](6-NLP/README.md)    | เรียนรู้พื้นฐานเกี่ยวกับ NLP โดยสร้างบอทง่ายๆ                                                                                  |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                        |
|      17       |                      งาน NLP ที่พบบ่อย ☕️                      |   [Natural language processing](6-NLP/README.md)    | เพิ่มพูนความรู้เกี่ยวกับ NLP โดยเข้าใจงานทั่วไปที่จำเป็นเมื่อจัดการกับโครงสร้างภาษา                                           |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                        |
|      18       |             การแปลและการวิเคราะห์อารมณ์ ♥️              |   [Natural language processing](6-NLP/README.md)    | การแปลและวิเคราะห์อารมณ์ด้วย Jane Austen                                                                                      |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                        |
|      19       |                  โรงแรมโรแมนติกในยุโรป ♥️                  |   [Natural language processing](6-NLP/README.md)    | วิเคราะห์อารมณ์กับรีวิวโรงแรม 1                                                                                               |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                        |
|      20       |                  โรงแรมโรแมนติกในยุโรป ♥️                  |   [Natural language processing](6-NLP/README.md)    | วิเคราะห์อารมณ์กับรีวิวโรงแรม 2                                                                                               |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                        |
|      21       |            บทนำสู่การพยากรณ์แบบอนุกรมเวลา             |        [Time series](7-TimeSeries/README.md)        | บทนำสู่การพยากรณ์แบบอนุกรมเวลา                                                                                              |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                       |
|      22       | ⚡️ การใช้พลังงานทั่วโลก ⚡️ - การพยากรณ์แบบอนุกรมเวลาด้วย ARIMA |        [Time series](7-TimeSeries/README.md)        | การพยากรณ์แบบอนุกรมเวลาด้วย ARIMA                                                                                           |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                       |
|      23       |  ⚡️ การใช้พลังงานทั่วโลก ⚡️ - การพยากรณ์แบบอนุกรมเวลาด้วย SVR  |        [Time series](7-TimeSeries/README.md)        | การพยากรณ์แบบอนุกรมเวลาด้วยการถดถอยโครงสร้างเวกเตอร์สนับสนุน (Support Vector Regressor)                                        |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                        |
|      24       |             บทนำสู่การเรียนรู้แบบเสริมแรง             | [Reinforcement learning](8-Reinforcement/README.md) | บทนำสู่การเรียนรู้แบบเสริมแรงด้วย Q-Learning                                                                                  |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                        |
|      25       |                 ช่วย Peter หลีกเลี่ยงหมาป่า! 🐺                  | [Reinforcement learning](8-Reinforcement/README.md) | กิมเกมสำหรับการเรียนรู้แบบเสริมแรง                                                                                            |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                        |
|  บทส่งท้าย  |            กรณีศึกษาและแอปพลิเคชัน ML ในโลกความจริง            |      [ML in the Wild](9-Real-World/README.md)       | แอปพลิเคชันที่น่าสนใจและเปิดเผยของ ML แบบคลาสสิกในโลกความจริง                                                                |                                             [Lesson](9-Real-World/1-Applications/README.md)                                              |                         ทีม                         |
|  บทส่งท้าย  |            การแก้ไขปัญหาแบบจำลองใน ML ด้วยแดชบอร์ด RAI          |      [ML in the Wild](9-Real-World/README.md)       | การแก้ไขปัญหาแบบจำลองใน Machine Learning โดยใช้ส่วนประกอบแดชบอร์ด Responsible AI                                               |                                             [Lesson](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                       |

> [ค้นหาแหล่งข้อมูลเพิ่มเติมสำหรับหลักสูตรนี้ได้ในคอลเลกชัน Microsoft Learn ของเรา](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## เข้าถึงแบบออฟไลน์

คุณสามารถรันเอกสารนี้แบบออฟไลน์โดยใช้ [Docsify](https://docsify.js.org/#/). ให้โคลนที่เก็บนี้, [ติดตั้ง Docsify](https://docsify.js.org/#/quickstart) บนเครื่องของคุณ จากนั้นในโฟลเดอร์รากของที่เก็บนี้ ให้พิมพ์ `docsify serve`. เว็บไซต์จะเปิดให้บริการบนพอร์ต 3000 ที่ localhost ของคุณ: `localhost:3000`.

## ไฟล์ PDF

ดาวน์โหลดไฟล์ pdf ของหลักสูตรพร้อมลิงก์ [ที่นี่](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf).


## 🎒 หลักสูตรอื่นๆ

ทีมของเราผลิตหลักสูตรอื่นๆ ด้วย! เช็คดูได้ที่:

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
 
### การเรียนรู้หลัก
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### ชุดเรื่อง Copilot
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## การขอความช่วยเหลือ

หากคุณติดขัดหรือมีคำถามใดๆ เกี่ยวกับการสร้างแอป AI เข้าร่วมกับผู้เรียนและนักพัฒนาที่มีประสบการณ์ในการอภิปรายเกี่ยวกับ MCP ชุมชนที่สนับสนุนซึ่งยินดีต้อนรับคำถามและแบ่งปันความรู้กันอย่างเสรี

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

หากคุณมีคำติชมเกี่ยวกับผลิตภัณฑ์หรือพบข้อผิดพลาดขณะสร้าง เข้าเยี่ยมชม:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## เคล็ดลับการเรียนรู้เพิ่มเติม

- ทบทวนสมุดบันทึกหลังแต่ละบทเรียนเพื่อความเข้าใจที่ดีขึ้น
- ฝึกฝนการนำอัลกอริธึมไปใช้ด้วยตนเอง
- สำรวจชุดข้อมูลจริงโดยใช้แนวคิดที่ได้เรียนรู้มา

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษาอัตโนมัติ [Co-op Translator](https://github.com/Azure/co-op-translator) แม้เราจะพยายามให้มีความถูกต้องสูงสุด แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถูกพิจารณาเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่มีความสำคัญ ขอแนะนำให้ใช้บริการแปลโดยมืออาชีพ เราจะไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้
<!-- CO-OP TRANSLATOR DISCLAIMER END -->