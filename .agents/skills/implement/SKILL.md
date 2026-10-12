---
name: implement
description: 依 feature 目錄中的 tasks.md 連續執行安全任務批次，直到任務全部完成；逐任務只讀 References，逐任務驗證通過後才打勾。Checkpoint 驗證失敗時，先修正所屬任務再重新驗證。
---

# SOP

## Phase 1: 讀取輸入與定位任務清單

1. Read 讀取使用者輸入並取得目標 feature 目錄、指定任務 ID，以及是否允許略過 checklist。
2. Think 決定目標 `tasks.md` 路徑為指定 feature 目錄或目前功能目錄中的任務清單。
3. Read 讀取目標 `tasks.md` 並取得任務格式、Phase、端點小節、未完成任務、References、Checkpoint 與 Dependencies 區段。
4. Read 讀取同目錄 `plan.md` 並取得原始碼落地位置、系統介面盤點、技術棧與驗證線索。

## Phase 2: 初始化執行紀錄

1. Read [執行紀錄規範](rules/執行紀錄規範.md)並取得重置、失敗原因與阻塞欄位要求。
2. Write 依已載入規範在目標 feature 目錄建立或覆寫 `implement-run.md`。

## Phase 3: 執行前檢查

1. Read 若 feature 目錄存在 `checklists/`，讀取 checklist 檔案並取得勾選狀態。
2. Think 若存在未完成 checklist 且使用者未允許略過，決定本次狀態為等待使用者確認。
3. Write 若本次狀態為等待使用者確認，將 checklist 狀態與是否繼續的問題寫入回覆 Artifact，並停止本次 SOP 的所有後續步驟。
4. Read 讀取專案根目錄的套件、測試、lint 與格式化設定檔並取得可用驗證命令。

## Phase 4: 選擇可執行任務批次

1. Read [任務選擇規範](rules/任務選擇規範.md)並取得任務選擇、Phase gate 與連續批次要求。
2. Read [平行執行規範](rules/平行執行規範.md)並取得平行批次准入與序列化要求。
3. Read [檢查點驗證規範](rules/檢查點驗證規範.md)並取得通過紀錄、驗證時機與失敗修正要求。
4. Think 依已載入規範決定本次目標批次，以及該批次是實作批次或只驗證 Checkpoint。
5. Write 依已載入規範將本次批次起點寫入 `implement-run.md`。

## Phase 5: 載入任務最小上下文

1. Read 若本次目標是實作批次且尚未載入 [任務上下文載入規範](rules/任務上下文載入規範.md)，讀取該規範並取得 References 與原始碼讀取要求。
2. Read 若本次目標是實作批次，依已載入規範逐任務讀取 References 位址並取得契約部位。
3. Read 若本次目標是實作批次，依已載入規範逐任務讀取目標檔案、相鄰測試檔與必要原始碼並取得既有實作模式。
4. Think 若本次目標是實作批次，依已載入規範決定每個已選任務的變更範圍與完成判定。

## Phase 6: 執行任務批次

1. Read 若本次目標是實作批次且尚未載入 [任務執行規範](rules/任務執行規範.md)，讀取該規範並取得變更範圍、測試任務與實作任務要求。
2. Write 若本次目標是實作批次且存在測試任務，依已載入規範逐任務將契約斷言寫入目標測試檔。
3. Delegate 若本次目標是實作批次且存在測試任務，依已載入規範使用專案既有測試指令逐任務取得預期失敗結果。
4. Write 若本次目標是實作批次且存在實作任務，依已載入規範逐任務將最小變更寫入目標檔案。
5. Think 若本次目標是實作批次，依已載入規範確認變更仍在本次目標批次內。

## Phase 7: 驗證與打勾

1. Read 若本次目標是實作批次且尚未載入 [驗證與打勾規範](rules/驗證與打勾規範.md)，讀取該規範並取得驗證、失敗處置與 checkbox 要求。
2. Think 若本次目標是實作批次，依已載入規範決定每個已選任務的驗證命令。
3. Delegate 若本次目標是實作批次，依已載入規範執行驗證並取得結果。
4. Read 若本次目標是實作批次，讀取驗證輸出並取得通過或失敗證據。
5. Read 若驗證失敗，讀取 `implement-run.md` 的 `失敗原因`。
6. Think 若驗證失敗，依已載入規範決定處置是修正、寫入範圍外阻塞或寫入範圍內阻塞。
7. Write 若處置是寫入範圍外阻塞，依已載入規範將 `阻塞` 與 `恢復條件` 寫入 `implement-run.md`。
8. Write 若處置是修正，依已載入規範更新 `implement-run.md` 的 `失敗原因`。
9. Write 若處置是修正，依已載入規範修正目標檔案，回到本 Phase 第 2 步，並停止本步驟之後的步驟。
10. Write 若處置是寫入範圍內阻塞，依已載入規範將 `阻塞` 與 `恢復條件` 寫入 `implement-run.md`。
11. Write 若任務驗證通過，依已載入規範將該任務 checkbox 從 `[ ]` 更新為 `[X]`。

## Phase 8: 驗證 Checkpoint

1. Read 讀取 `implement-run.md` 並取得 `阻塞` 與 `失敗原因`。
2. Think 依已載入規範決定驗證目標與要移除的失效通過紀錄；無須驗證時，驗證目標為空。
3. Write 若存在失效通過紀錄，依已載入規範從 `tasks.md` 移除該通過紀錄。
4. Delegate 若驗證目標不是空的，使用 Checkpoint 原文的驗證命令或手動檢查並取得結果。
5. Read 若已執行驗證，讀取驗證輸出並取得通過或失敗證據。
6. Write 若驗證通過，依已載入規範把通過紀錄寫入 `tasks.md` 的對應 Checkpoint。
7. Write 若驗證通過，依已載入規範清除 `implement-run.md` 的 `失敗原因`。

## Phase 9: 修正失敗的 Checkpoint

1. Read 讀取 `implement-run.md` 並取得 `阻塞` 與 `失敗原因`。
2. Read 若驗證失敗，讀取本次 Checkpoint 驗證輸出並取得本次失敗原因。
3. Think 依已載入規範比較本次失敗原因與紀錄中的 `失敗原因`，決定修正範圍；沒有可修正項目時，修正範圍為空。
4. Read 若修正範圍不是空的，讀取範圍內的目標檔案並取得對應實作。
5. Write 若修正範圍不是空的，依已載入規範將本次失敗原因寫入 `implement-run.md` 的 `失敗原因`。
6. Write 若修正範圍不是空的，依已載入規範將修正寫入所屬任務指向的目標檔案。
7. Write 若修正範圍為空且驗證失敗，依已載入規範將 `阻塞` 與 `恢復條件` 寫入 `implement-run.md`。
8. Think 若已寫入程式修正，決定回到 Phase 8，並停止本 Phase 之後的所有步驟。

## Phase 10: 決定是否繼續下一批

1. Read 讀取 `implement-run.md` 並取得 `阻塞`。
2. Read 讀取 `tasks.md` 並取得未完成任務與 Checkpoint 通過紀錄。
3. Think 依已載入規範決定下一個執行位置是 Phase 4 第 4 步或 Phase 11。
4. Write 若下一個執行位置是 Phase 4 第 4 步，依已載入規範清除 `implement-run.md` 的 `失敗原因`，回到 Phase 4 第 4 步，並停止本 Phase 之後的所有步驟。

## Phase 11: 回報並結束本次執行

1. Read 讀取 `implement-run.md` 並取得 `阻塞` 與 `恢復條件`。
2. Read 讀取 `tasks.md` 並取得已完成任務、Checkpoint 通過紀錄與未完成任務。
3. Think 決定完成的任務、驗證結果、Checkpoint 結果、未完成任務、阻塞事項與恢復執行條件。
4. Write 將完成的任務 ID、修改摘要、驗證結果、是否已打勾、Checkpoint 結果、未完成任務、阻塞事項與恢復執行條件寫入回覆 Artifact，並結束本次執行。
