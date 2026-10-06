---
name: specify
description: 將使用者的 Feature Prompt 轉換為可進入 planning 的 Feature Specification；當核心需求不明確時，先產生可澄清的 spec 初稿並轉交 clarify。
---

# SOP

## Phase 1: 讀取輸入與樣板

1. Read 讀取使用者輸入並取得原始 Feature Prompt、目標輸出意圖與已提供的澄清答案。
2. Read [規格輸出位置規範](rules/規格輸出位置規範.md)並取得目標路徑、檔名與寫入狀態要求。
3. Read [Spec Template 骨架](templates/spec.md)並取得 Feature Specification 的固定輸出結構。
4. Read [Spec Template 範例](templates/spec.example.md)並取得完整 Artifact 的填寫方式。
5. Think 依已載入規範決定目標 Feature Specification 路徑與本次輸出模式。

## Phase 2: 推導規格內容

1. Read [Spec 推導品質規範](rules/spec推導品質規範.md)並取得需求抽取、User Story 分群、FR/NFR 歸屬、全域需求與澄清轉交要求。
2. Think 依已載入規範從使用者輸入抽取明確需求、限制條件、資料物件、互動行為、未知點與可成立假設。
3. Think 依已載入規範決定 User Stories、Acceptance Scenarios、Functional Requirements、Non-Functional Requirements、Global Requirements、Edge Cases、Key Entities、Success Criteria 與 Assumptions。

## Phase 3: 判斷澄清需求

1. Think 依已載入規範判斷是否存在會影響核心規格的未回答缺口。
2. Write 當存在核心缺口時，依已載入樣板將可由明確資訊產生的內容寫入目標 Feature Specification，並將 Status 設為 `Needs Clarification`。
3. Delegate 當存在核心缺口時，交給 `clarify` 針對目標 Feature Specification 產生澄清問題。
4. Think 當已轉交 `clarify` 時，決定本次 `specify` 流程停止於澄清問題產出。

## Phase 4: 撰寫完整規格

1. Write 當不存在核心缺口或使用者答案已套用時，依已載入樣板將完整 Feature Specification 寫入目標檔案。

## Phase 5: 產生 Requirements Checklist

1. Read [Requirements Checklist 品質規範](rules/requirements-checklist品質規範.md)並取得獨立 Artifact 路徑、逐項驗證與修正閉環要求。
2. Think 決定目標 Requirements Checklist 路徑與本次 checklist 建立模式。
3. Read [Requirements Checklist 骨架](templates/requirements-checklist.md)並取得固定內容結構。
4. Read [Requirements Checklist 範例](templates/requirements-checklist.example.md)並取得完整使用方式。
5. Write 依已載入樣板與範例將 Requirements Checklist 寫入目標 Feature Specification 所屬 feature 目錄。

## Phase 6: 檢查規格與 Checklist 一致性

1. Read 依已載入規範檢查目標 Feature Specification 是否存在捏造澄清、需求錯誤歸屬、未處理核心缺口、矛盾需求、過時 Assumptions 或樣板結構偏離。
2. Read 依已載入規範逐項驗證目標 Requirements Checklist 並列出未通過項目。

## Phase 7: 修正規格並更新 Checklist

1. Write 修正目標 Feature Specification 中可由既有資訊處理的全部不符合已載入規範與樣板結構的問題。
2. Write 更新目標 Requirements Checklist 中各項通過狀態與 Notes。
