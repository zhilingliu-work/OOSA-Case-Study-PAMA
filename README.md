# 📊 大學課程專案：獲獎作品逆向工程與物件導向系統分析報告 (OOAD Case Study)

<p align="center">
  <img src="https://img.shields.io/badge/UML-Reverse%20Engineering-blue?style=for-the-badge&logo=diagramsdotnet&logoColor=white" alt="UML Analysis">
  <img src="https://img.shields.io/badge/Case%20Study-Award%20Winning%20System-emerald?style=for-the-badge" alt="Case Study">
  <img src="https://img.shields.io/badge/Database-Schema%20Design-orange?style=for-the-badge&logo=mysql&logoColor=white" alt="Database">
  <img src="https://img.shields.io/badge/Academic-Project-red?style=for-the-badge" alt="Academic">
</p>

## 📌 專案與團隊資訊

| 項目 | 詳細資訊 |
| :--- | :--- |
| **課程名稱** | 物件導向系統分析實習 (Object-Oriented System Analysis Practicum) |
| **研究對象** | 國立中山大學獲獎作品 —— PAMA 智慧會議助理 |
| **授課教師** | 江傳文 教授 |
| **團隊成員** | 國立高雄科技大學 電腦與通訊工程系 (電通二甲) <br> 👤 **組長：** 劉志凌 (C112110130) <br> 👥 **組員：** 郭宇恩 (C112110111)、葉剛廷 (C112110157) |
| **製作日期** | 民國 114 年 6 月 13 日 |
| **原作品演示** | [PAMA 系統簡介展示影片](https://www.youtube.com/watch?v=7189u0V7591) |

---

## 📖 專案背景與研究動機

本專案為大學「物件導向系統分析實習」課程之期末報告。為了深入理解現代智慧化協作系統的架構設計，本團隊選定國立中山大學推出的獲獎作品 **「PAMA 智慧會議助理」** 作為核心逆向工程與分析對象。

該系統旨在提升會議記錄、資料統整與創意思考的效率。本專案的目標**並非重新開發該系統**，而是以軟體工程的方法論，**「將一個現有的高質量應用，逆向還原出標準化的軟體工程規劃書」**，藉此鍛鍊團隊從表面功能需求推導出底層類別結構與資料庫模型的能力。

---

## 🔍 逆向工程分析：技術堆疊解構

透過原作品的功能展示與心智圖分析，本團隊對其背後的技術堆疊與模組設計進行了深度解構：

1. **語音轉文字模組：** 分析其整合 `Microsoft Azure Speech to Text` 的流程，理解語音即時轉錄與自動格式化排列的邏輯。
2. **文本與詞頻分析：** 分析其運用 `Jieba`、`TF-IDF` 演算法進行斷詞、計算詞頻，並透過 `d3.js` 視覺化為長條圖與關鍵字泡泡圖的資訊流。
3. **LLM 語意收斂與靈感延伸：** 分析其如何導入 `Meta Llama2`（進行外部資料匹配與摘要）與 `OpenAI GPT-3.5-turbo`（進行一鍵會議結論提煉與結構化表格生成）。

---

## 🎯 UML 軟體工程模型建構（本專案核心產出）

本團隊運用物件導向分析與設計（OOAD）方法論，為該獲獎作品重新建立了嚴密的軟體工程分析模型：

### 1. 需求描述與事件驅動模型 (Use Case & Event Tables)
* **需求與事件釐清：** 將系統功能拆解出「語音轉文字」、「一鍵摘要」、「外部詞資配對」等 17 項核心事件，並推導出其對應的觸發器、來源、回應與目的地。
* **使用案例圖 (Use Case Diagram)：** 定義系統邊界與行為者（Actors），並梳理出功能間的 `<<include>>` 依賴關係。

### 2. 動態行為模型 (Activity Diagrams & Case Description)
針對 12 大核心功能撰寫標準案例描述書（定義前置/後置條件），並繪製詳細的活動圖（Activity Diagram），精確規劃了諸如「驗證失敗」、「麥克風未授權」、「語音辨識異常」等例外路徑（Alternate Course）的系統應變邏輯。

### 3. 靜態結構模型 (Class Diagram)
逆向推導出系統的類別結構圖，定義包括 `User`、`Meeting`、`Transcript`、`SpeechProcessor`、`KeywordAnalyzer`、`BubbleChart`、`Summary` 等 9 大核心類別的屬性與方法，並建構出合理的物件關聯與依賴結構。

---

## 🗄️ 資料庫正規化設計 (Schema Normalization)

為了承接上述分析的物件模型，本團隊為該系統規劃了符合 **第三正規化 (3NF)** 規格的關係型資料庫邏輯架構，以確保數據一致性並消除資料冗餘：

* **User (使用者群)：** `userID` (PK), userName, email, password
* **Participants (與會人員關聯)：** `userID` (FK), userName, email
* **MeetingData (會議主檔)：** `meetingID` (PK), date, participants, transcript
* **Transcript (逐字稿明細)：** content, timestamp, speaker, paragraphs
* **Keywords (關鍵字權重)：** `keywordID` (PK), content, keywordFrequency
* **BubbleChart (視覺化圖表數據)：** `chartID` (PK), chartData, relationMap
* **Summary (會議結論摘要)：** `summaryID` (PK), summaryText, keyPoints

---

## 📁 儲存庫檔案清單

```markdown
├── 113-2_OOSA期末報告_C112110130_劉志凌.pdf   # 完整的系統分析書面報告書 (含事件表格、案例描述、活動圖與正規化說明)
├── PAMA.pdf                                # 高解析度標準 UML 使用案例圖 (Use Case Diagram)
├── PAMA智慧會議助理.jpg                     # 解構原作品技術堆疊與演算法應用之心智圖
├── 正規化.png                              # 經由逆向推導設計之資料庫實體關係與欄位結構圖
└── README.md                               # 本專案說明文件
---

## 🧠 學習收穫與團隊反思

透過將優秀獲獎作品作為分析標竿，團隊經歷了極具價值的軟體工程洗禮。在逆向工程的過程中，我們深刻體會到一套成熟的系統不能只考慮「理想開發路徑」，必須花費大量心力在例外路徑與防呆機制的規劃上（如辨識失敗、權限不足等處理）。

從最初的需求梳理、活動圖繪製，到最後建構出類別圖與正規化資料庫，這種循序漸進的邏輯推導，大幅提升了我們將抽象業務需求轉化為嚴密技術規格的「架構師思維」。這項能力不論是在未來的團隊協作還是實際的專案開發中，都將成為最堅實的技術基礎。
