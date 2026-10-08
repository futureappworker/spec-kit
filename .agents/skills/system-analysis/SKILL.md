---
name: system-analysis
description: 依使用者需求或 Feature Specification 產出 plan.md 中的系統分析規劃，先盤點需求涉及的技術端點與系統介面，再用 Wave 安排可平行委派的介面分析流程。
---

# SOP

## Phase 1: 讀取輸入與樣板

1. Read 讀取使用者輸入並取得需求來源、目標 `plan.md` 路徑、已知專案結構與技術偏好。
2. Read [系統分析規劃規範](rules/系統分析規劃規範.md)並取得系統介面盤點、端點類型與 Wave 排程要求。
3. Read [Plan Template 骨架](templates/plan.md)並取得系統分析規劃的固定輸出結構。
4. Read [Plan Template 範例](templates/plan.example.md)並取得完整 Artifact 的填寫方式。
5. Think 決定本次可用需求來源、目標輸出路徑與資訊是否足以產出系統分析規劃。
6. Write 當缺少必要需求來源或目標輸出路徑時，將缺少資訊清單與確認問題寫入回覆並停止。

## Phase 2: 讀取需求與專案結構

1. Read 讀取目標需求來源檔案或使用者輸入，取得需求原文、功能範圍、使用者操作、資料保存、外部服務與限制。
2. Read 讀取可用的專案結構資訊，取得本功能文件位置、原始碼目錄與既有技術端點線索。
3. Think 判斷需求來源與專案結構資訊是否足以推導系統介面盤點與分析流程安排。
4. Write 當資訊不足以推導規劃時，將缺少資訊清單與確認問題寫入回覆並停止。

## Phase 3: 推導系統分析規劃

1. Think 依已載入規範從需求部位推導系統介面盤點，取得每個介面的名稱、端點類型、需求依據與介面定位。
2. Think 依已載入規範按需求依賴程度安排分析 Wave，取得每個 Wave 的端點清單、Sub-agent 委派目標、需求依賴判斷與排程理由。
3. Think 決定專案結構描述與 Structure Decision，取得文件結構、原始碼結構與結構選擇理由。

## Phase 4: 撰寫 plan.md

1. Write 依已載入樣板與範例將系統分析規劃寫入目標 `plan.md`。

## Phase 5: 檢查 plan.md

1. Read 依已載入規範、骨架與範例檢查目標 `plan.md` 是否符合系統介面盤點、端點類型、需求依據、Wave 排程與規劃邊界要求。

## Phase 6: 修正 plan.md

1. Write 修正目標 `plan.md` 中可由既有資訊處理的全部不符合已載入規範、骨架與範例的問題。
