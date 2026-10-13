---
name: tasks
description: 將 Feature Specification 與 plan.md 的系統介面盤點轉成可由上往下執行的 tasks.md；每個任務只掛本端點契約的一個部位。
metadata:
  references:
    - project: GitHub Spec Kit
      url: https://github.com/github/spec-kit
      source: templates/commands/tasks.md
      license: MIT
      copyright: Copyright GitHub, Inc.
---

本 Skill 參考並改寫自 [GitHub Spec Kit](https://github.com/github/spec-kit) 的 [`templates/commands/tasks.md`](https://github.com/github/spec-kit/blob/main/templates/commands/tasks.md)。該原始碼以 MIT License 授權，Copyright GitHub, Inc.。完整授權聲明見 [NOTICE](NOTICE)。

# SOP

## Phase 1: 讀取輸入

1. Read 讀取使用者輸入並取得目標功能目錄、既有 tasks.md 與本次是建立或更新。
2. Think 決定任務清單路徑為該功能 `plan.md` 所在目錄的 `tasks.md`。

## Phase 2: 對齊故事與端點

1. Read 讀取目標功能的 `spec.md` 並取得使用者故事、優先級與可測試行為。
2. Read 讀取目標功能的 `plan.md` 並取得系統介面盤點、產出契約與原始碼落地位置。
3. Read 讀取目標功能的 `techstack.md` 採用技術表並取得 Setup 與環境任務要引用的 Area。
4. Read 讀取 plan.md「產出契約」列出的契約檔並取得 schema 名稱、Table 名稱與 frame id。
5. Read [任務清單輸出規範](rules/任務清單輸出規範.md)並取得輸出位置、端點層級、任務位址與測試順序要求。
6. Think 依已載入規範決定每則使用者故事的端點落點，以及每個任務要掛的單一契約部位。

## Phase 3: 撰寫任務清單

1. Read [Tasks 骨架](templates/tasks.md)並取得任務清單的固定欄位與階段結構。
2. Read [Tasks 範例](templates/tasks.example.md)並取得已確認任務清單的填寫方式。
3. Read [產出覆蓋規範](../constitution/rules/產出覆蓋規範.md)並取得憲法讀取時機、點名部位優先順序與停止寫入條件。
4. Read 若存在，讀取 `constitution/共同/憲法套用規範.md`，取得專案套用規則；檔案不存在時，專案套用規則為空。
5. Read 若存在，讀取 `constitution/tasks/tasks.md`，取得 `tasks.md` 的憲法 Rule；檔案不存在時，憲法 Rule 為空。
6. Think 依已載入規範決定本次是否停止寫入 `tasks.md`。
7. Write 當決定停止寫入時，將拒絕原因寫入回覆。
8. Think 當決定停止寫入時，決定本次流程停止於拒絕原因。
9. Write 當決定寫入時，依已載入規範、樣板與已載入的憲法 Rule，將任務清單寫入 Phase 1 決定的 `tasks.md`。

## Phase 4: 檢查任務清單

1. Read 依已載入規範與已載入的憲法 Rule 檢查目標 `tasks.md` 是否照抄範例任務、缺少端點層級、任務沒有部位位址、位址跨端、測試排在實作之後或憲法未通過，並列出不符合項目。

## Phase 5: 修正任務清單

1. Write 修正目標 `tasks.md` 中全部不符合已載入規範、樣板結構與已載入的憲法 Rule 的項目。
