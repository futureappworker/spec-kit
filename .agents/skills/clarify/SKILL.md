---
name: clarify
description: 針對既有 Feature Specification 的核心不確定處產生澄清問題，或將使用者回答回寫到 spec，使規格可進入後續 planning。
---

# SOP

## Phase 1: 讀取規格與輸入

1. Read 讀取使用者輸入並取得目標 Feature Specification 位置、澄清意圖與使用者提供的回答。
2. Read 讀取目標 Feature Specification 並取得 Feature metadata、Clarifications、User Stories、Requirements、Edge Cases、Success Criteria 與 Assumptions。

## Phase 2: 判斷澄清模式

1. Read [Clarification 品質規範](rules/clarification品質規範.md)並取得提問、套用答案、同步更新與完成判定要求。
2. Think 依已載入規範決定本次執行為提問模式或套用模式。

## Phase 3: 產生澄清問題

1. Think 當本次執行為提問模式時，依已載入規範決定最多三個核心澄清缺口與排序。
2. Read 當本次執行為提問模式時，讀取 [Clarification Question 骨架](templates/clarification-question.md)並取得固定內容結構。
3. Read 當本次執行為提問模式時，讀取 [Clarification Question 範例](templates/clarification-question.example.md)並取得完整使用方式。
4. Write 當本次執行為提問模式時，依已載入規範、樣板與範例將澄清問題與選項寫入回覆 Artifact。

## Phase 4: 套用澄清答案

1. Think 當本次執行為套用模式時，依已載入規範決定每個回答影響的 spec 章節。
2. Write 當本次執行為套用模式時，將澄清答案、受影響章節與規格狀態寫入目標 Feature Specification。

## Phase 5: 檢查規格一致性

1. Read 依已載入規範檢查目標 Feature Specification 是否仍有未處理核心缺口、矛盾需求、過時 Assumptions 或不同步章節。

## Phase 6: 修正規格一致性

1. Write 修正目標 Feature Specification 中全部不符合已載入規範的澄清、一致性與狀態問題。
