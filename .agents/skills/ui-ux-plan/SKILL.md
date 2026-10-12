---
name: ui-ux-plan
description: 分析前端端點、瀏覽器互動、畫面狀態與使用者流程，產出可供 API 與資料規劃對齊的 Pencil UI/UX 介面分析。
---

# SOP

## Phase 1: 讀取介面分析輸入

1. Read 讀取使用者輸入或上游委派內容並取得系統介面名稱、端點類型、需求依據、介面定位、所在 Wave、上游分析結果與目標輸出位置。
2. Think 判斷輸入資訊是否足以分析前端互動邊界、畫面狀態與使用者流程。
3. Delegate `clarify` 當缺少會影響 UI/UX 介面邊界的核心資訊時產生澄清問題。
4. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 2: 推導 UI/UX 介面分析

1. Think 從需求依據推導使用者流程、主要畫面、畫面狀態、使用者操作、系統回饋與錯誤狀態。
2. Think 推導前端需要讀取、提交、訂閱或暫存的資料，取得對 API 與資料端點的需求輸入。
3. Think 推導可用性、裝置限制、狀態一致性與資訊揭露限制，取得前端介面風險與後續依賴。

## Phase 3: 撰寫 UI/UX 介面分析

1. Read [Pencil 骨架](templates/interface.pen)並取得固定內容結構。
2. Read [Pencil 範例](templates/interface.example.pen)並取得完整使用方式。
3. Write 依已載入樣板與範例將 UI/UX 介面分析寫入目標 Pencil 檔案。

## Phase 4: 檢查 UI/UX 介面分析

1. Read 檢查 UI/UX 介面分析是否保留需求追溯、涵蓋使用者流程、畫面狀態、操作回饋、資料交換需求與待澄清缺口。

## Phase 5: 修正 UI/UX 介面分析

1. Write 修正 UI/UX 介面分析中可由既有資訊處理的全部不符合項目。
