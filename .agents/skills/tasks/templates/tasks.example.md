---

description: "線上商店結帳的實作任務清單"
---

# Tasks: 線上商店結帳

**Input**: Design documents from `/specs/001-store-checkout/`

**Prerequisites**: 本清單已對齊 plan.md（必要）與 spec.md（必要）。執行時由上往下，不要在開工時讀完 research.md、techstack.md 與 contracts/。每個任務下方的 **References** 才是載入時機，而且只讀該位址，不讀同一份文件的其他部位。路徑相對於 `/specs/001-store-checkout/`。本功能沒有 data-model.md；quickstart.md 由 Phase 6 補上。

**Tests**: 專案憲法原則 II 要求使用者可觀察行為、錯誤路徑、金額資料轉換與跨模組契約都有可重複測試，且不得把測試留成無主的最後步驟。下列測試任務必須先寫並確認失敗，再實作對應行為。

**Organization**: 任務依使用者故事分階段，使每則故事可獨立實作與驗證。Phase 3 起的每個使用者故事，以及 Phase 6，都用第三層標題依 plan.md「系統介面盤點」切開端點。每則使用者故事都包含後端、資料庫、前端三節。任務落在該端點的程式庫；啟動文件放在 Phase 6 的環境小節。契約部位掛在每個任務上，只指向該端點的那一處。

## Format: `[ID] [P?] [Story] Description`

- **[P]**: 可平行（不同檔案、不依賴同階段尚未完成的任務）
- **[Story]**: 該任務所屬使用者故事（US1、US2、US3）
- 描述含精確檔案路徑
- 使用者故事與 Phase 6 的端點小節使用 `###`，順序為後端（含測試）→ 資料庫 → 前端。Phase 6 在這三端之後加上環境小節。端點小節只標 **Codebase**，不列契約檔
- **References** 寫在任務正下方，一行一個位址。只列本端點文件裡、這個任務直接實作或斷言的部位。後端任務不寫 DBML 或畫面，資料庫任務不寫 OpenAPI 或畫面，前端畫面任務不寫 OpenAPI 或 DBML
- 位址寫法：OpenAPI schema 用 `contracts/openapi.yaml#/components/schemas/{Name}`，HTTP 操作用 `contracts/openapi.yaml#/paths/~1{path}/{method}`（`/` 寫成 `~1`）；DBML 用 `contracts/schema.dbml#Table/{name}`；畫面用 `contracts/interface.pen#{frameId}`；技術選型用 `techstack.md#採用技術/{Area}`；目錄用 `plan.md#原始碼：儲存庫根目錄`

## Path Conventions

- **Web app**: `backend/src/`、`backend/tests/`、`frontend/src/`
- 路徑依 plan.md 的 `frontend/`（Vite + TypeScript）與 `backend/`（Node.js 單體、REST、PostgreSQL）分離結構
- 端點與落地位置：前端端點 → `frontend/`；後端端點 → `backend/src/` 的 catalog、cart、orders、http，以及 `backend/tests/`；資料庫端點 → `backend/src/db/`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: 建立 plan.md 的目錄與雙專案骨架，對齊單實例同源 cookie 部署

- [ ] T001 依 plan.md 建立目錄 `backend/src/catalog/`、`backend/src/cart/`、`backend/src/orders/`、`backend/src/http/`、`backend/src/db/migrations/`、`backend/tests/unit/`、`backend/tests/integration/`、`frontend/src/screens/`
  - **References**: `plan.md#原始碼：儲存庫根目錄`
- [ ] T002 在 `backend/package.json` 與 `backend/tsconfig.json` 初始化 Node.js + TypeScript 專案，依賴 `pg`，`strict: true`，並提供 `node:test` 測試腳本
  - **References**: `techstack.md#採用技術/Backend Runtime`
- [ ] T003 [P] 在 `frontend/package.json`、`frontend/tsconfig.json`、`frontend/index.html`、`frontend/vite.config.ts` 初始化 Vite + TypeScript；開發伺服器為 `http://localhost:5173`，並將 `/session`、`/health`、`/products`、`/cart`、`/orders` 代理到後端 `http://localhost:3000`，使 HTTP-only cookie 同源
  - **References**: `techstack.md#採用技術/Frontend`
- [ ] T004 [P] 在 `frontend/src/styles.css` 建立色彩代幣：surface、text、muted、action `#2563EB`、danger `#DC2626`、success `#059669`，並支援 light／dark
  - **References**: `contracts/interface.pen#variables`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: 所有使用者故事共用的買家 session、PostgreSQL 連線、HTTP 路由與購物車／訂單視圖骨架

**⚠️ CRITICAL**: 本階段完成前不得開始任何使用者故事

- [ ] T005 在 `backend/src/db/connection.ts` 以 `pg` 連線 `DATABASE_URL` 指向的 PostgreSQL，並匯出查詢用的連線池
  - **References**: `techstack.md#採用技術/Persistence`
- [ ] T006 在 `backend/src/db/migrations/001_init.sql` 建立初始 schema，欄位約束依下列每個表原樣：`buyers.id` varchar PK NOT NULL、`email` varchar 可空、`created_at` datetime NOT NULL、`last_seen_at` datetime NOT NULL、`default_address_id` varchar 可空；`products.id` varchar PK NOT NULL、`sku` varchar NOT NULL、`name` varchar NOT NULL、`unit_price_cents` int NOT NULL、`stock_qty` int NOT NULL、`status` varchar NOT NULL（`draft | published | archived`）、`category` varchar NOT NULL、`sku` unique 名 `products_sku_unique`、索引 `(status, category)` 名 `products_status_category_idx`；`carts.id` varchar PK NOT NULL、`buyer_id` varchar NOT NULL、`status` varchar NOT NULL（`open | checked_out | expired`）、`currency` char(3) NOT NULL、`shipping_method` varchar 可空（`standard | express`）、`shipping_cents` int NOT NULL default 0、`address_id` varchar 可空、`expires_at` datetime 可空、`created_at`／`updated_at` datetime NOT NULL、同一買家僅一筆 `status=open` 的 unique 名 `carts_buyer_open_unique`；`cart_lines` 以 `(cart_id, product_id)` 為 PK、`qty` int NOT NULL、`unit_price_cents` int NOT NULL；`addresses.id` varchar PK NOT NULL、`buyer_id` varchar NOT NULL、`recipient_name` varchar NOT NULL、`line1` varchar NOT NULL、`city` varchar NOT NULL、`postal_code` varchar NOT NULL、`country_code` char(2) NOT NULL、`is_default` boolean NOT NULL default false；`orders.id` varchar PK NOT NULL、`buyer_id` varchar NOT NULL、`cart_id` varchar NOT NULL、`status` varchar NOT NULL（`pending | paid | cancelled | expired`）、`subtotal_cents` int NOT NULL、`shipping_cents` int NOT NULL、`total_cents` int NOT NULL、`placed_at` datetime NOT NULL、`expires_at` datetime 可空、`cart_id` unique 名 `orders_cart_unique`
  - **References**: `contracts/schema.dbml#Table/buyers`
  - **References**: `contracts/schema.dbml#Table/products`
  - **References**: `contracts/schema.dbml#Table/carts`
  - **References**: `contracts/schema.dbml#Table/cart_lines`
  - **References**: `contracts/schema.dbml#Table/addresses`
  - **References**: `contracts/schema.dbml#Table/orders`
- [ ] T007 [P] 在 `backend/src/http/session.ts` 實作 `POST /session`：可選 body `email`（`maxLength: 254`）、回應 201 的 `SessionCreated` 只含 `buyerId`、以 cookie 名 `buyer_session` 設定 `HttpOnly; Secure（生產）; SameSite=Lax; Path=/`、不得把 opaque token 回給 JS；過度請求回 429 `ApiError`（`code`=`RATE_LIMITED` 與 `message`）
  - **References**: `contracts/openapi.yaml#/paths/~1session/post`
- [ ] T008 在 `backend/src/http/server.ts` 掛載 `POST /session`、`GET /health`（200 body `{ "status": "ok" }`）、以及 `GET /session`（回傳目前買家或 401），預設監聽 port 3000
  - **References**: `contracts/openapi.yaml#/paths/~1session/post`
  - **References**: `contracts/openapi.yaml#/paths/~1health/get`
  - **References**: `contracts/openapi.yaml#/paths/~1session/get`
- [ ] T009 [P] 在 `backend/src/http/errors.ts` 定義 `Money`（必要 `amountCents` integer minimum 0 與 `currency` length 3）與 `ApiError.code` 列舉：`CART_EMPTY`、`OUT_OF_STOCK`、`INVALID_QTY`、`PRODUCT_UNAVAILABLE`、`ADDRESS_INVALID`、`SHIPPING_UNAVAILABLE`、`SESSION_INVALID`、`ORDER_EXPIRED`、`RATE_LIMITED`
  - **References**: `contracts/openapi.yaml#/components/schemas/Money`
  - **References**: `contracts/openapi.yaml#/components/schemas/ApiError`
- [ ] T010 在 `backend/src/http/session.ts` 以同源 cookie `buyer_session` 辨識買家；缺少或無效 session 時回 `SESSION_INVALID`，只留下路由分派骨架、不實作各故事操作
  - **References**: `contracts/openapi.yaml#/paths/~1session/get`
- [ ] T011 [P] 在 `backend/src/cart/cart-view.ts` 定義 `CartView`（必要 `cartId`、`status` 列舉 `open|checked_out|expired`、`currency`、`lines`、`subtotalCents`、`shippingCents`、`totalCents`；`addressId` 可空）與 `OrderView`（必要 `orderId`、`status` 列舉 `pending|paid|cancelled|expired`、`subtotalCents`、`shippingCents`、`totalCents`、`placedAt`、`lines`），組裝函式不得讀取其他買家的 carts 或 addresses
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
  - **References**: `contracts/openapi.yaml#/components/schemas/OrderView`
- [ ] T012 [P] 在 `backend/src/db/snapshot.ts` 提供寫入 buyers／products／carts／cart_lines／addresses／orders 的函式；PostgreSQL 是權威資料
  - **References**: `techstack.md#採用技術/Persistence`
- [ ] T013 在 `backend/src/cart/cart-service.ts` 建立 `status` 型別（`open | checked_out | expired`），尚不實作加入商品、地址或結帳
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
- [ ] T014 [P] 在 `frontend/src/session.ts` 呼叫 `POST /session` 建立買家身分；不得讀取或寫入 `buyer_session` 到 localStorage／sessionStorage
  - **References**: `techstack.md#採用技術/Session Identity`
- [ ] T015 [P] 在 `frontend/src/api-client.ts` 以 `fetch` 呼叫同源 JSON API，解析成功 body，並把 `ApiError` 交給呼叫端
  - **References**: `contracts/openapi.yaml#/components/schemas/ApiError`
- [ ] T016 在 `frontend/src/main.ts` 依序建立 session，並留下依 `CartView.status`／`OrderView` 切換畫面的路由器骨架
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`

**Checkpoint**: 買家 session、資料庫、HTTP 與視圖型別可用；使用者故事可開始

---

## Phase 3: User Story 1 - 由待結帳購物車建立訂單（Priority: P1）🎯 MVP

**Goal**: 購物車已有明細、收件地址與配送方式時，買家可送出訂單；庫存足夠則建立待處理訂單、扣減庫存、購物車改為已結帳，應付總額為小計加運費。購物車是空的、沒有地址、沒有配送方式或庫存不足時拒絕，且不寫訂單

**Independent Test**: 直接種入 `carts.status=open`、已有 `cart_lines`、已有 `address_id` 與 `shipping_method` 的購物車，不需目錄畫面或地址表單。送出後產生 `orders.status=pending`、庫存減少、購物車改為 `checked_out`；空車回 `CART_EMPTY`、庫存不足回 `OUT_OF_STOCK`，且都不寫訂單、不改庫存

### 後端端點：商品、購物車與訂單 HTTP API

**Codebase**: `backend/src/orders/`、`backend/src/cart/`、`backend/src/http/`、`backend/tests/`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] T017 [P] [US1] 在 `backend/tests/unit/pricing.test.ts` 撰寫金額單元測試：明細金額為 `unit_price_cents * qty`、小計為明細加總、應付總額為小計加 `shipping_cents`（FR-US1-005）；相同明細與運費的結果可重現（NFR-US1-002）；`subtotalCents`／`shippingCents`／`totalCents` 皆為 integer minimum 0
  - **References**: `contracts/openapi.yaml#/components/schemas/OrderTotals`
- [ ] T018 [P] [US1] 在 `backend/tests/integration/place-order.test.ts` 撰寫 `POST /orders` 整合測試：合法購物車建立 `status=pending` 的訂單、扣減 `stock_qty`、購物車改為 `checked_out`（FR-US1-001、FR-US1-002）；總額等於小計加運費（FR-US1-005）；沒有明細回 `CART_EMPTY`、沒有地址回 `ADDRESS_INVALID`、沒有配送方式回 `SHIPPING_UNAVAILABLE`、數量大於庫存回 `OUT_OF_STOCK`，且都不寫訂單、不改庫存（FR-US1-003、FR-US1-004）
  - **References**: `contracts/openapi.yaml#/components/schemas/PlaceOrderRequest`

**Implementation**:

- [ ] T019 [P] [US1] 在 `backend/src/orders/pricing.ts` 實作純函式計價，以整數 cents 計算明細、小計與總額，回傳 `OrderTotals`
  - **References**: `contracts/openapi.yaml#/components/schemas/OrderTotals`
- [ ] T020 [US1] 在 `backend/src/cart/cart-service.ts` 實作 `place_order`：僅 `status=open` 且已有明細、`address_id`、`shipping_method` 可送出；否則 `CART_EMPTY`、`ADDRESS_INVALID` 或 `SHIPPING_UNAVAILABLE` 且不寫訂單；任一明細 `qty` 大於 `stock_qty` 則 `OUT_OF_STOCK` 且不扣庫存；合法則寫入 `orders`（`status=pending`、`placed_at` NOT NULL、`total_cents` 為小計加運費）、扣減庫存、購物車改為 `checked_out`。訂單明細沿用該 cart 的 `cart_lines`，單價使用加入時寫入的 `unit_price_cents`
  - **References**: `contracts/openapi.yaml#/components/schemas/PlaceOrderRequest`
- [ ] T021 [US1] 在 `backend/src/cart/cart-view.ts` 組裝 `OrderView`：含 `orderId`、`status`、`subtotalCents`、`shippingCents`、`totalCents`、`placedAt`，以及該購物車的明細（`sku`、`name`、`qty`、`unitPriceCents`）；只回傳這位買家自己的訂單
  - **References**: `contracts/openapi.yaml#/components/schemas/OrderView`
- [ ] T022 [US1] 在 `backend/src/http/router.ts` 分派 `POST /orders`，成功後回傳 `OrderView`
  - **References**: `contracts/openapi.yaml#/components/schemas/PlaceOrderRequest`

### 資料庫端點：PostgreSQL 持久化介面

**Codebase**: `backend/src/db/`

**Implementation**:

- [ ] T023 [US1] 在 `backend/src/db/snapshot.ts` 於合法結帳時寫入 `orders` 並扣減 `products.stock_qty`，保留 `orders.cart_id` unique
  - **References**: `contracts/schema.dbml#Table/orders`
  - **References**: `contracts/schema.dbml#Table/products`

### 前端端點：瀏覽器店面互動介面

**Codebase**: `frontend/src/`

**Implementation**:

- [ ] T024 [P] [US1] 在 `frontend/src/screens/checkout.ts` 依「結帳」呈現明細（例如 `馬克杯 × 2 · $12.00`）、小計、運費、應付總額與「送出訂單」；購物車是空的或請求被拒時停用提交並顯示 `error.message`
  - **References**: `contracts/interface.pen#checkout`
- [ ] T025 [US1] 在 `frontend/src/main.ts` 收到可結帳的 `CartView` 時顯示 `frontend/src/screens/checkout.ts`，並在 2 秒目標內呈現送出後的 `OrderView`（NFR-US1-001）
  - **References**: `contracts/interface.pen#checkout`

**Checkpoint**: User Story 1 可藉種入待結帳購物車獨立驗證，不依賴目錄或地址 UI

---

## Phase 4: User Story 2 - 瀏覽上架商品並加入購物車（Priority: P2）

**Goal**: 買家可依分類列出上架商品，並以數量加入目前購物車；同一商品再次加入時合併數量。下架商品與小於 1 的數量不得加入

**Independent Test**: 已有 session 的買家呼叫 `GET /products` 只看到 `published`。對上架商品 `POST /cart/lines` 後數量增加，再次加入同一商品時合併成一列。`archived` 回 `PRODUCT_UNAVAILABLE`，數量 0 回 `INVALID_QTY`。不需結帳

### 後端端點：商品、購物車與訂單 HTTP API

**Codebase**: `backend/src/catalog/`、`backend/src/cart/`、`backend/src/http/`、`backend/tests/`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] T026 [P] [US2] 在 `backend/tests/unit/catalog-filter.test.ts` 撰寫目錄篩選測試：只保留 `status=published`；`category` 須完全相符，不得模糊比對
  - **References**: `contracts/openapi.yaml#/components/schemas/Product`
- [ ] T027 [P] [US2] 在 `backend/tests/integration/add-cart-line.test.ts` 撰寫 `GET /products` 與 `POST /cart/lines` 整合測試：目錄只回上架商品（FR-US2-001）；上架商品以 `qty` 加入，同一 `productId` 再次加入時合併數量並保留第一次的 `unit_price_cents`（FR-US2-002）；`archived` 回 `PRODUCT_UNAVAILABLE`（FR-US2-003）；`qty` 小於 1 回 `INVALID_QTY` 且不寫明細（FR-US2-004）
  - **References**: `contracts/openapi.yaml#/components/schemas/AddCartLineRequest`

**Implementation**:

- [ ] T028 [P] [US2] 在 `backend/src/catalog/product-query.ts` 查詢 `status=published` 的商品，有 `category` 時只回完全相符的分類
  - **References**: `contracts/openapi.yaml#/components/schemas/Product`
- [ ] T029 [US2] 在 `backend/src/cart/cart-service.ts` 實作 `add_line`：`qty` 為 integer minimum 1，否則 `INVALID_QTY`；商品不是 `published` 則 `PRODUCT_UNAVAILABLE` 且不寫明細；尚無 open cart 則建立一筆；同一商品合併 `qty`，`unit_price_cents` 以第一次加入時的單價為準
  - **References**: `contracts/openapi.yaml#/components/schemas/AddCartLineRequest`
- [ ] T030 [US2] 在 `backend/src/cart/cart-view.ts` 組裝 `CartView`：`CartLineView` 必要 `productId`、`sku`、`name`、`qty`、`unitPriceCents`、`lineTotalCents`，並含小計，供買家看到加入後的購物車（FR-US2-005）
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
  - **References**: `contracts/openapi.yaml#/components/schemas/CartLineView`
- [ ] T031 [US2] 在 `backend/src/http/router.ts` 分派 `GET /products` 與 `POST /cart/lines`，加入成功後回傳 `CartView`
  - **References**: `contracts/openapi.yaml#/components/schemas/AddCartLineRequest`

### 資料庫端點：PostgreSQL 持久化介面

**Codebase**: `backend/src/db/`

**Implementation**:

- [ ] T032 [US2] 在 `backend/src/db/snapshot.ts` 於建立購物車與加入明細時持久化 `carts` 與 `cart_lines`；同一 `(cart_id, product_id)` 只保留一列
  - **References**: `contracts/schema.dbml#Table/carts`
  - **References**: `contracts/schema.dbml#Table/cart_lines`

### 前端端點：瀏覽器店面互動介面

**Codebase**: `frontend/src/`

**Implementation**:

- [ ] T033 [P] [US2] 在 `frontend/src/screens/catalog.ts` 實作「商品目錄」：標題「商品目錄」、分類篩選、每列顯示名稱、價格與庫存，按鈕「加入購物車」，送出 `POST /cart/lines`
  - **References**: `contracts/interface.pen#catalog`
- [ ] T034 [P] [US2] 在 `frontend/src/screens/cart.ts` 實作「購物車」：顯示明細、數量、小計，以及「前往結帳」
  - **References**: `contracts/interface.pen#cart`
- [ ] T035 [US2] 在 `frontend/src/main.ts` 於尚未結帳時可開啟目錄與購物車，加入失敗時顯示 `error.message`（`PRODUCT_UNAVAILABLE`、`INVALID_QTY`）
  - **References**: `contracts/interface.pen#cart`

**Checkpoint**: User Story 2 可獨立驗證目錄篩選與加入購物車，不需送出訂單

---

## Phase 5: User Story 3 - 設定收件地址與配送方式（Priority: P3）

**Goal**: 買家儲存收件地址並選擇配送方式，購物車顯示對應運費；地址缺城市或配送方式不可用時拒絕，且尚未建立訂單

**Independent Test**: 種入已有明細的 `status=open` 購物車。儲存完整地址後可選 `standard` 或 `express`，購物車出現對應 `shippingCents`；缺 `city` 回 `ADDRESS_INVALID`；不存在的方式回 `SHIPPING_UNAVAILABLE`。不需 `POST /orders`

### 後端端點：商品、購物車與訂單 HTTP API

**Codebase**: `backend/src/cart/`、`backend/src/http/`、`backend/tests/`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] T036 [P] [US3] 在 `backend/tests/integration/address-shipping.test.ts` 撰寫地址與配送測試：完整地址可儲存並標成預設（FR-US3-001）；`standard` 運費 500、`express` 運費 1500，寫入後 `CartView` 的總額等於小計加運費（FR-US3-002）；缺 `city` 回 `ADDRESS_INVALID` 且不寫地址（FR-US3-003）；方式不是 `standard|express` 回 `SHIPPING_UNAVAILABLE` 且不改運費（FR-US3-004）；清除地址後 `addressId` 為 null、`shippingCents` 回到 0，必須重新儲存並再次選擇配送才可結帳
  - **References**: `contracts/openapi.yaml#/components/schemas/SaveAddressRequest`
  - **References**: `contracts/openapi.yaml#/components/schemas/SelectShippingRequest`

**Implementation**:

- [ ] T037 [US3] 在 `backend/src/cart/cart-service.ts` 實作 `save_address`：`recipientName`、`line1`、`city`、`postalCode`、`countryCode` 皆必填；`city` 為空則 `ADDRESS_INVALID` 且不寫入；成功時寫入 `addresses` 並可把 `is_default` 設為 true
  - **References**: `contracts/openapi.yaml#/components/schemas/SaveAddressRequest`
- [ ] T038 [US3] 在 `backend/src/cart/cart-service.ts` 實作 `select_shipping`：`shippingMethod` 僅 `standard` 或 `express`，否則 `SHIPPING_UNAVAILABLE`；`standard` 寫入 `shipping_cents=500`、`express` 寫入 `shipping_cents=1500`
  - **References**: `contracts/openapi.yaml#/components/schemas/SelectShippingRequest`
- [ ] T039 [US3] 在 `backend/src/cart/cart-service.ts` 把所選運費寫進 open cart，使 `CartView.totalCents` 等於小計加 `shipping_cents`
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
- [ ] T040 [US3] 在 `backend/src/cart/cart-service.ts` 實作清除地址：`address_id` 與 `shipping_method` 改回空值、`shipping_cents` 改回 0；之後必須重新 `save_address` 且再次 `select_shipping` 才可結帳
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
- [ ] T041 [US3] 在 `backend/src/cart/cart-view.ts` 確保 `CartView` 只含這位買家自己的地址與運費，組裝時不得讀取其他買家的 `addresses` 列
  - **References**: `contracts/openapi.yaml#/components/schemas/CartView`
- [ ] T042 [US3] 在 `backend/src/http/router.ts` 分派 `PUT /cart/address` 與 `PUT /cart/shipping`，成功後回傳更新後的 `CartView`
  - **References**: `contracts/openapi.yaml#/components/schemas/SaveAddressRequest`
  - **References**: `contracts/openapi.yaml#/components/schemas/SelectShippingRequest`

### 資料庫端點：PostgreSQL 持久化介面

**Codebase**: `backend/src/db/`

**Implementation**:

- [ ] T043 [US3] 在 `backend/src/db/snapshot.ts` 於 `save_address`、`select_shipping` 與清除地址時持久化 `addresses`、`carts` 的 `address_id`／`shipping_method`／`shipping_cents`，以及 `buyers.default_address_id`
  - **References**: `contracts/schema.dbml#Table/addresses`
  - **References**: `contracts/schema.dbml#Table/carts`
  - **References**: `contracts/schema.dbml#Table/buyers`

### 前端端點：瀏覽器店面互動介面

**Codebase**: `frontend/src/`

**Implementation**:

- [ ] T044 [P] [US3] 在 `frontend/src/screens/address.ts` 實作「收件與配送」：欄位收件人、地址、城市、郵遞區號、國家代碼，配送選項「標準配送」「快速配送」並顯示運費，按鈕「儲存並繼續」
  - **References**: `contracts/interface.pen#address`
- [ ] T045 [US3] 在 `frontend/src/main.ts` 於購物車已有明細且尚未有地址時顯示地址畫面，儲存並選好配送後改顯示結帳畫面；拒絕時顯示缺欄位或配送方式不可用
  - **References**: `contracts/interface.pen#address`
  - **References**: `contracts/interface.pen#checkout`

**Checkpoint**: User Stories 1、2、3 皆可獨立驗證；串起來即為目錄 → 購物車 → 地址與配送 → 結帳

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: 未付款訂單保留 30 分鐘、一致錯誤文案、瀏覽器版面與可量測回應時間

### 後端端點：商品、購物車與訂單 HTTP API

**Codebase**: `backend/src/cart/`、`backend/src/http/`、`backend/tests/`

**Tests**:

> **NOTE: 先寫這些測試並確認失敗，再寫本端與後續端點的實作**

- [ ] T046 [P] 在 `backend/tests/integration/order-hold.test.ts` 先寫保留測試：`pending` 訂單在 30 分鐘內仍可讀到原明細與總額；超過 30 分鐘回 `ORDER_EXPIRED`，訂單改為 `expired` 並把庫存加回（NFR-G-003、NFR-G-002）
  - **References**: `contracts/openapi.yaml#/components/schemas/ApiError`
- [ ] T047 [P] 在 `backend/tests/integration/response-time.test.ts` 斷言本機結帳路徑低於 2 秒（NFR-US1-001）、加入購物車與儲存地址低於 2 秒（NFR-US2-001、NFR-US3-001）
  - **References**: `techstack.md#採用技術/HTTP API`

**Implementation**:

- [ ] T048 在 `backend/src/cart/cart-service.ts` 以 `orders.expires_at` 實作 30 分鐘未付款保留；逾時將訂單標為 `expired`、加回庫存並呼叫快照
  - **References**: `techstack.md#採用技術/Order Hold`
- [ ] T049 在 `backend/src/http/session.ts` 於已登入請求更新 `buyers.last_seen_at`，之後的讀取仍回傳目前 `CartView` 或 `OrderView`
  - **References**: `contracts/openapi.yaml#/paths/~1session/get`

### 資料庫端點：PostgreSQL 持久化介面

**Codebase**: `backend/src/db/`

**Implementation**:

- [ ] T050 在 `backend/src/db/snapshot.ts` 於請求與逾時釋放時持久化 `last_seen_at`，並將 `orders.status` 寫為 `expired`
  - **References**: `contracts/schema.dbml#Table/buyers`
  - **References**: `contracts/schema.dbml#Table/orders`

### 前端端點：瀏覽器店面互動介面

**Codebase**: `frontend/src/`

**Implementation**:

- [ ] T051 [P] 在 `frontend/src/screens/checkout-error.ts` 實作「結帳與操作錯誤」：標題「無法完成操作」、說明未付款訂單保留 30 分鐘，並顯示 `CART_EMPTY`、`OUT_OF_STOCK`、`PRODUCT_UNAVAILABLE`、`ADDRESS_INVALID`、`ORDER_EXPIRED` 的 `message`
  - **References**: `contracts/interface.pen#checkout-error`
- [ ] T052 [P] 在 `frontend/src/styles.css` 讓目錄、購物車、地址、結帳、錯誤五個畫面在寬度 390px 的行動版面與桌面瀏覽器都可完成操作（NFR-G-001）
  - **References**: `contracts/interface.pen#catalog`
  - **References**: `contracts/interface.pen#cart`
  - **References**: `contracts/interface.pen#address`
  - **References**: `contracts/interface.pen#checkout`
  - **References**: `contracts/interface.pen#checkout-error`
- [ ] T053 在 `frontend/src/main.ts` 將拒絕操作與逾時連到 `frontend/src/screens/checkout-error.ts`，使買家知道目前能否繼續瀏覽、改購物車或結帳（NFR-G-002）
  - **References**: `contracts/interface.pen#checkout-error`

### 環境：單實例啟動

**Codebase**: `specs/001-store-checkout/quickstart.md`

- [ ] T054 在 `specs/001-store-checkout/quickstart.md` 撰寫單一 Node 程序與 PostgreSQL 的啟動步驟（含 `DATABASE_URL`、port 3000、Vite 5173 同源代理），不描述多實例
  - **References**: `techstack.md#採用技術/Deployment (v1)`

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 無前置，可立即開始
- **Foundational (Phase 2)**: 依賴 Setup；完成前阻擋全部使用者故事
- **User Stories (Phase 3+)**: 都依賴 Foundational
  - 故事邏輯可獨立驗證（US1 用種入的待結帳購物車、US2 只用目錄與加入購物車、US3 用種入的有明細購物車）
  - `backend/src/cart/cart-service.ts`、`backend/src/http/router.ts`、`backend/src/cart/cart-view.ts`、`backend/src/db/snapshot.ts`、`frontend/src/main.ts` 跨故事共用，這些檔案的任務須依 US1 → US2 → US3 順序改
- **Polish (Phase 6)**: 依賴希望交付的使用者故事都完成

### User Story Dependencies

- **User Story 1 (P1)**: Foundational 之後即可開始；不依賴 US2／US3 的 UI。整合測試自行插入 open cart、明細、地址、配送方式與庫存
- **User Story 2 (P2)**: Foundational 之後即可開始；不依賴結帳與地址。與 US1 同時改購物車服務檔會衝突，應在 US1 的該檔任務之後接上
- **User Story 3 (P3)**: Foundational 之後可用種入的有明細購物車獨立測試；使用者可見的完整路徑是 US2 加入商品之後才進入地址。運費與地址會被 US1 的結帳讀取

### Within Each User Story

- 該故事的測試寫在擁有該行為的端點小節裡，先寫並失敗，再實作該端與後續端點
- 純函式（計價、目錄篩選）先於服務轉換
- 服務轉換先於快照、視圖與路由分派
- 前端畫面檔可在契約型別就緒後與後端純函式平行；接到 `main.ts` 須等畫面檔完成
- 執行某個任務時只讀該任務列出的位址，不讀同一份文件裡沒被點名的 schema、資料表或畫面

### Parallel Opportunities

- T003 與 T002 可平行；T004 與 T002／T003 可平行
- T007、T009、T011、T012、T014、T015 在 T006 之後可平行
- T017 與 T018 可平行；完成後 T019 與 T024 可平行
- T026 與 T027 可平行；完成後 T028、T033、T034 可平行
- T036 完成後 T044 可與後端服務任務平行（不同檔）
- T046、T047、T051、T052 可平行

---

## Parallel Example: User Story 1

```bash
# 先一起寫 US1 測試並確認失敗：
Task: "在 backend/tests/unit/pricing.test.ts 撰寫金額單元測試"
Task: "在 backend/tests/integration/place-order.test.ts 撰寫 POST /orders 整合測試"

# 測試就位後，計價純函式與結帳畫面可平行：
Task: "在 backend/src/orders/pricing.ts 實作純函式計價"
Task: "在 frontend/src/screens/checkout.ts 實作結帳畫面"
```

## Parallel Example: User Story 2

```bash
Task: "在 backend/tests/unit/catalog-filter.test.ts 撰寫目錄篩選測試"
Task: "在 backend/tests/integration/add-cart-line.test.ts 撰寫加入購物車整合測試"

Task: "在 backend/src/catalog/product-query.ts 實作上架商品查詢"
Task: "在 frontend/src/screens/catalog.ts 實作商品目錄"
Task: "在 frontend/src/screens/cart.ts 實作購物車"
```

## Parallel Example: User Story 3

```bash
Task: "在 backend/tests/integration/address-shipping.test.ts 撰寫地址與配送測試"
Task: "在 frontend/src/screens/address.ts 實作收件與配送畫面"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. 完成 Phase 1: Setup
2. 完成 Phase 2: Foundational（阻擋所有故事）
3. 完成 Phase 3: User Story 1
4. **STOP and VALIDATE**: 以種入的待結帳購物車獨立跑 `place-order` 測試，確認總額、扣庫存、已結帳，以及空車與庫存不足被拒絕
5. 通過後再擴充目錄與地址

### Incremental Delivery

1. Setup + Foundational → 基礎可用
2. User Story 1 → 獨立驗證結帳與庫存 → MVP
3. User Story 2 → 獨立驗證目錄與加入購物車 → 可演示選商品進購物車
4. User Story 3 → 獨立驗證地址與運費 → 串起 spec 的完整路徑（目錄 → 購物車 → 地址與配送 → 結帳）
5. Polish → 30 分鐘未付款保留、錯誤畫面、回應時間上限與 quickstart

### Parallel Team Strategy

多人時仍先一起完成 Setup + Foundational。之後：

- 可平行的是各故事的測試、`pricing.ts`、`product-query.ts`，以及 `checkout.ts`／`catalog.ts`／`cart.ts`／`address.ts`
- `cart-service.ts`、`router.ts`、`cart-view.ts`、`snapshot.ts`、`main.ts` 請依 US1 → US2 → US3 由同一條變更序列修改，避免互相覆蓋

---

## Notes

- [P] 代表不同檔案且不依賴尚未完成的任務
- [US1]／[US2]／[US3] 對應 spec.md 的三則使用者故事
- 金額以最小貨幣單位（cents）的整數計算；加入購物車時快照 `unit_price_cents`
- 只有 `published` 商品可加入購物車；庫存不足不得建立訂單
- 初版只有單一 Node 程序與 PostgreSQL，不實作水平擴展
- 每個故事的檢查點都應能單獨停下來驗證
