# Volcatech 官網風格 Demo 接手指引 (Handover)

> **最後更新**：2026-08-10
> **本檔定位**：進度速查與接手指令集。
> **規格正本是 `docs/Volcatech_多風格_Build_Prompts.md`**——本檔與它衝突時，一律以它為準。
> 唯一例外：該檔 §B 的 style-3 選單定義（`Platform / Arsenal / Operations`）是**評選期歷史**，
> 0731 會後現行選單以 `style-3-soc/` 頁面為準（見下方 §2）。
> **例外資料夾**：`archive/` 是已凍結的評選歷史（含外部 AI 參考組
> `archive/Volcatech_Layout_Variants_GPT/`，唯讀、不異動也不 review，
> 規則見 `CLAUDE.md` 的「外部 AI 參考組」專節）；本檔所有任務與檢查指令皆不涵蓋它。

---

## 1. 目前狀態

**2026-07-31 內部評選已結束**：勝出組合＝**Style 3（SOC Console 深色色系）× 原版直落版型**，色系凍結。
**2026-08-05 會議又定案三件事**（結算正本：`docs/meeting_0805_end.md`）：①首頁收斂為兩案；
②選單改三層、第一層不可點、全站統一 Nav B；③內容頁改版——**0806 定案走守硬性規則的
inline CSS 版**（`lab/` 的 Tailwind 版落選），16 個內容頁與首頁已全數改用區塊元件。
**2026-08-12 新增視覺方向 A/B 提案**（`lab/restyle-0812/`，**待裁決**）：起點是
`docs/reports/refero_design風格範本調查_20260811.md`，使用者挑了 Supabase 與 Harness.io 兩個範本，
經四輪 grilling 裁決為**吸收手法、微調現行**（不換皮）。A ＝ 色彩用量（7 條 CSS，零解凍）；
B ＝ 表面與形態 ＋ **19 個 font-size 值收斂成 8 級階梯**（只有背景加深需解凍）。
範例頁 `<main>` 與正式頁逐字節相同、只有 CSS 不同。設計文件在 `docs/design/`，
「色系凍結」的範圍首次被定義於 `docs/adr/0005-colour-freeze-scope.md`。
**2026-08-10 第二輪**再定案 ArgusHack 重定位（決議 16–24，正本 `docs/meeting_0810.md` 附錄二）：
原 `CE-BAS` 經查證**不是沃凱自研**（原廠盧氪賽忒 Leukocyte-Lab，沃凱代理）→ 更名 **ArgusHack**、
升格獨立產品頁、選單第三組改為 `Validation — breach & attack simulation`、
首頁第 4 區改「我們自己維運」定位；`AI-PTaaS`／`SecPurple` 因素材不足全站移除。
細節見下方〈本輪完成的事（2026-08-10 第二輪）〉。

**2026-08-14 客戶 demo 前整備**（見下方〈本輪完成的事（2026-08-14）〉）：站上 384 處 `[TODO]`
降到 0（僅 `index-v1-proof.html` 刻意保留 10 處，且它已無任何入口連結）；頁尾法定資訊補實；
新增 `privacy.html` 與 `imprint.html`；移除「Demo notice」自白段、backlink 導覽列、
點不動的語言切換與 FortiEDR。**待補素材清單：`docs/待補素材清單_20260814.md`**（不進版控）。

現行維護對象 `style-3-soc/`，**共 40 頁**（0810 `argushack.html`；0813 `managed-gcp.html`；
0814 `privacy.html` ＋ `imprint.html`）：

- **2 個首頁**：`index.html`（現行版）、`index-v1-proof.html`（V1 信任前置，
  由 `docs/reports/build_v1_20260806.py` 產生，**不得手改**）。
- **3 個總覽頁**：`cloud.html`（CI）、`cybersecurity.html`（CS）、`services.html`（MS）。
- **7 個 GCP 分類頁**：`cloud-compute` / `cloud-storage` / `cloud-analytics` /
  `cloud-serverless` / `cloud-databases` / `cloud-ai` / `cloud-services`（CI-01〜07）。
- **19 個 GCP 產品頁**（2026-08-06 補齊，選單第三層）：18 個 GCP 產品各一頁，
  ＋ `gcp-cloud-armor.html`（**孤兒頁**：它所屬的 Edge security 那組已於 0805 移出選單，
  入口在 `cloud-services.html#cloud-armor` 與 `cloud.html` 的產品索引）。
  全部由 `build_gcp_pages_20260806.py` 的 `PAGES` 產生，**不要手改頁面**。
- **5 個資安產品頁**（0814 起選單與頁面皆無 FortiEDR）：`sentinelone` / `threatsonar` / `cybereyes` / `google-secops`
  ＋ **`argushack`（2026-08-10 新建**，BAS；原廠 Leukocyte-Lab，沃凱代理）；＋方案頁 `ess.html`。
- **1 個服務頁**：`managed-gcp.html`（MS-01，2026-08-13 新建；GCP 遷移與維運，
  素材出自地轉雲企劃書，內容正本 `docs/地轉雲線_內容規劃_20260813.md`；**手維護頁**，非產生器產出）。
- **2 個法務頁**（2026-08-14 新建）：`privacy.html`、`imprint.html`，
  由 `docs/reports/build_legal_pages_20260814.py` 以 `sentinelone.html` 為底檔產生，
  **不得手改**。入口在每頁頁尾，刻意不進選單，兩者都登記為孤兒頁。
- **全 40 頁選單統一為三層 Nav B**，不再有 Nav A。**0814 起全站無灰字項、無語言切換**。

**內容充實狀態（2026-08-11）**：19 個 GCP 產品頁**全部完成**（每頁 FAQ +2～3、規格 +2，
其中 12 頁有 SVG 示意圖、4 頁依「誠實優先」判定不做圖）；5 個資安產品頁與 ESS 皆有
`#pain`／`#pick`／`#faq` 三段決策支援內容。**根 `index.html` 已改造成進度儀表板**
（待做事項 ＋ 27 列產品表，正本 `docs/reports/build_updates_20260810.py`，
帶全專案唯一的行內 JS 破例；0814 修掉一個自 0813 起讓它 IndexError 跑不動的欄位位移 bug）。

另有 `lab/` 4 個檔（當初的兩案對照，**已定案走 inline 版**，留檔備查、隨時可刪）。
落選的 3 個風格、4 個版型變體、GPT 參考包，以及 0805 封存的 6 個首頁變體檔
（`archive/style-3-homepage-variants/`）都在 `archive/`（凍結）；
封存總覽為 `archive/index.html`；根 `index.html` 是 Demo hub。

### 定調的資訊架構（沿用不變）

- **3 條業務板塊**：`Cloud Infrastructure` / `Cybersecurity` / `Managed Services`
- **19 項服務**（清單與 slug 見規格正本 §A）：Cloud 6 + Cybersecurity 8 + Managed 5。
  **註（2026-08-04 定案）**：§A 的 SKU 代碼體系（`C-01`〜`C-06` 等）為 **pre-0731 歷史體系**，
  保留封存、不對齊、不上站；現行採**頁面層代碼**（Cloud 線＝`CI`／`CI-01`〜`CI-07`）。
  Cloud 線已由這 8 頁涵蓋，不再依 §A 的 Cloud 6 個 slug 逐項建頁。
- Cybersecurity 底下的第三個群組是 **Validation — breach & attack simulation**（ArgusHack）。
  ⚠ **2026-08-10 變更**：這一組原本叫「Built in-house — Volcatech AI Security」、掛
  CE-BAS / AI-PTaaS / SecPurple。查證確認 CE-BAS 的原廠是**盧氪賽忒（Leukocyte-Lab）**、
  沃凱是**代理商**，自研宣稱不成立 → 更名 **ArgusHack** 並升格獨立頁；
  AI-PTaaS / SecPurple 因**素材不足**（非否定其自研）全站移除，素材到位可加回。
  首頁仍有專屬的第 4 區（id `#built`）——現在的定位是「我們自己維運、自己驗證」，
  不再宣稱自研；它不是第 4 條產品線，**不進頂層導覽**
- H1 逐字定稿不變：`Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
- **section 順序不變**：`top` → `offer` → `built` → `why` → `trust` → `vendors` → `contact` → `legal`

### 0731 會後完成的事

1. **選單分類改名**：`Platform / Arsenal / Operations` → `Google Cloud / CyberSecurity / Services`
   （`CyberSecurity` 駝峰是會議指定的刻意寫法）。每個下拉第一行仍是 mono 白話對照。
   `Google Cloud` 下拉改為 **GCP 產品樹 6 組 18 項**（Compute / Storage / Analytics /
   Serverless / Databases / AI）——**當時狀態**，2026-08-04 已擴充為八組 22 項且全部連真頁，
   見下方本輪紀錄；`CyberSecurity` 維持原 8 項（EDR / SIEM / Built in-house
   三組）；`Services` 維持原 5 項。
2. **選單雙變體**：`index.html`＝Nav A（單層下拉、mono 小標分組）；`index-nav-b.html`＝Nav B
   （分組升級為第二層 flyout，hover / `:focus-within` 展開）；`sentinelone.html` 用 Nav A。
   兩首頁自 `<main>` 起**逐字節相同**（新一致性鐵則）。
   ⚠ **已於 2026-08-06 退場**：Nav B 勝出並升級為三層，Nav A 與 `index-nav-b.html` 都不再存在
   （後者已封存至 `archive/style-3-homepage-variants/`），該條鐵則由「全站 header 同源」取代。
3. **首頁 hero 文案（H1／副標／CTA）改置中**。
4. **歸檔**：style-1／2／4、layout 四個變體、GPT 參考包 → `archive/`；
   補建先前文件宣稱有但實際缺失的 `.nojekyll`。GitHub Pages 部署方式不變，
   `style-3-soc/` 線上路徑不變，被歸檔頁面的網址前多一層 `/archive/`。

（第一、二輪評選期間的完成事項——3 板塊重構、19 項服務擴充、四風格 Top Menu 差異化、
歐規頁尾、無障礙修正、文件收斂等——紀錄已隨頁面歸檔，詳見 git 歷史與 `archive/`。）

### 本輪完成的事（2026-08-03，commit 38ea337／c6116f8／5316d78）

1. **SIEM 群組改名「Detection — SIEM & WDR」**（38ea337）：CyberEyes 實為 WDR；
   下拉 head 白話行改「CyberSecurity — EDR · SIEM & WDR · Built in-house」，
   hero 的 Cybersecurity 卡文案改「EDR, SIEM and WDR from …」。
2. **新增 3 個產品頁**（c6116f8）：`threatsonar.html`、`cybereyes.html`、`google-secops.html`；
   ThreatSonar／CyberEyes／Google SecOps 在全站 nav 與 footer `#security-list` 都連真頁。
   `sentinelone.html` 功能卡 4→6（補 Vulnerability visibility、Device & network control）。
3. **新增 ESS 方案頁**（5316d78）：`ess.html`。**ESS（Enterprise Security Service）是沃凱
   打包方案**（CyberEyes WDR＋多品牌 EDR＋自有 7x24 SOC）——**方案層，非 19 項 SKU**；
   全頁零外部連結；入口在 `Services` 下拉最上方「Enterprise Security Service (ESS)」＋
   footer `#managed-list` 置頂，全站 7 檔同步（當時檔數）。
4. 根 `index.html`（Demo hub）主卡改為 7 連結（Nav A／Nav B／4 產品頁／ESS，當時狀態），
   說明文字同步。
5. 產品素材內部文件：`docs/product/`（gitignored）新增 7 個 md——README（索引＋紅線）、
   5 份產品簡述、`產品簡介總覽.md`（素材統一入口，文件提到素材正本時指向它）。

### 本輪完成的事（2026-08-04，Cloud 線建置；e5efa7b）

1. **新增 8 個 Cloud 頁**，`style-3-soc/` 由 7 檔增為 **15 檔**；全部用 Nav A：

   | 檔名 | 代碼 | h1 | 收錄 |
   |---|---|---|---|
   | `cloud.html` | CI | Cloud Infrastructure | 總覽：六分類導覽＋沃凱服務 |
   | `cloud-compute.html` | CI-01 | Compute on Google Cloud | Compute Engine／Kubernetes Engine／VMware Engine |
   | `cloud-storage.html` | CI-02 | Storage on Google Cloud | Cloud Storage／Filestore／Backup and DR |
   | `cloud-analytics.html` | CI-03 | Analytics on Google Cloud | BigQuery／Pub/Sub／Dataflow |
   | `cloud-serverless.html` | CI-04 | Serverless on Google Cloud | Cloud Run／App Engine／API Gateway |
   | `cloud-databases.html` | CI-05 | Databases on Google Cloud | AlloyDB／Cloud SQL／Datastore／Firestore |
   | `cloud-ai.html` | CI-06 | AI on Google Cloud | Vertex AI／Model Garden |
   | `cloud-services.html` | CI-07 | Cloud services and edge security | Cloud Armor＋沃凱雲端服務 3 項 |

2. **`Google Cloud` 下拉由「六組 18 項全是 `#offer` 佔位」改為八組 22 項且全部連真頁**
   （⚠ 這是 08-04 當時狀態；**08-05 已移除其中兩組**，現行是六組 18 項，見下方 08-05 紀錄）：
   原六組 18 項改為**深連結**（`分類頁#產品錨點`，例 `cloud-compute.html#compute-engine`），
   新增 `Edge security` 1 項與 `Volcatech cloud services` 3 項，下拉頂部另加 Overview 入口
   指向 `cloud.html`。**Google Cloud 線至此零佔位連結。**
3. **footer「Cloud Infrastructure」欄改為 8 行分類連結**（Overview／Compute／Storage／
   Analytics／Serverless／Databases／AI／Cloud services & Cloud Armor），
   取代舊的 6 項 SKU 列法（Compute Engine (VM)／Cloud SQL (Database)／Cloud Armor (WAF)／
   Cloud Migration & Kubernetes／Hybrid Cloud & Backup／Data & AI Engineering）。
4. **CSS 兩處調整**：全 15 檔加 `main [id]{scroll-margin-top:80px}`（深連結錨點不被 sticky
   header 遮住）；Nav A 的 `.dd ul` 加 `max-height:calc(100vh - 90px);overflow-y:auto`
   （22 項＋分組小標共 32 列會溢出視窗；**此為 08-04 當時列數，08-05 移除兩組後為 26 列**）。
   **Nav B 刻意不加**——加了會裁掉二層 flyout。
5. **SKU 代碼體系定案**：舊 §A 的 `C-01`〜`C-06` 等為 pre-0731 歷史體系，保留封存、
   不對齊、不上站；現行 Cloud 線用頁面層代碼 `CI`／`CI-01`〜`CI-07`。
6. 根 `index.html`（Demo hub）主卡擴為 15 連結；`CLAUDE.md` 同步更新。
7. **已知待補**：`cloud-services.html` 的沃凱自有服務 3 項（Cloud Migration & Kubernetes／
   Hybrid Cloud & Backup／Data & AI Engineering）內文為 `[TODO: service description]`——
   本次使用者指示不參考 `docs/公司_104.md`，目前無素材，屬待補項而非疏漏。
8. Cloud 線內容正本為內部文件 `docs/Cloud線_內容規劃_20260804.md`（gitignored，勿在頁面連結它）。

### 本輪完成的事（2026-08-04 下午，首頁版面變體）

> ⚠ 這是 08-04 當時狀態。**08-05 已收斂為 2 案**（V2/V3 封存）、**08-06 選單改三層 Nav B**，
> 下文的「8 個首頁」「23 檔」「Nav A/B」皆為歷史；現況見上方 08-06 那節與 §2。

**起因**：盤點現行首頁後找到三個結構性病灶（不是文案問題）——
①「產品有哪些」動線斷在頁尾錨點（三張卡只有 Cloud 有真總覽頁，另有 9 個項目完全沒落點）；
②「合作夥伴」只有六個純文字品牌名、不能點也沒說明；
③「公司做什麼」完全沒有交付流程段落，而這對 DACH／北歐採購的權重高於產品規格。

1. **新增 2 個總覽頁**：`cybersecurity.html`（CS，8 產品分 3 群、11 個錨點）、
   `services.html`（MS，6 服務、6 個錨點）。三條業務線至此都有真落點。
2. **全站 23 檔動線修復**：原本指向 `#offer` / `#built` 的**約 300 個佔位連結**改成深連結；
   CyberSecurity / Services 兩個下拉頂部各加 Overview 入口；頁尾三個欄標題變成連結。
   腳本：`docs/reports/sync_nav_20260804.py`。
3. **3 個首頁版面變體 × Nav A/B = 6 個新檔**（見下方 §版面變體）。
4. 根 `index.html` 改造成四方案橫向比較；8 個首頁底部加 backlink 切換列。
5. `CLAUDE.md` 的「兩變體一致性鐵則」改寫為**雙軸**（軸 1 同版面 A/B 逐字節相同、
   軸 2 跨版面凍結共用文案）。舊的單軸鐵則對多版面比對已失效。
6. **已知待補**：Managed Services 五項服務（SOC／ISMS／Pentest／FinOps／DX）與 FortiEDR
   無素材，內文一律 `[TODO]`；合作夥伴等級、ISO 27001、EU region、交付模式、SLA 同樣待確認。

### 本輪完成的事（2026-08-05，選單精簡）

> ⚠ 這是 08-05 當時狀態。**08-06 選單已重寫為三層 Nav B**，下文的「Nav A 共 26 列」與
> `remove_gcp_groups_20260805.py`（已封印）皆為歷史；移除兩組的結果現在直接體現在
> `rebuild_nav_20260806.py` 的 MENU 定義裡。

使用者指示：從 `Google Cloud` 下拉移除 **`Edge security`**（Cloud Armor）與
**`Volcatech cloud services`**（Cloud Migration & Kubernetes／Hybrid Cloud & Backup／
Data & AI Engineering）兩組，下拉由八組 22 項回到 **六組 18 項**（Nav A 共 26 列）。

**範圍僅限選單**（使用者明確裁決「只動選單」）——以下一律保留不動：
頁尾 Cloud Infrastructure 欄的「Cloud services & Cloud Armor」那列、`cloud.html` 內
指向 Cloud Armor 與沃凱服務的區塊、`cloud-services.html` 頁面本身（含 22 個錨點 id）。
因此 `cloud-services.html` 現在的入口是頁尾與 `cloud.html`，不在下拉選單內。

腳本：`docs/reports/remove_gcp_groups_20260805.py`（可重複執行；Nav A 刪 `li.grp` 區塊、
Nav B 刪兩個 `li.sub` flyout 區塊，全 23 檔每檔恰好命中一次）。
**已驗**：軸 1 四組全綠、軸 2 五句 8/8＋核心句 6、24 檔連結與錨點全可解析、
頁尾 14 檔逐字節相同、重跑 `build_variants_20260804.py` 後 6 個變體檔 md5 不變
（證明手動移除的結果與產生腳本一致）。

### 本輪完成的事（2026-08-06，選單三層化 ＋ 首頁收斂 ＋ 內容頁改版提案）

依 `docs/meeting_0805_end.md`。分兩軌：**軌 A 動結構（落地）**、**軌 B 出視覺提案（不落地）**。

**軌 A：**

1. **首頁收斂為 2 檔**：6 個變體檔 `git mv` 到 `archive/style-3-homepage-variants/`，
   相對連結由 `docs/reports/archive_homepage_variants_20260806.py` 重指回 `../../style-3-soc/`。
   留下的兩檔 backlink 列改成 `Layout: Current · V1`（Nav A/B 那組隨 Nav A 退場）。
2. **選單三層化 ＋ 全站 Nav B**（17 檔）：`docs/reports/rebuild_nav_20260806.py`。
   第一層改成 `<button>`（不可點，但保留 keyboard focusable 讓 `:focus-within` 生效）；
   `aria-current` 移到第二層真連結，第一層改掛非 ARIA 的 `class="on"`；
   `<header>` 加行內 `onkeydown`，Esc 把焦點交給 logo（補 WCAG 2.2 SC 1.4.13 Dismissible）。
3. **3 個 GCP 產品頁**：`docs/reports/build_gcp_pages_20260806.py`，以 `cloud-compute.html`
   為底檔、只換 `<main>`，所以 footer 自動與 `sentinelone.html` 逐字節相同。
4. 根 hub 四卡改兩卡、補 3 個新頁與 lab 入口；`archive/index.html` 補第三輪封存的導流。
5. `build_variants_20260804.py` 改造成 `build_v1_20260806.py`（只產 V1、只吃 index.html 一份母版）；
   `sync_nav_20260804.py` 與 `remove_gcp_groups_20260805.py` 檔頭加 `sys.exit` **封印**。

**軌 B：** `lab/` 四個檔（比對入口、守規則版分類頁改版、兩個 Tailwind 實驗頁）。
文案與被比對的頁面逐字相同，只有版型不同。**Tailwind 頁刻意違反禁 CDN／禁框架／色系凍結**，
那正是要被看見的成本；不得擴散到 `style-3-soc/`。

**踩到的三個坑（腳本內已註記）：**

1. `rebuild_nav` 第一版**不冪等**——它只用正則移除 `@media (max-width:1100px)` 區塊，
   卻沒移除自己上一輪留下的註解，跑第二次註解就疊一層。修法：註解與 media 分兩次清，
   並加後置條件檢查（四個切片各只能存在一份）。
2. **nav CSS 不是一段，是三段**（桌機／行動版／1100px），另加一個插入點。
   而且**不能用 `@media (max-width:900px){` 當行動版切片邊界**——當時的變體首頁有兩個同名
   media block，只有 17/23 檔唯一命中。改用 `.navbtn{display:block}` 當錨點。
3. 第一層 `<a>` 換成 `<button>` 後，`.menu a[aria-current="page"]` 這條 CSS 匹配不到 button，
   **10 個檔的「你在這裡」黃底線會靜默消失**——而 `grep -c 'aria-current'` 仍回報正常。
   這是「檢查說沒事、畫面壞了」的組合，必須改 CSS 選擇器並用瀏覽器實際確認。

**已驗**：`check_nav_20260806.py` PASS（並做過注入破壞測試，確認它抓得到）、
`check_links_20260806.py` 25 檔全通過、軸 2 五句 2/2＋核心句 1、footer 17/17 逐字節相同、
重跑 `build_v1_20260806.py` 產出與現況逐字節一致。

### 本輪完成的事（2026-08-06 下午，內容頁全面區塊化）

0805 的意見是「內容頁都是文字 list，看久了視覺疲勞；想要區塊、顏色區分、箭頭表關聯」。
0806 使用者裁決：**走守硬性規則的 inline CSS 版，Tailwind 版不採用**。

1. **共用元件 CSS 抽成唯一正本** `docs/reports/restyle_content_20260806.py`（`BLOCK_CSS`
   ＋ 35 個自繪 icon 的 `ICONS`），注入全部 36 頁。元件：`.probs`/`.uses`（琥珀左邊界）、
   `.trio`/`.quad`/`.duo`（icon 卡＋`.go` 連結）、`.steps`（真箭頭流程）、`.spec`（深色編號面板）、
   `.stack`（分層圖）。**零新色票**——區分只靠三層表面深度、一道琥珀邊界、一列真箭頭。
2. **16 個內容頁 ＋ 首頁的 `<main>` 全部改寫**。原本每頁重複三四次的 `.loglist`／`.cards2`
   已在 style-3-soc 絕跡（`grep -lE 'class="(loglist|cards2)"' *.html` → 無）。
3. **軸 3（新）：文案零漂移**。`docs/reports/check_copy_20260806.py` 拿 git 基準逐句比對
   `<main>`，少一句就 FAIL、多一句要在白名單（`.go` 標籤／箭頭／兩位數編號）。
   一次改 16 頁的版型，沒有這條就沒有東西擋得住某一頁被順手改字。
4. **軸 1 擴充成四段切片**：`check_nav_20260806.py` 現在也比對區塊元件 CSS，
   36 檔必須逐字節相同。已做注入破壞測試（改一頁的 `.spec` 字級 → 正確點名該檔）。
5. **`lab/` 定案留檔**：`lab/index.html` 與根 `index.html` 都已標記「已定案走 inline 版」。
   該資料夾隨時可整個刪掉。
6. **`build_gcp_pages_20260806.py` 不再自己注入 CSS**，改 import 共用正本的 `svg()`，
   icon 與元件樣式只剩一份定義。

**踩到的坑（下次會再遇到）**
1. **`.steps` 是最容易誤用的元件**。四張並列的交付卡硬插箭頭 = 假造推進關係。
   本輪有兩頁（cloud-storage／cloud-analytics）判定為並列而改用 `.quad`，理由寫在施工回報裡；
   cloud-analytics 的反證特別值得記：Data cleansing/ETL 與 Streaming pipelines 是兩種併行進料，
   箭頭無論指哪個方向都是錯的。**判不出順序就不要用 `.steps`。**
2. **`.probs`/`.uses` 預設三欄，四項會排成 3+1**（第四張只佔 1/3 寬）。四項要加 `.four`。
   而且 `.probs.four` 的優先權高於 `.probs`，兩個 media query 都得補上覆寫，否則窄螢幕維持四欄。
3. **`.vsrc` 搬進 `<h3>` 會繼承粗體**。它是 mono 微標籤不是標題的一部分，
   卡片內要 scope 覆寫成獨立一行、`font-weight:400`。
4. **元件 CSS 不能用 `@media (max-width:1100px)` 或 `(max-width:1024px)`**——
   `check_nav` 用這兩個查詢當切片邊界，各只能出現一次。本輪的四欄斷點因此改用 1040px。
5. **`ess.html` 的步驟編號寫在標題文字裡**（`01 · Data collection`），拆成 `.n` span 會讓軸 3
   判定少一句。這是文案凍結與版型一致性的真實衝突，已登記為已知缺口 7。

**已驗**：`check_nav` / `check_copy` / `check_links` 三支 PASS；36 頁無 `<img>`/`<script>`/
外部資源；外連全帶 `rel="noopener"`；`ess.html` 與 `services.html` 零外連；footer 17/17 逐字節相同；
22／8／3／6 個錨點 id 全在；軸 2 五句 2/2 ＋ 核心句 1；每頁 icon 無重複。
14 個 subagent 分 6 組施工並交叉驗收，**0 blocker**，6 項 advisory 已逐項處理或登記。

### 本輪完成的事（2026-08-06 晚，GCP 產品頁「吸引閱讀」改版）

前置：19 個 GCP 產品頁補齊＋產品卡雙出口＋`cloud.html` 產品索引已先 commit（`4037efc`），
讓軸 3 基準前進，本輪改動可獨立驗證。

1. **19 個 `gcp-*.html` 各加三段**（grilling 定案；研究底稿
   `docs/reports/gcp官網解剖_20260806.md`）：`#pain` 痛點（沿用 `probs`）→
   `#pick` 選型指引（新元件 `.pick`：情境 → `.node` 晶片，自身用 `.node.self`）→
   `#faq` 平鋪問答（新元件 `.faq`，mono 編號同 `.spec` 系統）。骨架順序：
   Hero → pain → value → features → usecases → pick → stack → faq → vendor → CTA。
2. **文案生產線**：6 組產文 agent 從 Google docs overview 頁改寫（19 產品 × 痛點 2–3／
   選型 2–4 列／FAQ 3–5 題／規格事實 0–2 條），6 組**獨立稽核**（抄襲 6 連詞比對、
   虛構、金額、英式拼寫、技術事實）——抓到 **10 處文字缺陷**（8 連字照抄、
   「single console」與官方支援矩陣矛盾、儲存級別取捨寫反、OpenAPI 版本過時、
   Cloud Armor 24/7 應變寫成 Enterprise 全含[實為 Annual 限定]、「prompts 不訓練」
   引錯來源頁等）全數修正、另補正 4 處來源，才整合進 `PAGES`。
3. **ADR 0004**：全站不放金額資訊，計價一律導向 Contact us；非金額規格事實
   （SLA %、容量上限）可寫進 `spec` 面板，來源 URL 以 `# src:` 註解存於 `PAGES` 條目旁。
4. **`.pick`／`.faq` 進 `BLOCK_CSS` 正本**（36 檔同步注入）；icon 規則放寬為
   「優先從 ICONS 挑，缺了以同風格自繪補進正本」（本輪 35 個夠用，未新增）。
5. 選型只比 19 個產品之間，**不與他雲比較**（競品座標句已否決）。

**已驗**：`check_nav`／`check_links` PASS；`check_copy` **少了=0**、多了=613
（全部是三個新段落的刻意新增，commit 後歸零）；三段齊備 19/19；stack 主角 19/19
（檢查已改為只掃 `#stack` 區——`.pick` 的自指列也用 `.node.self`，全檔數會多算）；
金額掃描（`[$€£]`/per month/free tier）全站零命中；CLAUDE.md 內容檢查組全綠。

踩過的坑（勿重犯）：整合腳本判斷「條目已整合」不能用寬鬆的 `"pains"` 字串——
最後一個條目的 region 延伸到檔尾，會把 `build_main()` 裡的 `p.get("pains")` 誤判成已整合，
要用插入時的精確樣式 `"pains": [`。

### 本輪完成的事（2026-08-07，資安線跟進三段 ＋ 會議材料 ＋ 素材需求單）

前置：0806 晚的 613 處新增已 commit＋push（`b18ca2c`，連同 `4037efc` 一起上線），
check_copy 基準前進歸零。**首頁二選一使用者裁決「兩案並存，留待會議」**——收斂程序暫不執行，
軸 2 與 `build_v1` 維持現役。當日 grilling 七題裁決：資安線跟進（A）、Services 線等素材（A）、
需求單先行（A）、`lab/` 留到會議後（B）、會議對照材料要做（A）、制度精簡＋備份升格同意提案。

1. **資安線 5 頁補 `#pick`／`#faq` 兩段**（`sentinelone`／`threatsonar`／`cybereyes`／
   `google-secops`／`ess`；`#pain` 0806 區塊化時已有）。CSS 零改造，渲染與 GCP 頁逐字同構；
   `#pick` 插於 `#why` 前、`#faq` 插於 vendor 區前（ess 無外連區，插 CTA band 前）。
   這 5 頁是**手維護頁**，整合腳本在 scratchpad（一次性），素材 JSON 同處。
2. **工序**：1 產文 agent（讀 `docs/product/` 內部 md）→ 1 獨立稽核 agent →
   修正 33 處 → 稽核員複驗 → 補修 2 處 → 整合。稽核抓到 **6 阻斷＋6 中度＋2 小項**：
   ThreatSonar 常駐模式 OS 宣稱建立在素材自相矛盾行上（整句移除）、SecOps 答案與同頁
   24/7 宣告打架、SentinelOne 離線處置與授權模式無素材依據、**AWS/Azure 具名打破全站
   不變式**（改 the major public clouds）、CyberEyes 自指列重述同頁痛點卡、
   picks 平均 14.2 詞 vs GCP house style 8.0（全面壓短至 8.7）。
3. **選型互連軸**：SentinelOne↔ThreatSonar（日常防護 vs 獵捕鑑識）、
   CyberEyes↔Google SecOps（託管 WDR vs 自建 SIEM）、每個單品頁一列指向 ESS、
   ESS 反向指回三單品。每頁 4 列、恰 1 列自指（`.node.self`）。
4. **FAQ 內 `[TODO]` 慣例**：純文字不包 span（`gcp-vertex-ai.html:506` 先例）、
   一律指名缺什麼（禁「to be confirmed」）。本輪留 3 個（rollout 工時、SecOps 接源工時、
   ESS onboarding 時程）。
5. **兩份文件**：`docs/reports/首頁兩案對照_20260807.md`（會議用一頁式，兩案結構
   對照＋取捨並列）；`docs/素材需求單_20260807.md`（全站 212 處 `[TODO]` 歸納成
   4 組 14 題，按「誰能答」分組供公司填答）。

**已驗**：`check_nav`／`check_links` PASS；`check_copy` 少了=0、多了=104（全落 5 個
資安頁，commit 後歸零）；三段齊備 5/5、`#pick` 區自指恰 1（5/5）；金額掃描零命中；
`ess.html` 外部連結仍為 0（零外連鐵則）；ESS 頁維持不指名方案內含品牌（`ess_product.md`
紅線）。政策觀察（未改，供裁決）：SentinelOne FAQ 提及該偵測流可進 ESS/SOC＋ESS 頁
picks 具名三單品，讀者可能對號入座——紅線技術上未踩，維持單品→方案的導流寫法。

### 本輪完成的事（2026-08-10 第一輪，ESS 瘦身 ＋ hub 儀表板 ＋ 七頁內容充實）

起因：業務對 demo 的回饋（`docs/meeting_0810.md` 原文），經 grilling 收斂為 15 項決議
（決議 1–15，正本在該檔附錄一）。commit：`242412d`（0807 文件同步）、`5646ddc`、
`2b763e2`、`d4a7570`。

1. **ESS 頁瘦身**：`ess.html` 移除 `#coverage`（時間軸）與 `#scenarios`（四個攻擊場景）
   兩區共 25 行——業務認為寫太細。`#pick`／`#faq` **保留**（那兩段是 0807 才加的決策支援
   元件，砍掉會讓 ESS 成為唯一沒有選型指引的方案頁）。
2. **根 Demo hub 改造成進度儀表板**：說明文字從兩大段沿革敘事改成四條「目前專注的點」，
   移除過時的「選單怎麼測」段；新增**待做事項清單 ＋ 28 列產品表**
   （欄位：更新日期｜產品類別｜產品名稱｜網址｜備注），日期由 `git log` 自動取。
   正本 `docs/reports/build_updates_20260810.py`，**手改 hub 的標記區會被下次執行覆蓋**。
   ⚠ **硬性規則破例**：hub 這一頁獲准使用約 15–20 行行內原生 JS 做表格排序，
   **僅限這一頁**，`style-3-soc/` 各頁仍禁止新增 `<script>`。已寫進 CLAUDE.md 硬性規則 1。
3. **七頁內容充實**（`2b763e2`）：GCP 試點 3 頁（Compute Engine／BigQuery／Cloud Run）
   各補 FAQ×3、規格事實×2、區塊級 SVG 示意圖×1；SentinelOne 補資料主權 FAQ 與
   telemetry 保留句；ThreatSonar 補情資匯入 FAQ 與遠端應變句；CyberEyes 補 vs NDR／
   vs EDR 兩題與攻擊鏈成效列；Google SecOps 補 300+ 整合成效列與 UEBA／Gemini FAQ。
   全部走**只加不改**：8 筆「少了」的句子都是原句＋句尾追加的逐字前綴。
4. **產生器新增四個選填欄位**（`build_gcp_pages_20260806.py`）：`extra_faqs`／`extra_specs`／
   `uses_extra`／`figures`（後者只能插 `value` 或 `features` 兩個 section）。
   **沒填欄位的條目輸出逐字節不變**，已用基線比對驗證——這是 16 頁鋪開的基礎。

**一個差點做錯的誤讀（記下來給未來的人）**：會議文件寫「index 頁面修改：調整該主頁內容呈現，
僅保留目前專注的點」。我原本解讀成 **`style-3-soc/` 的官網首頁要瘦身**，並據此問了兩輪問題；
使用者反問「這個我有說到要處理嗎」才發現——他指的是**根目錄的 Demo hub**。
兩個官網首頁最終**完全沒動**（對照組前提在這一輪仍然成立，是 0810 第二輪才終結的）。
教訓已寫進 `docs/CONTEXT.md` 新增的〈頁面身分〉詞條：**Hub（根 index.html）與
Homepage（style-3-soc 的兩個首頁）是兩個東西，講的時候一律指明是哪一個。**

### 本輪完成的事（2026-08-10 第二輪，ArgusHack 重定位 ＋ 兩品移除）

起因：查證確認掛在「Built in-house — Volcatech AI Security」底下的 `CE-BAS`
**不是沃凱自研**——原廠是台灣**盧氪賽忒股份有限公司（Leukocyte-Lab / LKC）**，
沃凱是**代理商**（使用者已確認）。研究底稿 `docs/reports/argushack_歸屬與功能研究_20260810.md`，
九項裁決（決議 16–24）記在 `docs/meeting_0810.md` 附錄二。這是**硬性規則等級的變更**
（原硬性規則 3 明文要求首頁列「自研 CE-BAS / AI-PTaaS / SecPurple」），使用者已裁決同意。

1. **產品更名 `ArgusHack`** 並**升格獨立產品頁** `style-3-soc/argushack.html`
   （骨架照資安產品頁，`#pain`／`#pick`／`#faq` 建頁時就帶齊；頁面標明原廠 by Leukocyte-Lab）。
   站上頁數 36 → **37**。
2. **選單 CyberSecurity 第三組改名**：`Built in-house — Volcatech AI Security`
   → **`Validation — breach & attack simulation`**，深連結目標由 `#in-house` 改為
   `#validation`，底下掛 `argushack.html`；下拉 head 白話行改
   `CyberSecurity — EDR · SIEM & WDR · BAS`。改的是 `rebuild_nav_20260806.py` 的 `MENU`
   （唯一正本）後重跑，全站 37 檔一次同步。
3. **`cybersecurity.html`** 的 `#in-house` 區改為 `#validation`（H2
   `The layer that tests the other layers.`），產品 id 由 8 個變 6 個
   （少 `ce-bas`／`ai-ptaas`／`secpurple`，多 `argushack`）。
4. **兩個首頁的第 4 區（`#built`）改寫**：不再宣稱自研——
   標題 `Tooling we operate, and evidence that it works.`，`.cols3` 改 `.duo`，
   只放有產品頁的 ArgusHack。V1 另改 partners 區（`Five vendors…三 services we build ourselves`
   → `Six vendors…`、浮水印 `Volcatech AI` → `Leukocyte-Lab`、tier 改 `[TODO: partner tier]`）
   與 catalogue（Cybersecurity `8 products` → `6 products`）。
   ⚠ **`index.html`「未經內容改動的對照組」前提就此終結**——本輪含兩個首頁一起改。
5. **`AI-PTaaS`／`SecPurple` 全站移除**（首頁、`cybersecurity.html` 區塊、全站頁尾清單、
   V1 catalogue 與網絡圖）。**理由是素材不足，不是否定它們是自研**；已列進 hub 待做事項，
   素材到位可加回。這一點與 0805 那批「只動選單、頁面保留」的處理**方向相反**，別搞混。
6. **`lab/inline-cloud-compute.html` 重跑 `build_lab_20260806.py`**——它的 header／footer
   取自 `cloud-compute.html`，第 4 步只換了 `style-3-soc/` 的頁尾，`lab/` 沒跟上，
   `check_links` 因此報 5 個死錨點（`#in-house`／`#ce-bas`×2／`#ai-ptaas`／`#secpurple`）。
   重跑後一併補上它從 0806 起就缺的區塊元件 CSS。**教訓：改選單或頁尾要順手重跑這支。**
7. **驗收時補修 3 處漏網的自研宣稱**：前四步改了區塊，但 `index.html` hero `#offer`
   的 Cybersecurity 卡與 `cybersecurity.html` hero 的 vendor／tag 兩行**摘要句**仍寫
   「three testing services we build ourselves」「· Built in-house」。這直接牴觸硬性規則 4，
   已改為「…plus breach and attack simulation to check that they hold.」與「· Leukocyte-Lab」，
   V1 重跑 `build_v1_20260806.py` 跟上。**教訓：改區塊時要一併搜同頁的摘要句／hero 標語**，
   它們常在別的區塊裡重述同一個宣稱。
8. **制度檔同步**：`CLAUDE.md`（硬性規則 3 改寫＋加日期註記、選單結構、頁數 36→37、
   驗證區指令與期望值、軸 2 理由換一套）、`HANDOVER.md`、`README.md`、
   `.github/copilot-instructions.md`；`build_updates_20260810.py` 的 `NOTES` key
   `CE-BAS` → `ArgusHack`，重跑後根 hub 產品表已含 ArgusHack、無 CE-BAS。

**已驗**：`check_nav` PASS（37 檔）、`check_links` PASS（42 檔，死錨點歸零）；
CLAUDE.md 驗證區 26 條指令逐條實跑、輸出與註解相符（footer 逐字節 34/34 OK、
`aria-current` 除兩個登記孤兒外皆 3、cybersecurity 6 產品＋3 區塊、金額掃描零命中）；
`grep -l 'CE-BAS\|AI-PTaaS\|SecPurple' style-3-soc/*.html` 全空。
`check_copy` **預期會報「少了」**——本輪是**刻意的文案變更**，逐句核對過每一句
都對應到決議 16–24（CE-BAS／AI-PTaaS／SecPurple／自研宣稱），無誤刪。

### 本輪完成的事（2026-08-11，其餘 16 個 GCP 產品頁充實；`d9bc995`）

0810 第一輪已用 3 頁試點驗證模式，本輪把剩下 16 頁（含孤兒頁 `gcp-cloud-armor.html`）一次鋪完。
**至此 19 個 GCP 產品頁全部完成充實。**

- **每頁 +2～3 題 FAQ、+2 列規格事實**（各附 `# src:` 來源 URL，只寫在產生器註解、不上頁）。
- **12 頁新增 SVG 示意圖；4 頁刻意不做**（API Gateway／Datastore／Filestore／Model Garden）。
  這是使用者裁定的**「誠實優先」原則**：SVG 只給真的有流程或架構可畫的頁，
  沒有機制可畫就不畫——**裝飾圖比不畫更糟**，跟「`.steps` 不得假造推進關係」同一個道理。
  稽核複核過不做圖的判斷，例如 Filestore 的效能／容量兩軸圖：官方文件根本沒有 IOPS 與
  吞吐量數字，沒有數字的軸線圖等於憑感覺畫。
- **一律改產生器再重跑**，沒有手改任何 HTML；三個試點頁重產後逐字節不變，
  這同時證明了選填欄位對未填條目零影響。

**獨立稽核擋下的兩個關鍵錯誤**（值得記住的類型）：

1. **Kubernetes Engine 的可用性宣稱寫反了**。原稿寫「zonal cluster 那一區出事時工作負載繼續跑」，
   但官方把那個保證綁在 **multi-zonal**；zonal 明文寫「該區出事時所有工作負載都不可用」。
   這種錯誤最經不起客戶查證。
2. **VMware Engine 的「單節點私有雲 60 天後刪除」整句拿掉**——兩份 Google 官方文件互相矛盾
   （一份寫 60 天刪除，一份寫單節點無時間限制）。依「說不準就不寫」移除，
   改用查得到的三項限制，換來的資訊反而更有決策價值（從「時間到會被刪」變成「留著會掉資料」）。

**已驗**：`check_nav`／`check_links` PASS；`check_copy` 192 項差異全落在這 16 頁，
15 筆「少了」逐句核對皆為原句＋句尾追加的逐字前綴；金額／他雲具名／hype 詞／美式拼寫零命中；
19 頁 `pain`／`pick`／`faq` 各恰 1、`stack` 區 `node self` 各恰 1、mono 編號連續不跳號。

### 本輪完成的事（2026-08-11 第二輪，版型改版：文字疲勞）

使用者訴求：「網頁文字過多、視覺疲勞，要調整版型，並讓各產品展現特色」。
先做量化體檢再動手（報告：`docs/reports/內容頁密度體檢_20260811.md`），
決議 25–34 記在 `docs/meeting_0810.md` 附錄三，施工正本 `docs/reports/版型改版規劃_20260811.md`。

**體檢推翻了直覺的診斷**：786 個段落中位數只有 17 詞、78% ≤30 詞——「段落太長」不成立。
真正的病灶是 **`#faq` 佔全頁 36–44%**（每頁最高的一道牆）＋ 19 頁 section 順序 100% 相同、
每頁 26–29 張同構卡片、後半頁全站無圖。最密頁與最鬆頁只差 1.30 倍 →
**模板層級的系統性過載**，不是哪幾頁寫太多。

改了四件事，全部**不動一個字**（只搬字，軸 3 除授權的一處外零漂移）：

1. **`.faq` 雙欄卡片**（CSS `columns:2`，640px 退單欄）——牆高砍半，仍全展開、Ctrl+F 找得到。
   0805「不做頁籤／不用 disclosure」的決議不重議。
2. **`.spec` 緊湊化**＋**節奏收斂**（`.phero~section .wrap` padding 80→64px）。
   ⚠ 靠 `.phero~section` 把兩個首頁排除在外——首頁沒有 `.phero` 所以天然免疫。
3. **`.fact` hero 代表事實列**（24 頁）：從該頁 `.spec` **搬**一列上 hero，面板該列不再渲染、
   **編號留空缺**當升格提示。晶片放列標題、**不放產品名**（H1 已有一次，重複就是軸 3 的 +1）。
   挑選規則：該頁獨有、內文 ≤26 詞——⚠ 特別避開 `Availability commitment`，
   它出現在 **17 頁**，挑它會讓一票頁的 hero 長一樣，正好毀掉這個欄位的目的。
   `ess.html` 豁免（方案頁、無 `.spec` 面板）。
4. **4 個無圖頁補抽象節奏元素**（`fig_motif()`）：放大的該頁 icon ＋ 點狀虛線，
   `aria-hidden`、無 title／figcaption／箭頭。**它不是機制圖**——0810 決議 16
   「沒機制可畫就不畫」仍然成立，這裡補的是視覺喘息不是資訊。

**唯一動到的文案**（使用者當場裁決）：`gcp-cloud-run.html` 的 spec 有兩列同名
`Availability commitment`，其中一列**標題與內文不符**（內文講的是「可擴到 1000 個執行個體」
的規模上限），改名為 `Scale ceiling`。`check_copy` 因此恰報 2 筆（少 1 多 1），逐句核對無誤。
另兩處純撞名（Compute Engine／Kubernetes Engine）依裁決本輪不動。

**發現但未修**（需使用者裁決才動）：`gcp-firestore.html` 的 spec 01 內文有
`back- end` 斷字瑕疵（全站唯一一處）。修它要動文案，本輪 hero 改挑 03 避開它。

**已驗**：`check_nav`／`check_links` PASS；`check_copy` 恰 2 筆且都在授權範圍；
CLAUDE.md 驗證區全套 grep 通過（24 頁各恰 1 列 `.fact`、晶片無產品名、footer 34/34、
金額與自研宣稱零命中）；**試點與全鋪各派一次 verifier fresh-context 驗收**——
試點 9 條（揪出 `aria-hidden` 掛錯層級，已修復複驗）、全鋪 11 條全 PASS
（含「搬移不是複製」逐頁核對、兩首頁 `<main>` 與改版前逐字節相同、色系凍結無新色票）。

⚠ **未驗的一項**：390／768／1024／1440 的**瀏覽器實機目測沒做過**。本輪動的是
`columns` 與 `padding`，恰好是腳本看不見的東西——下一個接手的人若要動這區，
先開瀏覽器確認四個寬度無水平捲軸、以及 901–1100px 的選單就地展開區間。

### 本輪完成的事（2026-08-11 第三輪，資安線內容補實）

0811 的待決盤點發現一件事：**「372 處 TODO 全部卡在公司素材」並不完全對**——
`docs/product/` 裡 CyberEyes 與 Google SecOps 的內部素材只用了三到五成，
這批內容**不用等公司回信就能做**。使用者裁決做，於是有了這一輪。

做法是三頁各走「差距分析 → 產文 → **獨立稽核**」，稽核由沒有參與產文的 agent 執行。
**三頁的初稿全部 FAIL**，這正是稽核存在的理由。抓到的類型值得記住：

| 類型 | 實例 |
| --- | --- |
| **虛構公司事實** | 初稿寫 CyberEyes 由「an independent security software company **in Taiwan**」開發——素材只記載原廠名稱，沒有一句寫公司性質或註冊國別。改成 `an independent software vendor`，法人名與註冊國進 `[TODO]` |
| **虛構產品功能** | 初稿在資料保護題裡寫「who can read them follows the roles you configure」，憑空給了產品一套角色權限模型——素材全篇沒有任何存取控制敘述 |
| **把限定條件講成通用** | 素材只說「雲端版資料保留 7 天可加購」，初稿把保留期限講成兩種部署模式通用 |
| **自打嘴巴的交付宣稱** | 初稿先斷言沃凱 deploys／tunes／wires／operates，句尾 `[TODO]` 又說夥伴關係範圍未定。改成照 `argushack.html` 先例只寫 `supplies it as a partner` |
| **邏輯不成立的效能宣稱** | 初稿把 ThreatSonar 的四階段防護講成「漏掉一層還有其他層接住」——四階段是時間序不是並聯冗餘，漏在中間時後面只剩一段 |

最後上站的是稽核修正版：三頁各補 3–4 題 FAQ、1–2 列成效、1 個 `#usecases` 場景區塊。
編號都接續且**保留了升格到 hero 那一號的空缺**。

**順帶修掉的既有瑕疵**：`cybereyes.html` 與 `google-secops.html` 各有一處美式拼寫
（`behavior`）是 0806 就在的漏網，違反專案自訂的英式拼寫規則，一併改掉。

⚠ **發現但未修，需要查證後才能動**：`threatsonar.html` 的 FAQ 02 說常駐模式僅支援 Windows，
但稽核比對 TeamT5 deck p64 的對照表，常駐模式作業系統欄列的是 **Windows 與 Linux**，
Windows 限定的只是其中四項標記功能（自我保護／還原保護／Protect Plus／Defense）。
**這是產品事實，改錯比不改更糟**——要動之前先請人核對原廠 deck 或向 TeamT5 確認。

**已驗**：`check_nav`／`check_links` PASS；`check_copy` 57 項差異全部核對——
**「少了」只有 2 處且都是上述拼寫修正**，其餘 55 處全是「多了」且只落在這三頁；
金額、hype、外部資源、`to be confirmed`、三段 section 計數全部通過。

### 本輪完成的事（2026-08-13，地轉雲線建頁：`managed-gcp.html`）

起點是使用者交來的繁中企劃書 `docs/地轉雲_GCP_網頁製作企劃書_V1.md`，要求把它變成選單 Services
底下那個灰字 `GCP Managed Services` 的內容。經四輪 grilling 定案 19 條決議，
**內容正本落在 `docs/地轉雲線_內容規劃_20260813.md`**（含逐區塊英文定稿文案與互連表）。

**這輪最需要先想清楚的一件事：企劃書講的不是 managed services。** 它的六大區塊重心是
**遷移全流程**（維運只佔第六階段與方案 C），而選單那格叫 managed services，兩者名實不符；
站上又早有一張 `cloud-services.html` 的 `Cloud Migration & Kubernetes` 卡在等素材，內容重疊。
裁決是**一頁通吃 migrate ＋ run**、選單標籤改名為 `GCP Migration & Managed Services`，
那張卡加一條 `.go` 指過來把重疊解掉（**卡內文的 `[TODO]` 刻意不填**——本輪素材授權只解禁新頁）。

**檔名 `managed-gcp.html` 是計算過的，不是隨手取的。** `gcp-managed-services.html` 會被
`gcp-*.html` 這個 glob 抓進去，讓四條驗證指令立刻紅（`#pain`/`#pick`/`#faq` 各須 1、
`#stack` 須恰一個 `.node.self`、`.stack a{scroll-margin-top}` 須 19 檔各 1、hero 晶片檢查）——
因為 `gcp-` 前綴在本專案是「Google 產品頁」的保留語意，而這頁是沃凱服務。
`cloud-managed.html` 會撞 `cloud-*` 兩條。只有 `managed-gcp.html` 零副作用。

**骨架 7 段**：`#pain`（`.probs.four`，**全站第一次用 `.four`**）→ `#process`（`.steps` 六階段，
每階段只有一句）→ `#services`（`.quad` 四卡）→ `#stack`（五層）→ `#pick`（4 列）→
`#plans`（`.trio` 三方案）→ `#faq`（6 題）。幾個刻意的取捨：

| 決定 | 理由 |
| --- | --- |
| **砍掉企劃書的「六大效益」整區** | 它與區塊一的七個痛點是同一件事的正反面，兩段都放＝同一件事講兩遍，正是 0811 密度體檢抓到的「節奏重複」病灶。效益改為吸收進痛點內文的反面與方案描述 |
| **`#services` 用 4 卡而非照企劃書的 6 項** | 六項服務與六階段流程條目重疊約七成；改成 4 卡讓兩段的節奏錯開（4 vs 6），角度也分得開——`#process` 講順序與里程碑，`#services` 講出什麼人做什麼事 |
| **`.pick` 只有 4 列，不是企劃書表格的 13 列** | 全站 `.pick` 一律 4 列；而 13 列裡有 **5 類產品站上根本沒有頁面**（Migration Center／VPC·VPN·Interconnect／LB·DNS·CDN／Cloud Identity·IAM／Logging·Monitoring）。那 5 類改寫進 `#process` 階段 03 的 landing zone 那一句，**不點產品名**——正是企劃書自己要求的「不要變成產品名稱清單」 |
| **`#stack` 頂層放沃凱自我節點而非某個 Google 產品** | 圖的意思因此從「產品目錄」變成「這幾層都在維運契約裡」。無 href 的節點在 `.stack` 會渲染成 `.node.self`，所以沒頁的產品**不能**塞進去，否則圖會宣稱「本頁就是 VPC」 |
| **`.fact` 豁免** | 它是產品頁的元件；服務頁比照 `ess.html` 不用。`.fact` 檔數因此仍是 24，零指令要改 |
| **24/7 只寫「監控與告警」** | 使用者裁決沿用站上既有的 24/7 SOC 宣稱，但「有人在」與「多久回」是兩種承諾——回應時間目標與 SLA 留 `[TODO: response time targets]`，是本頁唯一的佔位 |
| **零外部連結** | 比照 `ess.html` / `services.html` 兩個服務頁。企劃書 §六的 Google 官方參考只作為改寫依據，不上站 |

**企劃書有五類要求刻意不做**（全部登記為 Astro 正式版待辦，理由見內容正本 §6）：
攝影／情境主視覺（撞禁 `<img>`）、諮詢表單（純靜態無後端＋GDPR）、網頁追蹤（禁 JS ＋零追蹤）、
每區塊不同 CTA（全站一律 `Contact us`）、單頁式網站（本站是多頁架構）。

**獨立稽核抓到 26 項，全部修掉。** 做法是六個維度各一位稽核員（拼寫與語法／hype 與宣稱／
金額與佔位／事實與連結／素材忠實度／全站一致性），每一項發現再交給另一位 agent 做**反駁式複核**
（預設立場是「這可能是誤報」，只有親眼看到證據才判成立）——提出 39 項、成立 26 項、駁回 13 項。
值得記住的類型：

| 類型 | 實例 |
| --- | --- |
| **英文硬語法錯** | `so little of the platform's managed services get used`——`little` 是不可數量詞卻修飾可數複數，且動詞數也不對；`take budget and attention that were never meant to be an IT deliverable`——複數先行詞配單數表語，而且預算與注意力是投入不是產出 |
| **同頁自相矛盾** | FAQ 03 斷言現代化「pays it back in operations」（無條件回本），FAQ 02 卻誠實寫「Not automatically」——企劃書 §一.5 明文禁止這類保證。改成有條件句 |
| **分層圖畫錯事實** | `#stack` 原本是「Data ↓ **backed up to** → Storage(Cloud Storage · Filestore · Backup and DR)」，等於宣稱資料庫備份進 Filestore——但 Filestore 是即時掛載的 NFS 共享。改成儲存併入資料層、Backup and DR 獨立成最後一層用「protected by」收尾 |
| **文件宣稱與頁面不符** | 內容正本聲明企劃書痛點第 7 項（新系統／資料分析／AI 導入門檻）已被吸收進 Run and optimise 卡，實際頁面上沒有任何落點。補了一句 |
| **交代不完整** | 企劃書搭配表裡另有 4 項無站內頁的產品（Migrate to VMs／DMS／Persistent Disk／SCC）在文件裡毫無交代。前兩項補進階段 05 的不點名敘述，後兩項明文登記為不做 |
| **外圍文件沒跟上** | README／HANDOVER／copilot-instructions 有 9 處還寫著「GCP Managed Services 是灰字」，其中一處在〈可直接複製給下一位 AI 的 Prompts〉裡——那是會被整段複製去執行的 |

**⚠️ 施工踩到的坑，值得記住**：改全站 footer 的批次腳本，冪等守衛原本用
`managed-gcp.html">GCP Migration` 這個子字串——但它**同時命中 header 的選單項**
（`rebuild_nav` 先跑過了），於是 37 檔被靜默跳過只改到 1 檔。更糟的是當下的驗證
`grep -c` 也數不出來：每檔都「恰 1 次」，只是那 1 次在 header。
**是 footer 逐字節比對把它抓出來的。**改 footer 的腳本一律要**先切出 `<footer>` 區域再取代**，
而且不要拿「全檔子字串命中數」當驗證。

**連動改動清單**（下次補 Services 線服務頁照這張表走，CLAUDE.md〈常見任務怎麼做〉也有同一份）：
`MENU` 灰字改真連結並重跑 → `services.html` 加第 7 張卡（`.trio`→`.quad`，帶 `id`）→
38 檔 footer 加列 → `check_nav` 與 `restyle_content` **兩支腳本各自寫死的 `EXPECT_FILES` 都要 +1** →
重跑 `build_lab` 與 `build_restyle_samples`（header/footer 取自底檔）→
`build_updates_20260810.py` 的 `NOTES` 加一筆（key 必須與選單同名）→ 根 hub 頁面清單加連結 →
CLAUDE.md／README／HANDOVER／copilot-instructions 的「37 頁」全部改 38
（⚠ **標明日期的歷史紀錄段落不要改**，例如本檔第 381、409 行）。

### ⚠ 0814 確認：這個站的讀者是**歐洲合作夥伴**，不是終端客戶

使用者 0814 說明：這次 demo 的對象是**歐洲的合作夥伴**，他們要**拿這個網站在當地銷售
沃凱的相關服務**。這件事之前沒有寫下來過，而它改變不少判斷：

- 站上全部文案目前是「**我們賣給你**」的口吻，缺的是「**我們和你一起賣**」需要的東西——
  交付分工（哪些我方做、哪些夥伴做）、誰簽約誰開發票、以及夥伴一定會被他們的客戶問到的
  「你們的 24/7 SOC 在哪裡、誰輪班、歐洲時區誰接」。站上目前**沒有任何一處回答這些**。
- 因此「沒有 About 頁、零家公司證據（成立年份／客戶／案例／團隊／規模）」這一條的
  優先度上升：夥伴是拿自己的信用去背書，他要能對他的客戶交代沃凱是誰。
- 同理「Google Cloud 夥伴身分與等級」不只是文案缺口，它決定**夥伴能對外宣稱什麼**。
- 雙語的優先度也上升：夥伴要把這個站拿給德／法／荷的客戶看。

這些已列進根 hub 的待做事項，尚未動工。

### 本輪完成的事（2026-08-14，客戶 demo 前整備）

起點是使用者一句話：「這週末要 demo 給客戶，先把不確定的資訊（例如 TODO）移除，
移到待處理清單讓我後續補齊，先讓網站看起來像個成品。」經四輪 grilling 定案。

**先講盤點結果，因為它決定了整輪的優先序**：全站 384 處 `[TODO]` 裡，**79%（約 304 處）
不是內容缺口，是頁尾五個法定欄位**（Email／電話／統編／VAT／註冊地址）—— 真實存在的公司事實，
只是沒人交出來。使用者當場提供，一次解掉。剩下 80 處才是真正的內容問題。

**盤點時另外掃到三件比 `[TODO]` 更傷的事**，都不在原始需求裡：

1. **38 頁的頁尾都印著**「Demo notice: this page is published for internal design review only…
   The company details above are placeholders」。客戶讀到這句，前面看的一切就作廢了。
2. **38 頁的底部都有 `← Style home · Demo hub`**，點下去就是根目錄那個中文進度儀表板
   （首屏寫著「全站 372 處 [TODO]」「素材需求單 14 題自 0807 發出未回」）。
   原本以為只有兩個首頁有這一列 —— 實測是每一頁都有。
3. **語言切換的「繁中」是 `href="#"` 死連結**，而且 tooltip 寫著
   `Traditional Chinese version will be published with the production site`。

**做了什麼**（依影響面排序）：

| 動作 | 範圍 | 正本 |
| --- | --- | --- |
| 頁尾法定資訊補實 | 40 檔 × 8 處 ≈ 304 處 | `fix_footer_20260814.py` |
| 內容型佔位符改寫／刪除 | 18 檔 80 處 | `fix_content_todos_20260814.py` |
| 新增 `privacy.html` ＋ `imprint.html` | 2 檔 | `build_legal_pages_20260814.py` |
| 移除 Demo notice／backlink 列／語言切換 | 40 檔 | `fix_footer_20260814.py` ＋ `rebuild_nav_20260806.py` |
| FortiEDR 下架（選單、頁面卡、頁尾列、V1 夥伴卡與索引） | 全站 | `rebuild_nav` `MENU` ＋ 上述兩支 |
| 頁尾 `.legal` 灰字帶整塊移除（當日稍晚追加） | 40 檔 | `fix_footer_20260814.py` ⑥ |
| 產生待補素材清單 | — | `build_todo_backlog_20260814.py` |

⚠ 最後一列是**當日稍晚使用者追加的指示**（「先移除」），它把上面第一列補實的東西
又拿掉了一半：頁尾最底那條 mono 灰字帶（法人名／登記地址／統編／法務頁連結／©／
「零 cookie」那句）整塊不見。**沒有不見的**是頁尾聯絡 `<dl>`（Email／電話／登記地址）
與 Company 欄的 `Privacy notice` / `Imprint` 兩條連結 —— 法務頁入口沒有斷，
法定身分資料集中在 `imprint.html`。復原＝把該腳本的 `RESTORE_LEGAL` 改 `True` 跑一次
（`.legal` 的 6 行 CSS 刻意留在各頁 `<head>`，就是為了讓復原不必再碰 CSS）。
連帶：V1 的 `.legalrow` 原指 `#legal` 錨點，已改指兩個實頁（check_links 逼出來的）。

**佔位符的三種處置，分得很清楚**：

- **能寫實話的**（法定資訊、8 張服務卡）→ 寫實話。服務卡素材出自 `docs/公司_104.md`
  （**0814 局部解禁，僅限服務範圍描述，仍不得用來填法定資訊**）。
- **要看合約才知道的**（交付分工、回應時間、導入工時，約 30 處）→ 改成
  **「按案議定」**的寫法。不含數字、不含 SLA，因此不構成承諾；在真的還沒定服務等級之前，
  這正是最誠實的說法。
- **事實不能編的**（ISO 認證狀態、Google 夥伴等級、客戶案例、原廠法人名、合作範圍）→
  **刪句或改成 available on request**，一句都不猜。

**⚠ 兩件必須知道的事**：

1. **`index-v1-proof.html` 刻意保留 10 處佔位符**（使用者裁決 V1 先不動）。
   它 0814 起**沒有任何入口連結**，客戶動線走不到；但首頁若定案選 V1，這 10 處要先清掉。
2. **`privacy.html` 有一句與託管環境綁定**：「Volcatech 不會收到、不儲存、也不會併用
   那些存取紀錄」—— 在 GitHub Pages 上這是真的（repo 擁有者拿不到 access log）。
   **換託管環境時這一句必須重新查證。**

**踩到／發現的坑**：

- **`build_updates_20260810.py` 自 0813 起就跑不動了**（`IndexError`）。0813 那天 `MENU` 的
  `sub` 條目插了「白話說明」欄，子項清單從 `row[3]` 後移到 `row[4]`，`rebuild_nav._walk()`
  當天有跟著改，這支沒有。症狀是 hub 的產品表停在 0813 之前 —— 沒人發現，因為沒人重跑它。
  **同一份資料結構被兩支腳本各自解讀時，改了一支要 grep 另一支。**
- **HTML 註解會被寫進產出檔**。在 `build_v1` 裡用 HTML 註解說明「FortiEDR 已移除」，
  結果那段中文說明被渲染進 `index-v1-proof.html`，讓「全站不得殘留該產品名」的驗證掃到
  自己的說明文字（全域教訓簿 2026-08-04 那條的翻版）。說明要寫成 Python 註解。
- **`cp` 失敗被 `diff -q` 的 `||` 分支誤讀成「檔案不同步」**，差點去修一個沒壞的東西。
  scratchpad 目錄不存在 → `cp` 失敗 → `diff` 對不存在的檔案報錯 → 走進 `|| echo "有差異"`。
  **鏈式指令裡，前一段失敗會讓後一段的判斷失去意義。**

**連動改動清單**（新增頁面時照走，與 0813 那份合併看）：
`build_legal_pages` 產頁 → `rebuild_nav` → `restyle_content` → `fix_footer` →
`check_nav` 的 `EXPECT_FILES` 38→40 ＋ `ORPHANS` 加兩筆 ＋ 新增 `NOSECTION` 集合 →
`restyle_content` 的 `EXPECT_FILES` 38→40 → `build_updates` 的產品數守衛 28→27 →
重跑 `build_lab` 與 `build_restyle_samples` → 根 hub 與本檔的頁數敘述。

### V1 首頁（改它之前必讀）

**V1 不要手改。**它由 `docs/reports/build_v1_20260806.py` 從 `index.html` 產生：
hero / Built / Why / Trust / CTA 五個共用區塊直接**切片**取得，所以兩案必定逐字節相同。
要改 V1 就編輯該腳本內對應的區塊字串後**重跑**；要改共用區塊就改 `index.html` 再重跑。
`<main>` 以外全部繼承母版，所以母版的 header 換過之後重跑，V1 的選單會一起帶到。

踩過的坑（腳本內已註記，勿還原）：自我參照連結的替換若早於 backlink 列處理，
會把切換列裡的「Current」也改成 V1 自己——backlink 必須先換成佔位符隔離。

（V2/V3 已封存。它們留下的兩個教訓仍然有效：圖層標題不能單獨叫 `Operations` / `Platform`，
會撞到「舊選單術語不得殘留」的機械檢查而永遠誤報，連註解裡都不能出現該字串樣式。）

分層圖（`.stack`）的三條硬約束，現由 19 個 GCP 產品頁沿用，勿違反：
不得用 `position:absolute`（768/390px 會崩）；承載語意的線條用 `--muted` 不用 `--line`
（`--line #27344A` 在 `--bg` 上只有 **1.47:1**，不到 WCAG 1.4.11 的 3:1）；
箭頭用帶 `aria-hidden` 的真字元，不放 `::before content`，
也不用 `role="img"` 包整張圖（會把裡面的連結對輔助科技隱藏）。

---

## 2. 現行導覽結構速查（style-3-soc）

> **選單的唯一正本是 `docs/reports/rebuild_nav_20260806.py` 的 `MENU` 常數**，不是任何 HTML 檔。
> 改它 → 重跑腳本（40 檔一次同步）→ 跑 `check_nav_20260806.py`。手改必定漏。

2026-08-06 起全站統一**三層 Nav B**，不再有 Nav A：

- **第一層不可點**：`Google Cloud` / `CyberSecurity` / `Services` 是
  `<button type="button" aria-haspopup="true">`，只 hover / focus 展開。
  用 button 而非 span，是為了保留 keyboard focusable 讓 `:focus-within` 生效、不需要 JS。
- **第二層**＝分類頁；**第三層**＝產品。
- 頂層列：`● VOLCATECH` | `Home` | `Google Cloud ▾` | `CyberSecurity ▾` | `Services ▾` |
  `About` | `[Contact us]`。⚠ 0814 稍晚起 `Contact us` 是 `mailto:salesgroup@volcatech.com`,
  不再是 `index.html#contact` —— 在首頁上那原本是連到它自己所在的區塊,點了畫面不動。
  header 這顆的主旨是泛用的 `Website enquiry`(軸 1 要求 40 檔 header 逐字節相同,
  逐頁主旨會讓 check_nav 紅);`<main>` 內的 CTA 主旨帶該頁 h1。
  ⚠ **0814 起沒有語言切換**：原本尾端的 `EN 繁中` 已整組移除（繁中是 `href="#"` 死連結，
  且 title 自曝這不是正式站）。雙語留給正式 Astro 版。副作用是全站 `href="#"` 歸零。

各下拉內容（首行皆為 mono 白話對照）：

- `Google Cloud`：Overview（`cloud.html`）＋六組 18 項，
  **18 項全部連各自的 `gcp-*.html` 產品頁**（0806 補齊，不再有 `分類頁#錨點` 的過渡狀態）。
  第二層群組父項指向分類頁本身（`cloud-compute.html` 等）。
- `CyberSecurity`：Overview（`cybersecurity.html`）＋三組，
  head 白話行「CyberSecurity — EDR · SIEM & WDR · BAS」（0810 改，原為 `· Built in-house`）——
  Endpoint — EDR（SentinelOne／ThreatSonar，**0814 起只剩這兩項**——FortiEDR 因零素材下架，
  全站再無灰字項，`check_nav` 的 `class="off"` 期望值同步 1→0）／
  **Detection — SIEM & WDR**（CyberEyes／Google SecOps 連真頁；CyberEyes 實為 WDR，故群組改名）／
  **Validation — breach & attack simulation**（ArgusHack → `argushack.html`；
  0810 由「Built in-house — Volcatech AI Security」改名，理由見上方資訊架構節）。
  第二層群組父項是深連結（`cybersecurity.html#edr` / `#detection` / `#validation`）。
- `Services`（**扁平，無第二層**）：Overview（`services.html`）＋ ESS（`ess.html`）＋
  24/7 SOC & Incident Response（`services.html#soc`）＋
  **GCP Migration & Managed Services（`managed-gcp.html`，0813 建頁，原為灰字）**。

**0805 從選單移除、但頁面區塊全部保留的項目**（只動選單，不要「順手清乾淨」）：
ISMS / PIMS、Penetration Testing、Cloud FinOps、Digital Transformation，
以及更早移除的 Edge security（Cloud Armor）與 Volcatech cloud services 3 項。
它們在 `services.html` / `cloud-services.html` 的區塊、以及頁尾清單一律照舊。

⚠ **例外（2026-08-10）**：同批被 0805 移出選單的 **AI-PTaaS、SecPurple 已全站移除**——
頁面區塊、頁尾清單、首頁第 4 區都不再有，不屬於「只動選單」那一類。
理由是**素材不足**，不是否定它們是自研；素材到位後可加回（已列進 hub 待做事項）。
首頁第 4 區（`#built`）現在的內容是 ArgusHack ＋「我們自己維運、自己驗證」的定位，
**不得再宣稱自研 / not resold**。

### 現行注意事項（改 style-3-soc 前必讀）

1. 選單分類 `CyberSecurity` 的**駝峰寫法是 0731 會議指定的刻意寫法**，不要「修正」成
   Cybersecurity（僅限選單分類名；H1 等內文仍為定稿原文的正常拼寫）。
2. **一致性鐵則是雙軸**（正本在 `CLAUDE.md`；軸 1 已於 2026-08-06 換人）：
   - **軸 1**＝全站 header 同源。舊的「Nav A ↔ Nav B 自 `<main>` 起逐字節相同」隨 Nav A 退場而失效，
     接手的是：
     ```bash
     python3 docs/reports/check_nav_20260806.py     # 40 檔 header 正規化後逐字節相同
     python3 docs/reports/check_links_20260806.py   # 標籤配對 / 唯一 h1 / 連結與錨點
     ```
     ⚠ 這條檢查的存在意義：它是全站**唯一**能自動抓到「手改漏一檔」的東西。舊軸 1 死掉時
     一次要動 36 檔 × 4 個切片，正是最需要它的時候。已做過注入破壞測試，確認抓得到。
   - **軸 2** 兩個首頁凍結共用文案（五句定稿各命中 2 次；核心句只在 V1，共 1 次）。
3. **`aria-current` 與 `class="on"` 是兩個角色，不可混用**：
   `aria-current="page"` 掛「選單裡 href 等於本檔名的那個 `<a>`」（通常在第二層）；
   第一層 button 的視覺高亮用非 ARIA 的 `class="on"`。
   ⚠ 第一層從 `<a>` 換成 `<button>` 時，`.menu a[aria-current="page"]` 這條 CSS 會匹配不到，
   **10 個檔的黃底線會靜默消失，而 `grep -c` 仍回報正常**——改完必須用瀏覽器實際確認。
4. **孤兒頁**（選單裡沒有連結指向它，因此 header 內沒有 `aria-current`）目前有四個：
   `cloud-services.html`、`gcp-cloud-armor.html`（0806 補齊產品頁時一併產出，
   但它所屬的 Edge security 那組 0805 已移出選單），以及 0814 新建的
   `privacy.html`、`imprint.html`（入口在頁尾，刻意不進選單）。
   孤兒必須**明文登記**在 `check_nav_20260806.py` 的 `ORPHANS`，不能默默出現——腳本會擋。
   ⚠ 兩個法務頁還要登記在同檔的 `NOSECTION`：它們不隸屬任何板塊，
   第一層 button 不該有 `class="on"`，硬塞一個板塊會說謊。
5. **動 nav ＝ 改 `MENU` 後重跑腳本**（40 檔一次同步）；**動 footer 清單 ＝ 40 檔都要改**
   （footer 目前沒有產生器，靠「內容頁 footer 與 sentinelone 逐字節相同」把關；
   改 footer 的腳本必須**只在 `<footer>` 區域內取代**——寬鬆子字串會誤中 header 的選單項，
   0813 實際踩到，37 檔被靜默跳過而驗證指令當下看不出來）。
   `ess.html` 與 `services.html` **禁任何外部連結**；`cloud-services.html` 有 1 條
   Cloud Armor 官方連結、`cybersecurity.html` 有 5 條原廠連結，皆合法。
6. **`.dd ul` 絕不可加 overflow**——會變成 clip container 裁掉二層 flyout。
   Nav A 時代的 `max-height`/`overflow-y` 已隨 Nav A 一起退場（Nav B 面板最多 8 列，不需要捲動）。
   **`.sub` 的四條規則一律 scope 成 `.menu .sub`**——footer 有內文用的 `<p class="sub">`。
7. **901–1100px 這一段，二層改成在面板內就地展開**（`position:static`），不是側開 flyout——
   該區間視窗放不下側開的 flyout，窄端會跑出左緣。
8. 全 40 檔的 `main [id]` 都有 `scroll-margin-top:80px`，深連結錨點才不會被 sticky header 遮住；
   新增頁面時一併帶上。19 個 GCP 產品頁另需 `.stack a{scroll-margin-top:80px}`（圖中連結的鍵盤焦點）——
   0806 補齊產品頁後 19 頁全數具備，這裡原本寫「3 個」是補齊之前的狀態。
9. **`lab/` 的規則與 `style-3-soc/` 不同，而且只在 `lab/` 內有效**：那兩個 Tailwind 頁
   刻意違反禁外部 CDN / 禁框架 / 色系凍結。不得擴散；定案後整個資料夾刪掉。

---

## 3. 待辦（Roadmap）

- [x] **任務 1：內部評選——已完成（2026-07-31）**：勝出組合＝Style 3（SOC Console 色系）×
      原版直落版型，色系凍結。會後已完成：hero 文案置中、選單分類改名
      （`Google Cloud / CyberSecurity / Services`）＋ GCP 產品樹、選單雙變體（Nav A／Nav B）。
      落選風格與版型已歸檔至 `archive/`。會議紀錄見 `docs/meeting_0731.md`。
- [x] **任務 1d：選單變體定稿——已完成（2026-08-05 決議、08-06 實作）**：選 Nav B，
      並升級為三層、第一層不可點。全站 36 檔已統一，Nav A 退場。
- [ ] **任務 1e（進行中）：首頁兩案擇一定稿**：現行版 vs V1 信任前置，
      入口在根 `index.html`。0805 已先淘汰 V2／V3。定稿後把勝出方案的內容搬進 `index.html`，
      另一個移入 `archive/`，首頁收斂為 1 檔，一致性鐵則的軸 2 與
      `build_v1_20260806.py` 一併退場。
      **2026-08-07 裁決：兩案暫時並存，留待後續會議討論——勿催選、勿先行收斂**；
      會議用一頁式對照已備妥（`docs/reports/首頁兩案對照_20260807.md`）。
- [x] **任務 1f：內容頁視覺方向定案——已完成（2026-08-06）**：選**守硬性規則的 inline CSS 版**，
      Tailwind 版不採用（代價是外部 CDN、色系解凍與建置步驟，三項都與硬性規則衝突）。
      元件已套到全部 36 頁，`lab/` 留檔備查、隨時可刪。
- [ ] **任務 1g（新，2026-08-12）：視覺方向 A/B 擇一（或拆開採用）**：入口
      `lab/restyle-0812/index.html`，附六項判準表。四個選項——採 A、採 B、A 全採＋B 挑幾條、
      都不採。**B 可以拆**：字級收斂與圓角不需解凍，只有背景加深需要（ADR 0005）。
      規格與落地步驟在 `docs/design/`（`90_落地路線圖_20260812.md` 有逐步指令）。
      ⚠ 這輪推翻了 `refero_design風格範本調查_20260811.md` 第 6、95 行的「不會立即採用」註記。
- [ ] **任務 1f-2：`lab/` 第一層四檔何時刪**：它已完成階段任務，留著只有「當初為什麼沒選 Tailwind」
      的紀錄價值。⚠ 2026-08-12 起刪的是**第一層四檔**，不是整個 `lab/`——
      `lab/restyle-0812/` 還在待裁決中。刪掉時 `docs/reports/build_lab_20260806.py` 可一併移除，
      CLAUDE.md 已知缺口第 5 條也隨之消失。**刪除時機由專案負責人決定**（未 commit 前刪掉就找不回來）。
- [x] ~~**任務 1f-3：`cloud.html` 的 Overview 要不要展開到產品層**~~
      **2026-08-06 完成**（ADR 0002）：兩層都留——六領域卡在上當導覽，下面接 `.loglist`
      攤開全部 19 個產品。索引的描述句由 `link_products_20260806.py` 從分類頁抽取，
      不另寫一份會漂移的文案。
- [x] ~~**任務 1g：其餘 15 個 GCP 產品頁做不做**~~
      **2026-08-06 完成**（ADR 0003）：全部做，19 頁。
      ⚠ 原本的素材盤點結論「約 5 個產品內容撐不起一頁」**實測不成立**——
      `docs/GCP_Introduce_v2.md` 覆蓋 19 個產品全部、欄位齊備；唯一破格的是 Model Garden
      （沒有「關鍵特色」欄，改為模型清單）。這條錯誤的盤點差點讓 16 頁不做，
      教訓是**素材充足與否要逐產品實際打開來看，不能憑印象下結論**。
- [ ] **任務 2：補齊其餘產品/服務頁——待補 6 頁（原記 9 頁，2026-08-11 校正）**：
      Cybersecurity 已完成 5 項（SentinelOne／ThreatSonar／CyberEyes／Google SecOps／ArgusHack），
      **待補＝Managed Services 5 項**（0814 起 FortiEDR 因零素材下架，不再列為待補頁面，
      而是待補**素材**；素材到位要走加回流程，見 `docs/待補素材清單_20260814.md` §1）；
      原本的 9 頁裡，ArgusHack 已於 0810 建頁，AI-PTaaS 與 SecPurple 已因素材不足全站移除；
      **Cloud 線已由 8 個 `CI-*` 頁涵蓋，§A 的 Cloud 6 個 slug 不再逐項建頁**。
      另有 ESS 方案頁（方案層，**不計入 19 項 SKU**）。用下方 Prompt B。
      產品素材正本見 `docs/product/產品簡介總覽.md`（內部，gitignored）。
- [x] ~~**待辦：`cloud-services.html` 的沃凱自有服務 3 項補內文**~~ **2026-08-14 完成**：
      Cloud Migration & Kubernetes／Hybrid Cloud & Backup／Data & AI Engineering 三張卡
      （`cloud.html` 與 `cloud-services.html` 各一份，**同一段文案**）已依
      `docs/公司_104.md` 補寫 —— 該檔 0814 **局部解禁**，僅限服務範圍描述，
      仍不得用來填法定資訊。`services.html` 的另外 5 張服務卡同批補齊。
- [x] ~~**待辦：部分內容頁補詳細資訊**~~ **2026-08-10／08-11 完成**：19 個 GCP 產品頁
      （FAQ +2～3、規格事實 +2、12 頁 SVG）、S1／T5 小幅補強、CyberEyes／Google SecOps 擴充。
      素材依 Google 官方文件與 `docs/product/` 內部檔，每組都過獨立稽核
      （6 連詞抄襲比對、虛構、金額、英式拼寫、他雲具名）。
- [ ] **待辦：`argushack.html` 的沃凱交付素材**（交付主體、導入時程、回應承諾）。
      0814 起頁面上不再是 `[TODO]`，而是「按案議定」的寫法（不含承諾）；素材到位可換成具體內容。它是代理產品，**原廠 Leukocyte-Lab 的資格與量化宣稱一律不可搬**
      （金管會指定、APAC CIO Outlook 前五名、縮短 80% 報告時間等，研究報告已逐項標記）。
- [ ] **待辦：`AI-PTaaS`／`SecPurple` 素材**——0810 因素材不足全站移除，
      **非否定它們是自研**；`docs/product/` 對這兩品只有一句定位、零功能素材。
      素材到位可加回（首頁第 4 區、`cybersecurity.html`、全站頁尾清單、V1 catalogue）。
- [ ] **待辦：網站內容修改意見**——2026-08-11 使用者表示「晚點再給」，尚未收到。
- [x] ~~**任務 3：向公司取得法定資訊並替換 `[TODO`**~~ **2026-08-14 完成**：
      使用者提供法人名 `Volcatech Corporate Ltd.`（沃凱科技股份有限公司）、統編 `94269177`、
      中英地址、電話 `+886 2 2327 9668`、Email `salesgroup@volcatech.com` —— 一次解掉約 304 處。
      ⚠ **`VAT / tax ID` 那一列整列移除**而非填入統編：台灣公司沒有 EU VAT 號，
      填進去會讓歐洲買家拿去 VIES 查而查不到。現寫 `Company registration no. (Taiwan): 94269177`。
      ⚠ **0814 稍晚使用者又指示把頁尾最底那條 `.legal` 灰字帶整塊移除**：
      頁尾仍有聯絡 `<dl>`（Email／電話／登記地址）與 Company 欄的兩條法務頁連結，
      但法人名與統編只剩 `imprint.html` 一處。復原開關＝
      `docs/reports/fix_footer_20260814.py` 的 `RESTORE_LEGAL`。
      注意：`docs/公司_104.md` 是公司自述，**不是法定登記資料**，不能拿來填統編或地址
      （0814 的局部解禁只涵蓋服務範圍描述）。
- [ ] **任務 3b（0814 拆出）：認證與夥伴身分的證明文件**：
      **ISO 27001 認證狀態／範圍／證書號**與 **Google Cloud 夥伴身分與等級**仍未確認，
      站上一律寫 `available on request` 或整句不寫，**未經確認絕不可寫上去**。
      另需可對外引用的客戶案例。逐項清單見 `docs/待補素材清單_20260814.md` §1。
- [x] **任務 1b：版型變體 demo（第二輪評選）——已實作（2026-07-31）**，評選結束後已隨
      落選內容歸檔至 `archive/`（凍結）。規格正本 `docs/Volcatech_版型變體_Build_Prompts.md`、
      挑選背景 `docs/版型框架挑選指南.md` 保留為評選歷史。
- [x] **任務 1c：外部 AI 參考組收錄——已完成（2026-07-31）**，現位於
      `archive/Volcatech_Layout_Variants_GPT/`，**維持唯讀：不異動、不 review、不納入檢查**；
      規則正本在 `CLAUDE.md`「外部 AI 參考組」專節。
- [ ] **任務 4：建置正式版 Astro 專案**於 `site/`。用下方 Prompt C。
- [ ] （未來）繁體中文版與更多語系：i18n 架構已要求語系清單集中於單一陣列，新增語系不需改元件。

---

## 4. 可直接複製給下一位 AI 的 Prompts

### Prompt A：預覽與驗收檢查

```text
請讀取根目錄的 HANDOVER.md 與 CLAUDE.md。
先跑兩支檢查腳本，兩支都必須 PASS：
  python3 docs/reports/check_nav_20260806.py     # 軸1：40 檔 header 正規化後逐字節相同
  python3 docs/reports/check_links_20260806.py   # 標籤配對 / 唯一 h1 / 相對連結與錨點

再用 python3 -m http.server 8000 啟動本機伺服器，對 style-3-soc 的全部 40 頁做檢查
（用 ls style-3-soc/*.html 取得清單，不要用寫死的檔名）：
① 軸2：五句定稿文案在 2 個 index*.html 各命中 2 次、核心句
   「We operate what we sell, and we build what we cannot buy.」恰 1 次
   （對照組 index.html 刻意不含，不要「修正」成 2）
② 選單（三層 Nav B）：
   - 第一層 Google Cloud / CyberSecurity / Services **不可點**（是 <button> 不是 <a>）
   - 斜著移進第二層 flyout 不掉層；純鍵盤 Tab 全程可達
   - 下拉開著時按 Esc 會關閉（焦點回到左上角 logo）
   - **0814 起全站沒有灰字項**（FortiEDR 已下架），也**沒有語言切換**；
     因此每檔的 href="#" 應為 0 個。灰字若要加回，絕不可寫成 <a href="#">
③ 390 / 768 / 1024 / 1440px 無水平捲軸。特別測 **約 1000px**：
   二層應改成在面板內就地展開，不是側開 flyout（該區間 19 個原 Nav A 檔從沒測過）。
   390px：選單三層全部攤開成縮排清單。
④ 「你在這裡」的指示：開 cloud.html（Overview 型）、cloud-compute.html（第二層型）、
   sentinelone.html（第三層型）、gcp-cloud-run.html（第三層新頁）四種落點型態，
   確認 aria-current 的黃底線與第一層 button 的 .on 高亮都在。
   ⚠ grep -c 數的是行數不是語意——第一層換成 button 之後就算樣式壞了它仍回報正常。
⑤ 無任何外部資源請求、無新增 <script> 標籤；ess.html 與 services.html 全頁零外部連結
　（cloud-services.html 允許 1 條 Cloud Armor 官方連結、cybersecurity.html 允許 5 條原廠連結）
⑥ 三個下拉的深連結目標錨點都存在（Cloud 22 個、cybersecurity 8 個＝5 產品＋3 區塊、services 7 個），
   跳轉後標題不被 sticky header 遮住。首頁的同頁錨點（#offer / #built）是合法的，
   判準是「該 id 在同一頁存在」而非「有沒有 # 開頭」。
⑦ 0805 從選單移除的 4 項（ISMS／Pentest／FinOps／DX）：
   **header 區內應為 0，但頁面區塊與頁尾清單必須還在**——只動選單是使用者的明確裁決，
   不要當成殘留清掉。
   ⚠ 同批的 AI-PTaaS／SecPurple 已於 0810 **全站移除**（頁面區塊也不留），
   驗法相反：`grep -l 'AI-PTaaS\|SecPurple' *.html` 應為空；
   `grep -l 'CE-BAS' *.html` 同樣應為空（產品一律叫 ArgusHack）。
⑧ 內容真實性：合作等級、認證、SLA、客戶數**未經確認一律不寫**。
   ⚠ 0814 起這些位置**不再是 [TODO] 佔位**——改成 available on request、
   「按案議定」的敘述、或整句刪除。因此驗法變成「站上不得出現未經確認的等級／認證／
   數字承諾」，而不是「應該看到 [TODO]」。全站 [TODO] 應為 0
   （唯一例外 index-v1-proof.html，刻意保留且無入口連結）。
   仍不得出現「Google SecOps 認證經銷商 / Cloud Security MSSP / Premier Partner」
   （那是蓋亞的資格，不是沃凱的）
檢查範圍：根 index.html、style-3-soc/、lab/。**不含 archive/**（已凍結，不 review）。
lab/ 的兩個 Tailwind 頁刻意違反禁 CDN／禁框架／色系凍結，那是預期的，不要當成缺陷回報；
但要確認它們沒有擴散到 style-3-soc/。
回報每項 PASS/FAIL 與證據，不要順手改檔案。
```

### Prompt B：為勝出風格補齊其餘 9 頁

```text
勝出風格已定為 style-3-soc（2026-07-31 評選）。
請依 docs/接手開發_Prompts.md 的「P2」執行——該處已列出 18 個 slug、
文案要求與驗收條件；其中 threatsonar / cybereyes / google-secops 已完成
（2026-08-03），Cloud 線已於 2026-08-04 改由 8 個 cloud*.html 分類頁涵蓋
（P2 的 Cloud 6 個 slug 不再逐項建頁），
因此只做 Managed Services 剩下的 5 項，頁面結構參考既有 5 個資安產品頁或
managed-gcp.html（服務頁骨架，索引碼走 MS-NN 序列，下一個是 MS-02）。
⚠ 0810 起 Cybersecurity 線已完成 5 項（SentinelOne／ThreatSonar／CyberEyes／
Google SecOps／ArgusHack）；曾列在這裡的另外三項——兩項自研測試服務 0810 因素材不足
全站移除、FortiEDR 0814 因零素材下架——**都不要照這份 prompt 重新建頁**，
它們缺的是素材不是頁面。
產品素材正本見 docs/product/產品簡介總覽.md（內部文件）。特別注意：
- pentest.html 是 human-led、scoped engagement with report and retest；
  它與「自動化、持續、訂閱制」的滲透測試服務是不同的東西，不得混淆
  （這是採購方最容易問的問題）
- 導覽列與頁尾維持 style-3-soc 現行結構（三層 Nav B；Google Cloud / CyberSecurity /
  Services；CyberSecurity 駝峰是刻意寫法）
- header **不要手寫**：新頁建好後跑 docs/reports/rebuild_nav_20260806.py，
  aria-current 與第一層的 class="on" 會自動落到正確位置；
  並把該項在 MENU 常數裡的 href 從錨點改成新頁檔名
- 動 nav ＝ 改 MENU 後重跑腳本（40 檔一次同步）；動 footer ＝ 40 檔都要改
  （footer 沒有產生器，靠「與 sentinelone.html 逐字節相同」把關）
- 改完跑 docs/reports/check_nav_20260806.py 與 check_links_20260806.py，兩支都要 PASS
- 新頁的動線落點：現在 Cybersecurity 與 Managed Services 各項在
  cybersecurity.html / services.html 的名冊已有錨點，補頁後把該列改成連到新頁
```

### Prompt C：產生正式版 Astro 網站

```text
請讀取 docs/Volcatech_多風格_Build_Prompts.md（全案唯一事實來源）。
勝出風格為 Style 3（SOC Console，2026-07-31 評選定案）。
請結合「A. 共用基底 Prompt」與「風格 3 模組」，
在 site/ 目錄初始化全新 Astro 專案（不要改動現有 demo 資料夾），實現
19 個產品/服務頁 × 雙語（EN / ZH-TW）鏡像、3 個總覽頁、GDPR 隱私頁與 Imprint、
sitemap/hreflang，以及 GitHub Actions 自動化部署。
注意：該檔 §B 風格 3 模組的選單定義（Platform / Arsenal / Operations）是評選期歷史，
0731 會後選單分類已改為 Google Cloud / CyberSecurity / Services（含 GCP 產品樹），
一律以 style-3-soc/ 現行頁面為準。
驗收依該檔的【品質底線(驗收)】——不要用 docs/官網建置計畫_Build_Prompt_v3.md 的 §9，
那份已凍結失效。
```

---

## 5. 本地測試

```bash
# 在專案根目錄執行
python3 -m http.server 8000

# 瀏覽器開啟：
# Demo hub：                http://localhost:8000/
#
# 2 個首頁（頁面底部有 Layout 切換列，不必回 hub）
# 現行版（對照組）：        http://localhost:8000/style-3-soc/index.html
# V1 信任前置：             http://localhost:8000/style-3-soc/index-v1-proof.html
#
# lab/ 內容頁改版提案（三欄比對；Tailwind 頁需連網）
# 比對入口：                http://localhost:8000/lab/
#
# 3 個 GCP 產品頁（選單第三層樣板）
# Compute Engine：          http://localhost:8000/style-3-soc/gcp-compute-engine.html
# Cloud Run：               http://localhost:8000/style-3-soc/gcp-cloud-run.html
# BigQuery：                http://localhost:8000/style-3-soc/gcp-bigquery.html
#
# Cloud 總覽（CI）：        http://localhost:8000/style-3-soc/cloud.html
# Cybersecurity 總覽（CS）：http://localhost:8000/style-3-soc/cybersecurity.html
# Managed Services（MS）：  http://localhost:8000/style-3-soc/services.html
# Cloud Compute（CI-01）：  http://localhost:8000/style-3-soc/cloud-compute.html
# Cloud Storage（CI-02）：  http://localhost:8000/style-3-soc/cloud-storage.html
# Cloud Analytics（CI-03）：http://localhost:8000/style-3-soc/cloud-analytics.html
# Cloud Serverless（CI-04）：http://localhost:8000/style-3-soc/cloud-serverless.html
# Cloud Databases（CI-05）：http://localhost:8000/style-3-soc/cloud-databases.html
# Cloud AI（CI-06）：       http://localhost:8000/style-3-soc/cloud-ai.html
# Cloud services（CI-07）： http://localhost:8000/style-3-soc/cloud-services.html
# 產品頁 SentinelOne：      http://localhost:8000/style-3-soc/sentinelone.html
# 產品頁 ThreatSonar：      http://localhost:8000/style-3-soc/threatsonar.html
# 產品頁 CyberEyes：        http://localhost:8000/style-3-soc/cybereyes.html
# 產品頁 Google SecOps：    http://localhost:8000/style-3-soc/google-secops.html
# 產品頁 ArgusHack：        http://localhost:8000/style-3-soc/argushack.html
# 方案頁 ESS：              http://localhost:8000/style-3-soc/ess.html
# 舊評選總覽（已凍結）：    http://localhost:8000/archive/index.html
```
