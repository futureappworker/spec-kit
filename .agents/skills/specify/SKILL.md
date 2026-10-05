---
name: specify
description: 將使用者的自然語言產品需求推導成結構完整、可驗證的 Feature Specification，並寫入 specs/xxx/spec.md。Use when the user asks to specify a feature, turn an idea into a spec, or produce a feature specification from a prompt.
---

# SOP

## Phase 1: 讀取需求與樣板

1. Read 讀取使用者輸入並取得原始需求文字與可用輸出位置。
2. Read [規格輸出位置規範](rules/規格輸出位置規範.md)並取得預設檔案路徑與編號要求。
3. Think 依已載入規範決定本次 Feature Specification 的輸出檔案路徑。
4. Read [Spec 骨架](templates/spec.md)並取得目標 Artifact 的固定結構。
5. Read [Spec 範例](templates/spec.example.md)並取得完整填寫後的參考品質。

## Phase 2: 抽取需求事實

1. Read [Spec 推導品質規範](rules/spec推導品質規範.md)並取得需求抽取、澄清、分類與檢查要求。
2. Think 依已載入規範從原始需求文字建立需求事實清單。
3. Think 依已載入規範決定需要澄清的核心缺口與可記入假設的非阻塞前提。

## Phase 3: 建立規格內容

1. Think 依已載入規範決定 Feature metadata、Status 與 Clarifications 內容。
2. Think 依已載入規範拆分 User Stories 並決定每個 Story 的優先級、價值理由與獨立測試。
3. Think 依已載入規範為每個 User Story 建立 Acceptance Criteria。
4. Think 依已載入規範將需求分類為 Functional Requirements、Non-Functional Requirements、Global Requirements 與 Key Entities。
5. Think 依已載入規範建立 Edge Cases、Success Criteria 與 Assumptions。

## Phase 4: 產出規格 Artifact

1. Write 依已載入樣板、範例與規範將完整 Feature Specification 寫入已決定的輸出檔案路徑。

## Phase 5: 檢查規格 Artifact

1. Read 依已載入規範檢查已寫入的 Feature Specification 檔案並列出不符合項目。

## Phase 6: 修正規格 Artifact

1. Write 修正已決定輸出檔案中的全部不符合項目。

## Phase 7: 銜接澄清流程

1. Delegate `clarify` 當 Feature Specification 的 Status 為 `Needs Clarification` 時，交付已寫入的規格檔案路徑進行提問模式。
2. 當使用者提供澄清答案時，Delegate `clarify` 套用答案並回寫同一規格檔案。

## Phase 8: 完成並停止

1. Think 確認 Feature Specification 已寫入 `specs/<NNN>-<feature-slug>/spec.md`（或使用者指定路徑），且 Status 為 `Ready for Planning` 或仍待澄清。
2. 回覆僅報告輸出檔案路徑與 Status；若 Status 為 `Needs Clarification`，回覆澄清問題並等待使用者回答。
3. 完成後直接停止，不得建議或委派後續流程（如 planning、開發或其他 Skill）。
