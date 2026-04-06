# SDD 願景與現實

本文基於以下連結彙整 SDD 設計願景與其實務問題。

+ [Spec-Driven Development: From Code to Contract in the Age of AI Coding Assistants](https://arxiv.org/pdf/2602.00180)
+ [Spec-Driven Development(SDD) 的美好願景與殘酷現實](https://ihower.tw/blog/13480-sdd-spec-driven-development)

## 什麼是 Spec-Driven Development (SDD)？

SDD 的核心流程是在讓 AI 寫程式碼之前，先要求 LLM（大語言模型）生成一套結構化的規格文件：

**產品需求 (PRD) → 技術設計 (Design Doc) → 任務清單 (Task List)**

最後才將這些規格交給 Coding Agent 執行。目前的代表工具有 GitHub Spec-Kit、AWS Kiro 與 Tessl。

簡單來說，Spec-Driven Development (SDD，規格驅動開發) 視為一種試圖在「AI 自動化編碼」與「傳統軟體工程嚴謹性」之間取得平衡的新興方法論，其核心概念是：「不要讓 AI 直接寫程式碼，要讓 AI 先寫規格，經由人類確認後，再由 AI 根據規格執行實作。」

### 1. SDD 的核心流程：從「Vibe」轉向「Spec」

在 AI 輔助開發的初期，很多開發者傾向於「Vibe Coding」（憑感覺開發），直接給 AI 一段模糊的需求。SDD 則要求建立一個結構化的流水線：

+ 階段一：需求規格化 (Product Spec)
將模糊的想法轉化為結構化的 Markdown 文件，定義功能邊界與使用者故事。

+ 階段二：技術設計 (Technical Design)
AI 根據需求，主動分析現有程式碼庫（Context），提出要修改的檔案清單、新增的 API 介面、資料庫 Schema 變動。

+ 階段三：任務拆解 (Task Breakdown)
將設計轉化為原子化的實作步驟（例如：1. 修改 User Model, 2. 建立 Migration, 3. 實作 Controller）。

+ 階段四：執行與驗證 (Execution & Verification)
Coding Agent 依照任務清單撰寫程式碼與單元測試。

### 2. 為什麼我們需要 SDD ?

從架構師的角度看，直接讓 AI 寫大段程式碼會面臨以下問題，而 SDD 正是針對這些問題的解藥：

+ 幻覺控制 (Hallucination Control)： 透過先寫「設計文件」，人類可以在程式碼產生前就發現 AI 的邏輯錯誤，省下除錯時間。

+ 上下文管理 (Context Management)： AI 的上下文視窗有限。SDD 透過「規格」將大任務拆成小任務，讓 AI 每次只專注於一個小的實作區塊。

+ 可維護性 (Maintainability)： 規格文件成為了 Source of Truth (事實來源)。未來維護時，開發者是看規格而非翻找 AI 隨興產生的註釋。

### 3. SDD 的層次：從輔助到自動化

我們可以將 SDD 的實踐分為三個演進層次：

+ Spec-first (規格優先)： 規格只是開發過程的藍圖，用完即丟。
+ Spec-anchored (規格錨定)： 規格與程式碼同步更新，作為長期維護的文件。
+ Spec-as-source (規格即原始碼)： 這是終極願景，人類只編輯高階規格，底層程式碼完全由 AI 根據規格生成並維護，人類不再手寫程式碼。

## 各篇文獻的優劣分析總結

### 1. François Zaninotto：瀑布流的回歸

+ 劣勢（痛點）：
	- 脈絡盲區： Agent 依賴文字搜尋，容易遺漏舊功能需求。
	- Markdown 地獄： 產出過多冗長文件，開發者得從文字海中找錯誤，反而增加負擔。
	- 審查成本翻倍： 必須先審規格再審實作，效率減半。
	- 虛假安全感： Agent 可能只完成了「文件標記」，卻沒寫實際測試。
+ 優勢（反向建議）： 主張採用 Lean Startup（精實創業） 模式，以小步迭代與最小實驗來驗證，而非過度規劃。

### 2. Gojko Adzic：BDD 的進階還是災難？

+ 劣勢（觀察）：
	- 規格過於抽象： 產出的內容較像「工作範圍」，而非開發所需的「精準規格」。
	- 機器讀而非人讀： 產生的文字是給工具追蹤用的，人類開發者通常會直接跳過。
	- 缺乏範圍定義： 容易導致工具失控，產出過多不必要的測試與程式碼。
+ 優勢（潛力）： 若能加入明確的 Scoping（範圍定義），有潛力成為可執行的規格。

### 3. Birgitta Böckeler (Thoughtworks)：工具評測

+ 劣勢（現狀）：
	- 過度工程化： 用 Kiro 修小 Bug 卻產生大量 User Stories，殺雞用牛刀。
	- 控制感幻覺： Agent 經常忽略指示，甚至重複生成既有程式碼。
	- Verschlimmbesserung： 德文詞意指「越幫越忙」，試圖改善卻讓事情變更糟。
+ 優勢（分類價值）： 將 SDD 分為三個層次：Spec-first（當下用）、Spec-anchored（長期維護用）、Spec-as-source（規格即原始碼）。這為架構規劃提供了清晰的願景。


## 總結

目前的 SDD 仍處於「美好願景」多於「實際效益」的階段。以下是實務建議：

+ 避免 Markdown 地獄： 除非專案極其複雜且需要高度合規性，否則應避免生成過於結構化的長篇文件。
+ 優先強化「工程實踐」： 與其花時間寫規格給 AI 讀，不如花時間完善 自動化測試 (CI/CD)。這是目前驗證 AI 產出最可靠的「規格」。
+ 小步迭代： 採用 Birgitta Böckeler 提到的 Spec-first 即可（先有簡單計畫再開發），不需追求一步到位實現 Spec-as-source。
+ 適才適所： 對於新專案或獨立模組，可以嘗試 SDD 工具；對於既有的大型系統，應採取 Vibe Engineering 結合傳統測試的方式。
