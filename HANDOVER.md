# Volcatech 官網風格 Demo 接手指引 (Handover)

> **最後更新**：2026-08-04
> **本檔定位**：進度速查與接手指令集。
> **規格正本是 `docs/Volcatech_多風格_Build_Prompts.md`**——本檔與它衝突時，一律以它為準。
> 唯一例外：該檔 §B 的 style-3 選單定義（`Platform / Arsenal / Operations`）是**評選期歷史**，
> 0731 會後現行選單以 `style-3-soc/` 頁面為準（見下方 §2）。
> **例外資料夾**：`archive/` 是已凍結的評選歷史（含外部 AI 參考組
> `archive/Volcatech_Layout_Variants_GPT/`，唯讀、不異動也不 review，
> 規則見 `CLAUDE.md` 的「外部 AI 參考組」專節）；本檔所有任務與檢查指令皆不涵蓋它。

---

## 1. 目前狀態

**2026-07-31 內部評選已結束**：勝出組合＝**Style 3（SOC Console 深色色系）× 原版直落版型**，
色系凍結。現行維護對象只有 `style-3-soc/`，**共 15 頁**：`index.html`＝Nav A、
`index-nav-b.html`＝Nav B、8 個 Cloud 頁（`cloud.html` 總覽＋`cloud-compute`／`cloud-storage`／
`cloud-analytics`／`cloud-serverless`／`cloud-databases`／`cloud-ai`／`cloud-services` 七個分類頁）、
4 個產品頁（`sentinelone.html`／`threatsonar.html`／`cybereyes.html`／`google-secops.html`）、
1 個方案頁（`ess.html`）；所有子頁用 Nav A。
落選的 3 個風格、4 個版型變體與 GPT 參考包已全部移入 `archive/`（凍結），
舊評選總覽為 `archive/index.html`，根 `index.html` 重寫為 Demo hub（主卡 15 連結）。

### 定調的資訊架構（沿用不變）

- **3 條業務板塊**：`Cloud Infrastructure` / `Cybersecurity` / `Managed Services`
- **19 項服務**（清單與 slug 見規格正本 §A）：Cloud 6 + Cybersecurity 8 + Managed 5。
  **註（2026-08-04 定案）**：§A 的 SKU 代碼體系（`C-01`〜`C-06` 等）為 **pre-0731 歷史體系**，
  保留封存、不對齊、不上站；現行採**頁面層代碼**（Cloud 線＝`CI`／`CI-01`〜`CI-07`）。
  Cloud 線已由這 8 頁涵蓋，不再依 §A 的 Cloud 6 個 slug 逐項建頁。
- 自研 **CE-BAS / AI-PTaaS / SecPurple** 屬 Cybersecurity 底下的第三個群組，
  但首頁另有專屬的 **Built by Volcatech** 區塊——它不是第 4 條產品線，**不進頂層導覽**
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

2. **`Google Cloud` 下拉由「六組 18 項全是 `#offer` 佔位」改為八組 22 項且全部連真頁**：
   原六組 18 項改為**深連結**（`分類頁#產品錨點`，例 `cloud-compute.html#compute-engine`），
   新增 `Edge security` 1 項與 `Volcatech cloud services` 3 項，下拉頂部另加 Overview 入口
   指向 `cloud.html`。**Google Cloud 線至此零佔位連結。**
3. **footer「Cloud Infrastructure」欄改為 8 行分類連結**（Overview／Compute／Storage／
   Analytics／Serverless／Databases／AI／Cloud services & Cloud Armor），
   取代舊的 6 項 SKU 列法（Compute Engine (VM)／Cloud SQL (Database)／Cloud Armor (WAF)／
   Cloud Migration & Kubernetes／Hybrid Cloud & Backup／Data & AI Engineering）。
4. **CSS 兩處調整**：全 15 檔加 `main [id]{scroll-margin-top:80px}`（深連結錨點不被 sticky
   header 遮住）；Nav A 的 `.dd ul` 加 `max-height:calc(100vh - 90px);overflow-y:auto`
   （22 項＋分組小標共 32 列會溢出視窗）。**Nav B 刻意不加**——加了會裁掉二層 flyout。
5. **SKU 代碼體系定案**：舊 §A 的 `C-01`〜`C-06` 等為 pre-0731 歷史體系，保留封存、
   不對齊、不上站；現行 Cloud 線用頁面層代碼 `CI`／`CI-01`〜`CI-07`。
6. 根 `index.html`（Demo hub）主卡擴為 15 連結；`CLAUDE.md` 同步更新。
7. **已知待補**：`cloud-services.html` 的沃凱自有服務 3 項（Cloud Migration & Kubernetes／
   Hybrid Cloud & Backup／Data & AI Engineering）內文為 `[TODO: service description]`——
   本次使用者指示不參考 `docs/公司_104.md`，目前無素材，屬待補項而非疏漏。
8. Cloud 線內容正本為內部文件 `docs/Cloud線_內容規劃_20260804.md`（gitignored，勿在頁面連結它）。

---

## 2. 現行導覽結構速查（style-3-soc）

> 兩變體的選單分類與各下拉內容**完全相同**，差別只在「分組的呈現層級」。

| 變體 | 檔案 | 結構 |
|---|---|---|
| **Nav A（單層下拉）** | `index.html` 與全部 13 個子頁（8 個 Cloud 頁＋`sentinelone`／`threatsonar`／`cybereyes`／`google-secops`／`ess`） | `● VOLCATECH` \| `Home` \| `Google Cloud ▾` \| `CyberSecurity ▾` \| `Services ▾` \| `About` \| `[Contact us]` \| `EN 繁中`；下拉內以 mono 小標分組 |
| **Nav B（二層 flyout）** | `index-nav-b.html` | 頂層同 Nav A；下拉內的分組升級為第二層 flyout（hover / `:focus-within` 展開） |

各下拉內容（首行皆為 mono 白話對照）：

- `Google Cloud`：頂部 Overview 入口（連 `cloud.html`）＋**八組 22 項**——GCP 產品樹六組 18 項
  （Compute / Storage / Analytics / Serverless / Databases / AI，每項為深連結
  `分類頁#產品錨點`，例 `cloud-compute.html#compute-engine`）／`Edge security` 1 項
  （Cloud Armor）／`Volcatech cloud services` 3 項；**本下拉零佔位連結**
- `CyberSecurity`：8 項三組，head 白話行「CyberSecurity — EDR · SIEM & WDR · Built in-house」——
  Endpoint — EDR（SentinelOne、ThreatSonar 連真頁；FortiEDR 捲首頁）／
  **Detection — SIEM & WDR**（CyberEyes、Google SecOps 連真頁；CyberEyes 實為 WDR，故群組改名）／
  Built in-house（CE-BAS、AI-PTaaS、SecPurple → `#built`）
- `Services`：「Enterprise Security Service (ESS)」置頂（連 `ess.html`）＋ 原 5 項

舊風格與版型（Style 1／2／4、Layout 1–4）的導覽結構已隨頁面**歸檔至 `archive/`**（凍結），
逐字定義見規格正本 §B（評選歷史，僅供回顧）。

### 現行注意事項（改 style-3-soc 前必讀）

1. 選單分類 `CyberSecurity` 的**駝峰寫法是 0731 會議指定的刻意寫法**，不要「修正」成
   Cybersecurity（僅限選單分類名；H1 等內文仍為定稿原文的正常拼寫）。
2. **兩首頁變體自 `<main>` 起逐字節相同**（一致性鐵則）：改任何 `<main>` 之後的內容，
   兩檔必須同步，改完用 diff 驗證：
   `diff <(sed -n '/<main/,$p' style-3-soc/index.html) <(sed -n '/<main/,$p' style-3-soc/index-nav-b.html)`
3. 全部 13 個子頁（`cloud`／`cloud-compute`／`cloud-storage`／`cloud-analytics`／
   `cloud-serverless`／`cloud-databases`／`cloud-ai`／`cloud-services`／`sentinelone`／
   `threatsonar`／`cybereyes`／`google-secops`／`ess`）用 Nav A；
   **若會議選 Nav B，要換 header 的頁面現在是這 13 個子頁**（技術債，擇一定稿後一次處理；
   2026-08-04 Cloud 線建置後成本已明顯上升）。
4. **動 nav 或 footer＝全站 15 檔同步**（兩首頁變體＋13 個子頁）；`ess.html` 全頁
   **禁任何外部連結**（ESS 是方案層，非 19 項 SKU，footer `#managed-list` 也以它置頂）。
   零外部連結規則**只適用 `ess.html`**——`cloud-services.html` 有 1 條 Cloud Armor 官方連結。
5. **Nav A 的 `.dd ul` 有 `max-height:calc(100vh - 90px);overflow-y:auto`**（Google Cloud
   下拉 32 列會溢出視窗）；**Nav B 刻意沒有**——加上去會裁掉二層 flyout。改選單 CSS 時勿「順手統一」。
6. 全 15 檔的 `main [id]` 都有 `scroll-margin-top:80px`，深連結錨點才不會被 sticky header 遮住；
   新增頁面時一併帶上。

---

## 3. 待辦（Roadmap）

- [x] **任務 1：內部評選——已完成（2026-07-31）**：勝出組合＝Style 3（SOC Console 色系）×
      原版直落版型，色系凍結。會後已完成：hero 文案置中、選單分類改名
      （`Google Cloud / CyberSecurity / Services`）＋ GCP 產品樹、選單雙變體（Nav A／Nav B）。
      落選風格與版型已歸檔至 `archive/`。會議紀錄見 `docs/meeting_0731.md`。
- [ ] **任務 1d（進行中）：選單變體擇一定稿**：比對 `index.html`（Nav A）與
      `index-nav-b.html`（Nav B），擇一後併回單一 `index.html`；**若選 Nav B，
      需同步 13 個子頁的 header**（8 個 Cloud 頁＋sentinelone／threatsonar／cybereyes／
      google-secops／ess），並注意 Nav B 不可套用 Nav A 的 `.dd ul` max-height。
- [ ] **任務 2：補齊其餘產品/服務頁——待補 9 頁（2026-08-04）**：
      Cybersecurity 8 項已完成 4 項（SentinelOne／ThreatSonar／CyberEyes／Google SecOps），
      **待補＝Cybersecurity 剩 4 項＋Managed Services 5 項**；
      **Cloud 線已由 8 個 `CI-*` 頁涵蓋，§A 的 Cloud 6 個 slug 不再逐項建頁**。
      另有 ESS 方案頁（方案層，**不計入 19 項 SKU**）。用下方 Prompt B。
      產品素材正本見 `docs/product/產品簡介總覽.md`（內部，gitignored）。
- [ ] **待辦：`cloud-services.html` 的沃凱自有服務 3 項補內文**（Cloud Migration & Kubernetes／
      Hybrid Cloud & Backup／Data & AI Engineering），現為 `[TODO: service description]`；
      需使用者提供素材（本次指示不參考 `docs/公司_104.md`）。
- [ ] **待辦：部分內容頁補詳細資訊**（範圍待使用者指定）。
- [ ] **任務 3：向公司取得法定資訊並替換 `[TODO`**：
      註冊地址、統一編號、VAT／稅籍編號、對外聯絡 Email、電話（+886 國際格式）。
      另外 **ISO 27001 等認證狀態**與 **Google Cloud 合作等級**未經確認**絕不可寫上去**。
      注意：`docs/公司_104.md` 是公司自述，**不是法定登記資料**，不能拿來填統編或地址。
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
用 python3 -m http.server 8000 啟動本機伺服器，對 style-3-soc 的 15 頁
（index、index-nav-b、cloud、cloud-compute、cloud-storage、cloud-analytics、
cloud-serverless、cloud-databases、cloud-ai、cloud-services、sentinelone、
threatsonar、cybereyes、google-secops、ess）做檢查：
① HTML 標籤配對（python html.parser）
② 兩首頁變體自 <main> 起逐字節相同（diff 驗證）
③ 390 / 768 / 1024 / 1440px 無水平捲軸（Nav B 的二層 flyout 特別看窄幅；
   Nav A 的 Google Cloud 下拉 32 列要能在視窗內捲動）
④ 確認頁面無任何外部資源請求；ess.html 另須確認全頁零外部連結
　（cloud-services.html 例外：允許 1 條 Cloud Armor 官方連結）
⑤ 各子頁 aria-current="page" 掛在自己那一項、語言切換 EN 連結自指本頁
⑥ Google Cloud 下拉的 18 個深連結目標錨點都存在（分類頁#產品錨點），跳轉後標題不被 header 遮住
檢查範圍不含 archive/（已凍結的評選歷史，不 review）。
回報每項 PASS/FAIL 與證據，不要順手改檔案。
```

### Prompt B：為勝出風格補齊其餘 9 頁

```text
勝出風格已定為 style-3-soc（2026-07-31 評選）。
請依 docs/接手開發_Prompts.md 的「P2」執行——該處已列出 18 個 slug、
文案要求與驗收條件；其中 threatsonar / cybereyes / google-secops 已完成
（2026-08-03），Cloud 線已於 2026-08-04 改由 8 個 cloud*.html 分類頁涵蓋
（P2 的 Cloud 6 個 slug 不再逐項建頁），
因此只做其餘 9 個（Cybersecurity 剩 4 項＋Managed Services 5 項），
頁面結構參考既有 4 個產品頁。
產品素材正本見 docs/product/產品簡介總覽.md（內部文件）。特別注意：
- pentest.html 是 human-led、scoped engagement with report and retest
- ai-ptaas.html 是 automated、continuous、subscription
  兩者不得混淆（這是採購方最容易問的問題）
- 導覽列與頁尾維持 style-3-soc 現行結構（Google Cloud / CyberSecurity / Services，
  用 Nav A；CyberSecurity 駝峰是刻意寫法）
- 新產品頁三個常見坑：① aria-current="page" 掛在自己那一項；
  ② 語言切換的 EN 連結自指本頁檔名；③ 該項改真連結後刪掉 title="Demo: …" 提示
- 動 nav / footer＝全站 15 檔（含新頁遞增）同步；兩首頁自 <main> 起逐字節相同
- 完成後把指向 index.html#offer / #built 的暫代錨點換成實際檔案連結
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
# 首頁 Nav A（單層下拉）：  http://localhost:8000/style-3-soc/index.html
# 首頁 Nav B（二層 flyout）：http://localhost:8000/style-3-soc/index-nav-b.html
# Cloud 總覽（CI）：        http://localhost:8000/style-3-soc/cloud.html
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
# 方案頁 ESS：              http://localhost:8000/style-3-soc/ess.html
# 舊評選總覽（已凍結）：    http://localhost:8000/archive/index.html
```
