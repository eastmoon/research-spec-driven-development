# 語意編程

本文基於以下連結彙整基於語意的設計概念與編寫方式。

+ [Domain-Driven Design — Eric Evans (2003)](https://en.wikipedia.org/wiki/Domain-driven_design)
+ [Semantic Software Design — Eben Hewitt (O'Reilly, 2019)](https://www.oreilly.com/library/view/semantic-software-design/9781492045946/)
+ [copilot-cli-for-beginners - development workflows](https://copilot-cli-for-beginners.gh.miniasp.com/03-development-workflows/)
+ [從 Prompting 基本結構到 Agent Prompting 設計原則](https://ihower.tw/blog/13093-agent-prompting-design)

## 語意架構（Semantic Architecture）

語意架構是一種以意義 ( meaning ) 為中心的系統設計方法，強調系統中各元件、介面、資料、行為不只要在技術層面正確，更要在語意層面一致且可理解。

其核心概念為，「不只關心**怎麼做**，更關心**這代表什麼意思**」。

### 語意衝突

傳統架構設計關注的是結構 ( 模組如何組合 ) 與行為 ( 系統如何運作 )，但隨著系統規模擴大，便出現了幾個常見問題：

+ 不同團隊對同一個詞彙有不同理解（例如「訂單」在財務和物流部門的定義不同）
+ API 介面技術上相容，但業務語意不一致導致 bug
+ 資料在系統間流動時，意義被扭曲或遺失
+ 微服務拆分後，邊界模糊，職責不清

語意架構就是為了解決這些「意義層面的混亂」。

### 語意架構概念

語意架構主要包過四個核心概念：

1. 統一語言（Ubiquitous Language）
來自 DDD（領域驅動設計），要求開發者、架構師、業務人員使用同一套詞彙，且這套詞彙直接反映在程式碼中。
2. 語意邊界（Semantic Boundary）
等同於 DDD 的 Bounded Context，每個邊界內詞彙有明確定義，跨邊界時需要明確的翻譯、映射層。
3. 語意契約（Semantic Contract）
介面不只是定義資料格式的語法契約，還要定義意義、約束、前後置條件，類似 [Design by Contract](https://zh.wikipedia.org/zh-tw/%E5%A5%91%E7%BA%A6%E5%BC%8F%E8%AE%BE%E8%AE%A1) 的精神。
4. 語意一致性（Semantic Consistency）
同一個概念在整個系統中，從 UI 到 DB，應有一致的表達方式。

## 提示詞 ( Prompt ) 撰寫

### Normal Prompt vs Agent Prompt

| 面向 | Normal Prompt | Agent Prompt |
| :- | :--- | :--- |
| 結構 | 高度結構化、線性 | 彈性、概念導向 |
| 設計長度 | 可能很長且詳細 | 一開始簡短，逐步迭代增加 |
| 範例使用 | 大量 few-shot 範例 | 最少範例，避免過度限制 |
| 指令類型 | 步驟性指令 | 啟發式規則和原則 |
| 重點 | 單次正確執行 | 自主循環執行和適應 |

針對 Agent 的 Prompting 核心理念是賦能而非限制，給予足夠的指引讓 Agent 理解任務和邊界，但保留其自主決策和創造性解決問題的空間。

針對一般 Prompt 的概念則是規制流程，如同教導新進員工的規範手冊，確保無論多少次執行都能出現相近的結果。

### [技能 vs. 代理程式 vs. MCP](https://copilot-cli-for-beginners.gh.miniasp.com/05-skills/#%E6%8A%80%E8%83%BD-vs-%E4%BB%A3%E7%90%86%E7%A8%8B%E5%BC%8F-vs-mcp)

技能只是 GitHub Copilot 擴充模型的一個環節。以下是它們與代理程式和 MCP 伺服器的比較。

| 功能 | 作用 | 使用時機 |
| :- | :--- | :--- |
| 代理程式 | 改變 AI 的思考方式 | 需要跨多項任務的專業知識 |
| 技能 | 提供任務特定的指令 | 具有詳細步驟的特定、可重複任務 |
| MCP | 連接外部服務 | 需要 API 的即時資料 |

代理程式用於廣泛的專業知識，技能用於特定任務指令，MCP 用於外部資料。在對話過程中，代理程式可以使用一個或多個技能。例如，當您要求代理程式檢查程式碼時，它可能會自動同時套用 security-audit 技能和 code-checklist 技能。

## 總結

對於何謂程式，個人有如下見解：

「程式是基於其程式語言，在執行環境的規範與限制下，運行開發者編寫的邏輯。」

語意架構是一種設計方法論，其目標就是如何制定一套嚴謹的設計文本，確保跨產業、系統間的詞語一致；但無論語意架構如何設計與規範，最終仍需要開發人員遵守才能得以實踐。

但若基於語意架構的設計與規劃，讓提示詞具有相應的嚴謹度，並用於規範技能 ( Skills )、代理人 ( Agent )，最終可將其運用於開發流程。

這樣的過程，實質上也遵循者軟體編程的過程，若講究其差異，僅是用何種語言、編譯器。

| | 軟體編程 | 語意編程 |
| :- | :- | :- |
| 語言 | 程式語言 ( C++、Java etc.) | 自然語言 |
| 撰寫規範 | 程式語法規範 | 提示詞規範 |
| 編譯器 | 程式語言對應編譯器 | 大語言模型 |
| 單元測試 | 程式語言對應測試框架 | 大語言模型 |
| 執行 | 編譯產生可執行檔，並運行相應作業環境 | 依據產出交付給直譯程式運行或編譯為可執行檔 |
