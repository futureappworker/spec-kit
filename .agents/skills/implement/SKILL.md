---
name: implement
description: 依 feature 目錄中的 tasks.md，依序一次實作一個未完成任務，直到全部完成。標有 TDD 步驟的任務交給 tdd 只做該步驟。規格品質清單仍有未完成項且使用者未允許略過時，先停下詢問。全部任務完成後把 spec.md 標為 Implemented。
metadata:
  references:
    - project: GitHub Spec Kit
      url: https://github.com/github/spec-kit
      source: templates/commands/implement.md
      license: MIT
      copyright: Copyright GitHub, Inc.
---

本 Skill 參考並改寫自 [GitHub Spec Kit](https://github.com/github/spec-kit) 的 [`templates/commands/implement.md`](https://github.com/github/spec-kit/blob/main/templates/commands/implement.md)。該原始碼以 MIT License 授權，Copyright GitHub, Inc.。完整授權聲明見 [NOTICE](NOTICE)。

# SOP

## Phase 1: 讀取輸入與定位任務清單

1. Read 讀取使用者輸入並取得目標 feature 目錄，以及是否允許略過規格品質清單。
2. Think 決定目標 `tasks.md` 路徑為指定 feature 目錄或目前功能目錄中的任務清單。
3. Read 讀取目標 `tasks.md` 並取得未完成任務、任務描述與 References。
4. Read 讀取同目錄 `plan.md` 並取得原始碼落地位置。

## Phase 2: 確認規格品質清單

1. Read 若 feature 目錄存在 `checklists/`，讀取其中的 checklist 檔案並取得勾選狀態。
2. Read [規格品質清單確認規範](rules/規格品質清單確認規範.md)並取得未完成項目與略過條件。
3. Think 依已載入規範決定本次是停下詢問，或繼續執行任務。
4. Write 若本次是停下詢問，將未完成的 checklist 項目與是否繼續的問題寫入回覆，並停止本次 SOP 的所有後續步驟。

## Phase 3: 選擇下一個任務

1. Read 讀取 `tasks.md` 並取得未完成任務。
2. Read 若尚未載入 [任務選擇規範](rules/任務選擇規範.md)，讀取該規範並取得單一任務的選擇要求。
3. Think 依已載入規範決定本次唯一目標任務；沒有未完成任務時，目標任務為空。
4. Think 若目標任務為空，決定進入 Phase 12，並停止本 Phase 之後、Phase 12 之前的所有步驟。

## Phase 4: 載入任務最小上下文

1. Read 若尚未載入 [任務上下文載入規範](rules/任務上下文載入規範.md)，讀取該規範並取得 References 與原始碼讀取要求。
2. Read 依已載入規範讀取本次目標任務的 References 位址並取得契約部位。
3. Read 依已載入規範讀取本次目標任務的目標檔案、相鄰測試檔與必要原始碼並取得既有實作模式。

## Phase 5: 執行任務

1. Read 若尚未載入 [任務執行規範](rules/任務執行規範.md)，讀取該規範並取得變更範圍、測試任務與實作任務要求。
2. Read 若尚未載入 [TDD步驟委派規範](rules/TDD步驟委派規範.md)，讀取該規範並取得有 TDD 步驟的任務委派要求。
3. Think 依已載入規範決定本次目標任務是 TDD 步驟或一般任務，以及該任務的完成判定。
4. Delegate 若本次目標任務標有 TDD 步驟，依已載入規範將該任務的步驟名稱、測試計劃案例位址與目標檔交給 `tdd`。
5. Write 若本次目標任務是沒有 TDD 步驟的測試任務，依已載入規範將契約斷言寫入目標測試檔。
6. Delegate 若本次目標任務是沒有 TDD 步驟的測試任務，依已載入規範使用專案既有測試指令取得預期失敗結果。
7. Write 若本次目標任務是沒有 TDD 步驟的實作任務，依已載入規範將最小變更寫入目標檔案。

## Phase 6: 驗證任務

1. Read 若尚未讀取，讀取專案根目錄的套件、測試、lint 與格式化設定檔並取得可用驗證命令。
2. Read 若尚未載入 [任務驗證規範](rules/任務驗證規範.md)，讀取該規範並取得驗證與修正要求。
3. Think 依已載入規範決定本次目標任務的驗證命令。
4. Delegate 依已載入規範使用專案既有測試、lint 或 typecheck 指令驗證本次目標任務並取得結果。
5. Read 讀取本次驗證輸出並取得通過或失敗證據。
6. Think 依已載入規範決定處置是通過或修正目標任務。
7. Think 若處置是通過，決定進入 Phase 8，並停止本 Phase 之後、Phase 8 之前的所有步驟。

## Phase 7: 修正未通過的任務

1. Delegate 若本次目標任務標有 TDD 步驟，依已載入規範將同一個 TDD 步驟、測試計劃案例位址與目標檔交給 `tdd`，回到 Phase 6 第 3 步，並停止本步驟之後的步驟。
2. Write 若本次目標任務沒有 TDD 步驟，依已載入規範修正該任務的目標檔案，回到 Phase 6 第 3 步，並停止本步驟之後的步驟。

## Phase 8: 打勾

1. Read 若本次尚未載入 [產出覆蓋規範](../constitution/rules/產出覆蓋規範.md)，讀取該規範並取得憲法讀取時機與停止寫入條件。
2. Read 若本次尚未載入，讀取 `constitution/共同/憲法套用規範.md`；檔案不存在時，專案套用規則為空。
3. Read 若本次尚未載入，讀取 `constitution/tasks/tasks.md`，取得 `tasks.md` 的憲法 Rule；檔案不存在時，憲法 Rule 為空。
4. Read 若尚未載入 [任務打勾規範](rules/任務打勾規範.md)，讀取該規範並取得 checkbox 的寫入與符合狀態要求。
5. Think 依已載入規範決定本次是更新目標任務 checkbox，或因憲法停止寫入。
6. Write 若本次是因憲法停止寫入，將拒絕原因寫入回覆。
7. Write 若本次是更新 checkbox，依已載入規範與已載入的憲法 Rule 將該任務 checkbox 從 `[ ]` 更新為 `[X]`。

## Phase 9: 檢查勾選

1. Read 讀取 `tasks.md` 並依已載入規範檢查本次目標任務的 checkbox，列出不符合項目。

## Phase 10: 修正勾選

1. Write 依已載入規範與已載入的憲法 Rule 修正 `tasks.md` 中本次目標任務 checkbox 的不符合項目。

## Phase 11: 決定下一個任務

1. Read 若尚未載入 [連續執行規範](rules/連續執行規範.md)，讀取該規範並取得下一個執行位置的要求。
2. Read 讀取 `tasks.md` 並取得本次目標任務的勾選狀態。
3. Think 依已載入規範決定下一個執行位置是 Phase 3 或 Phase 15。
4. Think 若下一個執行位置是 Phase 3，決定回到 Phase 3，並停止本 Phase 之後的所有步驟。
5. Think 若下一個執行位置是 Phase 15，決定進入 Phase 15，並停止本 Phase 之後、Phase 15 之前的所有步驟。

## Phase 12: 標記規格完成狀態

1. Read 讀取 `tasks.md` 並取得未完成任務。
2. Read 讀取目標 `spec.md` 的狀態列；檔案不存在時，規格狀態為空。
3. Read [規格完成狀態規範](rules/規格完成狀態規範.md)並取得完成狀態的寫入條件與狀態值。
4. Think 依已載入規範決定本次是否滿足完成狀態的寫入條件。
5. Read 若滿足寫入條件且本次尚未載入 [產出覆蓋規範](../constitution/rules/產出覆蓋規範.md)，讀取該規範並取得憲法讀取時機與停止寫入條件。
6. Read 若滿足寫入條件且本次尚未載入，讀取 `constitution/共同/憲法套用規範.md`；檔案不存在時，專案套用規則為空。
7. Read 若滿足寫入條件且本次尚未載入，讀取 `constitution/specify/spec.md`，取得 `spec.md` 的憲法 Rule；檔案不存在時，憲法 Rule 為空。
8. Think 若滿足寫入條件，依已載入規範決定本次是更新目標 `spec.md` 的狀態，或因憲法停止寫入。
9. Write 若本次是因憲法停止寫入，將拒絕原因寫入回覆。
10. Write 若本次是更新狀態，依已載入規範與已載入的憲法 Rule 只更新目標 `spec.md` 的狀態列。

## Phase 13: 檢查規格完成狀態

1. Read 讀取目標 `spec.md` 的狀態列，並依已載入規範檢查完成狀態，列出不符合項目；檔案不存在時，規格狀態為空。

## Phase 14: 修正規格完成狀態

1. Write 依已載入規範與已載入的憲法 Rule 修正目標 `spec.md` 狀態列的不符合項目。

## Phase 15: 回報並結束本次執行

1. Read 讀取 `tasks.md` 並取得已完成任務與未完成任務。
2. Read 讀取目標 `spec.md` 的狀態列；檔案不存在時，規格狀態為空。
3. Think 決定完成的任務、驗證結果、規格狀態、未完成任務、憲法停止寫入的拒絕原因與回覆內容。
4. Write 將完成的任務 ID、修改摘要、驗證結果、是否已打勾、規格狀態與未完成任務寫入回覆，並結束本次執行。
