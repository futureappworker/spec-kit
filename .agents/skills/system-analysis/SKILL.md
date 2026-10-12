---
name: system-analysis
description: 依 Feature Specification、同目錄 research.md 與 techstack.md 產出並執行 plan.md 中的系統分析規劃，先盤點需求涉及的技術端點與系統介面，再用 Wave 委派對應 Planner Skill 完成介面分析。
---

# SOP

## Phase 1: 讀取輸入與樣板

1. Read 讀取使用者輸入並取得需求來源、目標 `plan.md` 路徑、同目錄 `research.md` 與 `techstack.md` 路徑，以及已知專案結構。
2. Read [系統分析規劃規範](rules/系統分析規劃規範.md)並取得系統介面盤點、端點類型與 Wave 排程要求。
3. Read [Plan Template 骨架](templates/plan.md)並取得系統分析規劃的固定輸出結構。
4. Read [Plan Template 範例](templates/plan.example.md)並取得完整 Artifact 的填寫方式。
5. Think 決定本次可用需求來源、目標 `plan.md` 路徑、`research.md` 路徑、`techstack.md` 路徑與資訊是否足以產出系統分析規劃。
6. Delegate `clarify` 當缺少必要需求來源、目標 `plan.md` 路徑、`research.md` 路徑或 `techstack.md` 路徑時產生澄清問題。
7. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 2: 讀取需求、技術決策與專案結構

1. Read 讀取目標需求來源檔案，取得需求原文、功能範圍、使用者操作、資料保存、外部服務與限制。
2. Read 讀取目標 `research.md`，取得已決定的技術取捨、理由與被排除的替代方案。
3. Read 讀取目標 `techstack.md`，取得採用技術、延後或不採用技術與規劃影響。
4. Read 讀取可用的專案結構資訊，取得本功能文件位置、原始碼目錄與既有技術端點線索。
5. Think 判斷需求來源、技術研究、技術堆疊與專案結構資訊是否足以推導系統介面盤點與分析流程安排。
6. Delegate `clarify` 當資訊不足以推導規劃時產生澄清問題。
7. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 3: 推導系統分析規劃

1. Read [系統分析委派執行規範](rules/系統分析委派執行規範.md)並取得 Planner Skill 選擇、Wave 執行與澄清轉交要求。
2. Think 依已載入規範從需求部位推導系統介面盤點，取得每個介面的名稱、端點類型、需求依據，以及對齊已讀取採用技術的介面定位。
3. Think 依已載入規範為每個系統介面決定委派目標，取得 `ui-ux-plan`、`api-plan`、`data-plan` 或 `clarify` 的對應結果。
4. Delegate `clarify` 當任一系統介面只能對應到 `clarify` 時產生澄清問題。
5. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。
6. Think 依已載入規範按需求依賴程度安排分析 Wave，取得每個 Wave 的端點清單、Planner Skill 委派目標、需求依賴判斷與排程理由。
7. Think 依已讀取的採用技術與規劃影響決定專案結構描述與 Structure Decision，取得文件結構、原始碼結構與結構選擇理由。

## Phase 4: 撰寫 plan.md

1. Write 依已載入樣板與範例將系統分析規劃寫入目標 `plan.md`。

## Phase 5: 執行分析 Wave

1. Think 依已載入規範決定各 Wave 的執行順序、可平行委派清單、上游分析結果輸入與停止條件。
2. Delegate `ui-ux-plan`、`api-plan` 或 `data-plan` 依 Wave 順序分析各自被分配的系統介面。
3. Delegate `clarify` 當 Wave 執行前或 Planner Skill 回報核心缺口時產生澄清問題。
4. Think 當已轉交 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 6: 收斂介面分析結果

1. Think 彙整各 Planner Skill 的介面分析結果，取得跨介面依賴、衝突、待澄清缺口與可進入後續 planning 的結論。
2. Write 將介面分析結果與剩餘缺口寫入使用者指定的目標檔案或回覆 Artifact。

## Phase 7: 檢查 plan.md 與分析結果

1. Read 依已載入規範、骨架與範例檢查目標 `plan.md` 是否符合系統介面盤點、端點類型、需求依據、Wave 排程與規劃邊界要求。
2. Read 依已載入規範檢查介面分析結果是否符合 Planner Skill 委派目標、Wave 依賴順序、澄清轉交與跨介面一致性要求。

## Phase 8: 修正 plan.md 與分析結果

1. Write 修正目標 `plan.md` 中可由既有資訊處理的全部不符合已載入規範、骨架與範例的問題。
2. Write 修正介面分析結果中可由既有資訊處理的全部不符合已載入規範的問題。
