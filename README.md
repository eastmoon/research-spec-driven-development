# Spec-Driven Development

## 簡介

Spec-Driven Development 的根源可追溯至 1960 年代 NASA 的工作流程，以及早期強調邏輯驗證優先於編碼的形式化方法（Formal Methods）。
> [Spec-driven_development - Wikipedia](https://en.wikipedia.org/wiki/Spec-driven_development)

規格 ( Spec ) 一詞在軟體工程中早有應用先例，如分散式運算與 RPC 通訊中，Spec 作為異質系統間的通訊契約；在行為驅動開發（BDD）中，Spec 則作為與業務使用者協作的媒介，以情境與範例形式撰寫，成為系統行為的文件；然而，Spec 在產業的實務中存在最大問題，是「文件歸文件，程式歸程式」，結果未必會與定義的文件、規範一致。

直到 AI 大語言模型崛起，SDD 得到了新的詮釋，GitHub Blog 於 2025 年 9 月正式發布 Spec Kit，宣告「我們正從『程式碼是真理來源』轉向『意圖是真理來源』—— AI 讓規格變得可執行」。

## 大語言模型編程

在大語言模型崛起後，相關用大語言模型替代程式設計的概念百家爭鳴，在此整理相關的詞語與定義，並請大語言模型比較兩者差異。

+ Vibe Coding：快速驗證想法，不在意品質與可維護性
+ Spec-Driven Development：以規格驅動 AI 生成，確保品質與可預測性
+ Agentic Engineering：SDD 的延伸：人員撰寫 Spec，以多 Agent 平行實作，並回歸人員擔任架構治理者與最終審查者

### Vide Coding

[Vibe Coding](https://x.com/karpathy/status/1886192184808149383) 是由 AI 研究員 Andrej Karpathy 在 2025 年初提出的概念，核心思想是：完全依賴 AI 產生程式碼，開發者不深入閱讀或理解產出的程式碼，只靠「感覺」( vibe ) 驅動開發；開發者只需用自然語言描述需求，讓 AI ( 如 Claude、Cursor、GitHub Copilot 等 ) 生成程式碼，遇到錯誤就把錯誤訊息丟回給 AI 修正，如此反覆迭代，直到功能「看起來能跑」為止。

Vibe Coding 是一把雙面刃。作為快速驗證工具，它非常有價值；但 AI 大語言模型本身的不可預測性與缺乏架構、結構審查，若用於生產環境的核心系統，就是在累積定時炸彈。

### Spec-Driven Development

[Spec-Driven Development](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/) 是由 GitHub Blog 於 2025 年 9 月提出的概念，在 Spec Kit 的介紹描述如下：

規範驅動開發顛覆了傳統的軟體開發模式。幾十年來，程式碼至上——規範只是搭建的框架，一旦開始「真正的」編碼工作，規範就會被棄之不用。規範驅動開發改變了這一切：規範變得可執行，能夠直接產生可運行的實現，而不僅僅是指導實現過程。
> From [spec-kit](https://github.com/github/spec-kit)

Spec-Driven Development 與 Vibe Coding 的核心差異：

| | Spec-Driven Development | Vibe Coding |
| 驅動力| 規格、契約、可驗證的 | 感覺、直覺、即興 |
| 需求起點 | 結構化的規格文件 | 一句話描述 |
| 程式碼審查 | 嚴格對照 Spec 驗證 | 幾乎不看 |
| 可預測性 | 高 | 低 |
| 適用場景 | 生產系統、團隊協作 | 原型、週末 project |

### Agentic Engineering

[Agentic Engineering](https://x.com/karpathy/status/2019137879310836075) 是由 Andrej Karpathy 於 2026 年 2 月在 X 上提出的概念，作為 Vibe Coding 的進化版與專業化版本。Karpathy 在命名上刻意拆解為兩個部分：「Agentic」代表開發者 99% 的時間不再直接撰寫程式碼，而是指揮 AI Agent 執行任務並擔任監督者；「Engineering」則強調這是一門有藝術、有科學、有專業深度的技能，是可以學習並持續精進的。

Agentic Engineering 保留了 AI 大語言模型帶來的生產力革命，但要求開發者從「使用者」升級為「架構治理者」，更加重視規劃、審查等機制。

Agentic Engineering 與 Vibe Coding 的核心差異：

| | Agentic Engineering | Vibe Coding |
| :- | :- | :- |
| 人的角色 | 架構師、監督者、協調者 | 提示者、使用者 |
| 程式碼審查 | 嚴格審查 | 幾乎不看 |
| 適用場景 | 生產環境、企業系統技術 | 週末 side project |
| 門檻高低 | 高 ( 需系統設計能力) | 低 ( 僅需對軟體的認知 ) |
| Agent 數量 | 多 Agent 平行協作 | 單一對話 |

## 文獻討論

+ [SDD 遠景與現實](./docs/sdd-vision-and-reality.md)
+ [語意編程](./docs/semantic-coding.md)
