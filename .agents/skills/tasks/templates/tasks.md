---

description: "{{TASKS_DESCRIPTION}}"
---

# Tasks: {{FEATURE_NAME}}

**Input**: Design documents from `{{SPEC_DIRECTORY}}`

**Prerequisites**: 本清單已對齊 plan.md（必要）與 spec.md（必要）。執行時由上往下，不要在開工時讀完 research.md、techstack.md 與 contracts/。每個任務下方的 **References** 才是載入時機，而且只讀該位址，不讀同一份文件的其他部位。路徑相對於 `{{SPEC_DIRECTORY}}`。{{MISSING_DESIGN_DOCS}}

**Tests**: {{TESTS_POLICY}}

**Organization**: 任務依使用者故事分階段，使每則故事可獨立實作與驗證。Phase 3 起的每個使用者故事，以及 Phase 6，都用第三層標題依 plan.md「系統介面盤點」切開端點。每則使用者故事都包含{{ENDPOINT_SECTION_NAMES}}。任務落在該端點的程式庫；啟動文件放在 Phase 6 的環境小節。契約部位掛在每個任務上，只指向該端點的那一處。

## Format: `[ID] [P?] [Story] Description`

- **[P]**: 可平行（不同檔案、不依賴同階段尚未完成的任務）
- **[Story]**: 該任務所屬使用者故事（{{STORY_LABELS}}）
- 描述含精確檔案路徑
- {{ENDPOINT_SECTION_ORDER}}
- **References** 寫在任務正下方，一行一個位址。只列本端點文件裡、這個任務直接實作或斷言的部位。後端任務不寫 DBML 或畫面，資料庫任務不寫 OpenAPI 或畫面，前端畫面任務不寫 OpenAPI 或 DBML
- {{REFERENCE_ADDRESS_GRAMMAR}}

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
- [ ] {{T004_TASK}}
  - **References**: `{{T004_REFERENCE_1}}`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: {{PHASE_2_PURPOSE}}

**⚠️ CRITICAL**: 本階段完成前不得開始任何使用者故事

- [ ] {{T005_TASK}}
  - **References**: `{{T005_REFERENCE_1}}`
- [ ] {{T006_TASK}}
  - **References**: `{{T006_REFERENCE_1}}`
  - **References**: `{{T006_REFERENCE_2}}`
  - **References**: `{{T006_REFERENCE_3}}`
  - **References**: `{{T006_REFERENCE_4}}`
  - **References**: `{{T006_REFERENCE_5}}`
  - **References**: `{{T006_REFERENCE_6}}`
- [ ] {{T007_TASK}}
  - **References**: `{{T007_REFERENCE_1}}`
- [ ] {{T008_TASK}}
  - **References**: `{{T008_REFERENCE_1}}`
  - **References**: `{{T008_REFERENCE_2}}`
  - **References**: `{{T008_REFERENCE_3}}`
- [ ] {{T009_TASK}}
  - **References**: `{{T009_REFERENCE_1}}`
  - **References**: `{{T009_REFERENCE_2}}`
- [ ] {{T010_TASK}}
  - **References**: `{{T010_REFERENCE_1}}`
- [ ] {{T011_TASK}}
  - **References**: `{{T011_REFERENCE_1}}`
  - **References**: `{{T011_REFERENCE_2}}`
- [ ] {{T012_TASK}}
  - **References**: `{{T012_REFERENCE_1}}`
- [ ] {{T013_TASK}}
  - **References**: `{{T013_REFERENCE_1}}`
- [ ] {{T014_TASK}}
  - **References**: `{{T014_REFERENCE_1}}`
- [ ] {{T015_TASK}}
  - **References**: `{{T015_REFERENCE_1}}`
- [ ] {{T016_TASK}}
  - **References**: `{{T016_REFERENCE_1}}`

**Checkpoint**: {{PHASE_2_CHECKPOINT}}

---

## Phase 3: User Story 1 - {{USER_STORY_1_TITLE}}（Priority: {{USER_STORY_1_PRIORITY}}）

**Goal**: {{USER_STORY_1_GOAL}}

**Independent Test**: {{USER_STORY_1_INDEPENDENT_TEST}}

### {{USER_STORY_1_BACKEND_HEADING}}

**Codebase**: `{{USER_STORY_1_BACKEND_CODEBASE}}`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] {{T017_TASK}}
  - **References**: `{{T017_REFERENCE_1}}`
- [ ] {{T018_TASK}}
  - **References**: `{{T018_REFERENCE_1}}`

**Implementation**:

- [ ] {{T019_TASK}}
  - **References**: `{{T019_REFERENCE_1}}`
- [ ] {{T020_TASK}}
  - **References**: `{{T020_REFERENCE_1}}`
- [ ] {{T021_TASK}}
  - **References**: `{{T021_REFERENCE_1}}`
- [ ] {{T022_TASK}}
  - **References**: `{{T022_REFERENCE_1}}`

### {{USER_STORY_1_DATABASE_HEADING}}

**Codebase**: `{{USER_STORY_1_DATABASE_CODEBASE}}`

**Implementation**:

- [ ] {{T023_TASK}}
  - **References**: `{{T023_REFERENCE_1}}`
  - **References**: `{{T023_REFERENCE_2}}`

### {{USER_STORY_1_FRONTEND_HEADING}}

**Codebase**: `{{USER_STORY_1_FRONTEND_CODEBASE}}`

**Implementation**:

- [ ] {{T024_TASK}}
  - **References**: `{{T024_REFERENCE_1}}`
- [ ] {{T025_TASK}}
  - **References**: `{{T025_REFERENCE_1}}`

**Checkpoint**: {{USER_STORY_1_CHECKPOINT}}

---

## Phase 4: User Story 2 - {{USER_STORY_2_TITLE}}（Priority: {{USER_STORY_2_PRIORITY}}）

**Goal**: {{USER_STORY_2_GOAL}}

**Independent Test**: {{USER_STORY_2_INDEPENDENT_TEST}}

### {{USER_STORY_2_BACKEND_HEADING}}

**Codebase**: `{{USER_STORY_2_BACKEND_CODEBASE}}`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] {{T026_TASK}}
  - **References**: `{{T026_REFERENCE_1}}`
- [ ] {{T027_TASK}}
  - **References**: `{{T027_REFERENCE_1}}`

**Implementation**:

- [ ] {{T028_TASK}}
  - **References**: `{{T028_REFERENCE_1}}`
- [ ] {{T029_TASK}}
  - **References**: `{{T029_REFERENCE_1}}`
- [ ] {{T030_TASK}}
  - **References**: `{{T030_REFERENCE_1}}`
  - **References**: `{{T030_REFERENCE_2}}`
- [ ] {{T031_TASK}}
  - **References**: `{{T031_REFERENCE_1}}`

### {{USER_STORY_2_DATABASE_HEADING}}

**Codebase**: `{{USER_STORY_2_DATABASE_CODEBASE}}`

**Implementation**:

- [ ] {{T032_TASK}}
  - **References**: `{{T032_REFERENCE_1}}`
  - **References**: `{{T032_REFERENCE_2}}`

### {{USER_STORY_2_FRONTEND_HEADING}}

**Codebase**: `{{USER_STORY_2_FRONTEND_CODEBASE}}`

**Implementation**:

- [ ] {{T033_TASK}}
  - **References**: `{{T033_REFERENCE_1}}`
- [ ] {{T034_TASK}}
  - **References**: `{{T034_REFERENCE_1}}`
- [ ] {{T035_TASK}}
  - **References**: `{{T035_REFERENCE_1}}`

**Checkpoint**: {{USER_STORY_2_CHECKPOINT}}

---

## Phase 5: User Story 3 - {{USER_STORY_3_TITLE}}（Priority: {{USER_STORY_3_PRIORITY}}）

**Goal**: {{USER_STORY_3_GOAL}}

**Independent Test**: {{USER_STORY_3_INDEPENDENT_TEST}}

### {{USER_STORY_3_BACKEND_HEADING}}

**Codebase**: `{{USER_STORY_3_BACKEND_CODEBASE}}`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] {{T036_TASK}}
  - **References**: `{{T036_REFERENCE_1}}`
  - **References**: `{{T036_REFERENCE_2}}`

**Implementation**:

- [ ] {{T037_TASK}}
  - **References**: `{{T037_REFERENCE_1}}`
- [ ] {{T038_TASK}}
  - **References**: `{{T038_REFERENCE_1}}`
- [ ] {{T039_TASK}}
  - **References**: `{{T039_REFERENCE_1}}`
- [ ] {{T040_TASK}}
  - **References**: `{{T040_REFERENCE_1}}`
- [ ] {{T041_TASK}}
  - **References**: `{{T041_REFERENCE_1}}`
- [ ] {{T042_TASK}}
  - **References**: `{{T042_REFERENCE_1}}`
  - **References**: `{{T042_REFERENCE_2}}`

### {{USER_STORY_3_DATABASE_HEADING}}

**Codebase**: `{{USER_STORY_3_DATABASE_CODEBASE}}`

**Implementation**:

- [ ] {{T043_TASK}}
  - **References**: `{{T043_REFERENCE_1}}`
  - **References**: `{{T043_REFERENCE_2}}`
  - **References**: `{{T043_REFERENCE_3}}`

### {{USER_STORY_3_FRONTEND_HEADING}}

**Codebase**: `{{USER_STORY_3_FRONTEND_CODEBASE}}`

**Implementation**:

- [ ] {{T044_TASK}}
  - **References**: `{{T044_REFERENCE_1}}`
- [ ] {{T045_TASK}}
  - **References**: `{{T045_REFERENCE_1}}`
  - **References**: `{{T045_REFERENCE_2}}`

**Checkpoint**: {{USER_STORY_3_CHECKPOINT}}

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: {{PHASE_6_PURPOSE}}

### {{PHASE_6_BACKEND_HEADING}}

**Codebase**: `{{PHASE_6_BACKEND_CODEBASE}}`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] {{T046_TASK}}
  - **References**: `{{T046_REFERENCE_1}}`
- [ ] {{T047_TASK}}
  - **References**: `{{T047_REFERENCE_1}}`

**Implementation**:

- [ ] {{T048_TASK}}
  - **References**: `{{T048_REFERENCE_1}}`
- [ ] {{T049_TASK}}
  - **References**: `{{T049_REFERENCE_1}}`

### {{PHASE_6_DATABASE_HEADING}}

**Codebase**: `{{PHASE_6_DATABASE_CODEBASE}}`

**Implementation**:

- [ ] {{T050_TASK}}
  - **References**: `{{T050_REFERENCE_1}}`
  - **References**: `{{T050_REFERENCE_2}}`

### {{PHASE_6_FRONTEND_HEADING}}

**Codebase**: `{{PHASE_6_FRONTEND_CODEBASE}}`

**Implementation**:

- [ ] {{T051_TASK}}
  - **References**: `{{T051_REFERENCE_1}}`
- [ ] {{T052_TASK}}
  - **References**: `{{T052_REFERENCE_1}}`
  - **References**: `{{T052_REFERENCE_2}}`
  - **References**: `{{T052_REFERENCE_3}}`
  - **References**: `{{T052_REFERENCE_4}}`
  - **References**: `{{T052_REFERENCE_5}}`
- [ ] {{T053_TASK}}
  - **References**: `{{T053_REFERENCE_1}}`

### {{PHASE_6_ENVIRONMENT_HEADING}}

**Codebase**: `{{PHASE_6_ENVIRONMENT_CODEBASE}}`

- [ ] {{T054_TASK}}
  - **References**: `{{T054_REFERENCE_1}}`

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 無前置，可立即開始
- **Foundational (Phase 2)**: 依賴 Setup；完成前阻擋全部使用者故事
- **User Stories (Phase 3+)**: 都依賴 Foundational
  - {{STORY_INDEPENDENT_VALIDATION}}
  - {{SHARED_FILE_ORDER}}
- **Polish (Phase 6)**: 依賴希望交付的使用者故事都完成

### User Story Dependencies

- **User Story 1 ({{USER_STORY_1_PRIORITY}})**: {{USER_STORY_1_DEPENDENCY}}
- **User Story 2 ({{USER_STORY_2_PRIORITY}})**: {{USER_STORY_2_DEPENDENCY}}
- **User Story 3 ({{USER_STORY_3_PRIORITY}})**: {{USER_STORY_3_DEPENDENCY}}

### Within Each User Story

- 該故事的測試寫在擁有該行為的端點小節裡，先寫並失敗，再實作該端與後續端點
- {{WITHIN_STORY_ORDER_PURE_FUNCTIONS}}
- {{WITHIN_STORY_ORDER_STATE_MACHINE}}
- {{WITHIN_STORY_ORDER_FRONTEND}}
- 執行某個任務時只讀該任務列出的位址，不讀同一份文件裡沒被點名的 schema、資料表或畫面

### Parallel Opportunities

- {{PARALLEL_SETUP}}
- {{PARALLEL_FOUNDATIONAL}}
- {{PARALLEL_USER_STORY_1}}
- {{PARALLEL_USER_STORY_2}}
- {{PARALLEL_USER_STORY_3}}
- {{PARALLEL_POLISH}}

---

## Parallel Example: User Story 1

```bash
# {{PARALLEL_EXAMPLE_USER_STORY_1_COMMENT_1}}
Task: "{{PARALLEL_EXAMPLE_USER_STORY_1_TASK_1}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_1_TASK_2}}"

# {{PARALLEL_EXAMPLE_USER_STORY_1_COMMENT_2}}
Task: "{{PARALLEL_EXAMPLE_USER_STORY_1_TASK_3}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_1_TASK_4}}"
```

## Parallel Example: User Story 2

```bash
Task: "{{PARALLEL_EXAMPLE_USER_STORY_2_TASK_1}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_2_TASK_2}}"

Task: "{{PARALLEL_EXAMPLE_USER_STORY_2_TASK_3}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_2_TASK_4}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_2_TASK_5}}"
```

## Parallel Example: User Story 3

```bash
Task: "{{PARALLEL_EXAMPLE_USER_STORY_3_TASK_1}}"
Task: "{{PARALLEL_EXAMPLE_USER_STORY_3_TASK_2}}"
```

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
4. {{INCREMENTAL_USER_STORY_3}}
5. {{INCREMENTAL_POLISH}}

### Parallel Team Strategy

多人時仍先一起完成 Setup + Foundational。之後：

- {{PARALLEL_TEAM_INDEPENDENT_FILES}}
- {{PARALLEL_TEAM_SHARED_FILES}}

---

## Notes

- [P] 代表不同檔案且不依賴尚未完成的任務
- {{NOTES_STORY_LABELS}}
- {{NOTES_DOMAIN_RULES}}
- {{NOTES_TURN_RULE}}
- {{NOTES_DEPLOYMENT_LIMIT}}
- 每個故事的檢查點都應能單獨停下來驗證
