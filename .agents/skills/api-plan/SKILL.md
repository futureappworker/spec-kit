---
name: api-plan
description: 分析後端端點、API、WebSocket、服務狀態機與權威判定邊界，產出可供前端與資料規劃對齊的 OpenAPI 介面分析。
---

# SOP

## Phase 1: 讀取介面分析輸入

1. Read 讀取使用者輸入或上游委派內容並取得系統介面名稱、端點類型、需求依據、介面定位、所在 Wave、上游分析結果與目標輸出位置。
2. Think 判斷輸入資訊是否足以分析後端入口、服務責任與狀態轉換邊界。
3. Delegate `clarify` 當缺少會影響 API 介面邊界的核心資訊時產生澄清問題。
4. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 2: 推導 API 介面分析

1. Think 從需求依據與上游結果推導後端入口、請求事件、回應資料、推送事件、錯誤回應與權限判定。
2. Think 推導服務狀態機、業務不變量、同步一致性、重試或重連語意，取得後端執行邊界。
3. Think 推導後端需要讀取、寫入或鎖定的資料，取得對資料端點的需求輸入。

## Phase 3: 撰寫 API 介面分析

1. Read [OpenAPI 骨架](templates/openapi.yaml)並取得固定內容結構。
2. Read [OpenAPI 範例](templates/openapi.example.yaml)並取得完整使用方式。
3. Write 依已載入樣板與範例將 API 介面分析寫入目標 OpenAPI 檔案。

## Phase 4: 檢查 API 介面分析

1. Read 檢查 API 介面分析是否保留需求追溯、涵蓋入口事件、回應或推送資料、服務判定、狀態轉換、資料依賴與待澄清缺口。

## Phase 5: 修正 API 介面分析

1. Write 修正 API 介面分析中可由既有資訊處理的全部不符合項目。
