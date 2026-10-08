# spec-kit

Cursor Agent Skills 集合。產品規格由自然語言推到可規劃的 Feature Specification；Skill 本身則用同一套模組化流程來建立與維護。

Skills 放在 `.agents/skills/`。每個 Skill 的入口是該目錄下的 `SKILL.md`。

## 產品規格

把一個功能想法寫成規格，並把會擋住後續規劃的缺口問清楚。

| Skill | 做什麼 |
| --- | --- |
| [specify](.agents/skills/specify/SKILL.md) | 把自然語言需求推成結構完整、可驗證的 Feature Specification，寫入 `specs/<NNN>-<feature-slug>/spec.md`。內容涵蓋 User Stories、驗收條件、功能與非功能需求、邊界情況與成功標準。規格若仍有核心缺口，Status 為 `Needs Clarification`，並交給 `clarify` 提問。 |
| [clarify](.agents/skills/clarify/SKILL.md) | 針對既有規格的核心不確定處工作。提問模式最多提出三個澄清問題；套用模式把使用者的回答回寫進同一份 spec，並同步受影響章節與狀態，使規格可以進入後續 planning。 |
| [technical-research](.agents/skills/technical-research/SKILL.md) | 在 `/specify` 產出的 Feature Specification 之後執行，將可進入 planning 的規格推導成 `research.md` 與 `techstack.md`。`research.md` 聚焦技術決策、理由與替代方案；`techstack.md` 彙整採用、延後或不採用的技術堆疊與 planning 約束。 |
| [system-analysis](.agents/skills/system-analysis/SKILL.md) | 依 Feature Specification 或使用者需求產出 `plan.md` 中的系統分析規劃。先盤點需求涉及的技術端點與系統介面（名稱、端點類型、需求依據），再依依賴關係排成可平行委派的分析 Wave，並描述專案文件與原始碼結構及 Structure Decision。 |

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
