---
name: artifact-to-skill-engineering
description: 從已確認滿意的 Artifact Example 反推出可穩定產出該 Artifact 的目標 Skill，並編排 skill-form-template 與 skill-engineering 完成最小必要工程。
---

# SOP

## Phase 1: 取得目標與參考 Artifact

1. Read 讀取使用者輸入並取得目標 Skill 名稱、參考 Artifact Example 來源、預期輸入 Prompt 類型與客製化意圖。
2. Read [Artifact-to-Skill 工程規範](rules/artifact-to-skill工程規範.md)並取得參考 Artifact、客製化確認、Template 倒抽與 Skill Engineering 交付要求。
3. Think 依已載入規範決定本次要工程化的目標 Artifact 類型、目標 Skill 邊界與仍缺少的必要輸入。

## Phase 2: 客製化與確認 Artifact Example

1. Think 依已載入規範比較參考 Artifact Example 與使用者客製化意圖，決定需要修改的 Artifact 內容範圍。
2. Write 依使用者客製化需求修改目標 Artifact Example。
3. Think 依已載入規範判斷使用者是否已明確確認 Artifact Example 滿意。
4. Write 當使用者尚未確認 Artifact Example 滿意時，將需要確認或繼續調整的內容寫入回覆 Artifact。

## Phase 3: 倒抽 Template

1. Delegate 當使用者已確認 Artifact Example 滿意時，交給 `skill-form-template` 依該 Artifact Example 建立或更新成對 Template。
2. Read 讀取已產出的 Template 骨架與 Template 範例，取得目標 Artifact 的固定結構與範例對應關係。
3. Think 依已載入規範判斷 Template 是否足以作為目標 Skill 的可靠產物契約。

## Phase 4: 編排 Skill Engineering

1. Think 依已載入規範整理目標 Skill 的用途、觸發條件、輸入 Prompt 類型、目標 Artifact Template、可靠度要求與工程邊界。
2. Delegate 交給 `skill-engineering` 依已整理的目標建立或優化目標 Skill。

## Phase 5: 檢查整體結果

1. Read 讀取目標 Skill 的 `SKILL.md`、`rules/`、`templates/` 與 `scripts/`，取得 SOP、模組使用關係與產物結構。
2. Think 依已載入規範判斷目標 Skill 是否能由預期輸入 Prompt 可靠產出已確認的 Artifact Template。
3. Write 修正目標 Skill 中未被 SOP 載入、委派或不符合已載入規範的孤兒模組與過度工程問題。
