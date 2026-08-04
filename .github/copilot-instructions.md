# Copilot 專案指示 — Volcatech 官網 Demo(勝出風格 style-3-soc)

一律以繁體中文回覆;程式碼與技術術語保留原文。完整規則見根目錄 `CLAUDE.md`,重點如下:

- 本專案為靜態官網 demo。**2026-07-31 內部評選已結束**:勝出組合 = Style 3(SOC Console
  深色色系)× 原版直落版型,色系凍結。現行維護對象只有 `style-3-soc/` **十五頁**:
  `index.html`(Nav A,單層下拉)、`index-nav-b.html`(Nav B,二層 flyout)、
  8 個 Cloud 頁(總覽 `cloud.html`＝代碼 CI;分類頁 `cloud-compute.html` /
  `cloud-storage.html` / `cloud-analytics.html` / `cloud-serverless.html` /
  `cloud-databases.html` / `cloud-ai.html` / `cloud-services.html`＝代碼 CI-01〜CI-07)、
  4 個產品頁(`sentinelone.html` / `threatsonar.html` / `cybereyes.html` /
  `google-secops.html`)與 1 個方案頁(`ess.html`),子頁全用 Nav A;
  根 `index.html` 是 Demo hub(主卡 15 連結)。
  正式版依 `docs/Volcatech_多風格_Build_Prompts.md`(**唯一事實來源**)產生 Astro 版;
  但該檔 §B 的 style-3 選單定義(Platform / Arsenal / Operations)是評選期歷史,
  現行選單以 `style-3-soc/` 頁面為準。`docs/官網建置計畫_Build_Prompt_v3.md` 已凍結為
  legacy,其規格一律不採信。
- **`archive/` 是已凍結的評選歷史(落選風格、版型變體、舊總覽):一律不修改、不 review、
  不納入任何檢查**。其中 `archive/Volcatech_Layout_Variants_GPT/` 是外部 AI 參考組,唯讀;
  它自帶的 `CLAUDE.md` / `README.md` / `HANDOVER.md` 只描述它自己,**不適用本專案**,
  規則衝突時一律以根目錄 `CLAUDE.md` 為準。
- **兩變體一致性鐵則**:`style-3-soc/index.html` 與 `index-nav-b.html` 自 `<main>` 起
  必須**逐字節相同**;改 `<main>` 之後的內容,兩檔必須同步並用 diff 驗證。
- 頂部選單分類為 `Google Cloud / CyberSecurity / Services`;`CyberSecurity` 駝峰是
  0731 會議指定的**刻意寫法**,不要「修正」成 Cybersecurity(僅限選單分類名,
  H1 等內文仍為定稿原文)。每個下拉第一行是 mono 白話對照;CyberSecurity 的 SIEM 群組
  標籤為「Detection — SIEM & WDR」(CyberEyes 實為 WDR),白話行為
  「CyberSecurity — EDR · SIEM & WDR · Built in-house」。`Services` 下拉以
  「Enterprise Security Service (ESS)」置頂。
- **`Google Cloud` 下拉 = 頂部 Overview 入口(`cloud.html`)加上八組 22 項**:GCP 產品樹
  六組 18 項(Compute / Storage / Analytics / Serverless / Databases / AI)、
  `Edge security` 1 項、`Volcatech cloud services` 3 項。18 項 GCP 產品**全部是深連結**
  (`分類頁#產品錨點`,例 `cloud-compute.html#compute-engine`),**本下拉零佔位連結**,
  不要改回 `#offer`。
- **動 nav 或 footer = 全站 15 檔同步**(兩首頁變體 + 13 個子頁),
  兩首頁自 `<main>` 起仍須逐字節相同。頁尾「Cloud Infrastructure」欄為
  8 行分類連結(Overview / Compute / Storage / Analytics / Serverless / Databases /
  AI / Cloud services & Cloud Armor),不是舊的 6 項 SKU。
- **選單 CSS 兩處刻意的不對稱,勿「順手統一」**:Nav A 的 `.dd ul` 有
  `max-height:calc(100vh - 90px);overflow-y:auto`(Google Cloud 下拉 32 列會溢出視窗),
  **Nav B 刻意沒有**(加了會裁掉二層 flyout);全 15 檔的 `main [id]` 都有
  `scroll-margin-top:80px`,新增頁面要一併帶上。
- **新增/修改產品頁三個常見坑**,完成前自查:① 導覽列 `aria-current="page"` 掛在
  **自己那一項**;② 語言切換的 EN 連結**自指本頁**檔名;③ 該項在 nav/footer 改為
  真連結後,**刪掉** `title="Demo: …"` 提示(那是暫代錨點專用)。
- `ess.html` 是方案頁:ESS(Enterprise Security Service)為沃凱打包方案
  (CyberEyes WDR + 多品牌 EDR + 自有 7x24 SOC),**方案層、非 19 項 SKU**;
  **全頁禁任何外部連結**。此規則**只適用 `ess.html`**——`cloud-services.html` 有
  1 條指向 Cloud Armor 官方頁的外部連結(合法)。
- `cloud-services.html` 的沃凱自有服務 3 項(Cloud Migration & Kubernetes /
  Hybrid Cloud & Backup / Data & AI Engineering)內文是 `[TODO: service description]`,
  素材未定案,**這是已知待補項,不要自行編內容補上**。
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
