# Rule 1 - 需求事實必須可追溯

- 需求事實必須來自使用者原始需求、使用者後續澄清或已明確標記的 Assumptions。
- 使用者明確說出的功能、限制、互動、資料物件與禁止事項必須保留到 Feature Specification 的對應段落。
- 不得把未被使用者明講的技術方案、平台、架構、儲存方式或第三方服務寫成需求事實。
- 推導內容必須與原始需求相容；若推導內容超出原始需求，必須放入 Assumptions 或先提出 Clarification。

## Good Example

- 明確保留使用者要求的日期分組、拖放排序與禁止巢狀相簿，且未加入未被要求的技術方案。

```markdown
需求事實：
- 使用者要將照片依日期整理到相簿。
- 使用者要在主頁透過拖放重新排列照片。
- 相簿不得嵌套在其他相簿中。

Assumptions：
- 日期分組預設使用照片可取得的拍攝日期。
```

## Bad Example

- 忽略相簿不得嵌套的限制，並加入使用者沒有要求的雲端同步技術。

```markdown
需求事實：
- 使用者要建立可多層分類的照片資料夾。
- 系統必須使用雲端同步保存照片。
```

# Rule 2 - 澄清與假設必須分流

- 當缺口會改變核心行為、資料歸屬、使用者旅程或驗收結果時，必須提出 Clarification。
- 當缺口不阻塞核心規格且可以用保守前提繼續推導時，必須記入 Assumptions。
- Clarification 必須是可回答的具體問題，不得詢問泛泛的偏好或實作細節。
- Assumption 必須描述目前採用的前提，不得偽裝成使用者已確認的需求。

## Good Example

- 原始需求沒有說照片缺少日期時如何處理，這會影響分類結果，因此提出澄清；未明確指定使用者類型，則以假設承接。

```markdown
Clarifications：
- Q: 照片缺少可辨識日期時應如何處理? -> A: 放入未分類日期相簿

Assumptions：
- 目標使用者是整理個人照片的一般使用者。
```

## Bad Example

- 把會影響分類結果的缺口當成已確認需求，也詢問不影響規格的實作偏好。

```markdown
Clarifications：
- Q: 按鈕要用藍色還是綠色?

Assumptions：
- 使用者已確認缺少日期的照片會自動刪除。
```

# Rule 3 - User Story 必須以使用者價值切分

- 每個 User Story 必須描述一段可獨立驗證的使用者旅程。
- P1 必須代表最小可用核心價值，P2 與 P3 必須依後續價值排序。
- User Story 不得以技術層、資料層或內部模組作為切分依據。
- 每個 User Story 必須包含價值理由與獨立測試方式。

## Good Example

- 三個故事分別對應整理、排序與預覽三段使用者價值，且都可以單獨驗證。

```markdown
### User Story 1 - 依日期整理照片相簿 (Priority: P1)

使用者希望匯入照片後自動依日期分組，讓照片能依時間脈絡被找到。

**Why this priority**: 日期分組是整理照片的核心價值。

**Independent Test**: 加入不同日期照片後，確認每張照片出現在正確日期相簿中。
```

## Bad Example

- 以內部技術層切分故事，無法直接呈現使用者價值。

```markdown
### User Story 1 - 建立資料庫資料表 (Priority: P1)

系統需要建立資料表保存照片資料。

**Why this priority**: 因為後端需要資料表。

**Independent Test**: 檢查資料表是否存在。
```

# Rule 4 - Requirements 必須可驗證且歸屬正確

- Functional Requirement 必須描述使用者可觀察的能力、行為或資料規則。
- Non-Functional Requirement 必須描述品質屬性、限制或可衡量的服務水準。
- Global Requirement 必須只收納跨越多個 User Story 的需求。
- 屬於單一 User Story 的需求不得放入 Global Requirements。
- Requirement 不得只描述願望、口號或無法驗證的抽象品質。

## Good Example

- FR 描述可觀察行為，NFR 描述可衡量品質，Global Requirement 描述跨故事限制。

```markdown
**Functional Requirements**:

- **FR-001**: 系統必須允許使用者加入照片到整理範圍中。

**Non-Functional Requirements**:

- **NFR-001**: 照片分組完成後，系統應讓使用者能清楚辨識哪些照片仍缺少可辨識日期。

### Global Functional Requirements

- **GFR-001**: 系統必須保證相簿為單層結構，且任何相簿不得嵌套在其他相簿中。
```

## Bad Example

- 需求不可驗證，且把單一故事的能力錯放到 Global Requirement。

```markdown
**Functional Requirements**:

- **FR-001**: 系統必須很好用。

### Global Functional Requirements

- **GFR-001**: 使用者必須能開啟某個相簿並查看照片。
```

# Rule 5 - Acceptance Criteria 與 Success Criteria 必須可測量

- Acceptance Criteria 必須使用 Given、When、Then 描述可驗證情境。
- Acceptance Criteria 必須驗證使用者可觀察結果，不得只驗證內部實作狀態。
- Success Criteria 必須包含可觀察或可量測的結果。
- Success Criteria 應該包含數量、比例、時間、成功率或可驗證的使用者結果。

## Good Example

- 驗收條件描述具體情境，成功標準包含可測量數字。

```markdown
**Acceptance Criteria**:

1. **Given** 使用者有多張包含拍攝日期的照片，**When** 使用者完成加入照片，**Then** 系統會自動依照片日期建立或更新相簿分組。

### Measurable Outcomes

- **SC-001**: 使用者加入 100 張照片後，90% 的使用者能在 2 分鐘內完成依日期分組的整理流程。
```

## Bad Example

- 驗收條件只檢查內部實作，成功標準沒有可測量結果。

```markdown
**Acceptance Criteria**:

1. **Given** 系統有資料庫，**When** 函式被呼叫，**Then** 內部旗標被設為 true。

### Measurable Outcomes

- **SC-001**: 使用者會覺得體驗很好。
```

# Rule 6 - Artifact 必須完整符合樣板

- Feature Specification 必須填滿已載入樣板中的全部固定章節。
- Feature Specification 不得保留任何 `{{UPPER_SNAKE_CASE}}` 占位符。
- Feature Specification 的 FR、NFR、GFR、GNFR 與 SC 編號必須連續且不得重複。
- Feature Specification 必須保持明確需求、推導內容與 Assumptions 的邊界。
- Feature Specification 不得新增與樣板無關的操作說明、流程說明或 Skill 使用說明。

## Good Example

- Artifact 完整填寫章節、移除占位符，且編號連續。

```markdown
## Success Criteria

### Measurable Outcomes

- **SC-001**: 使用者加入 100 張照片後，90% 的使用者能在 2 分鐘內完成依日期分組的整理流程。
- **SC-002**: 對於包含可辨識日期的照片，至少 99% 會被分配到正確日期相簿。
```

## Bad Example

- Artifact 留下占位符、跳號，並混入操作說明。

```markdown
## Success Criteria

### Measurable Outcomes

- **SC-001**: {{SUCCESS_CRITERION_001}}
- **SC-003**: 使用者會很滿意。

請複製本段並替換占位符。
```

# Rule 7 - Status 必須指向下一步

- 若仍有會改變功能範圍、資料歸屬、使用者旅程或驗收結果的核心缺口，Status 必須為 `Needs Clarification`。
- 若所有核心缺口都已由使用者需求、Clarifications 或 Assumptions 處理，Status 必須為 `Ready for Planning`。
- Status 為 `Needs Clarification` 時，Clarifications 必須列出需要由 `clarify` 處理的具體問題。
- Status 為 `Ready for Planning` 時，Clarifications 不得保留未回答的核心問題。

## Good Example

- 狀態明確指出下一步需要先澄清，且 Clarifications 有具體問題。

```markdown
**Status**: Needs Clarification

## Clarifications

### Session 2026-10-05

- Q: 缺少可辨識日期的照片應如何處理? -> A: [NEEDS CLARIFICATION]
```

## Bad Example

- 狀態標示可進入 planning，但仍保留未回答的核心問題。

```markdown
**Status**: Ready for Planning

## Clarifications

### Session 2026-10-05

- Q: 缺少可辨識日期的照片應如何處理? -> A: [NEEDS CLARIFICATION]
```
