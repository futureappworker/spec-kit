---
name: data-plan
description: 分析資料庫端點、持久化模型、查詢、快照與資料保留邊界，產出可供前端與 API 規劃對齊的 DBML 資料介面分析。
metadata:
  references:
    - project: GitHub Spec Kit
      url: https://github.com/github/spec-kit
      source: templates/commands/plan.md
      scope: Phase 1 data-model.md
      license: MIT
      copyright: Copyright GitHub, Inc.
---

本 Skill 參考並改寫自 [GitHub Spec Kit](https://github.com/github/spec-kit) 的 [`templates/commands/plan.md`](https://github.com/github/spec-kit/blob/main/templates/commands/plan.md)（Phase 1 data-model.md）。該原始碼以 MIT License 授權，Copyright GitHub, Inc.。完整授權聲明見 [NOTICE](NOTICE)。

# SOP

## Phase 1: 讀取介面分析輸入

1. Read 讀取使用者輸入或上游委派內容並取得系統介面名稱、端點類型、需求依據、介面定位、所在 Wave、上游分析結果與目標輸出位置。
2. Think 判斷輸入資訊是否足以分析資料模型、持久化責任與查詢邊界。
3. Delegate `clarify` 當缺少會影響資料介面邊界的核心資訊時產生澄清問題。
4. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 2: 推導資料介面分析

1. Think 從需求依據與上游結果推導核心實體、資料關係、唯一性、生命週期與保存責任。
2. Think 推導寫入時機、讀取查詢、更新規則、快照需求、重建狀態方式與資料保留限制。
3. Think 推導資料一致性、隱私或揭露限制、遷移風險與 API 端需要遵守的資料不變量。

## Phase 3: 撰寫資料介面分析

1. Read [DBML 骨架](templates/schema.dbml)並取得固定內容結構。
2. Read [DBML 範例](templates/schema.example.dbml)並取得完整使用方式。
3. Write 依已載入樣板與範例將資料介面分析寫入目標 DBML 檔案。

## Phase 4: 檢查資料介面分析

1. Read 檢查資料介面分析是否保留需求追溯、涵蓋實體關係、寫入時機、查詢需求、生命週期、不變量與待澄清缺口。

## Phase 5: 修正資料介面分析

1. Write 修正資料介面分析中可由既有資訊處理的全部不符合項目。
