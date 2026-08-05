# Copilot 專案指示 — Volcatech 官網 Demo(勝出風格 style-3-soc)

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為靜態官網 demo。**2026-07-31 內部評選已結束**:勝出組合 = Style 3(SOC Console
  深色色系)× 原版直落版型,色系凍結。現行維護對象只有 `style-3-soc/` **二十三頁**:
  **8 個首頁** = 4 個版面方案 × Nav A/B(`index` 現行對照組 / `index-v1-proof` 信任前置 /
  `index-v2-catalogue` 型錄前置 / `index-v3-flow` 參考架構圖,Nav B 版加 `-nav-b` 後綴)、
  3 個總覽頁(`cloud.html`＝CI、`cybersecurity.html`＝CS、`services.html`＝MS)、
  7 個 Cloud 分類頁(`cloud-compute` / `cloud-storage` / `cloud-analytics` /
  `cloud-serverless` / `cloud-databases` / `cloud-ai` / `cloud-services`＝CI-01〜CI-07)、
  4 個產品頁(`sentinelone` / `threatsonar` / `cybereyes` / `google-secops`)
  與 1 個方案頁(`ess.html`),子頁全用 Nav A;
  根 `index.html` 是 Demo hub(首屏為四方案橫向比較)。
- **版面變體檔不要手改**:6 個 `index-v*.html` 由 `docs/reports/build_variants_20260804.py`
  產生(共用區塊直接從 `index.html` 切片,確保跨變體逐字節相同)。要改就改腳本後重跑。
  正式版依 `docs/Volcatech_多風格_Build_Prompts.md`(**唯一事實來源**)產生 Astro 版;
  但該檔 §B 的 style-3 選單定義(Platform / Arsenal / Operations)是評選期歷史,
  現行選單以 `style-3-soc/` 頁面為準。`docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為
  legacy,其規格一律不採信。
- **`archive/` 是已凍結的評選歷史(落選風格、版型變體、舊總覽):一律不修改、不 review、
  不納入任何檢查**。其中 `archive/Volcatech_Layout_Variants_GPT/` 是外部 AI 參考組,唯讀;
  它自帶的 `CLAUDE.md` / `README.md` / `HANDOVER.md` 只描述它自己,**不適用本專案**,
  規則衝突時一律以根目錄 `CLAUDE.md` 為準。
- **一致性鐵則是雙軸**(2026-08-04 起,舊的單軸版本已失效):
  **軸 1** 同一版面的 Nav A ↔ Nav B 自 `<main>` 起**逐字節相同**(共 4 組 diff 必須全綠);
  **軸 2** 跨版面方案凍結共用文案——H1、副標、Why H2、CTA 橫幅 H2、footer 品牌句這五句
  在 8 個首頁檔逐字相同,且四方案的 hero 區塊完全一致。核心句
  `We operate what we sell, and we build what we cannot buy.` 只在三個變體出現(6 檔),
  `index.html` / `index-nav-b.html` 是**未經內容改動的對照組**,不得為了湊一致而改它。
- 頂部選單分類為 `Google Cloud / CyberSecurity / Services`;`CyberSecurity` 駝峰是
  0731 會議指定的**刻意寫法**,不要「修正」成 Cybersecurity(僅限選單分類名,
  H1 等內文仍為定稿原文)。每個下拉第一行是 mono 白話對照;CyberSecurity 的 SIEM 群組
  標籤為「Detection — SIEM & WDR」(CyberEyes 實為 WDR),白話行為
  「CyberSecurity — EDR · SIEM & WDR · Built in-house」。`Services` 下拉以
  「Enterprise Security Service (ESS)」置頂。
- **三個下拉都零佔位連結,不要改回 `#offer` / `#built`**:
  `Google Cloud` = Overview(`cloud.html`)＋**六組 18 項**(2026-08-05 起,
  `Edge security` 與 `Volcatech cloud services` 兩組已從選單移除;
  **只動選單**——頁尾那列、`cloud.html` 區塊與 `cloud-services.html` 頁面都保留),18 項 GCP 產品是
  `分類頁#產品錨點` 深連結(例 `cloud-compute.html#compute-engine`);
  `CyberSecurity` = Overview(`cybersecurity.html`)＋ 8 項,連產品頁或 `cybersecurity.html#錨點`;
  `Services` = Overview(`services.html`)＋ ESS ＋ 5 項 `services.html#錨點`。
  Nav B 的第二層群組父項也是深連結(`cybersecurity.html#edr` / `#detection` / `#in-house`)。
- **動 nav 或 footer = 全站 23 檔同步**(8 首頁 + 15 個子頁);手改必定漏,
  用腳本(參考 `docs/reports/sync_nav_20260804.py`)產生後跑 `CLAUDE.md` §驗證方式。
  同版面的 A/B 自 `<main>` 起仍須逐字節相同。頁尾三個欄標題(Cloud Infrastructure /
  Cybersecurity / Managed Services)都是連到對應總覽頁的連結。
- **選單 CSS 兩處刻意的不對稱,勿「順手統一」**:Nav A 的 `.dd ul` 有
  `max-height:calc(100vh - 90px);overflow-y:auto`(Google Cloud 下拉 26 列在矮視窗會溢出),
  **Nav B 刻意沒有**(加了會裁掉二層 flyout);全 23 檔的 `main [id]` 都有
  `scroll-margin-top:80px`,新增頁面要一併帶上。
- **V3 參考架構圖(`index-v3-flow*.html`)的三條硬約束**:① 不得用 `position:absolute`
  (768/390px 會崩,層間箭頭走 normal flow);② 承載語意的線條用 `--muted` 不用 `--line`
  ——`--line #27344A` 在 `--bg #0E141F` 上只有 **1.47:1**,不到 WCAG 1.4.11 的 3:1;
  ③ 箭頭用帶 `aria-hidden="true"` 的真字元,不放進 `::before content`,
  也不用 `role="img"` 包整張圖(會把裡面的連結對輔助科技隱藏)。
  圖層標題不能單獨叫 `Operations` / `Platform`——會誤觸「舊選單術語不得殘留」的檢查。
- **新增/修改產品頁三個常見坑**,完成前自查:① 導覽列 `aria-current="page"` 掛在
  **自己那一項**;② 語言切換的 EN 連結**自指本頁**檔名;③ 該項在 nav/footer 改為
  真連結後,**刪掉** `title="Demo: …"` 提示(那是暫代錨點專用)。
- `ess.html` 是方案頁:ESS(Enterprise Security Service)為沃凱打包方案
  (CyberEyes WDR + 多品牌 EDR + 自有 7x24 SOC),**方案層、非 19 項 SKU**;
  **全頁禁任何外部連結**。此規則**只適用 `ess.html`**——`cloud-services.html` 有
  1 條指向 Cloud Armor 官方頁的外部連結(合法)。
- **已知待補項,不要自行編內容補上**:`cloud-services.html` 的沃凱自有服務 3 項
  (Cloud Migration & Kubernetes / Hybrid Cloud & Backup / Data & AI Engineering);
  `services.html` 的 5 項服務(24/7 SOC & IR / ISMS & PIMS / Penetration Testing /
  Cloud FinOps / Digital Transformation);`cybersecurity.html` 的 FortiEDR 描述;
  以及全站的合作夥伴等級、ISO 27001、EU region、交付模式、SLA 回應時間。
  ⚠ **紅線**:「Google SecOps 認證經銷商 / Cloud Security MSSP / Premier Partner」
  是**蓋亞(另一家公司)的資格**,寫成沃凱的等於不實陳述(見 `docs/product/google-secops.md`)。
- **SKU 代碼體系**:唯一事實來源 §A 的 `C-01`〜`C-06` 等是 **pre-0731 歷史體系**,
  保留封存、不對齊、不上站;現行 Cloud 線用頁面層代碼 `CI` / `CI-01`〜`CI-07`。
- 純靜態、單檔自足:HTML + inline CSS,禁止外部 CDN(含 Google Fonts)、禁止框架與建置步驟。
- 全站相對路徑(GitHub Pages 子路徑相容)。
- 首頁首屏必須保留:H1 + 明列**三條業務板塊**
  (Cloud Infrastructure / Cybersecurity / Managed Services)各附入口。
  H1 定稿(不得改寫):
  `Cloud infrastructure, cybersecurity and managed services — from one turn-key partner.`
- 首頁必備 **Built by Volcatech** 區塊(自研 CE-BAS / AI-PTaaS / SecPurple);
  它不是第 4 條產品線,**不進頂層導覽**。
- 公司事實(統編、地址、認證、案例)一律 `[TODO: 說明]` 佔位,不得虛構;
  **全案只用這一種佔位語法**(不得用 `{{TODO}}`)。公司事實來源為 `docs/公司_104.md`,
  但該檔只可用於服務範圍與願景,不可用來填統編/VAT/地址。
- `style-3-soc/` 的 design tokens(`:root` CSS variables)獨立,不可從 `archive/` 舊風格
  混入;十五頁的 tokens 與共用區塊需同步修改。
- WCAG 2.2 AA、`:focus-visible`、`prefers-reduced-motion`、RWD(390/768/1024/1440)、每頁唯一 h1;
  非英文片段(如「繁中」、中文公司名)必須帶 `lang` 屬性。
- 文案為歐洲 B2B 直述語氣,禁 hype 形容詞(leading / best-in-class / cutting-edge)與
  絕對化承諾(every / all / 100%);禁正文 ALL CAPS;原廠產品描述必須改寫,不得複製。
