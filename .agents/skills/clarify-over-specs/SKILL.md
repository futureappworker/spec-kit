---
name: clarify-over-specs
description: 在 specify 寫完 Feature Specification 之後，依使用者要求對 spec.md 做專業需求澄清。掃描覆蓋與影響後委派 clarify 提問，並把回答寫回規格。
---

# SOP

## Phase 1: 讀取規格與澄清輸入

1. Read 讀取使用者輸入並取得目標 Feature Specification 路徑、本次要提問或套用答案，以及使用者提供的回答。
2. Read 讀取目標 spec.md，取得狀態、澄清紀錄、使用者故事、需求、關鍵實體、邊界情境、成功標準與假設。

## Phase 2: 判斷執行模式

1. Think 依使用者輸入決定本次執行為提問模式或套用模式。

## Phase 3: 掃描並委派提問

1. Read 當本次為提問模式時，讀取 [規格覆蓋分類規範](rules/規格覆蓋分類規範.md)並取得十類掃描分類與各類檢查點。
2. Read 當本次為提問模式時，讀取 [覆蓋與挑題規範](rules/覆蓋與挑題規範.md)並取得挑題、需求高度與委派題目要求。
3. Think 當本次為提問模式時，依已載入規範產出內部覆蓋結果與最多五個要提問的缺口。
4. Think 當沒有會改變規格或驗收的缺口時，決定不委派提問並以現有規格繼續。
5. Delegate `clarify` 當已選定缺口時，依已載入規範把鎖定題目交給它產生澄清問題。
6. Think 當已委派 `clarify` 時，決定本次流程停止於澄清問題產出。

## Phase 4: 寫回澄清答案

1. Read 當本次為套用模式時，讀取 [答案寫回規範](rules/答案寫回規範.md)並取得章節歸屬、矛盾替換、可測標準、狀態與 checklist 要求。
2. Think 當本次為套用模式時，依已載入規範決定每個回答要改的章節、假設、狀態與 checklist 項目。
3. Write 當本次為套用模式時，依已載入規範將澄清答案與受影響內容寫入目標 spec.md。
4. Write 當本次為套用模式且 feature 目錄已有 `checklists/requirements.md` 時，依已載入規範更新其中通過狀態已改變的項目。

## Phase 5: 檢查寫回結果

1. Read 當本次已寫回規格時，依已載入規範檢查目標 spec.md 與 checklist 是否仍有矛盾決策、過時假設、未處理核心缺口或未同步內容，並列出不符合項目。

## Phase 6: 修正寫回結果

1. Write 當檢查發現不符合項目時，修正目標 spec.md 中全部不符合已載入規範的內容。
2. Write 當 checklist 存在且檢查發現其狀態不符合時，修正 `checklists/requirements.md` 中通過狀態已改變的項目。
