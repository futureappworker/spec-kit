---

description: "{{TASKS_DESCRIPTION}}"
---

# Tasks: {{FEATURE_NAME}}

**Input**: Design documents from `{{SPEC_DIRECTORY}}`

**Prerequisites**: 本清單已對齊 testplan.md（必要）、plan.md（必要）與 spec.md（必要）。開發任務的案例與順序來自 testplan.md 各章的 TDD 順序。執行時由上往下，不要在開工時讀完 research.md、techstack.md、contracts/ 或整份 testplan.md。每個任務下方的 **References** 才是載入時機，而且只讀該位址。路徑相對於 `{{SPEC_DIRECTORY}}`。

**Tests**: 每個原子案例依所屬章的 TDD 順序拆成紅燈、綠燈、重構。紅燈先寫該案例並執行到預期失敗。綠燈只做該案例通過所需的最小實作。重構在該案例綠燈之後；沒有可做的結構調整時保持行為不變，並確認測試仍通過。

**Organization**: Phase 3 起每個使用者故事對應 testplan.md 的一則使用者故事，最後一個 Phase 對應跨故事章。有案例的介面才用 `###` 開端點小節。{{STORY_ENDPOINT_SUMMARY}} Setup 與 Foundational 沒有案例，不標 TDD 步驟。

## Format: `[ID] [P?] [Story] Description`

- **[P]**: 可平行（不同檔案、不依賴同階段尚未完成的任務）。同一章的紅燈、綠燈、重構依該章順序串行，不標 [P]
- **[Story]**: 該任務所屬使用者故事（{{STORY_LABELS}}）。跨故事任務不標 [Story]
- 描述含精確檔案路徑
- 使用者故事與跨故事章的端點小節使用 `###`。端點小節只標 **Codebase**
- **TDD 步驟** 寫在有案例的任務下方，值為 `紅燈`、`綠燈` 或 `重構` 之一
- **References** 寫在任務正下方，一行一個位址。TDD 任務兩行：`testplan.md#{案例 ID}`，以及該案例受測操作的一個契約位址。後端任務不寫 DBML 或畫面。前端畫面任務不寫 OpenAPI 或 DBML
- 位址寫法：案例用 `testplan.md#{{CASE_ID_EXAMPLE}}` 這種案例 ID；HTTP 操作用 `contracts/openapi.yaml#/paths/~1{path}/{method}`（`/` 寫成 `~1`）；畫面用 `contracts/interface.pen#{frameId}`；DBML 用 `contracts/schema.dbml#Table/{name}`；技術選型用 `techstack.md#採用技術/{Area}`；目錄用 `plan.md#原始碼：儲存庫根目錄`

## Path Conventions

- **Web app**: {{PATH_CONVENTION_WEB_APP}}
- {{PATH_CONVENTION_STACK}}
- {{PATH_CONVENTION_ENDPOINTS}}

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: {{PHASE_1_PURPOSE}}

- [ ] {{T001_TASK}}
  - **References**: `{{T001_REFERENCE_1}}`
- [ ] {{T002_TASK}}
  - **References**: `{{T002_REFERENCE_1}}`
- [ ] {{T003_TASK}}
  - **References**: `{{T003_REFERENCE_1}}`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: {{PHASE_2_PURPOSE}}

**⚠️ CRITICAL**: 本階段完成前不得開始任何使用者故事

- [ ] {{T004_TASK}}
  - **References**: `{{T004_REFERENCE_1}}`
- [ ] {{T005_TASK}}
  - **References**: `{{T005_REFERENCE_1}}`

**Checkpoint**: {{PHASE_2_CHECKPOINT}}

---

## Phase 3: User Story 1 - {{USER_STORY_1_TITLE}}（Priority: {{USER_STORY_1_PRIORITY}}）🎯 MVP

**Goal**: {{USER_STORY_1_GOAL}}

**Independent Test**: {{USER_STORY_1_INDEPENDENT_TEST}}

### {{USER_STORY_1_BACKEND_HEADING}}

**Codebase**: `{{USER_STORY_1_BACKEND_CODEBASE}}`

- [ ] {{T006_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T006_REFERENCE_1}}`
  - **References**: `{{T006_REFERENCE_2}}`
- [ ] {{T007_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T007_REFERENCE_1}}`
  - **References**: `{{T007_REFERENCE_2}}`
- [ ] {{T008_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T008_REFERENCE_1}}`
  - **References**: `{{T008_REFERENCE_2}}`
- [ ] {{T009_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T009_REFERENCE_1}}`
  - **References**: `{{T009_REFERENCE_2}}`
- [ ] {{T010_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T010_REFERENCE_1}}`
  - **References**: `{{T010_REFERENCE_2}}`
- [ ] {{T011_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T011_REFERENCE_1}}`
  - **References**: `{{T011_REFERENCE_2}}`

### {{USER_STORY_1_FRONTEND_HEADING}}

**Codebase**: `{{USER_STORY_1_FRONTEND_CODEBASE}}`

- [ ] {{T012_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T012_REFERENCE_1}}`
  - **References**: `{{T012_REFERENCE_2}}`
- [ ] {{T013_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T013_REFERENCE_1}}`
  - **References**: `{{T013_REFERENCE_2}}`
- [ ] {{T014_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T014_REFERENCE_1}}`
  - **References**: `{{T014_REFERENCE_2}}`

**Checkpoint**: {{USER_STORY_1_CHECKPOINT}}

---

## Phase 4: User Story 2 - {{USER_STORY_2_TITLE}}（Priority: {{USER_STORY_2_PRIORITY}}）

**Goal**: {{USER_STORY_2_GOAL}}

**Independent Test**: {{USER_STORY_2_INDEPENDENT_TEST}}

### {{USER_STORY_2_BACKEND_HEADING}}

**Codebase**: `{{USER_STORY_2_BACKEND_CODEBASE}}`

- [ ] {{T015_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T015_REFERENCE_1}}`
  - **References**: `{{T015_REFERENCE_2}}`
- [ ] {{T016_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T016_REFERENCE_1}}`
  - **References**: `{{T016_REFERENCE_2}}`
- [ ] {{T017_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T017_REFERENCE_1}}`
  - **References**: `{{T017_REFERENCE_2}}`

### {{USER_STORY_2_FRONTEND_HEADING}}

**Codebase**: `{{USER_STORY_2_FRONTEND_CODEBASE}}`

- [ ] {{T018_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T018_REFERENCE_1}}`
  - **References**: `{{T018_REFERENCE_2}}`
- [ ] {{T019_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T019_REFERENCE_1}}`
  - **References**: `{{T019_REFERENCE_2}}`
- [ ] {{T020_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T020_REFERENCE_1}}`
  - **References**: `{{T020_REFERENCE_2}}`

**Checkpoint**: {{USER_STORY_2_CHECKPOINT}}

---

## Phase 5: 跨故事 - {{CROSS_STORY_TITLE}}

**Purpose**: {{CROSS_STORY_PURPOSE}}

### {{CROSS_STORY_BACKEND_HEADING}}

**Codebase**: `{{CROSS_STORY_BACKEND_CODEBASE}}`

- [ ] {{T021_TASK}}
  - **TDD 步驟**: 紅燈
  - **References**: `{{T021_REFERENCE_1}}`
  - **References**: `{{T021_REFERENCE_2}}`
- [ ] {{T022_TASK}}
  - **TDD 步驟**: 綠燈
  - **References**: `{{T022_REFERENCE_1}}`
  - **References**: `{{T022_REFERENCE_2}}`
- [ ] {{T023_TASK}}
  - **TDD 步驟**: 重構
  - **References**: `{{T023_REFERENCE_1}}`
  - **References**: `{{T023_REFERENCE_2}}`

**Checkpoint**: {{CROSS_STORY_CHECKPOINT}}

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 無前置，可立即開始
- **Foundational (Phase 2)**: 依賴 Setup；完成前阻擋全部使用者故事
- **User Stories (Phase 3+)**: 都依賴 Foundational
- **跨故事 (Phase 5)**: {{CROSS_STORY_DEPENDENCY}}

### User Story Dependencies

- **User Story 1 ({{USER_STORY_1_PRIORITY}})**: {{USER_STORY_1_DEPENDENCY}}
- **User Story 2 ({{USER_STORY_2_PRIORITY}})**: {{USER_STORY_2_DEPENDENCY}}

### Within Each User Story

- 每個案例的順序是紅燈、綠燈、重構
- 綠燈只滿足該案例的預期輸出，不提前實作下一個案例
- 重構只整理該案例綠燈觸及的實作
- 執行某個任務時只讀該任務列出的位址

### Parallel Opportunities

- {{PARALLEL_OPPORTUNITIES}}

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. 完成 Phase 1: Setup
2. 完成 Phase 2: Foundational（阻擋所有故事）
3. 完成 Phase 3: User Story 1
4. **STOP and VALIDATE**: {{MVP_VALIDATION}}
5. {{MVP_NEXT}}

### Incremental Delivery

1. Setup + Foundational → 基礎可用
2. {{INCREMENTAL_USER_STORY_1}}
3. {{INCREMENTAL_USER_STORY_2}}
4. {{INCREMENTAL_CROSS_STORY}}

---

## Notes

- {{NOTES_STORY_LABELS}}
- 每個開發任務的 **TDD 步驟** 是紅燈、綠燈、重構三者之一
- 紅燈任務以該案例作為已確認接縫，從撰寫失敗測試開始
- 重構任務的完成包含不調整結構，並確認該案例測試仍通過
- {{NOTES_EXCLUDED_REQUIREMENT}}
