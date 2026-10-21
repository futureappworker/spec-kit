# spec-kit

Cursor Agent Skills 集合。產品規格由自然語言推到可規劃的 Feature Specification；Skill 本身則用同一套模組化流程來建立與維護。

Skills 放在 `.agents/skills/`。每個 Skill 的入口是該目錄下的 `SKILL.md`。

## 流程

同一功能的文件都在 `specs/<NNN>-<feature-slug>/`。前一步就緒才進入下一步。規格仍有核心缺口時先澄清，答案寫回後再繼續。寫入每份產出時會讀 `constitution/` 的共同套用規範與該產出的憲法 Rule。

1. `specify` 寫 `spec.md` 與 checklist。Status 為 `Needs Clarification` 時，交給 `clarify-over-specs` 提問；回答後由它寫回規格。
2. `technical-research` 寫 `research.md` 與 `techstack.md`。
3. `system-analysis` 寫 `plan.md`，再依 Wave 交給 `ui-ux-plan`、`api-plan`、`data-plan` 完成介面分析。
4. `testplan` 依規格與介面契約寫 `testplan.md`。
5. `tasks` 依測試計劃寫 `tasks.md`，每個案例拆成紅燈、綠燈、重構。
6. `implement` 依序一次實作一個未完成任務，直到全部完成。標有 TDD 步驟的交給 `tdd`，只做該步。任務全部完成後，把 `spec.md` 標為 `Implemented`。

Skill 本身的建立與維護走另一條線：已有確認滿意的 Artifact 時，從 `artifact-to-skill-engineering` 倒抽 Template，再交給 `skill-engineering`。直接新建或優化時用 `skill-engineering`：新建先定邊界再寫 SOP，優化先確認根因再改寫。要外移的步驟交給 `skill-derive-rule`、`skill-derive-template` 或 `skill-derive-script`；直接改某一類檔案時，用對應的 `skill-form-*`。

## 產品規格

把一個功能想法寫成規格，並把會擋住後續規劃的缺口問清楚。寫入產出時會讀取 `constitution/` 的共同套用規範與該產出的憲法 Rule；規則要求停止時不寫入。

| Skill | 做什麼 |
| --- | --- |
| [specify](.agents/skills/specify/SKILL.md) | 把自然語言需求推成結構完整、可驗證的 Feature Specification，寫入 `specs/<NNN>-<feature-slug>/spec.md`。內容涵蓋 User Stories、驗收條件、功能與非功能需求、邊界情況與成功標準。未指定既有路徑時，跳過狀態為 `Implemented` 的規格並建立下一個流水號；尚未完成的規格有兩份以上時，先詢問要使用哪一份。明確指定路徑時更新該檔，寫入的 Status 只會是 `Draft`、`Needs Clarification` 或 `Ready for Planning`。規格與 checklist 寫完後，若仍有核心缺口、Status 為 `Needs Clarification`，把該規格交給 `clarify-over-specs` 以提問模式產生澄清問題。 |
| [clarify](.agents/skills/clarify/SKILL.md) | 針對任何任務、Artifact 或決策中會擋住後續工作的核心不確定處產生澄清問題。依影響排序，最多五題；每題提供 A、B、C 與 Custom，並標出恰好一個推薦選項與理由。當問題涉及流程、狀態、關係或結構，且缺少圖就無法判斷範圍時，在選項前附上描述該情境的 mermaid 圖。回答不寫入目標檔案。 |
| [clarify-over-specs](.agents/skills/clarify-over-specs/SKILL.md) | 在 `/specify` 寫完 `spec.md` 之後做專業需求澄清。`specify` 在狀態為 `Needs Clarification` 時以提問模式交給它；使用者也能直接要求提問或套用答案。先掃描規格覆蓋並依影響挑出最多五題，再委派 `clarify` 提問；使用者回答後，由這個 Skill 把答案寫回規格的對應章節。 |
| [technical-research](.agents/skills/technical-research/SKILL.md) | 在 `/specify` 產出的 Feature Specification 之後執行，將可進入 planning 的規格推導成 `research.md` 與 `techstack.md`。`research.md` 聚焦技術決策、理由與替代方案；`techstack.md` 彙整採用、延後或不採用的技術堆疊與 planning 約束，不另列後續技術問題。選型資訊不足時把缺口交回使用者，且不得把這兩份文件標為 Ready for Planning。 |
| [system-analysis](.agents/skills/system-analysis/SKILL.md) | 依 Feature Specification、同目錄 `research.md` 與 `techstack.md` 產出並執行 `plan.md` 中的系統分析規劃。先盤點技術端點與系統介面，再依依賴關係排成分析 Wave，並委派 `ui-ux-plan`、`api-plan`、`data-plan` 完成對應介面分析。介面契約需要修改時，交回擁有該契約的 Planner Skill 修正。 |
| [testplan](.agents/skills/testplan/SKILL.md) | 在系統介面分析完成後，依 `spec.md`、`plan.md` 與契約檔制定 `testplan.md`。使用者故事各成一章，其後每條有案例的全域 NFR 各成一章。使用者故事中可觀察的 FR 與 NFR，以及有可觀察結果的全域 NFR，寫成原子案例，每個案例指向一個上游契約位址。各章自帶 TDD 順序。全域功能需求、成功標準，以及沒有可觀察結果的全域 NFR，列為不列為案例。 |
| [ui-ux-plan](.agents/skills/ui-ux-plan/SKILL.md) | 分析前端端點、瀏覽器互動、畫面狀態與使用者流程，依 Pencil 樣板 `templates/interface.pen` 產出可供 API 與資料規劃對齊的 UI/UX 介面分析。 |
| [api-plan](.agents/skills/api-plan/SKILL.md) | 分析後端端點、API、WebSocket、服務狀態機與權威判定邊界，依 OpenAPI 樣板 `templates/openapi.yaml` 產出可供前端與資料規劃對齊的 API 介面分析。 |
| [data-plan](.agents/skills/data-plan/SKILL.md) | 分析資料庫端點、持久化模型、查詢、快照與資料保留邊界，依 DBML 樣板 `templates/schema.dbml` 產出可供前端與 API 規劃對齊的資料介面分析。 |
| [tasks](.agents/skills/tasks/SKILL.md) | 在 `testplan.md` 完成後，依測試計劃的 User Story、全域 NFR 與各章 TDD 順序產出 `tasks.md`。每個原子案例依序拆成紅燈、綠燈、重構三個任務，並同時指向該案例與它的契約位址。每條有案例的全域 NFR 各成一個 Phase，排在全部使用者故事之後。 |
| [implement](.agents/skills/implement/SKILL.md) | 依 feature 目錄中的 `tasks.md`，依序一次實作一個未完成任務，直到全部完成。標有 TDD 步驟的任務交給 `tdd`，只做紅燈、綠燈或重構其中一步；其餘任務只讀該任務列出的 References。該任務驗證通過後才把 checkbox 從 `[ ]` 改為 `[X]`。`checklists/` 仍有未勾項目且未允許略過時，先停下詢問。全部任務完成後，把該 feature 的 `spec.md` 狀態改為 `Implemented`。 |
| [tdd](.agents/skills/tdd/SKILL.md) | 以紅燈、綠燈、重構推進一條已確認接縫。使用者直接呼叫且未指定步驟時，先確認接縫，再跑完整循環。`implement` 傳入一個步驟與測試計劃案例時，該案例就是已確認接縫，本次只做那一步。受測部位是瀏覽器時，用 Playwright 寫並執行該案例。 |
| [constitution](.agents/skills/constitution/SKILL.md) | 依使用者需求撰寫專案憲法。使用者要求必要憲法、共同憲法、共用憲法、共同套用，或 `constitution/共同/憲法套用規範.md` 時，若該檔不存在，先寫入基本版。要為已確認的 Skill 產出增量撰寫憲法 Rule 時，目標 Skill、產出物、部位與必備或禁止內容能從描述判斷則直接採用，判斷不出來才問下一個缺口，一次寫入一條 Rule。 |

## Skill 工程

建立新 Skill，或針對輸出不滿意的既有 Skill 做根因分析後再改寫。`skill-engineering` 負責編排；底下的 form 與 derive 負責單一種類的產物。

| Skill | 做什麼 |
| --- | --- |
| [artifact-to-skill-engineering](.agents/skills/artifact-to-skill-engineering/SKILL.md) | 從使用者確認滿意的 Artifact Example 出發，先客製化範例，再委派 `skill-form-template` 倒抽 Template，最後交給 `skill-engineering` 反推可穩定產出該 Artifact 的目標 Skill。 |
| [skill-engineering](.agents/skills/skill-engineering/SKILL.md) | 編排整次建立或優化。新建時先定用途與邊界，再交給 `skill-form-sop` 寫出最小可執行 SOP。優化時先做根因分析，等確認後才改寫。接著決定哪些步驟留在 SOP、哪些要拆成 Rule、Template 或 Script，並刪掉不再被載入的過時模組。 |

### 撰寫與檢查

直接寫或改某一類檔案，寫完依該類規範檢查並修正。

| Skill | 做什麼 |
| --- | --- |
| [skill-form-sop](.agents/skills/skill-form-sop/SKILL.md) | 撰寫、檢查並修正 `SKILL.md` 裡的 SOP，管結構、可執行性，以及精簡與按需載入。 |
| [skill-form-rule](.agents/skills/skill-form-rule/SKILL.md) | 撰寫、檢查並修正 `rules/` 下的 Rule File。 |
| [skill-form-template](.agents/skills/skill-form-template/SKILL.md) | 撰寫、檢查並修正 `templates/` 下由骨架與範例組成的 Template。 |
| [skill-form-script](.agents/skills/skill-form-script/SKILL.md) | 撰寫、檢查並修正 `scripts/` 下可由 AI 直接執行的 Python Script，含介面、依賴與受控驗證。 |

### 從既有 SOP 衍生

目標 Skill 已經有 SOP 時，把指定步驟裡適合外移的部分抽成獨立檔案，再接回原流程。建立檔案時會交給對應的 form Skill，改 SOP 時交給 `skill-form-sop`。

| Skill | 做什麼 |
| --- | --- |
| [skill-derive-rule](.agents/skills/skill-derive-rule/SKILL.md) | 為指定步驟衍生按需載入的 Rule File，用來加強該步驟的把關規則。 |
| [skill-derive-template](.agents/skills/skill-derive-template/SKILL.md) | 為指定的檔案生成步驟衍生骨架與範例，讓固定輸出格式用樣板表達。 |
| [skill-derive-script](.agents/skills/skill-derive-script/SKILL.md) | 為指定步驟衍生可自動執行的 Python Script，把可確定性自動化的職責從 SOP 交出去。 |
