[![GitHub license](https://img.shields.io/github/license/microsoft/ML-For-Beginners.svg)](https://github.com/microsoft/ML-For-Beginners/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/issues/)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/ML-For-Beginners.svg)](https://GitHub.com/microsoft/ML-For-Beginners/pulls/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/ML-For-Beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/ML-For-Beginners/watchers/)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/ML-For-Beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/ML-For-Beginners/network/)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/ML-For-Beginners.svg?style=social&label=Star)](https://GitHub.com/microsoft/ML-For-Beginners/stargazers/)

### 🌐 การรองรับหลายภาษา

#### รองรับผ่าน GitHub Action (อัตโนมัติ & อัปเดตเสมอ)

<!-- CO-OP TRANSLATOR LANGUAGES TABLE START -->
[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh-CN/README.md) | [Chinese (Traditional, Hong Kong)](../zh-HK/README.md) | [Chinese (Traditional, Macau)](../zh-MO/README.md) | [Chinese (Traditional, Taiwan)](../zh-TW/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Estonian](../et/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Kannada](../kn/README.md) | [Khmer](../km/README.md) | [Korean](../ko/README.md) | [Lithuanian](../lt/README.md) | [Malay](../ms/README.md) | [Malayalam](../ml/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Nigerian Pidgin](../pcm/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../pt-BR/README.md) | [Portuguese (Portugal)](../pt-PT/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Tamil](../ta/README.md) | [Telugu](../te/README.md) | [Thai](./README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

> **ชอบโคลนลงเครื่องไหม?**
>
> ที่เก็บนี้มีการแปลภาษา 50+ ภาษา ซึ่งเพิ่มขนาดดาวน์โหลดอย่างมาก หากต้องการโคลนโดยไม่รวมการแปล ให้ใช้ sparse checkout:
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
> นี่จะให้ทุกสิ่งที่คุณต้องการเพื่อทำคอร์สเสร็จได้อย่างรวดเร็วขึ้นมาก
<!-- CO-OP TRANSLATOR LANGUAGES TABLE END -->

#### เข้าร่วมชุมชนของเรา

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

เรามีซีรีส์ Discord เรียนรู้กับ AI ดำเนินอยู่ เรียนรู้เพิ่มเติมและเข้าร่วมกับเราได้ที่ [Learn with AI Series](https://aka.ms/learnwithai/discord) ระหว่างวันที่ 18 - 30 กันยายน 2025 คุณจะได้รับเคล็ดลับและเทคนิคการใช้ GitHub Copilot สำหรับวิทยาศาสตร์ข้อมูล

![Learn with AI series](../../translated_images/th/3.9b58fd8d6c373c20.webp)

# การเรียนรู้เครื่องสำหรับผู้เริ่มต้น - หลักสูตร

> 🌍 เดินทางรอบโลกไปกับการสำรวจการเรียนรู้เครื่องผ่านวัฒนธรรมโลก 🌍

Cloud Advocates ที่ Microsoft ยินดีนำเสนอหลักสูตร 12 สัปดาห์ 26 บทเรียนที่เกี่ยวกับ **การเรียนรู้เครื่อง** ในหลักสูตรนี้คุณจะได้เรียนรู้เกี่ยวกับสิ่งที่บางครั้งเรียกว่า **การเรียนรู้เครื่องแบบคลาสสิก** โดยใช้เป็นหลักไลบรารี Scikit-learn และหลีกเลี่ยงการเรียนรู้เชิงลึก ซึ่งครอบคลุมในหลักสูตร [AI สำหรับผู้เริ่มต้น](https://aka.ms/ai4beginners) ของเรา จับคู่บทเรียนเหล่านี้กับหลักสูตร ['วิทยาศาสตร์ข้อมูลสำหรับผู้เริ่มต้น'](https://aka.ms/ds4beginners) ของเราเช่นกัน!

เดินทางกับเราไปรอบโลกขณะที่เรานำเทคนิคคลาสสิกเหล่านี้ไปใช้กับข้อมูลจากหลายภูมิภาคของโลก ในแต่ละบทเรียนจะมีแบบทดสอบก่อนและหลังบทเรียน คำแนะนำเป็นลายลักษณ์อักษรในการทำบทเรียนให้เสร็จสมบูรณ์ ตัวอย่างโค้ด การมอบหมาย และอื่นๆ แนวทางการสอนแบบโครงการช่วยให้คุณเรียนรู้ไปพร้อมกับการสร้างงานจริง ซึ่งเป็นวิธีที่พิสูจน์แล้วว่าสำหรับทักษะใหม่จะ "ติดตัว"

**✍️ ขอขอบคุณอย่างจริงใจต่อผู้เขียนของเรา** Jen Looper, Stephen Howell, Francesca Lazzeri, Tomomi Imura, Cassie Breviu, Dmitry Soshnikov, Chris Noring, Anirban Mukherjee, Ornella Altunyan, Ruth Yakubu และ Amy Boyd

**🎨 ขอบคุณด้วยสำหรับนักวาดภาพประกอบ** Tomomi Imura, Dasani Madipalli และ Jen Looper

**🙏 ขอบคุณพิเศษ 🙏 ต่อ Microsoft Student Ambassador ผู้แต่ง ทบทวน และช่วยเติมเนื้อหา** โดยเฉพาะ Rishit Dagli, Muhammad Sakib Khan Inan, Rohan Raj, Alexandru Petrescu, Abhishek Jaiswal, Nawrin Tabassum, Ioan Samuila และ Snigdha Agarwal

**🤩 ขอบคุณเพิ่มเติมสำหรับ Microsoft Student Ambassadors Eric Wanjau, Jasleen Sondhi และ Vidushi Gupta สำหรับบทเรียน R ของเรา!**

# การเริ่มต้น

ทำตามขั้นตอนเหล่านี้:
1. **Fork ที่เก็บนี้**: คลิกที่ปุ่ม "Fork" ที่มุมขวาบนของหน้านี้
2. **โคลนที่เก็บ**:   `git clone https://github.com/microsoft/ML-For-Beginners.git`

> [ค้นหาทรัพยากรเพิ่มเติมสำหรับคอร์สนี้ในคอลเลกชัน Microsoft Learn ของเรา](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

> 🔧 **ต้องการความช่วยเหลือ?** ตรวจสอบ [คู่มือแก้ไขปัญหา](TROUBLESHOOTING.md) สำหรับวิธีแก้ปัญหาที่พบบ่อยเกี่ยวกับการติดตั้ง, การตั้งค่า และการรันบทเรียน

**[นักเรียน](https://aka.ms/student-page)** ในการใช้หลักสูตรนี้ ให้ fork รีโปทั้งหมดไปยังบัญชี GitHub ของคุณเอง และทำแบบฝึกหัดด้วยตัวเองหรือเป็นกลุ่ม:

- เริ่มต้นด้วยแบบทดสอบก่อนบรรยาย
- อ่านบรรยายและทำกิจกรรมหยุดคิดและทบทวนในแต่ละจุดตรวจสอบความเข้าใจ
- พยายามสร้างโครงการโดยเข้าใจบทเรียนแทนการรันโค้ดตัวอย่าง อย่างไรก็ตาม โค้ดตัวอย่างนั้นมีอยู่ในโฟลเดอร์ `/solution` ในบทเรียนที่เน้นโครงการแต่ละบท
- ทำแบบทดสอบหลังบรรยาย
- ทำความท้าทาย
- ทำการบ้าน
- หลังจากจบบทเรียนชุดหนึ่ง เยี่ยมชม [กระดานอภิปราย](https://github.com/microsoft/ML-For-Beginners/discussions) และ "เรียนรู้ออกเสียง" โดยกรอก PAT rubric ที่เหมาะสม 'PAT' คือเครื่องมือประเมินความก้าวหน้าที่คุณกรอกเพื่อเสริมการเรียนรู้ คุณยังสามารถตอบสนองต่อ PAT ของคนอื่นเพื่อให้เราเรียนรู้ร่วมกัน

> สำหรับการศึกษาต่อ เราแนะนำให้ติดตามโมดูลและเส้นทางการเรียนรู้ [Microsoft Learn](https://docs.microsoft.com/en-us/users/jenlooper-2911/collections/k7o7tg1gp306q4?WT.mc_id=academic-77952-leestott)

**สำหรับครูผู้สอน** เรามี [คำแนะนำบางส่วน](for-teachers.md) ว่าจะใช้งานหลักสูตรนี้อย่างไร

---

## วิดีโอสอน

บทเรียนบางบทมีวิดีโอสั้นๆ คุณสามารถหาบทเรียนเหล่านี้ได้ในแต่ละบท หรือบน [เพลย์ลิสต์ ML for Beginners บนช่อง Microsoft Developer YouTube](https://aka.ms/ml-beginners-videos) โดยคลิกที่ภาพด้านล่าง

[![ML for beginners banner](../../translated_images/th/ml-for-beginners-video-banner.63f694a100034bc6.webp)](https://aka.ms/ml-beginners-videos)

---

## แนะนำทีมงาน

[![Promo video](../../images/ml.gif)](https://youtu.be/Tj1XWrDSYJU)

**Gif โดย** [Mohit Jaisal](https://linkedin.com/in/mohitjaisal)

> 🎥 คลิกที่ภาพด้านบนเพื่อดูวิดีโอเกี่ยวกับโครงการและทีมงานผู้สร้าง!

---

## แนวทางการสอน

เราเลือกใช้สองหลักการทางการสอนเมื่อสร้างหลักสูตรนี้: การทำให้เป็น **โครงการปฏิบัติจริง** และการมี **แบบทดสอบบ่อยครั้ง** นอกจากนี้หลักสูตรนี้ยังมี **ธีม** ร่วมเพื่อความสอดคล้อง

โดยการทำให้เนื้อหาสอดคล้องกับโครงการจะช่วยกระตุ้นให้นักเรียนสนุกกับการเรียน และเพิ่มความจำในแนวคิด นอกจากนี้ แบบทดสอบไม่กดดันก่อนชั้นเรียนจะช่วยตั้งใจของนักเรียนในการเรียนรู้หัวข้อ และแบบทดสอบที่สองหลังเรียนยังช่วยย้ำความจำ หลักสูตรนี้ถูกออกแบบให้ยืดหยุ่นและสนุกสนาน สามารถเรียนทั้งหมดหรือบางส่วนได้ โครงการเริ่มจากง่ายและเพิ่มความซับซ้อนขึ้นจนถึงสิ้นสุดรอบ 12 สัปดาห์ หลักสูตรนี้ยังมีตอนท้ายเกี่ยวกับการประยุกต์ใช้ในโลกจริงของ ML ซึ่งสามารถใช้เป็นเครดิตพิเศษหรือฐานการอภิปราย

> ค้นหา [จรรยาบรรณ](CODE_OF_CONDUCT.md), [การมีส่วนร่วม](CONTRIBUTING.md), [การแปล](..), และ [แก้ไขปัญหา](TROUBLESHOOTING.md) ของเรา เรายินดีรับฟังคำติชมเชิงสร้างสรรค์ของคุณ!

## แต่ละบทเรียนประกอบด้วย

- สเก็ตช์โน้ต (ถ้ามี)
- วิดีโอเสริม (ถ้ามี)
- วิดีโอสอน (บางบทเรียนเท่านั้น)
- [แบบทดสอบอบอุ่นก่อนบรรยาย](https://ff-quizzes.netlify.app/en/ml/)
- บทเรียนเป็นลายลักษณ์อักษร
- สำหรับบทเรียนโครงการ มีคำแนะนำทีละขั้นตอนการสร้างโครงการ
- ตรวจสอบความรู้
- ความท้าทาย
- การอ่านเสริม
- การบ้าน
- [แบบทดสอบหลังบรรยาย](https://ff-quizzes.netlify.app/en/ml/)
> **บันทึกเกี่ยวกับภาษา**: บทเรียนเหล่านี้ส่วนใหญ่เขียนด้วย Python แต่หลายบทเรียนก็มีในภาษา R ด้วย หากต้องการทำบทเรียน R ให้ไปที่โฟลเดอร์ `/solution` และหาบทเรียนในภาษา R จะมีนามสกุล .rmd ซึ่งหมายถึงไฟล์ **R Markdown** ที่สามารถนิยามได้ง่ายๆ ว่าเป็นการฝัง `code chunks` (ของภาษา R หรือภาษาอื่น ๆ) กับ `YAML header` (ที่กำหนดวิธีการจัดรูปแบบผลลัพธ์ เช่น PDF) ลงใน `Markdown document` ดังนั้นจึงเป็นกรอบการเขียนที่ดีเยี่ยมสำหรับการทำวิทยาศาสตร์ข้อมูล เพราะช่วยให้คุณสามารถรวมโค้ดของคุณ ผลลัพธ์ของโค้ด และความคิดของคุณโดยการเขียนทั้งหมดในรูปแบบ Markdown ยิ่งไปกว่านั้น เอกสาร R Markdown สามารถแปลงเป็นรูปแบบผลลัพธ์ เช่น PDF, HTML หรือ Word ได้

> **บันทึกเกี่ยวกับแบบทดสอบ**: แบบทดสอบทั้งหมดจะอยู่ใน [โฟลเดอร์ Quiz App](../../quiz-app) ซึ่งมีทั้งหมด 52 แบบทดสอบ แต่ละแบบมีสามคำถาม สามารถเข้าถึงได้จากบทเรียนต่าง ๆ แต่แอปแบบทดสอบนี้สามารถรันในเครื่องของคุณได้โดยตรง ให้ทำตามคำแนะนำในโฟลเดอร์ `quiz-app` เพื่อโฮสต์หรือดีพลอยไปยัง Azure

| หมายเลขบทเรียน |                             หัวข้อ                              |                   กลุ่มบทเรียน                   | วัตถุประสงค์การเรียนรู้                                                                                                             |                                                              บทเรียนที่เชื่อมโยง                                                               |                        ผู้เขียน                        |
| :--------------: | :------------------------------------------------------------: | :-----------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------: |
|       01         |                แนะนำการเรียนรู้ของเครื่อง                      |      [Introduction](1-Introduction/README.md)       | เรียนรู้แนวคิดพื้นฐานเบื้องหลังการเรียนรู้ของเครื่อง                                                                        |                                             [Lesson](1-Introduction/1-intro-to-ML/README.md)                                             |                       Muhammad                         |
|       02         |                ประวัติของการเรียนรู้ของเครื่อง                 |      [Introduction](1-Introduction/README.md)       | เรียนรู้ประวัติพื้นฐานของสาขานี้                                                                                             |                                            [Lesson](1-Introduction/2-history-of-ML/README.md)                                            |                     Jen and Amy                         |
|       03         |                 ความยุติธรรมและการเรียนรู้ของเครื่อง            |      [Introduction](1-Introduction/README.md)       | อะไรคือปัญหาปรัชญาที่สำคัญเกี่ยวกับความยุติธรรมที่นักเรียนควรพิจารณาเมื่อสร้างและใช้โมเดล ML                               |                                              [Lesson](1-Introduction/3-fairness/README.md)                                               |                        Tomomi                          |
|       04         |                เทคนิคสำหรับการเรียนรู้ของเครื่อง               |      [Introduction](1-Introduction/README.md)       | นักวิจัย ML ใช้เทคนิคอะไรในการสร้างโมเดล ML?                                                                                 |                                          [Lesson](1-Introduction/4-techniques-of-ML/README.md)                                           |                    Chris and Jen                        |
|       05         |                   แนะนำการถดถอย                              |        [Regression](2-Regression/README.md)         | เริ่มต้นกับ Python และ Scikit-learn สำหรับโมเดลถดถอย                                                                         |         [Python](2-Regression/1-Tools/README.md) • [R](../../2-Regression/1-Tools/solution/R/lesson_1.html)          |      Jen • Eric Wanjau       |
|       06         |                ราคาฟักทองในอเมริกาเหนือ 🎃                   |        [Regression](2-Regression/README.md)         | สร้างภาพและทำความสะอาดข้อมูลเพื่อเตรียมพร้อมสำหรับ ML                                                                        |          [Python](2-Regression/2-Data/README.md) • [R](../../2-Regression/2-Data/solution/R/lesson_2.html)          |      Jen • Eric Wanjau       |
|       07         |                ราคาฟักทองในอเมริกาเหนือ 🎃                   |        [Regression](2-Regression/README.md)         | สร้างโมเดลถดถอยเชิงเส้นและถดถอยหลายพจน์                                                                                   |        [Python](2-Regression/3-Linear/README.md) • [R](../../2-Regression/3-Linear/solution/R/lesson_3.html)        |      Jen and Dmitry • Eric Wanjau       |
|       08         |                ราคาฟักทองในอเมริกาเหนือ 🎃                   |        [Regression](2-Regression/README.md)         | สร้างโมเดลถดถอยลอจิสติก                                                                                                      |     [Python](2-Regression/4-Logistic/README.md) • [R](../../2-Regression/4-Logistic/solution/R/lesson_4.html)      |      Jen • Eric Wanjau       |
|       09         |                          เว็บแอป 🔌                            |           [Web App](3-Web-App/README.md)            | สร้างเว็บแอปเพื่อใช้โมเดลที่ฝึกไว้                                                                                            |                                                 [Python](3-Web-App/1-Web-App/README.md)                                                  |                         Jen                            |
|       10         |                 แนะนำการจัดหมวดหมู่                            |    [Classification](4-Classification/README.md)     | ทำความสะอาด เตรียม และแสดงภาพข้อมูลของคุณ เป็นการแนะนำการจัดหมวดหมู่                                                         | [Python](4-Classification/1-Introduction/README.md) • [R](../../4-Classification/1-Introduction/solution/R/lesson_10.html)  | Jen and Cassie • Eric Wanjau |
|       11         |             อาหารเอเชียและอินเดียอร่อย ๆ 🍜                   |    [Classification](4-Classification/README.md)     | แนะนำเครื่องมือจัดหมวดหมู่                                                                                                   | [Python](4-Classification/2-Classifiers-1/README.md) • [R](../../4-Classification/2-Classifiers-1/solution/R/lesson_11.html) | Jen and Cassie • Eric Wanjau |
|       12         |             อาหารเอเชียและอินเดียอร่อย ๆ 🍜                   |    [Classification](4-Classification/README.md)     | เครื่องมือจัดหมวดหมู่เพิ่มเติม                                                                                                 | [Python](4-Classification/3-Classifiers-2/README.md) • [R](../../4-Classification/3-Classifiers-2/solution/R/lesson_12.html) | Jen and Cassie • Eric Wanjau |
|       13         |             อาหารเอเชียและอินเดียอร่อย ๆ 🍜                   |    [Classification](4-Classification/README.md)     | สร้างเว็บแอปแนะนำโดยใช้โมเดลของคุณ                                                                                            |                                              [Python](4-Classification/4-Applied/README.md)                                              |                         Jen                            |
|       14         |                   แนะนำการจัดกลุ่ม                              |        [Clustering](5-Clustering/README.md)         | ทำความสะอาด เตรียม และแสดงภาพข้อมูลของคุณ แนะนำการจัดกลุ่ม                                                                   |         [Python](5-Clustering/1-Visualize/README.md) • [R](../../5-Clustering/1-Visualize/solution/R/lesson_14.html)         |      Jen • Eric Wanjau       |
|       15         |              สำรวจรสนิยมเพลงนีจีเรีย 🎧                      |        [Clustering](5-Clustering/README.md)         | สำรวจวิธีการจัดกลุ่ม K-Means                                                                                                |           [Python](5-Clustering/2-K-Means/README.md) • [R](../../5-Clustering/2-K-Means/solution/R/lesson_15.html)           |      Jen • Eric Wanjau       |
|       16         |        แนะนำการประมวลผลภาษาธรรมชาติ ☕️                      |   [Natural language processing](6-NLP/README.md)    | เรียนรู้พื้นฐานการประมวลผลภาษาธรรมชาติโดยการสร้างบอทง่าย ๆ                                                                 |                                             [Python](6-NLP/1-Introduction-to-NLP/README.md)                                              |                       Stephen                          |
|       17         |                      งาน NLP ทั่วไป ☕️                        |   [Natural language processing](6-NLP/README.md)    | เสริมความรู้เรื่อง NLP โดยเข้าใจงานทั่วไปที่ต้องทำเมื่อทำงานกับโครงสร้างภาษา                                               |                                                    [Python](6-NLP/2-Tasks/README.md)                                                     |                       Stephen                          |
|       18         |             การแปลและการวิเคราะห์ความรู้สึก ♥️               |   [Natural language processing](6-NLP/README.md)    | การแปลและการวิเคราะห์ความรู้สึกด้วย Jane Austen                                                                             |                                            [Python](6-NLP/3-Translation-Sentiment/README.md)                                             |                       Stephen                          |
|       19         |                  โรงแรมโรแมนติกในยุโรป ♥️                     |   [Natural language processing](6-NLP/README.md)    | วิเคราะห์ความรู้สึกด้วยรีวิวโรงแรม 1                                                                                        |                                               [Python](6-NLP/4-Hotel-Reviews-1/README.md)                                                |                       Stephen                          |
|       20         |                  โรงแรมโรแมนติกในยุโรป ♥️                     |   [Natural language processing](6-NLP/README.md)    | วิเคราะห์ความรู้สึกด้วยรีวิวโรงแรม 2                                                                                        |                                               [Python](6-NLP/5-Hotel-Reviews-2/README.md)                                                |                       Stephen                          |
|       21         |            แนะนำการพยากรณ์ชุดข้อมูลตามเวลา                    |        [Time series](7-TimeSeries/README.md)        | แนะนำการพยากรณ์ชุดข้อมูลตามเวลา                                                                                           |                                             [Python](7-TimeSeries/1-Introduction/README.md)                                              |                      Francesca                         |
|       22         | ⚡️ การใช้พลังงานโลก ⚡️ - การพยากรณ์ชุดข้อมูลตามเวลาด้วย ARIMA |        [Time series](7-TimeSeries/README.md)        | การพยากรณ์ชุดข้อมูลตามเวลาด้วยโมเดล ARIMA                                                                          |                                                 [Python](7-TimeSeries/2-ARIMA/README.md)                                                 |                      Francesca                         |
|       23         |  ⚡️ การใช้พลังงานโลก ⚡️ - การพยากรณ์ชุดข้อมูลตามเวลาด้วย SVR  |        [Time series](7-TimeSeries/README.md)        | การพยากรณ์ชุดข้อมูลตามเวลาด้วย Support Vector Regressor                                                                   |                                                  [Python](7-TimeSeries/3-SVR/README.md)                                                  |                       Anirban                          |
|       24         |             แนะนำการเรียนรู้เสริมแรง                          | [Reinforcement learning](8-Reinforcement/README.md) | แนะนำการเรียนรู้เสริมแรงด้วย Q-Learning                                                                                    |                                             [Python](8-Reinforcement/1-QLearning/README.md)                                              |                        Dmitry                          |
|       25         |                 ช่วยปีเตอร์หลบหมาป่า! 🐺                      | [Reinforcement learning](8-Reinforcement/README.md) | การเรียนรู้เสริมแรง Gym                                                                                                    |                                                [Python](8-Reinforcement/2-Gym/README.md)                                                 |                        Dmitry                          |
|  บทส่งท้าย     |            กรณีศึกษาและแอปพลิเคชัน ML ในโลกจริง              |      [ML in the Wild](9-Real-World/README.md)       | แอปพลิเคชันที่น่าสนใจและเปิดเผยของ ML แบบคลาสสิกในโลกจริง                                                                |                                             [Lesson](9-Real-World/1-Applications/README.md)                                              |                         Team                           |
|  บทส่งท้าย     |            การดีบักโมเดล ML ด้วยแดชบอร์ด RAI                 |      [ML in the Wild](9-Real-World/README.md)       | การดีบักโมเดล ML ด้วยส่วนประกอบแดชบอร์ด Responsible AI                                                                     |                                             [Lesson](9-Real-World/2-Debugging-ML-Models/README.md)                                              |                         Ruth Yakubu                    |

> [ค้นหาทรัพยากรเพิ่มเติมทั้งหมดสำหรับหลักสูตรนี้ในคอลเลกชัน Microsoft Learn ของเรา](https://learn.microsoft.com/en-us/collections/qrqzamz1nn2wx3?WT.mc_id=academic-77952-bethanycheum)

## การใช้งานแบบออฟไลน์

คุณสามารถใช้เอกสารนี้แบบออฟไลน์ได้โดยใช้ [Docsify](https://docsify.js.org/#/) ทำการโคลนรีโปนี้, [ติดตั้ง Docsify](https://docsify.js.org/#/quickstart) บนเครื่องของคุณ จากนั้นในโฟลเดอร์รากของรีโปนี้ให้พิมพ์ `docsify serve` เว็บไซต์จะถูกเสิร์ฟบนพอร์ต 3000 ที่โฮสต์เครื่องของคุณ: `localhost:3000`

## ไฟล์ PDF

ดาวน์โหลด PDF ของหลักสูตรพร้อมลิงก์ได้ [ที่นี่](https://microsoft.github.io/ML-For-Beginners/pdf/readme.pdf).


## 🎒 หลักสูตรอื่น ๆ

ทีมงานของเราผลิตหลักสูตรอื่น ๆ ด้วย! ตรวจสอบได้ที่:

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
 
### ชุดปัญญาประดิษฐ์สร้างสรรค์
[![Generative AI for Beginners](https://img.shields.io/badge/Generative%20AI%20for%20Beginners-8B5CF6?style=for-the-badge&labelColor=E5E7EB&color=8B5CF6)](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
[![Generative AI (.NET)](https://img.shields.io/badge/Generative%20AI%20(.NET)-9333EA?style=for-the-badge&labelColor=E5E7EB&color=9333EA)](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
[![Generative AI (Java)](https://img.shields.io/badge/Generative%20AI%20(Java)-C084FC?style=for-the-badge&labelColor=E5E7EB&color=C084FC)](https://github.com/microsoft/generative-ai-for-beginners-java?WT.mc_id=academic-105485-koreyst)
[![Generative AI (JavaScript)](https://img.shields.io/badge/Generative%20AI%20(JavaScript)-E879F9?style=for-the-badge&labelColor=E5E7EB&color=E879F9)](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)

---
 
### การเรียนรู้แกนหลัก
[![ML for Beginners](https://img.shields.io/badge/ML%20for%20Beginners-22C55E?style=for-the-badge&labelColor=E5E7EB&color=22C55E)](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
[![Data Science for Beginners](https://img.shields.io/badge/Data%20Science%20for%20Beginners-84CC16?style=for-the-badge&labelColor=E5E7EB&color=84CC16)](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
[![AI for Beginners](https://img.shields.io/badge/AI%20for%20Beginners-A3E635?style=for-the-badge&labelColor=E5E7EB&color=A3E635)](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
[![Cybersecurity for Beginners](https://img.shields.io/badge/Cybersecurity%20for%20Beginners-F97316?style=for-the-badge&labelColor=E5E7EB&color=F97316)](https://github.com/microsoft/Security-101?WT.mc_id=academic-96948-sayoung)
[![Web Dev for Beginners](https://img.shields.io/badge/Web%20Dev%20for%20Beginners-EC4899?style=for-the-badge&labelColor=E5E7EB&color=EC4899)](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
[![IoT for Beginners](https://img.shields.io/badge/IoT%20for%20Beginners-14B8A6?style=for-the-badge&labelColor=E5E7EB&color=14B8A6)](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
[![XR Development for Beginners](https://img.shields.io/badge/XR%20Development%20for%20Beginners-38BDF8?style=for-the-badge&labelColor=E5E7EB&color=38BDF8)](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)

---
 
### ชุด Copilot
[![Copilot for AI Paired Programming](https://img.shields.io/badge/Copilot%20for%20AI%20Paired%20Programming-FACC15?style=for-the-badge&labelColor=E5E7EB&color=FACC15)](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
[![Copilot for C#/.NET](https://img.shields.io/badge/Copilot%20for%20C%23/.NET-FBBF24?style=for-the-badge&labelColor=E5E7EB&color=FBBF24)](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
[![Copilot Adventure](https://img.shields.io/badge/Copilot%20Adventure-FDE68A?style=for-the-badge&labelColor=E5E7EB&color=FDE68A)](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)
<!-- CO-OP TRANSLATOR OTHER COURSES END -->

## ขอความช่วยเหลือ

หากคุณติดขัดหรือมีคำถามเกี่ยวกับการสร้างแอป AI เข้าร่วมกับผู้เรียนและนักพัฒนาที่มีประสบการณ์ในการอภิปรายเกี่ยวกับ MCP เป็นชุมชนที่ให้การสนับสนุนซึ่งยินดีต้อนรับคำถามและแบ่งปันความรู้กันอย่างเสรี

[![Microsoft Foundry Discord](https://dcbadge.limes.pink/api/server/nTYy5BXMWG)](https://discord.gg/nTYy5BXMWG)

หากคุณมีคำติชมหรือพบข้อผิดพลาดขณะสร้างโปรดไปที่:

[![Microsoft Foundry Developer Forum](https://img.shields.io/badge/GitHub-Microsoft_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)
## เคล็ดลับการเรียนรู้เพิ่มเติม

- ทบทวนสมุดบันทึกหลังจากแต่ละบทเรียนเพื่อความเข้าใจที่ดีขึ้น
- ฝึกฝนการนำอัลกอริธึมไปใช้ด้วยตนเอง
- สำรวจชุดข้อมูลจริงโดยใช้แนวคิดที่เรียนรู้มา

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้มีความถูกต้อง โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความคลาดเคลื่อนได้ เอกสารต้นฉบับในภาษาต้นทางควรถูกพิจารณาเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้การแปลโดยผู้เชี่ยวชาญด้านมนุษย์ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดที่เกิดขึ้นจากการใช้การแปลนี้
<!-- CO-OP TRANSLATOR DISCLAIMER END -->