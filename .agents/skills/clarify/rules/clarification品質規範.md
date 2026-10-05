# Rule 1 - 澄清目標必須影響核心規格

- Clarification 必須用於會改變功能範圍、資料歸屬、使用者旅程、驗收結果、安全隱私要求或後續 planning 邊界的缺口。
- 不影響核心規格且可以保守推導的缺口必須寫入 Assumptions。
- Clarification 不得詢問實作技術、介面樣式偏好、內部架構或可以由後續 planning 決定的細節。
- 每次提問模式最多必須輸出三個 Clarification，且必須依影響排序。

## Good Example

- 問題會改變資料歸屬與驗收結果，因此適合提出 Clarification。

```markdown
## Question 1: 原始照片檔案處理

**Context**: Spec 只說使用者加入照片，但沒有說整理時是否搬移原始檔案。

**What we need to know**: 系統整理照片時應如何處理原始照片檔案?
```

## Bad Example

- 問題只涉及介面顏色，沒有改變核心規格或驗收結果。

```markdown
## Question 1: 按鈕顏色

**Context**: Spec 尚未指定主要按鈕顏色。

**What we need to know**: 主要按鈕要使用藍色還是綠色?
```

# Rule 2 - 澄清問題必須具體且可回答

- 每個 Clarification 必須包含 Context、What we need to know、Suggested Answers 與 Your choice。
- Context 必須引用或摘要 spec 中造成不確定的內容。
- What we need to know 必須是一個具體問題。
- Suggested Answers 必須提供 A、B、C 與 Custom 四個選項。
- 每個選項必須說明對 spec 的影響。

## Good Example

- 問題有上下文、具體決策點、可選答案與每個答案的規格影響。

```markdown
## Question 1: 缺少日期的照片分類

**Context**: Spec 要求依日期分組，但沒有定義缺少可辨識日期的照片如何處理。

**What we need to know**: 缺少可辨識日期的照片應歸入哪裡?

**Suggested Answers**:

| Option | Answer | Implications |
|--------|--------|--------------|
| A | 放入「未分類日期」相簿 | 所有照片都可被找到，需新增特殊分組與狀態說明 |
| B | 要求使用者先補日期 | 匯入流程會多一步手動補資料 |
| C | 排除缺少日期的照片 | 整理結果不包含這些照片，需明確告知使用者 |
| Custom | 使用者提供其他處理方式 | 依使用者答案更新分組與驗收規則 |

**Your choice**: _請回覆 Q1: A/B/C 或 Custom - 你的答案_
```

## Bad Example

- 問題沒有明確上下文與選項影響，使用者難以知道回答會改變什麼。

```markdown
## Question 1

照片日期怎麼辦?

A/B/C?
```

# Rule 3 - 提問排序必須依風險與影響

- Clarification 必須依 `scope > security/privacy > data ownership > user journey > acceptance result > UX detail` 排序。
- 當可提出的問題超過三個時，必須只保留排序最高的三個。
- 被排除且不阻塞核心規格的缺口必須轉為 Assumptions。
- 被排除但仍阻塞核心規格的缺口必須保留在 spec 狀態中，使狀態維持 `Needs Clarification`。

## Good Example

- 問題排序先處理範圍與資料歸屬，再處理操作細節。

```markdown
1. 是否包含多人協作相簿? (scope)
2. 原始照片檔案是否被搬移或保留? (data ownership)
3. 缺少日期的照片如何分類? (acceptance result)
```

## Bad Example

- 排序先問低風險介面細節，卻延後會影響規格範圍的問題。

```markdown
1. 相簿卡片要多大? (UX detail)
2. 拖放動畫要不要彈性效果? (UX detail)
3. 是否包含多人協作相簿? (scope)
```

# Rule 4 - 使用者答案必須回寫到全部受影響章節

- 套用模式必須把使用者回答記錄到 Clarifications 的最新 Session。
- 套用模式必須同步更新受影響的 User Stories、Acceptance Criteria、Functional Requirements、Non-Functional Requirements、Global Requirements、Edge Cases、Key Entities、Success Criteria 與 Assumptions。
- 當答案取代既有 Assumption 時，必須刪除或改寫該 Assumption。
- 套用模式不得只新增 Q/A 而不更新正文需求。

## Good Example

- 答案同時寫入 Clarifications，並同步改寫需求與假設。

```markdown
## Clarifications

### Session 2026-10-05

- Q: 缺少可辨識日期的照片應歸入哪裡? -> A: 放入「未分類日期」相簿

**Functional Requirements**:

- **FR-004**: 系統必須將缺少可辨識日期的照片放入「未分類日期」相簿，並清楚標示原因。

## Assumptions

- 目標使用者是整理個人照片的一般使用者。
```

## Bad Example

- 只記錄答案，正文仍保留舊假設或缺少對應需求。

```markdown
## Clarifications

### Session 2026-10-05

- Q: 缺少可辨識日期的照片應歸入哪裡? -> A: 放入「未分類日期」相簿

## Assumptions

- 缺少日期的照片處理方式尚未決定。
```

# Rule 5 - 規格狀態必須反映澄清完成度

- 若仍有核心缺口未回答，Status 必須為 `Needs Clarification`。
- 若所有核心缺口已回答或剩餘缺口已合理轉為 Assumptions，Status 必須為 `Ready for Planning`。
- 若使用者答案造成章節矛盾且尚未修正，Status 必須維持 `Needs Clarification`。
- Status 不得在仍有未處理核心缺口時標示為 `Ready for Planning`。

## Good Example

- 狀態和剩餘缺口一致，可判斷是否能進入 planning。

```markdown
**Status**: Ready for Planning

## Clarifications

### Session 2026-10-05

- Q: 是否支援多人共同整理相簿? -> A: 不支援，僅單一使用者整理個人照片
```

## Bad Example

- 仍有未回答的核心問題，卻標示為可進入 planning。

```markdown
**Status**: Ready for Planning

## Clarifications

### Session 2026-10-05

- Q: 是否支援多人共同整理相簿? -> A: [NEEDS CLARIFICATION]
```

# Rule 6 - 澄清結果不得引入實作方案

- 使用者回答若包含技術方案，套用時必須只保留產品需求層面的決策。
- Clarification 回寫不得新增程式語言、框架、資料庫、API、雲服務或內部模組設計，除非使用者明確把該技術限制定義為產品需求。
- 需要技術取捨的內容必須留給後續 planning。
- Clarification 必須維持 Feature Specification 面向使用者價值與可驗收行為。

## Good Example

- 使用者提到技術，但回寫時轉成產品層面的可驗收需求。

```markdown
使用者回答：用 SQLite 存排序，重開 App 後順序要留著。

回寫需求：
- **FR-008**: 系統必須保留使用者調整後的照片排序，直到使用者再次變更。
```

## Bad Example

- 回寫內容把實作技術寫入 Feature Specification。

```markdown
使用者回答：用 SQLite 存排序，重開 App 後順序要留著。

回寫需求：
- **FR-008**: 系統必須使用 SQLite 儲存照片排序資料。
```
